# 🧰 Tổng Hợp Công Cụ - N8N AI Assistant

> Tài liệu này liệt kê tất cả công cụ, API và dịch vụ sẽ tích hợp vào hệ thống.

---

## 📋 Mục Lục

1. [Nền tảng chính](#1-nền-tảng-chính)
2. [AI / LLM](#2-ai--llm)
3. [TTS - Text to Speech](#3-tts---text-to-speech)
4. [OCR - Nhận dạng chữ](#4-ocr---nhận-dạng-chữ)
5. [Image Generation](#5-image-generation)
6. [Video Generation](#6-video-generation)
7. [Storage & Database](#7-storage--database)
8. [Messaging](#8-messaging)

---

## 1. Nền Tảng Chính

### n8n (Automation Platform)

| Thuộc tính | Giá trị |
|------------|---------|
| **Loại** | Self-hosted (Docker) |
| **URL** | `http://localhost:5678` |
| **Vai trò** | Điều phối toàn bộ workflow |
| **Trạng thái** | ✅ Đã cài đặt |

---

## 2. AI / LLM

### Google Gemini API (Miễn phí)

| Thuộc tính | Giá trị |
|------------|---------|
| **Loại** | Cloud API |
| **Lấy API Key** | https://aistudio.google.com/apikey |
| **Model khuyến nghị** | `gemini-2.0-flash` (nhanh, miễn phí) |
| **Model backup** | `gemini-1.5-pro` (phức tạp hơn) |
| **Giới hạn miễn phí** | 15 requests/phút, 1500/ngày |
| **Vai trò** | Bộ não AI - phân tích, viết content |
| **Trạng thái** | ⏳ Chưa cấu hình |

**Các tác vụ sử dụng Gemini:**
- Phân tích intent từ tin nhắn Telegram
- Suy luận kênh đăng phù hợp
- Viết kịch bản, title, caption
- Tạo prompt cho image/video
- Hội thoại ngữ cảnh

---

## 3. TTS - Text to Speech

### 3.1 Valtec-TTS ⭐ (Khuyến nghị)

| Thuộc tính | Giá trị |
|------------|---------|
| **Loại** | Local (Python) |
| **GitHub** | https://github.com/tronghieuit/valtec-tts |
| **Ngôn ngữ** | Tiếng Việt |
| **Speakers** | `male`, `female` |
| **Yêu cầu** | Python 3.8+, GPU (tùy chọn) |
| **Cài đặt** | `pip install git+https://github.com/tronghieuit/valtec-tts.git` |
| **Trạng thái** | ⏳ Chưa cài |

**Code mẫu:**
```python
from valtec_tts import TTS

tts = TTS()  # Tự download model
tts.speak("Xin chào các bạn", speaker="female", output_path="output.wav")
```

**Ưu điểm:**
- ✅ Cài đặt đơn giản (1 dòng pip)
- ✅ 2 giọng male/female
- ✅ Điều chỉnh tốc độ
- ✅ Hỗ trợ GPU và CPU

---

### 3.2 VieNeu-TTS (Voice Cloning)

| Thuộc tính | Giá trị |
|------------|---------|
| **Loại** | Local (Python) |
| **GitHub** | https://github.com/pnnbao97/VieNeu-TTS |
| **Ngôn ngữ** | Tiếng Việt |
| **Tính năng đặc biệt** | Clone giọng từ audio mẫu |
| **Yêu cầu** | Python 3.12+, eSpeak NG, GPU NVIDIA (khuyến nghị) |
| **Trạng thái** | ⏳ Chưa cài |

**Yêu cầu cài đặt:**
1. eSpeak NG: https://github.com/espeak-ng/espeak-ng/releases
2. CUDA Toolkit (nếu dùng GPU)
3. Clone repo và chạy `uv sync`

**Ưu điểm:**
- ✅ Clone giọng nói tùy ý
- ✅ Chất lượng 24kHz
- ✅ Real-time inference

**Nhược điểm:**
- ❌ Cài đặt phức tạp hơn
- ❌ Cần GPU mạnh để tối ưu

---

### 3.3 NGHI-TTS (Browser-based)

| Thuộc tính | Giá trị |
|------------|---------|
| **Loại** | Web App (Node.js) |
| **GitHub** | https://github.com/nghimestudio/nghitts |
| **Ngôn ngữ** | Tiếng Việt |
| **Chạy trên** | Browser (Web Workers) |
| **Yêu cầu** | Node.js 18+ |
| **Cài đặt** | `npm install` → `npm run dev` |
| **Trạng thái** | ⏳ Chưa cài |

**Tính năng xử lý tiếng Việt:**
- Số → chữ (0 đến hàng tỷ)
- Ngày tháng, thời gian
- Tiền tệ (VND, USD)
- Phần trăm, số điện thoại

**Ưu điểm:**
- ✅ Không cần GPU
- ✅ Chạy 100% trên browser
- ✅ Xử lý text tiếng Việt tốt

**Nhược điểm:**
- ❌ Khó tích hợp API với n8n (browser-based)

---

## 4. OCR - Nhận Dạng Chữ

### PaddleOCR

| Thuộc tính | Giá trị |
|------------|---------|
| **Loại** | Local (Python) |
| **GitHub** | https://github.com/PaddlePaddle/PaddleOCR |
| **Ngôn ngữ hỗ trợ** | 100+ (có tiếng Việt) |
| **Cài đặt** | `pip install paddleocr` |
| **Trạng thái** | ⏳ Chưa cài |

**Tính năng:**
- OCR cơ bản (text từ ảnh)
- Table Recognition (nhận dạng bảng)
- Document Parser (PDF → Text)
- Layout Analysis (phân tích bố cục)

**Code mẫu:**
```python
from paddleocr import PaddleOCR

ocr = PaddleOCR(use_angle_cls=True, lang='vi')
result = ocr.ocr('image.png')

for line in result[0]:
    text = line[1][0]
    confidence = line[1][1]
    print(f"{text} ({confidence:.2%})")
```

**Ưu điểm:**
- ✅ Miễn phí, mạnh mẽ
- ✅ Hỗ trợ tiếng Việt tốt
- ✅ Nhiều tính năng nâng cao

---

## 5. Image Generation

### 5.1 Replicate API

| Thuộc tính | Giá trị |
|------------|---------|
| **Loại** | Cloud API |
| **Website** | https://replicate.com |
| **Models** | Flux, SDXL, Stable Diffusion |
| **Giá** | Pay-per-use (có free tier) |
| **Trạng thái** | ⏳ Chưa cấu hình |

### 5.2 Leonardo AI

| Thuộc tính | Giá trị |
|------------|---------|
| **Loại** | Cloud API |
| **Website** | https://leonardo.ai |
| **Free tier** | 150 credits/ngày |
| **Trạng thái** | ⏳ Chưa cấu hình |

### 5.3 Gemini Image Generation

| Thuộc tính | Giá trị |
|------------|---------|
| **Loại** | Cloud API (trong Gemini) |
| **Model** | `gemini-2.0-flash` với image output |
| **Giá** | Miễn phí (trong quota) |
| **Trạng thái** | ⏳ Chưa test |

---

## 6. Video Generation

### 6.1 Remotion (Programmatic Video)

| Thuộc tính | Giá trị |
|------------|---------|
| **Loại** | Local (Node.js) |
| **Website** | https://remotion.dev |
| **Tính năng** | Tạo video từ code React |
| **Phù hợp** | Video slide, infographic |
| **Trạng thái** | ⏳ Chưa cài |

### 6.2 FFmpeg

| Thuộc tính | Giá trị |
|------------|---------|
| **Loại** | Local CLI |
| **Tính năng** | Ghép ảnh + audio → video |
| **Trạng thái** | ⏳ Chưa cài |

### 6.3 Runway / Pika (AI Video)

| Thuộc tính | Giá trị |
|------------|---------|
| **Loại** | Cloud API |
| **Tính năng** | AI tạo video từ text/image |
| **Giá** | Trả phí |
| **Trạng thái** | ⏳ Tùy chọn sau |

---

## 7. Storage & Database

### 7.1 Google Sheets (Database đơn giản)

| Thuộc tính | Giá trị |
|------------|---------|
| **Loại** | Cloud |
| **Vai trò** | Lưu Accounts, Memory, Content |
| **Trạng thái** | ⏳ Chưa tạo |

**Các sheet cần tạo:**

| Sheet | Mục đích |
|-------|----------|
| `Accounts` | Thông tin các kênh (ngôn ngữ, hashtag, chuyên môn) |
| `Memory` | Lịch sử hội thoại (ngữ cảnh) |
| `Content` | Hàng đợi sản xuất (NEW → PLANNED → READY → DONE) |

### Google Drive (File Storage)

| Thuộc tính | Giá trị |
|------------|---------|
| **Loại** | Cloud |
| **Vai trò** | Lưu ảnh, video, audio đã render |
| **Trạng thái** | ⏳ Chưa cấu hình |

### 7.2 Supabase (PostgreSQL + Realtime)

| Thuộc tính | Giá trị |
|------------|---------|
| **Loại** | Cloud (hoặc Self-hosted) |
| **Website** | https://supabase.com |
| **Database** | PostgreSQL |
| **Tính năng** | Auth, Realtime, Storage, Edge Functions |
| **Free tier** | 500MB database, 1GB storage |
| **Trạng thái** | ⏳ Tùy chọn |

**Ưu điểm:**
- ✅ PostgreSQL mạnh mẽ, query phức tạp
- ✅ Realtime subscriptions
- ✅ Built-in Auth
- ✅ REST API tự động
- ✅ n8n có sẵn Supabase node

### 7.3 Firebase (Google) ⭐

| Thuộc tính | Giá trị |
|------------|---------|
| **Loại** | Cloud |
| **Website** | https://firebase.google.com |
| **Database** | Firestore (NoSQL) + Realtime Database |
| **Tính năng** | Auth, Hosting, Cloud Functions, Analytics |
| **Free tier** | Spark plan khá rộng rãi |
| **Trạng thái** | ⏳ Tùy chọn |

**Tính năng đặc biệt - Realtime Database:**
- 🔥 Sync data realtime giữa các client
- 🔥 Offline support (cache local)
- 🔥 Phù hợp cho: chat, notifications, live status

**Ưu điểm:**
- ✅ Realtime Database cực mạnh
- ✅ Tích hợp tốt với Google ecosystem
- ✅ n8n có sẵn Firebase Realtime Database node
- ✅ SDK cho mọi platform

**So sánh nhanh:**

| Tiêu chí | Sheets | Supabase | Firebase |
|----------|--------|----------|----------|
| Độ phức tạp | Thấp | Trung bình | Trung bình |
| Query | Giới hạn | SQL đầy đủ | NoSQL |
| Realtime | ❌ | ✅ | ✅✅ (rất mạnh) |
| Free tier | Unlimited | 500MB | Rộng rãi |
| n8n support | ✅ | ✅ | ✅ |

---

## 8. Messaging

### Telegram Bot

| Thuộc tính | Giá trị |
|------------|---------|
| **Loại** | Cloud API |
| **Tạo bot** | Nhắn @BotFather trên Telegram |
| **Vai trò** | Giao tiếp 2 chiều với người dùng |
| **Trạng thái** | ⏳ Chưa tạo |

**Các lệnh bot dự kiến:**
- `/start` - Bắt đầu
- `/status` - Xem tiến độ sản xuất
- `/list` - Danh sách nội dung
- Chat tự nhiên - AI xử lý

---

## 📊 Tổng Hợp Trạng Thái

| Công cụ | Loại | Trạng thái | Ưu tiên |
|---------|------|------------|---------|
| n8n | Platform | ✅ Đã cài | - |
| Google Gemini | AI/LLM | ⏳ Chưa cấu hình | 🔴 Cao |
| Valtec-TTS | TTS | ⏳ Chưa cài | 🟡 Trung bình |
| VieNeu-TTS | TTS | ⏳ Chưa cài | 🟢 Thấp |
| NGHI-TTS | TTS | ⏳ Chưa cài | 🟢 Thấp |
| PaddleOCR | OCR | ⏳ Chưa cài | 🟡 Trung bình |
| Replicate | Image Gen | ⏳ Chưa cấu hình | 🟡 Trung bình |
| Telegram Bot | Messaging | ⏳ Chưa tạo | 🔴 Cao |
| Google Sheets | Database | ⏳ Chưa tạo | 🔴 Cao |
| Google Drive | Storage | ⏳ Chưa cấu hình | 🟡 Trung bình |

---

## 🔗 Kiến Trúc Tích Hợp (Dự kiến)

```
┌─────────────────────────────────────────────────────────────┐
│                        TELEGRAM                              │
│                     (Giao tiếp người dùng)                   │
└─────────────────────────────────────────────────────────────┘
                              ↕
┌─────────────────────────────────────────────────────────────┐
│                          N8N                                 │
│                   (Điều phối trung tâm)                      │
└─────────────────────────────────────────────────────────────┘
        ↕              ↕              ↕              ↕
┌───────────┐  ┌───────────┐  ┌───────────┐  ┌───────────┐
│  GEMINI   │  │ LOCAL API │  │  SHEETS   │  │   DRIVE   │
│   (AI)    │  │ TTS + OCR │  │    (DB)   │  │ (Storage) │
└───────────┘  └───────────┘  └───────────┘  └───────────┘
                    ↑
        ┌───────────┴───────────┐
        │                       │
   ┌─────────┐            ┌─────────┐
   │Valtec   │            │Paddle   │
   │TTS      │            │OCR      │
   └─────────┘            └─────────┘
```

---

> 📝 **Ghi chú:** File này sẽ được cập nhật khi có thêm công cụ hoặc thay đổi trạng thái.
