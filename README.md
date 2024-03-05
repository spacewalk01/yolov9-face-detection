<h1 align="center"><span>YOLOv9 for Face Detection</span></h1>

The face detection task identifies and pinpoints human faces in images or videos. This repo demonstrates how to train a YOLOv9 model for highly accurate face detection on the WIDER Face dataset. 

<p align="center" margin: 0 auto;>
  <img src="assets/result.jpg" />
</p>

## ⚙️ Installation
Clone this repo and install [requirements.txt](https://github.com/spacewalk01/yolov9-face-detection/blob/main/yolov9/requirements.txt) for YOLOv9:
```
git clone https://github.com/spacewalk01/yolov9-face-detection
cd yolov9-face-detection/yolov9
pip install -r requirements.txt
```

## 🤖 Pretrained Model

Download the pretrained `yolov9-c.pt` model from [google drive](https://drive.google.com/file/d/15K4e08lcZiiQrXmdsnm2BhcoNS3MOMmx/view?usp=sharing). Note that this model was trained on the WIDER dataset for 240 epochs.

## 📚 Data Preparation

The WIDER dataset comprises of more than 30k images with more than 390k faces, each with bouding box and other various label formats.

**Dataset structure**
```
${ROOT}
└── yolov9
└── datasets/    
    └── widerface/
        └── train/
        └── val/
    └── original-widerface/
        └── train/
            └── images/
            └── label.txt
        └── val/
            └── images/
            └── label.txt
└── train2yolo.py
└── val2yolo.py
└── widerface.yaml
```

To prepare the data:

1. Download the [WIDER-FACE](http://shuoyang1213.me/WIDERFACE) datasets.
2. Download the annotation files from [google drive](https://drive.google.com/file/d/1tU_IjyOwGQfGNUvZGwWWM4SwxKp2PUQ8/view?usp=sharing).

Run the following commands:

```shell
python train2yolo.py datasets/original-widerface/train datasets/widerface/train
python val2yolo.py datasets/original-widerface datasets/widerface/val
```

These scripts will convert your annotation files to YOLO format, creating one .txt file per image. Each row in the file will represent a single object in the format: `class x_center y_center width height`.

## 🏋️ Training

To train the model, use the following command:

``` shell
cd yolov9
python train_dual.py --workers 4 --device 0 --batch 4 --data ../widerface.yaml --img 640 --cfg models/detect/yolov9-c.yaml --weights '' --name yolov9-c --hyp hyp.scratch-high.yaml --min-items 0 --epochs 500 --close-mosaic 15
```

## 🌱 Inference

For inference, run the following command:

``` shell
python detect.py --weights runs/train/yolov9-c5/weights/best.pt --source assets/worlds-largest-selfie.jpg
```

Or if you want to use the trained model, download it from the above link and run the following command:

``` shell
python detect.py --weights best.pt --source assets/worlds-largest-selfie.jpg
```

## 🔗 Reference
* [YOLOv9](https://github.com/WongKinYiu/yolov9) - YOLOv9: Learning What You Want to Learn Using Programmable Gradient Information
* [WIDER FACE](http://shuoyang1213.me/WIDERFACE) - WIDER FACE: A Face Detection Benchmark
* [YOLO5Face](https://github.com/deepcam-cn/yolov5-face) - YOLO5Face: Why Reinventing a Face Detector
