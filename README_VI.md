# Hệ Thống Nhận Diện Món Ăn Và Thanh Toán Tự Động Cho Căn Tin

**Ngôn ngữ:** [English](README.md) \| [Tiếng Việt](README_VI.md)

------------------------------------------------------------------------

## 1. Giới thiệu dự án

Trong bối cảnh trí tuệ nhân tạo ngày càng được ứng dụng rộng rãi vào đời
sống, các hệ thống nhận diện vật thể và định giá sản phẩm đã xuất hiện
tại nhiều cửa hàng tiện lợi và siêu thị như Circle K, Bách Hóa Xanh,
GS25, CoopMart,... Tuy nhiên, nhiều giải pháp hiện nay vẫn dựa vào công
nghệ quét mã vạch hoặc nhận diện các sản phẩm có bao bì đóng gói sẵn.

Tại những môi trường như căn tin trường học, bệnh viện hoặc khu công
nghiệp, phương thức quét mã vạch gặp nhiều hạn chế. Món ăn thường được
chế biến tại chỗ, không có bao bì tiêu chuẩn và có thể thay đổi linh
hoạt theo ngày. Vì vậy, việc áp dụng mã vạch cho những môi trường này
gần như không khả thi.

Dự án mang đến một hệ thống tự động nhận diện các món ăn trên khay cơm
và tính tiền nhanh chóng, chính xác.

Trái tim của hệ thống là sự kết hợp giữa:

-   **YOLO:** Phát hiện và xác định vị trí của từng món ăn trên khay.
-   **Mạng nơ-ron tích chập (CNN):** Phân loại các món ăn đã được phát
    hiện bằng mô hình được huấn luyện chuyên biệt.
-   **Tính tiền tự động:** Tính tổng chi phí dựa trên bảng giá được
    thiết lập sẵn.
-   **Tạo mã QR:** Tạo mã QR dẫn đến trang thanh toán giả lập trực quan.

### Điểm nổi bật

-   **Tiết kiệm thời gian:** Giảm các thao tác nhận diện món ăn và tính
    tiền thủ công, từ đó rút ngắn thời gian chờ.
-   **Giảm tải nhân lực:** Tự động hóa các công việc lặp lại trong quy
    trình thanh toán để nhân viên tập trung vào những nhiệm vụ khác.
-   **Nâng cao trải nghiệm người dùng:** Mang đến quy trình thanh toán
    tiện lợi, nhanh chóng và hiện đại.
-   **Nhận diện đáng tin cậy:** Kết hợp phát hiện đối tượng và phân loại
    ảnh để nhận diện món ăn.
-   **Khả năng mở rộng linh hoạt:** Có thể bổ sung món ăn mới, cập nhật
    bảng giá và phát triển tính năng nhận diện từ camera trực tiếp.

------------------------------------------------------------------------

## 2. Hướng dẫn cài đặt nhanh chóng

### Yêu cầu trước khi cài đặt

