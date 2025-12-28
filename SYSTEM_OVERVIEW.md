# 🤖 N8N AI SUPER ASSISTANT - TỔNG HỢP HỆ THỐNG

> Tài liệu tổng hợp toàn bộ chức năng, công cụ và kiến trúc hệ thống.

---

## 📋 MỤC LỤC

1. [Tổng quan hệ thống](#1-tổng-quan-hệ-thống)
2. [Chức năng cơ bản](#2-chức-năng-cơ-bản)
3. [Chức năng nâng cao](#3-chức-năng-nâng-cao)
4. [Công cụ & Dịch vụ](#4-công-cụ--dịch-vụ)
5. [Kiến trúc tổng thể](#5-kiến-trúc-tổng-thể)
6. [Ưu tiên triển khai](#6-ưu-tiên-triển-khai)

---

## 1. TỔNG QUAN HỆ THỐNG

### Tầm nhìn
Xây dựng **"Quản lý Kênh AI"** - một trợ lý thông minh qua Telegram:
- 🧠 Hiểu ngôn ngữ tự nhiên, ghi nhớ ngữ cảnh
- 📝 Tự động lên kế hoạch nội dung
- 🎬 Tự động sản xuất video/ảnh
- 📊 Theo dõi và báo cáo tiến độ
- 🤖 Tạo & vận hành Virtual KOL

### Nền tảng chính
- **n8n** (self-hosted Docker) - Điều phối workflow
- **Telegram Bot** - Giao tiếp với người dùng
- **Google Gemini** - Bộ não AI (miễn phí)

---

## 2. CHỨC NĂNG CƠ BẢN

| # | Chức năng | Mô tả |
|---|-----------|-------|
| 1 | **Hội thoại thông minh** | Hiểu ngôn ngữ tự nhiên, nhớ ngữ cảnh, hỏi lại khi cần |
| 2 | **Tạo ý tưởng nội dung** | "làm 5 video về AI" → thêm vào queue |
| 3 | **Suy luận kênh đăng** | Tự đề xuất kênh phù hợp với nội dung |
| 4 | **Xem tiến độ** | Status: NEW → PLANNED → READY → DONE |
| 5 | **Tìm & quản lý** | Tìm, sửa, xóa, đổi lịch nội dung |
| 6 | **Auto lên kế hoạch** | AI viết kịch bản, title, caption, hashtags |
| 7 | **Auto sản xuất** | TTS + Render ảnh/video |
| 8 | **Phê duyệt** | Duyệt trước khi đăng (tùy chọn) |
| 9 | **Báo cáo** | Thống kê tuần/tháng |
| 10 | **Cấu hình kênh** | Thêm/sửa thông tin kênh |

---

## 3. CHỨC NĂNG NÂNG CAO

| # | Chức năng | Mô tả | Công cụ chính |
|---|-----------|-------|---------------|
| 1 | **Video Processing** | Cắt, ghép, convert video | FFmpeg |
| 2 | **Video Remake** | Transcribe → Viết lại → Output mới | Whisper, Gemini |
| 3 | **Hot Post Analyzer** | Phân tích viral → Viết bài hay hơn | Firecrawl, Gemini |
| 4 | **Virtual KOL** | Influencer ảo với AI face | HeyGen/DeepFaceLive |
| 5 | **AI Video Gen** | Text/Image → Video | Google Veo 3 + NanoAI |
| 6 | **Tóm tắt tài liệu** | Upload file → AI đọc & tóm tắt | Gemini Vision |

### Chi tiết chức năng nâng cao:

#### 🎬 Video Remake
```
Link YouTube → Download → Transcribe + Vision → Viết lại → Video/Bài viết mới
```

#### 🔥 Hot Post Analyzer
```
Link bài hot → Scrape → Phân tích viral → Viết bài tương tự/chuyên sâu hơn
```

#### 🤖 Virtual KOL
```
AI Face + Video body → Face Swap → Đăng bài định kỳ như người thật
```

#### 🎥 AI Video Gen (Veo 3 + AUTO_VEO3)
```
Text prompt → Gemini (chia scene) → NanoAI API → Veo 3 → FFmpeg merge → Video hoàn chỉnh

AUTO_VEO3 Workflow (162K+ stars):
├── AI Agent tự động chia scene
├── Loop tạo nhiều clips
├── FFmpeg merge thành 1 video
└── Auto upload & cleanup
```

---

## 4. CÔNG CỤ & DỊCH VỤ

### 4.1 AI / LLM

| Công cụ | Loại | Chi phí | Vai trò |
|---------|------|---------|---------|
| **Google Gemini 2.0 Flash** | API | Miễn phí | Bộ não chính |
| **Google Gemini 1.5 Pro** | API | Miễn phí | Tác vụ phức tạp |
| **Gemini Vision** | API | Miễn phí | Phân tích hình ảnh |

### 4.2 TTS - Text to Speech (Tiếng Việt)

| Công cụ | Loại | Chi phí | Đặc điểm |
|---------|------|---------|----------|
| **Valtec-TTS** ⭐ | Local | Miễn phí | 2 giọng, dễ cài |
| **VieNeu-TTS** | Local | Miễn phí | Clone giọng |
| **NGHI-TTS** | Browser | Miễn phí | Chạy trên web |

### 4.3 Video Generation

| Công cụ | Loại | Chi phí | Đặc điểm |
|---------|------|---------|----------|
| **Google Veo 3** | API | ~50đ/video | Text/Image → Video |
| **NanoAI API** | API | ~50đ/video | Bypass reCaptcha |
| **FFmpeg** | Local | Miễn phí | Xử lý video |
| **Remotion** | Local | Miễn phí | Video từ code |

### 4.4 Face Swap

| Công cụ | Loại | Chi phí | Chất lượng |
|---------|------|---------|------------|
| **HeyGen** | Cloud | $$$ | ⭐⭐⭐⭐⭐ |
| **D-ID** | Cloud | $$ | ⭐⭐⭐⭐ |
| **DeepFaceLive** | Local | Miễn phí | ⭐⭐⭐⭐ |

### 4.5 OCR & Document

| Công cụ | Loại | Chi phí | Đặc điểm |
|---------|------|---------|----------|
| **PaddleOCR** | Local | Miễn phí | 100+ ngôn ngữ |
| **Unstructured.io** | Local | Miễn phí | Document parsing |

### 4.6 Database & Storage

| Công cụ | Loại | Chi phí | Đặc điểm |
|---------|------|---------|----------|
| **Google Sheets** | Cloud | Miễn phí | Đơn giản, dễ dùng |
| **Firebase Realtime DB** | Cloud | Miễn phí | Realtime sync |
| **Supabase** | Cloud | Miễn phí | PostgreSQL + Realtime |
| **Google Drive** | Cloud | Miễn phí | Lưu files |

### 4.7 Utilities

| Công cụ | Loại | Vai trò |
|---------|------|---------|
| **yt-dlp** | Local | Download video |
| **Whisper** | Local/API | Transcribe audio |
| **Firecrawl** | API | Scrape web content |
| **Serper API** | API | Search trends |

---

## 5. KIẾN TRÚC TỔNG THỂ

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                              NGƯỜI DÙNG                                      │
│                            (Telegram Bot)                                    │
└─────────────────────────────────────────────────────────────────────────────┘
                                    ↕
┌─────────────────────────────────────────────────────────────────────────────┐
│                               N8N BRAIN                                      │
│            (Workflow điều phối trung tâm - Docker localhost:5678)            │
└─────────────────────────────────────────────────────────────────────────────┘
         │              │              │              │              │
         ↓              ↓              ↓              ↓              ↓
┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐
│   GEMINI    │ │   LOCAL     │ │  DATABASE   │ │   STORAGE   │ │   SOCIAL    │
│    (AI)     │ │   TOOLS     │ │             │ │             │ │             │
├─────────────┤ ├─────────────┤ ├─────────────┤ ├─────────────┤ ├─────────────┤
│ • Gemini    │ │ • FFmpeg    │ │ • Sheets    │ │ • Drive     │ │ • YouTube   │
│ • Veo 3    │ │ • TTS       │ │ • Firebase  │ │ • R2        │ │ • TikTok    │
│ • Vision   │ │ • Whisper   │ │ • Supabase  │ │             │ │ • Facebook  │
│             │ │ • OCR       │ │             │ │             │ │ • Instagram │
└─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘
```

### Luồng xử lý chính:

```
👤 User gửi tin nhắn Telegram
         ↓
    [Đọc Memory + Accounts]
         ↓
    [Gemini phân tích Intent]
         ↓
    ┌────────────────────────────────────────────────────────┐
    │                    SWITCH INTENT                        │
    ├────────────────────────────────────────────────────────┤
    │ create_idea    → Thêm vào Content Sheet (NEW)          │
    │ find_content   → Tìm & trả về kết quả                  │
    │ check_status   → Báo cáo tiến độ                       │
    │ remake_video   → Bắt đầu quy trình Video Remake        │
    │ analyze_post   → Bắt đầu Hot Post Analyzer             │
    │ gen_video      → Gọi Veo 3 tạo video                   │
    │ clarify        → Hỏi lại cho rõ                        │
    │ general_chat   → Trả lời chung                         │
    └────────────────────────────────────────────────────────┘
         ↓
    [Lưu Memory + Gửi phản hồi Telegram]

========== BACKGROUND JOBS (Schedule) ==========

⏰ Mỗi 1 giờ: [WF-PLANNED]
   NEW → AI viết kịch bản → PLANNED

⏰ Mỗi 2 giờ: [WF-RENDER]  
   PLANNED → TTS + Video Gen → READY

⏰ Mỗi ngày: [WF-VIRTUAL-KOL]
   Calendar → Generate → Face Swap → Post
```

---

## 6. ƯU TIÊN TRIỂN KHAI

### Phase 1: MVP (Tuần 1-2) 🔴
> Mục tiêu: Bot hoạt động cơ bản

| # | Task | Công cụ |
|---|------|---------|
| 1 | Setup n8n Docker | n8n |
| 2 | Tạo Telegram Bot | @BotFather |
| 3 | Cấu hình Gemini API | Google AI Studio |
| 4 | Tạo Google Sheets (Accounts, Memory, Content) | Sheets |
| 5 | Workflow cơ bản: nhận tin → Gemini → trả lời | n8n |
| 6 | Thêm ý tưởng vào queue | n8n + Sheets |

### Phase 2: Auto Content (Tuần 3-4) 🟡
> Mục tiêu: Tự động lên kế hoạch và render

| # | Task | Công cụ |
|---|------|---------|
| 7 | Cài đặt Valtec-TTS | Python |
| 8 | Cài đặt FFmpeg | choco/apt |
| 9 | Workflow: NEW → PLANNED | n8n + Gemini |
| 10 | Workflow: PLANNED → READY (video slide) | n8n + TTS + FFmpeg |
| 11 | Upload Google Drive | n8n |

### Phase 3: Advanced Features (Tuần 5-6) 🟢
> Mục tiêu: Các tính năng nâng cao

| # | Task | Công cụ |
|---|------|---------|
| 12 | Video Remake workflow | yt-dlp, Whisper |
| 13 | Veo 3 integration | NanoAI API |
| 14 | Hot Post Analyzer | Firecrawl |
| 15 | Document summarizer | Gemini Vision |

### Phase 4: Virtual KOL (Tuần 7-8) 🟣
> Mục tiêu: Influencer ảo tự động

| # | Task | Công cụ |
|---|------|---------|
| 16 | Tạo AI face cố định | AI Image Gen |
| 17 | Thu thập video library | Quay/Stock |
| 18 | Face swap pipeline | HeyGen/DeepFaceLive |
| 19 | Auto posting schedule | n8n + Platform APIs |

---

## 📊 TỔNG HỢP CHI PHÍ

| Hạng mục | Chi phí/tháng | Ghi chú |
|----------|---------------|---------|
| **n8n** | $0 | Self-hosted |
| **Gemini API** | $0 | Free tier |
| **Google Sheets/Drive** | $0 | Free |
| **Valtec-TTS** | $0 | Local |
| **FFmpeg** | $0 | Local |
| **NanoAI (Veo 3)** | ~50k VND | ~1000 video |
| **Firebase** | $0 | Spark plan |
| **HeyGen (tùy chọn)** | $29-89 | Nếu cần face swap cloud |

**Tổng chi phí tối thiểu: ~50k VND/tháng** (chỉ Veo 3)

---

## 📁 CẤU TRÚC THƯ MỤC DỰ ÁN

```
e:\N8N Super Assistant\
├── 📄 TOOLS_INVENTORY.md        # Danh sách công cụ
├── 📄 FEATURES_AND_WORKFLOW.md  # Chức năng cơ bản
├── 📄 ADVANCED_FEATURES.md      # Chức năng nâng cao
├── 📄 SYSTEM_OVERVIEW.md        # File này - Tổng hợp
├── 📁 workflows/                # JSON workflows cho n8n
│   ├── 0.WF-Bot-Assistant.json
│   ├── 4.WF-PLANNED.json
│   ├── 5.WF-RENDER.json
│   └── 6.WF-VEO3.json
├── 📁 docs/                     # Tài liệu hướng dẫn
└── 📁 images/                   # Hình ảnh workflow
```

---

> 📝 **Ghi chú:** Tài liệu này sẽ được cập nhật khi có thêm tính năng hoặc thay đổi.
> 
> **Cập nhật lần cuối:** 2025-12-28
