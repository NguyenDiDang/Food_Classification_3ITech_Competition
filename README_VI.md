# Hệ Thống Nhận Diện Món Ăn & Tính Tiền Tự Động Cho Căn Tin (3ITech Competition)

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![YOLOv8](https://img.shields.io/badge/YOLOv8-Ultralytics-orange.svg)](https://github.com/ultralytics/ultralytics)
[![TensorFlow Lite](https://img.shields.io/badge/TensorFlow%20Lite-Inference-FF6F00.svg)](https://www.tensorflow.org/lite)
[![Gradio](https://img.shields.io/badge/Gradio-UI-orange.svg)](https://www.gradio.app/)
[![Competition](https://img.shields.io/badge/3ITech-Competition-brightgreen.svg)]()

**Ngôn ngữ:** [English](README.md) | [Tiếng Việt](README_VI.md)

---

## 1. Giới thiệu dự án

Quy trình thanh toán thủ công tại căn tin trường học, bệnh viện hay nhà ăn doanh nghiệp thường xuyên bị quá tải vào giờ cao điểm. Khác với các siêu thị sử dụng mã vạch tiêu chuẩn trên bao bì đóng gói sẵn, suất ăn căn tin được chế biến tại chỗ, không có bao bì cố định và thực đơn thay đổi linh hoạt mỗi ngày.

Dự án này mang đến một giải pháp Thị giác máy tính (Computer Vision) hoàn chỉnh từ đầu đến cuối: tự động định vị các món ăn trên khay cơm, phân loại chính xác từng món và tự động tính tổng tiền thanh toán theo thời gian thực.

### Sơ đồ quy trình xử lý (Pipeline)

```
┌──────────────────┐       ┌───────────────────────┐       ┌─────────────────────────┐
│  Ảnh khay cơm    │ ────> │   YOLOv8 Detection    │ ────> │   Cắt vùng món ăn       │
└──────────────────┘       │  (Định vị các món)    │       │ (Resize chuẩn 224x224)  │
                           └───────────────────────┘       └───────────┬─────────────┘
                                                                       │
┌──────────────────┐       ┌───────────────────────┐       ┌───────────▼─────────────┐
│  Giao diện Web   │ <──── │  Tra bảng giá &       │ <──── │  CNN (TensorFlow Lite)  │
│    (Gradio)      │       │  tính tổng tiền       │       │  (Phân loại 10 món ăn)  │
└──────────────────┘       └───────────────────────┘       └─────────────────────────┘
```

1. **Phát hiện đối tượng (YOLOv8):** Quét toàn bộ khay cơm và xác định vị trí từng món ăn (bounding box).
2. **Tiền xử lý ảnh:** Cắt các vùng món ăn được phát hiện, chuẩn hóa kích thước về 224 × 224 và đưa về phân phối chuẩn đầu vào.
3. **Phân loại tối ưu (CNN qua TensorFlow Lite):** Sử dụng mô hình `code_cnn.tflite` (đã được lượng tử hóa/tối ưu hóa) thông qua `tf.lite.Interpreter` để nhận diện chính xác 10 lớp món ăn với độ trễ thấp và tiết kiệm bộ nhớ.
4. **Tính tiền tự động:** Tự động tra cứu đơn giá tương ứng của từng món ăn trong cơ sở dữ liệu và cộng dồn tổng tiền hóa đơn.
5. **Giao diện trực quan (Gradio):** Cho phép người dùng tải ảnh lên, xem trực tiếp khung nhận diện món ăn và bảng kê hóa đơn chi tiết.

---

## 2. Điểm nổi bật về mặt kỹ thuật

* **Kiến trúc thị giác 2 giai đoạn (Two-Stage Pipeline):** Tách biệt khâu định vị vị trí món (Detection) và khâu phân loại chi tiết (Classification), giúp độ chính xác nhận diện cao hơn vượt trội so với phân loại một bước trên toàn bộ ảnh.
* **Tối ưu hóa suy luận (Edge-Optimized Inference):** Sử dụng mô hình TensorFlow Lite (`code_cnn.tflite`) giúp ứng dụng chạy nhẹ nhàng, mượt mà trên các thiết bị máy tính thông thường hoặc phần cứng nhúng.
* **Sẵn sàng chạy ngay (Out-of-the-box):** Cả 2 file trọng số mô hình đã huấn luyện (`yolov8trained.pt` và `code_cnn.tflite`) đều được đính kèm sẵn trong repository, không cần cài đặt thêm trọng số bên ngoài.

---

## 3. Hướng dẫn cài đặt & Khởi chạy

### Yêu cầu hệ thống

* Python phiên bản **3.8 đến 3.11** ([Tải Python](https://www.python.org/downloads/))
* Git

### Bước 1 — Clone mã nguồn về máy

```bash
git clone https://github.com/NguyenDiDang/Food_Classfication_3ITech_Competition.git
cd Food_Classfication_3ITech_Competition
```

### Bước 2 — Tạo và kích hoạt môi trường ảo

* **Trên Windows (PowerShell):**
  ```powershell
  python -m venv venv
  .\venv\Scripts\activate
  ```
* **Trên macOS / Linux:**
  ```bash
  python3 -m venv venv
  source venv/bin/activate
  ```

### Bước 3 — Cài đặt các thư viện phụ thuộc

```bash
pip install -r requirements.txt
```

---

## 4. Chạy ứng dụng

Khởi chạy ứng dụng giao diện web bằng lệnh:

```bash
python giaodien.py
```

Sau khi chạy lệnh, terminal sẽ cung cấp đường dẫn cục bộ (thông thường là `http://127.0.0.1:7860`). Bạn chỉ cần mở trình duyệt và truy cập:
1. Tải ảnh chụp một khay cơm bất kỳ lên giao diện.
2. Nhấn nút để hệ thống xử lý.
3. Theo dõi các vùng món ăn được phát hiện kèm hóa đơn tính tiền tự động.

---

## 5. Cấu trúc thư mục Repository

```text
Food_Classfication_3ITech_Competition/
├── giaodien.py              # Mã nguồn chính chạy giao diện Gradio & pipeline suy luận
├── yolov8trained.pt         # Trọng số mô hình YOLOv8 phát hiện món ăn
├── code_cnn.tflite          # Mô hình CNN TensorFlow Lite phân loại 10 nhóm món ăn
├── requirements.txt         # Danh sách các thư viện cần thiết
├── README.md                # Tài liệu dự án bằng tiếng Anh
└── README_VI.md             # Tài liệu dự án bằng tiếng Việt
```

---

## 6. Nền tảng công nghệ sử dụng

| Công nghệ | Vai trò trong hệ thống |
| :--- | :--- |
| **Ultralytics YOLOv8** (`ultralytics`) | Định vị và phát hiện bounding box các đĩa/món ăn trên khay |
| **TensorFlow / TFLite** (`tensorflow`) | Chạy suy luận tối ưu cho mô hình CNN phân loại 10 lớp món ăn |
| **OpenCV** (`opencv-python`) | Cắt ảnh (crop bbox), resize kích thước 224x224 và tiền xử lý màu |
| **NumPy** (`numpy`) | Xử lý mảng đa chiều và chuyển đổi tensor |
| **Pillow** (`Pillow`) | Thao tác nhập/xuất tệp ảnh |
| **Gradio** (`gradio`) | Xây dựng giao diện web tương tác thân thiện, nhanh chóng |

---

## 7. Định hướng mở rộng

- [ ] Kết nối camera góc rộng từ trên cao để tự động chụp và nhận diện khay cơm theo thời gian thực (không cần tải ảnh thủ công).
- [ ] Mở rộng dữ liệu phân loại ngoài 10 món ăn cơ bản để áp dụng cho thực đơn phong phú hơn.
- [ ] Tích hợp mã QR động liên kết với cổng thanh toán điện tử (VietQR, MoMo, VNPay).
- [ ] Chuyển đổi toàn bộ pipeline sang định dạng TensorRT để chạy trực tiếp trên các vi máy tính nhúng (NVIDIA Jetson Nano/Orin).

---

## 8. Tác giả & Cuộc thi

* **Tác giả:** Nguyễn Di Đăng — Ngành Kỹ thuật Robot & Trí tuệ Nhân tạo, Đại học Kinh tế TP. Hồ Chí Minh (UEH)
* **GitHub:** [@NguyenDiDang](https://github.com/NguyenDiDang)
* **Bối cảnh:** Dự án phát triển tham gia **Cuộc thi 3ITech**.
