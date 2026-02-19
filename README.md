# 🚧 Real-Time Pothole Detection on Raspberry Pi 4 (YOLOv5n)

## 📌 Overview
This project implements real-time pothole detection using **YOLOv5n** deployed on a **Raspberry Pi 4**.  
The system is optimized for lightweight edge inference while maintaining acceptable FPS and high recall.

---

## 🎯 Objectives
- Train a lightweight YOLO model for pothole detection  
- Deploy on Raspberry Pi 4  
- Achieve >5 FPS real-time inference  
- Optimize using INT8 quantization (TFLite)  
- Maximize recall to avoid missing potholes  

---

## 🛠️ Hardware
- Raspberry Pi 4 (4GB)
- Pi Camera
- 32GB SD Card
- Heat sink

---

## 🧠 Model Details
- Model: **YOLOv5n**
- Input Size: 320x320
- Confidence Threshold: 0.2
- IoU Threshold: 0.45
- Training Format: `.pt`
- Deployment Format: `.tflite (INT8)`

---

## 📂 Project Structure

```
pothole-detection/
│
├── runs/
│   └── train/exp/weights/
│       ├── best.pt
│       └── last.pt
│
├── models/
│   ├── best.pt
│   └── best-int8.tflite
│
├── inference.py
├── export.py
├── requirements.txt
└── README.md
```

---

## 📊 Dataset
- Collected from Roboflow  
- Includes positive and negative images  
- Split into train / validation / test  

> Negative images improve robustness and reduce false positives.

---

## 🚀 Training

Clone YOLOv5:
```bash
git clone https://github.com/ultralytics/yolov5
cd yolov5
pip install -r requirements.txt
```

Train:
```bash
python train.py --img 320 --batch 16 --epochs 80 \
--data pothole.yaml \
--weights yolov5n.pt \
--name pothole_model
```

Best weights:
```
runs/train/exp/weights/best.pt
```

---

## 🔄 Export to TFLite (INT8)

```bash
python export.py --weights best.pt --include tflite --int8
```

Output:
```
best-int8.tflite
```

---

## 🖥️ Raspberry Pi Deployment

Install dependencies:
```bash
pip install opencv-python
pip install tflite-runtime
```

Run inference:
```bash
python inference.py
```

---

## ⚡Performance

| Model        | Device        | FPS      |
|--------------|---------------|----------|
| YOLOv5n      | Pi 4 (4GB)    | 4–6 FPS  |
| TFLite       | Pi 4 (4GB)    | 5–8 FPS  |
| INT8 TFLite  | Optimized     | 9-12 FPS  |

> Proper cooling improves sustained performance.

---

## 📈 Evaluation Focus
- High Recall - 0.712
- Balanced Precision - 0.803
- Strong mAP@0.5 - 0.778

Missing potholes is worse than detecting extra ones.

---

## 🔧 Optimizations Used
- YOLOv5n (Nano)
- 320x320 input resolution
- INT8 quantization
- Layer fusion
- Lightweight inference pipeline

---

## 🧪 Future Improvements
- Coral TPU acceleration  
- YOLOv8n comparison  
- GPS logging  
- Alert system integration  
- Cloud logging dashboard  

---

## 📌 Status
- Model trained ✅  
- Best weights obtained ✅  
- TFLite exported ✅  
- Deployed on Raspberry Pi ✅  
- FPS optimization ongoing 🔄  

---

## 📜 License
Academic / Research Use


