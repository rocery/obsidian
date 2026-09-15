CONVEYOR
══════════════════════════════════════►

              ┌──────────────┐
              │ LED LIGHTING │
              └──────────────┘

                    CAMERA
                       ↓
                       ↓
                 ┌──────────┐
                 │   BOX    │
                 └──────────┘
                       │
                       ▼
                 YOLO Detection
                       │
                       ▼
                    Tracker
                       │
                       ▼
                 Product Class
                       │
                 ┌─────┴─────┐
                 ▼           ▼
              Color         OCR
                 │           │
                 └─────┬─────┘
                       ▼
                 Product ID
                       │
                       ▼
                  COUNT LINE
                       │
                       ▼
                    Counter

YOLO
  +
Object Tracking
  +
Visual Classification
  +
OCR sebagai verification
  +
Counting Line

Apa metode ini masuk akal:  
YOLO = tolov8n
Object Tracking = Samakan seperti project sebelumnya
Visual Classification = EfficientNet-B0 atau ResNet18/34?
OCR sebagai verification = PaddleOCR
Counting Line


Detection : YOLOv8n Tracking : ByteTrack Classification: EfficientNet-B0 OCR : PaddleOCR Counting : Virtual Line + Track ID CV Framework : Python + OpenCV Inference : PyTorch / ONNX Runtime API : FastAPI Database : MySQL Dashboard : Laravel + Filament

EfficientNet-B0 cocok karena relatif ringan untuk CPU dibanding model classifier yang lebih besar.

Saya akan menggunakan **transfer learning**, bukan melatih EfficientNet-B0 dari nol.