# 🎙️ Audio Keyword Spotting (KWS) — Tiếng Việt

> **Môn học:** ELE1421 — Mạng Cảm Biến  
> **Học viện:** Công nghệ Bưu chính Viễn thông (PTIT) — Cơ sở TP.HCM  
> **Lớp:** D23CQCI01-N  
> **GVHD:** Hồ Nhựt Minh  

---

## 📌 Giới thiệu đề tài

Đề tài xây dựng hệ thống **nhận dạng từ khóa (Keyword Spotting)** cho 2 lệnh giọng nói tiếng Việt cơ bản là **"có"** và **"không"**, phục vụ cho ứng dụng điều khiển thiết bị thông minh trong hệ thống IoT/mạng cảm biến.

Hệ thống sử dụng đặc trưng **MFCC** kết hợp mô hình **CNN** được huấn luyện và triển khai trên nền tảng **Edge Impulse Studio**, hướng tới mục tiêu chạy trực tiếp trên thiết bị edge mà không cần kết nối Internet.

---

## 🎯 Mục tiêu

- Nhận dạng 2 từ khóa tiếng Việt: `"có"` và `"không"`
- Phân loại thêm 2 nhãn phụ: `"noise"` và `"unknown"`
- Đạt **F1-score > 0.90** cho 2 lệnh chính
- Triển khai mô hình dưới dạng **TensorFlow Lite** cho thiết bị edge

---

## 📊 Kết quả đạt được

### Validation Set

| Nhãn | F1-Score |
|------|----------|
| co | 0.95 |
| khong | 0.93 |
| unknown | 0.89 |
| noise | 0.88 |
| **Weighted F1** | **0.91** ✅ |

### Test Set (Float32)

| Nhãn | Accuracy | F1-Score |
|------|----------|----------|
| co | 100% | **1.00** 🏆 |
| khong | 100% | **1.00** 🏆 |
| unknown | 91.7% | 0.96 |
| noise | 92.3% | 0.92 |
| **Weighted F1** | **96%** | **0.98** ✅ |

> AUC-ROC = **1.00** trên tập test

---

## 🛠️ Công nghệ sử dụng

| Thành phần | Công nghệ |
|-----------|-----------|
| Nền tảng | [Edge Impulse Studio](https://studio.edgeimpulse.com) |
| Thu âm | Thiết bị di động kết nối Edge Impulse |
| Feature extraction | MFCC (Mel-Frequency Cepstral Coefficients) |
| Model | CNN (1D Convolutional Neural Network) |
| Output format | TensorFlow Lite Float32 |
| Sample rate | 16.000 Hz |
| Sample length | 1.000 ms |

---

## 📁 Cấu trúc thư mục

```
Audio-KWS-Vietnamese/
│
├── README.md                          # File mô tả dự án (file này)
│
├── report/
│   └── HoTen_final_cuoiky.docx        # Tiểu luận Word
│
├── slides/
│   └── HoTen_slide_cuoiky.pptx        # Slide thuyết trình
│
├── model/
│   └── kws_model.tflite               # Model TFLite xuất từ Edge Impulse
│
└── results/
    ├── feature_explorer.png           # Ảnh Feature Explorer (MFCC)
    ├── confusion_matrix_val.png       # Confusion matrix validation set
    ├── confusion_matrix_test.png      # Confusion matrix test set
    └── metrics.png                    # Bảng metrics kết quả
```

---

## 🔗 Edge Impulse Project

Project công khai trên Edge Impulse:  
👉 **https://studio.edgeimpulse.com/studio/1009314**

---

## ▶️ Cách tái tạo thực nghiệm

### Bước 1 — Tạo tài khoản Edge Impulse
Vào [studio.edgeimpulse.com](https://studio.edgeimpulse.com) → Đăng ký tài khoản miễn phí

### Bước 2 — Clone project (nếu có quyền)
Hoặc tạo project mới và làm theo các bước sau:

### Bước 3 — Thu thập dữ liệu
- Kết nối điện thoại qua QR code trong tab **Data Acquisition**
- Thu ~50 mẫu/nhãn cho 4 nhãn: `co`, `khong`, `noise`, `unknown`
- Sample length: 1000ms | Sample rate: 16kHz

### Bước 4 — Tạo Impulse
```
Time series input:  Window size = 1000ms, Stride = 500ms
Processing block:   Audio (MFCC) — cấu hình mặc định
Learning block:     Classification (Keras/CNN)
```

### Bước 5 — Generate Features
- Vào tab **MFCC** → **Save parameters** → **Generate features**

### Bước 6 — Train Model
```
Training cycles:  300
Learning rate:    0.001
Validation set:   20%
Model version:    Float32
```

### Bước 7 — Đánh giá & Export
- Tab **Model testing** → **Classify all** → xem kết quả
- Tab **Deployment** → **TensorFlow Lite (Float32)** → **Build** → Download

---

## 👤 Thành viên

| Họ và tên | MSSV | Lớp |
|-----------|------|-----|
| [Họ và tên sinh viên] | [MSSV] | D23CQCI01-N |

---

## 📚 Tài liệu tham khảo

1. P. Warden, *"Speech Commands: A Dataset for Limited-Vocabulary Speech Recognition,"* arXiv:1804.03209, 2018.
2. Y. Zhang et al., *"Hello Edge: Keyword Spotting on Microcontrollers,"* arXiv:1711.07128, 2017.
3. Edge Impulse Inc., *"Edge Impulse Documentation,"* 2024. https://docs.edgeimpulse.com
4. D. Banbury et al., *"Benchmarking TinyML Systems,"* arXiv:2003.04821, 2020.
5. TensorFlow Team, *"TFLite for Microcontrollers,"* Google, 2023. https://tensorflow.org/lite/microcontrollers

---

<p align="center">
  <b>PTIT HCM · ELE1421 Mạng Cảm Biến · 2026</b>
</p>
