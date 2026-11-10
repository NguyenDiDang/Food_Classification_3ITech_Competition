# AI-Powered Canteen Food Recognition & Automated Billing System

**Language:** [English](README.md) \| [Tiếng Việt](README_VI.md)

------------------------------------------------------------------------

## 1. Project Overview

Artificial intelligence is increasingly being adopted in everyday
services. Product recognition and automated pricing systems are already
used in many convenience stores and supermarkets, such as Circle K, Bách
Hóa Xanh, GS25, and CoopMart. However, many of these solutions still
rely on barcode scanning or the recognition of pre-packaged products.

Barcode-based checkout is less practical in places such as school
cafeterias, hospitals, and industrial canteens. Meals are often prepared
on-site, do not have standardized packaging, and can change from day to
day. As a result, applying conventional barcode scanning to these
environments is difficult.

This project introduces an automated system that recognizes food items
on a meal tray and calculates the bill quickly and accurately.

At the core of the system is a combination of:

-   **YOLO object detection** to locate individual food items on the
    tray.
-   **A custom-trained Convolutional Neural Network (CNN)** to classify
    the detected food items.
-   **Automatic price calculation** based on a predefined price list.
-   **QR-code generation** that directs users to a visual, simulated
    payment page.

### Key Benefits

-   **Faster checkout:** Reduces manual food identification and price
    calculation, helping shorten customer waiting times.
-   **Reduced staffing workload:** Automates repetitive checkout tasks
    so staff can focus on other responsibilities.
-   **Better user experience:** Provides a convenient, fast, and modern
    checkout process.
-   **Reliable recognition:** Combines object detection and image
    classification to identify food items.
-   **Flexible expansion:** Makes it possible to add food categories,
    update prices, and extend the system to support direct camera input.

------------------------------------------------------------------------

## 2. Quick Start

### Prerequisites

-   Python **3.8 or later**: [Download
    Python](https://www.python.org/downloads/)
-   [Visual Studio Code](https://code.visualstudio.com/) (recommended)
-   Git, or download the project source code as a ZIP archive.

### Installation

**Step 1 --- Get the source code**

Clone the repository or download and extract its ZIP archive.

``` bash
git clone <repository-url>
cd <project-folder>
```

Replace the placeholders with the actual repository URL and folder name.

**Step 2 --- Open the project**

Open the project folder in Visual Studio Code, then open its integrated
terminal.

**Step 3 --- Create a virtual environment**

``` bash
python -m venv venv
```

**Step 4 --- Activate the virtual environment**

Windows:

``` powershell
.\venv\Scripts\activate
```

macOS / Linux:

``` bash
source venv/bin/activate
```

**Step 5 --- Install dependencies**

``` bash
pip install -r requirements.txt
```

------------------------------------------------------------------------

## 3. Run the Application

Before launching the application, make sure the trained CNN model is
available in the project directory under the filename `model.h5`. The
YOLO model files and their configured paths must also be available as
expected by the application.

**Step 1 --- Start the application**

``` bash
python app.py
```

**Step 2 --- Open the interface**

Once the application starts, use the Gradio interface displayed in the
terminal to open the local web application.

**Step 3 --- Select a meal-tray image**

Upload an image of a meal tray through the interface.

**Step 4 --- Let the system process the image**

The system performs the following operations:

1.  YOLO detects the locations of food items on the tray.
2.  The CNN classifies each detected food item.
3.  The application looks up the corresponding prices and calculates the
    total.
4.  A QR code is generated to direct the user to the simulated payment
    page.

> **Note:** The payment page described in this project is a simulation.
> This README does not imply integration with a real payment gateway.

------------------------------------------------------------------------

## 4. Technology Stack

The project uses the following libraries and tools. The exact installed
versions are specified in `requirements.txt`.

  ---------------------------------------------------------------------------------
  Technology                                    Purpose
  --------------------------------------------- -----------------------------------
  [OpenCV](https://opencv.org/)                 Image processing and computer
  (`opencv-python`)                             vision operations

  [NumPy](https://numpy.org/) (`numpy`)         Numerical computing and
                                                multidimensional array operations

  [Ultralytics](https://www.ultralytics.com/)   YOLO-based object detection
  (`ultralytics`)                               

  [TensorFlow](https://www.tensorflow.org/)     Building and running the CNN
  (`tensorflow`)                                classification model

  [Pillow](https://python-pillow.org/)          Image loading and image-format
  (`Pillow`)                                    handling

  [Gradio](https://www.gradio.app/) (`gradio`)  Building the interactive web
                                                interface

  Python `threading`                            Running tasks concurrently where
                                                implemented by the application
  ---------------------------------------------------------------------------------

------------------------------------------------------------------------

## 5. Project Structure

The project organizes food-category data into separate directories.
Example category names include:

``` text
project/
├── app.py
├── model.h5
├── requirements.txt
├── Com Trang/
├── Thit kho/
└── Trung chien/
```

The tree above is illustrative; the actual repository may contain
additional files, model assets, configuration files, and directories.

Keeping food categories separate makes the training data easier to
manage and supports future updates. New food categories can be added by
preparing the corresponding data and updating the model and application
configuration as required.

The Gradio interface provides a straightforward way to upload and
process meal-tray images. The application can also be extended to
support direct camera input, subject to the required camera integration
and real-time processing changes.

------------------------------------------------------------------------

## 6. Future Improvements

Potential extensions include:

-   Adding more food categories and updating the price list.
-   Integrating a live camera feed for real-time recognition.
-   Improving detection and classification performance under different
    lighting and tray arrangements.
-   Connecting the simulated checkout flow to a real payment service, if
    required.

------------------------------------------------------------------------

## 7. Notes

-   The trained CNN model is expected to be named `model.h5`.
-   Make sure the YOLO weights and configuration paths used by `app.py`
    are correctly set up.
-   The sample directory tree is for illustration and may differ from
    the actual repository.
-   The QR code leads to a simulated payment flow, not necessarily a
    real transaction.

------------------------------------------------------------------------
