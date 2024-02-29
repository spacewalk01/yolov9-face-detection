<h1 align="center"><span>YOLOv9 for Face Detection</span></h1>

<p align="center" margin: 0 auto;>
  <img src="assets/worlds-largest-selfie.jpg" />
</p>

## Pretrained Model
- 

## Data Preparation


## Training
``` shell
cd yolov9
python train_dual.py --workers 4 --device 0 --batch 4 --data ../widerface.yaml --img 640 --cfg models/detect/yolov9-c.yaml --weights '' --name yolov9-c --hyp hyp.scratch-high.yaml --min-items 0 --epochs 500 --close-mosaic 15
```

## Inference
``` shell
python detect.py --weights runs\train\yolov9-c5\weights\best.pt --source worlds-largest-selfie.jpg
```

## 🔗 Reference
* [YOLOv9](https://github.com/WongKinYiu/yolov9) - YOLOv9: Learning What You Want to Learn Using Programmable Gradient Information
