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

```
# from paddleocr import PaddleOCR

  

# # Uses PP-OCRv6 models by default

# ocr = PaddleOCR(

#     use_doc_orientation_classify=False, # Disables document orientation classification model via this parameter

#     use_doc_unwarping=False, # Disables text image rectification model via this parameter

#     use_textline_orientation=False, # Disables text line orientation classification model via this parameter

# )

# ocr = PaddleOCR(lang="en") # Uses English model by specifying language parameter

# # ocr = PaddleOCR(ocr_version="PP-OCRv6") # Switches to PP-OCRv6 version via ocr_version parameter

# # ocr = PaddleOCR(ocr_version="PP-OCRv4") # Switches to PP-OCRv4 version via ocr_version parameter

# # ocr = PaddleOCR(device="gpu") # Enables GPU acceleration for model inference via device parameter

# ocr = PaddleOCR(

#     # text_detection_model_name="PP-OCRv5_mobile_det",

#     # text_recognition_model_name="PP-OCRv5_mobile_rec",

#     use_doc_orientation_classify=False,

#     use_doc_unwarping=False,

#     use_textline_orientation=False,

# ) # Switch to PP-OCRv6 mobile models

# ocr = PaddleOCR(enable_mkldnn=False)

# result = ocr.predict("e.jpg")  

# for res in result:  

#     res.print()  

#     res.save_to_img("output")  

#     res.save_to_json("output")

from paddleocr import PaddleOCR

  

ocr = PaddleOCR(

    enable_mkldnn=False,

    lang="id",

  

    # Disable document preprocessing

    use_doc_orientation_classify=False,

    use_doc_unwarping=False,

  

    # Disable text-line orientation

    use_textline_orientation=False,

)

  

output = ocr.predict("b.png")

  

for res in output:

    res.print()

    res.save_to_img("output")  

    res.save_to_json("output")
```