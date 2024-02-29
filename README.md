<h1 align="center"><span>YOLOv9 for Face Detection</span></h1>

In this repo, I have trained yolov9-c on the WIDER face dataset. The WIDER dataset comprises of more than 30k images with more than 390k faces, each with bouding box and other various label formats.


<p align="center" margin: 0 auto;>
  <img src="assets/result.jpg" />
</p>

## 🛠️ Installation
Clone this repo and install YOLOv9. 
```
# Clone
git clone https://github.com/spacewalk01/yolov9-face-detection
cd yolov9-face-detection/yolov9
pip install -r requirements.txt
```

## Pretrained Model
- Download the pretrained yolov9-c.pt model from [google drive](https://drive.google.com/file/d/15K4e08lcZiiQrXmdsnm2BhcoNS3MOMmx/view?usp=sharing). Note that this model was trained on wider dataset for 240 epoches.

## Data Preparation
Dataset structure:
```
${ROOT}
└── yolov9
└── dataset/    
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
```

1. Download [WIDER-FACE](http://shuoyang1213.me/WIDERFACE) datasets.
2. Download annotation files from [google drive](https://drive.google.com/file/d/1tU_IjyOwGQfGNUvZGwWWM4SwxKp2PUQ8/view?usp=sharing).

```shell
cd data
python train2yolo.py datasets/original-widerface/train [datasets/widerface/train]
python val2yolo.py  datasets/original-widerface [datasets/widerface/val]
```

## Training
``` shell
cd yolov9
python train_dual.py --workers 4 --device 0 --batch 4 --data ../widerface.yaml --img 640 --cfg models/detect/yolov9-c.yaml --weights '' --name yolov9-c --hyp hyp.scratch-high.yaml --min-items 0 --epochs 500 --close-mosaic 15
```

## Inference
``` shell
python detect.py --weights runs/train/yolov9-c5/weights/best.pt --source assets/worlds-largest-selfie.jpg
```

## 🔗 Reference
* [YOLOv9](https://github.com/WongKinYiu/yolov9) - YOLOv9: Learning What You Want to Learn Using Programmable Gradient Information
* [WIDER FACE](http://shuoyang1213.me/WIDERFACE) - WIDER FACE: A Face Detection Benchmark
