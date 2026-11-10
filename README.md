# AI-Powered Cafeteria Food Recognition & Automated Billing System

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![YOLOv8](https://img.shields.io/badge/YOLOv8-Ultralytics-orange.svg)](https://github.com/ultralytics/ultralytics)
[![TensorFlow Lite](https://img.shields.io/badge/TensorFlow%20Lite-Inference-FF6F00.svg)](https://www.tensorflow.org/lite)
[![Gradio](https://img.shields.io/badge/Gradio-UI-orange.svg)](https://www.gradio.app/)
[![Competition](https://img.shields.io/badge/3ITech-Competition-brightgreen.svg)]()

**Language:** [English](README.md) | [Tiếng Việt](README_VI.md)

---

## 1. Project Overview

Manual checkout at self-service canteens, school cafeterias, and industrial dining halls is often a bottleneck during peak hours. Unlike supermarkets with standardized barcodes, cooked cafeteria meals are prepared fresh, plated without packaging, and vary daily.

This project delivers an end-to-end Computer Vision system that automatically detects dishes on a meal tray, classifies each item, and computes the total bill in real time.

### Core Processing Pipeline

```
┌─────────────────┐       ┌──────────────────────┐       ┌────────────────────────┐
│ Meal-Tray Image │ ────> │  YOLOv8 Detection    │ ────> │ Bounding Box Cropping  │
└─────────────────┘       │ (Locate Food Dishes) │       │   (Resize to 224x224)  │
                          └──────────────────────┘       └───────────┬────────────┘
                                                                     │
┌─────────────────┐       ┌──────────────────────┐       ┌───────────▼────────────┐
│   Gradio UI     │ <──── │ Pricing & Billing    │ <──── │  CNN (TensorFlow Lite) │
│ (Visual Bill)   │       │ (Total Calculation)  │       │ (10-Class Recognition) │
└─────────────────┘       └──────────────────────┘       └────────────────────────┘
```

1. **Object Detection (YOLOv8):** Scans the input tray image and localizes all dish boundaries.
2. **Image Preprocessing:** Crops each detected bounding box and resizes it to 224 × 224 with normalization.
3. **Optimized Classification (CNN via TensorFlow Lite):** Evaluates the cropped dish features using a quantized lightweight TFLite model across 10 distinct cafeteria food classes.
4. **Automated Billing Engine:** Maps predicted classes to an itemized price sheet and sums the final total.
5. **Interactive UI (Gradio):** Provides a visual dashboard to upload tray images, display bounding boxes, and review itemized receipts.

---

## 2. Key Technical Highlights

* **Two-Stage Vision Architecture:** Separates dish localization from fine-grained food classification, significantly boosting accuracy over single-stage end-to-end classifiers.
* **Edge-Optimized Inference:** Employs `code_cnn.tflite` via `tf.lite.Interpreter` for minimal memory footprint and fast inference.
* **Turnkey Execution:** Both trained model weights (`yolov8trained.pt` and `code_cnn.tflite`) are included directly in the repository for immediate out-of-the-box local execution.

---

## 3. Quick Start & Installation

### Prerequisites

* Python **3.8 to 3.11** ([Download Python](https://www.python.org/downloads/))
* Git installed

### Step 1 — Clone the Repository

```bash
git clone https://github.com/NguyenDiDang/Food_Classfication_3ITech_Competition.git
cd Food_Classfication_3ITech_Competition
```

### Step 2 — Create and Activate a Virtual Environment

* **Windows (PowerShell):**
  ```powershell
  python -m venv venv
  .\venv\Scripts\activate
  ```
* **macOS / Linux:**
  ```bash
  python3 -m venv venv
  source venv/bin/activate
  ```

### Step 3 — Install Dependencies

```bash
pip install -r requirements.txt
```

---

## 4. Run the Application

Launch the interactive Gradio interface by running:

```bash
python giaodien.py
```

Once loaded, the terminal will provide a local URL (typically `http://127.0.0.1:7860`). Open this link in your browser to test:
1. Upload any meal-tray photograph.
2. Click **Submit / Process**.
3. Inspect the detected bounding boxes, classified dishes, and the automated itemized receipt.

---

## 5. Repository Structure

```text
Food_Classfication_3ITech_Competition/
├── giaodien.py              # Main Gradio application & end-to-end inference pipeline
├── yolov8trained.pt         # Trained YOLOv8 weights for food dish detection
├── code_cnn.tflite          # Quantized TensorFlow Lite CNN model (10 classes)
├── requirements.txt         # Project package dependencies
├── README.md                # English project documentation
└── README_VI.md             # Vietnamese project documentation
```

---

## 6. Technology Stack

| Technology | Purpose |
| :--- | :--- |
| **Ultralytics YOLOv8** (`ultralytics`) | Object detection and dish boundary localization |
| **TensorFlow / TFLite** (`tensorflow`) | Efficient inference of the 10-class CNN classifier |
| **OpenCV** (`opencv-python`) | Image manipulation, cropping, resizing, and color space transformations |
| **NumPy** (`numpy`) | Tensor/array operations and preprocessing |
| **Pillow** (`Pillow`) | Image I/O handling |
| **Gradio** (`gradio`) | Responsive, interactive web user interface |

---

## 7. Roadmap & Future Improvements

- [ ] Support live video stream input directly from an overhead canteen camera.
- [ ] Expand dataset beyond 10 categories to support diverse regional cuisines.
- [ ] Connect with standard cashless payment gateways (VietQR, MoMo, ZaloPay).
- [ ] Export the full pipeline to TensorRT for deployment on embedded edge hardware (e.g., NVIDIA Jetson).

---

## 8. Author & Acknowledgments

* **Author:** Nguyen Di Dang — Robotics & AI Engineering, University of Economics Ho Chi Minh City (UEH)
* **GitHub:** [@NguyenDiDang](https://github.com/NguyenDiDang)
* **Context:** Developed as a practical project for the **3ITech Competition**.