-   Python phiên bản **3.8 trở lên**: [Tải
    Python](https://www.python.org/downloads/)
-   [Visual Studio Code](https://code.visualstudio.com/) (khuyến nghị)
-   Git, hoặc tải mã nguồn dự án dưới dạng file ZIP.

### Các bước cài đặt

**Bước 1 --- Tải mã nguồn**

Clone repository hoặc tải và giải nén file ZIP của dự án.

``` bash
git clone <repository-url>
cd <project-folder>
```

Thay các phần giữ chỗ bằng URL repository và tên thư mục thực tế.

**Bước 2 --- Mở dự án**

Mở thư mục dự án bằng Visual Studio Code, sau đó mở Terminal tích hợp.

**Bước 3 --- Tạo môi trường ảo**

``` bash
python -m venv venv
```

**Bước 4 --- Kích hoạt môi trường ảo**

Windows:

``` powershell
.\venv\Scripts\activate
```

macOS / Linux:

``` bash
source venv/bin/activate
```

**Bước 5 --- Cài đặt các thư viện cần thiết**

``` bash
pip install -r requirements.txt
```

------------------------------------------------------------------------

## 3. Khám phá cách hệ thống hoạt động

Trước khi khởi chạy, hãy đảm bảo mô hình CNN đã được huấn luyện và đặt
trong thư mục dự án với tên `model.h5`. Các tệp mô hình YOLO cùng đường
dẫn cấu hình tương ứng cũng cần được chuẩn bị đúng như cách ứng dụng
đang sử dụng.

**Bước 1 --- Khởi chạy ứng dụng**

``` bash
python app.py
```

**Bước 2 --- Mở giao diện**

Sau khi ứng dụng khởi chạy, sử dụng địa chỉ giao diện Gradio được hiển
thị trong Terminal để mở ứng dụng web cục bộ.

**Bước 3 --- Chọn ảnh khay cơm**

Tải ảnh khay cơm lên thông qua giao diện.

**Bước 4 --- Theo dõi quá trình xử lý**

Hệ thống tự động thực hiện các công việc:

1.  YOLO phát hiện vị trí của từng món ăn trên khay cơm.
2.  CNN phân loại từng món ăn đã được phát hiện.
3.  Ứng dụng tra cứu giá tương ứng và tính tổng chi phí.
4.  Hệ thống tạo mã QR dẫn đến trang thanh toán giả lập.

> **Lưu ý:** Trang thanh toán trong mô tả dự án là trang giả lập. Điều
> này không đồng nghĩa hệ thống đã tích hợp với cổng thanh toán thực tế.

------------------------------------------------------------------------

## 4. Nền tảng công nghệ

Dự án sử dụng các thư viện và công cụ dưới đây. Phiên bản cụ thể của
từng thư viện được khai báo trong `requirements.txt`.

  ---------------------------------------------------------------------------------
  Công nghệ                                     Vai trò
  --------------------------------------------- -----------------------------------
  [OpenCV](https://opencv.org/)                 Xử lý ảnh và các tác vụ thị giác
  (`opencv-python`)                             máy tính

  [NumPy](https://numpy.org/) (`numpy`)         Tính toán số học và xử lý mảng đa
                                                chiều

  [Ultralytics](https://www.ultralytics.com/)   Hỗ trợ phát hiện đối tượng bằng
  (`ultralytics`)                               YOLO

  [TensorFlow](https://www.tensorflow.org/)     Xây dựng và chạy mô hình CNN phân
  (`tensorflow`)                                loại

  [Pillow](https://python-pillow.org/)          Đọc ảnh và xử lý các định dạng ảnh
  (`Pillow`)                                    

  [Gradio](https://www.gradio.app/) (`gradio`)  Xây dựng giao diện web tương tác

  Python `threading`                            Hỗ trợ chạy các tác vụ đồng thời
                                                tại những phần được triển khai
                                                trong ứng dụng
  ---------------------------------------------------------------------------------

------------------------------------------------------------------------

## 5. Kiến trúc chương trình

Dữ liệu các nhóm món ăn được tổ chức trong những thư mục riêng biệt. Một
số tên thư mục ví dụ:

``` text
project/
├── app.py
├── model.h5
├── requirements.txt
├── Com Trang/
├── Thit kho/
└── Trung chien/
```

Đây là cấu trúc minh họa; repository thực tế có thể chứa thêm các tệp mã
nguồn, mô hình, tệp cấu hình và thư mục khác.

Việc phân chia dữ liệu theo từng nhóm món ăn giúp quá trình quản lý dữ
liệu huấn luyện thuận tiện hơn, đồng thời tạo điều kiện để cập nhật và
mở rộng hệ thống. Khi bổ sung món ăn mới, cần chuẩn bị dữ liệu tương ứng
và cập nhật mô hình cũng như cấu hình ứng dụng khi cần thiết.

Giao diện Gradio giúp người dùng dễ dàng tải ảnh khay cơm lên và theo
dõi kết quả xử lý. Trong tương lai, hệ thống có thể được mở rộng để nhận
hình ảnh trực tiếp từ camera sau khi bổ sung phần tích hợp camera và xử
lý thời gian thực phù hợp.

------------------------------------------------------------------------

## 6. Hướng phát triển

Một số hướng mở rộng tiềm năng:

-   Bổ sung thêm các nhóm món ăn và cập nhật bảng giá.
-   Tích hợp camera trực tiếp để nhận diện món ăn theo thời gian thực.
-   Cải thiện khả năng phát hiện và phân loại trong các điều kiện ánh
    sáng, góc chụp và cách sắp xếp khay cơm khác nhau.
-   Tích hợp quy trình thanh toán giả lập với một dịch vụ thanh toán
    thực tế nếu có nhu cầu.

------------------------------------------------------------------------

## 7. Lưu ý

-   Mô hình CNN được sử dụng trong hướng dẫn này có tên `model.h5`.
-   Cần đảm bảo các tệp trọng số YOLO và đường dẫn cấu hình mà `app.py`
    sử dụng đã được chuẩn bị chính xác.
-   Cấu trúc thư mục trong README chỉ mang tính minh họa và có thể khác
    với repository thực tế.
-   Mã QR dẫn đến quy trình thanh toán giả lập, không mặc định thực hiện
    giao dịch thật.

------------------------------------------------------------------------
