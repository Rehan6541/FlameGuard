🔥 Flame Guard: Fire Detection with YOLOv10

Flame Guard is an advanced fire detection system leveraging the power of the YOLOv10 object detection algorithm. It is trained using a custom fire dataset from Roboflow and can detect flames in both images and videos with high accuracy.

📌 Features

Trained using YOLOv10n on a custom Fire Detection dataset.

Detects fire in real-time from images and videos.

Visual outputs include detection bounding boxes, confidence scores, and evaluation plots.

Uses Roboflow for dataset management and preprocessing.

Fine-tuned with 30 epochs, batch size of 32.

🧠 Model Variants

Pretrained weights used:yolov10n.pt (nano)

Also supports: yolov10s.pt, yolov10m.pt, yolov10b.pt, yolov10l.pt, yolov10x.pt

🚀 Installation

# Install YOLOv10 from source
!pip install -q git+https://github.com/THU-MIG/yolov10.git

# Install Roboflow
!pip install -q roboflow

# Download pretrained YOLOv10 weights
!wget -q https://github.com/jameslahm/yolov10/releases/download/v1.0/yolov10n.pt

📁 Dataset

Source: Roboflow Fire Detection Dataset

Version: 1

Format: YOLOv8 compatible

from roboflow import Roboflow

rf = Roboflow(api_key="YOUR_API_KEY")

project = rf.workspace("rehman-2vlay").project("fire-detection-vdtmc")

version = project.version(1)

dataset = version.download("yolov8")

🏋️‍♂️ Training

!yolo task=detect mode=train epochs=30 batch=32 plots=True \

model='/content/yolov10n.pt' \

data='/content/Fire-Detection-1/data.yaml'

📊 Results

Training evaluation metrics are stored in runs/detect/train*/

Sample visualization:

from IPython.display import Image

Image(filename='/content/runs/detect/train3/results.png', width=600)

Image(filename='/content/runs/detect/train3/confusion_matrix.png', width=600)

🔎 Inference on Images

from yolov10 import YOLOv10

model_path = '/content/runs/detect/train3/weights/best.pt'

model = YOLOv10(model_path)

results = model(source='/content/Fire-Detection-1/test/images', conf=0.25, save=True)

import glob

images = glob.glob('/content/runs/detect/predict/*.jpg')

for image in images:

  display(Image(filename=image, width=400))


📢 Acknowledgements

YOLOv10

Roboflow

Pretrained weights from JamesLahm GitHub


