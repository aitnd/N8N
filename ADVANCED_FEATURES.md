# 🚀 Chức Năng Nâng Cao - N8N AI Assistant

> Bổ sung các tính năng advanced cho hệ thống content automation.

---

## 📋 Tổng Quan Chức Năng Mới

| # | Chức năng | Mô tả |
|---|-----------|-------|
| 1 | **Video Processing** | Xử lý video với FFmpeg |
| 2 | **Video Remake** | Transcribe video → Viết lại → Tạo version mới |
| 3 | **Hot Post Analyzer** | Phân tích bài hot → Viết bài tương tự/chuyên sâu |
| 4 | **Virtual KOL** | Tạo influencer ảo với AI face |
| 5 | **AI Video Gen (Veo 3)** | Text/Image → Video bằng Google Veo 3 |

---

## 1️⃣ VIDEO PROCESSING (FFmpeg)

### Công cụ: FFmpeg

| Thuộc tính | Giá trị |
|------------|---------|
| **Loại** | Local CLI |
| **Tính năng** | Cắt, ghép, convert, extract audio |
| **Cài đặt** | `choco install ffmpeg` (Windows) |

### Các thao tác FFmpeg trong hệ thống:

```
┌─────────────────────────────────────────────────────────┐
│                    FFmpeg Tasks                          │
├─────────────────────────────────────────────────────────┤
│ • Extract audio từ video (cho transcription)            │
│ • Ghép ảnh + audio → Video slide                        │
│ • Thêm subtitle vào video                               │
│ • Resize/compress video cho các platform                │
│ • Cắt video theo timestamp                              │
│ • Ghép nhiều video clips                                │
│ • Extract frames từ video (cho AI analysis)             │
└─────────────────────────────────────────────────────────┘
```

---

## 2️⃣ VIDEO REMAKE (Content Repurposing)

### Mô tả
Lấy video từ link → Hiểu toàn bộ nội dung → Viết lại theo phong cách riêng → Output video/bài viết

### Luồng hoạt động

```
┌─────────────────────────────────────────────────────────────────────┐
│                        VIDEO REMAKE FLOW                             │
└─────────────────────────────────────────────────────────────────────┘

👤 User: "Remake video này: [YouTube link]"
                    ↓
┌─────────────────────────────────────────────────────────────────────┐
│ BƯỚC 1: DOWNLOAD & EXTRACT                                          │
│ ├── yt-dlp download video                                           │
│ ├── FFmpeg extract audio → audio.mp3                                │
│ └── FFmpeg extract frames → frames/*.jpg (mỗi 5 giây)               │
└─────────────────────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────────────────────┐
│ BƯỚC 2: TRANSCRIPTION & VISION                                      │
│ ├── Whisper/Gemini transcribe audio → text                          │
│ └── Gemini Vision phân tích từng frame → mô tả hình ảnh             │
└─────────────────────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────────────────────┐
│ BƯỚC 3: AI UNDERSTANDING                                            │
│ ├── Kết hợp transcript + image descriptions                         │
│ ├── Gemini tóm tắt nội dung chính                                   │
│ ├── Xác định: chủ đề, key points, tone, style                       │
│ └── Output: Content Blueprint                                        │
└─────────────────────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────────────────────┐
│ BƯỚC 4: AI REWRITE                                                   │
│ ├── Viết lại nội dung với góc nhìn/phong cách mới                   │
│ ├── Thêm insights, ví dụ riêng                                      │
│ ├── Điều chỉnh ngôn ngữ (tiếng Việt/Anh)                            │
│ └── Tạo: script mới, caption, hashtags                              │
└─────────────────────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────────────────────┐
│ BƯỚC 5: OUTPUT (User chọn)                                          │
│ ├── Option A: VIDEO                                                  │
│ │   ├── TTS tạo voice từ script                                     │
│ │   ├── AI tạo hình ảnh mới (hoặc dùng stock)                       │
│ │   └── FFmpeg ghép → video hoàn chỉnh                              │
│ │                                                                    │
│ └── Option B: BÀI VIẾT                                               │
│     ├── Format bài blog/social post                                  │
│     └── Thêm hình ảnh minh họa                                       │
└─────────────────────────────────────────────────────────────────────┘
```

### Công cụ cần thiết

| Công cụ | Vai trò | Loại |
|---------|---------|------|
| **yt-dlp** | Download video | Local CLI |
| **FFmpeg** | Extract audio/frames | Local CLI |
| **Whisper** | Transcribe audio | Local/API |
| **Gemini Vision** | Phân tích hình ảnh | API |
| **Gemini** | Viết lại nội dung | API |
| **TTS (Valtec)** | Tạo voice mới | Local |
| **Image Gen** | Tạo hình minh họa | API |

### Ví dụ sử dụng

```
👤: Remake video này thành tiếng Việt: https://youtube.com/watch?v=xxx

🤖: Em đang xử lý video (5 phút)...
    ✅ Download xong
    ✅ Transcribe xong (12 phút nội dung)
    ✅ Phân tích hình ảnh xong (45 frames)
    
    📋 TÓM TẮT VIDEO GỐC:
    • Chủ đề: 10 AI Tools giúp tăng năng suất
    • Tone: Casual, friendly
    • Key points: [danh sách]
    
    Bạn muốn:
    1️⃣ Tạo video mới (tiếng Việt)
    2️⃣ Viết bài blog
    3️⃣ Cả hai

👤: 1

🤖: ✅ Đã tạo video mới!
    📎 Link: [Google Drive]
    ⏱️ Thời lượng: 8 phút
    🎤 Voice: Female Vietnamese
```

---

## 3️⃣ HOT POST ANALYZER (Trend Hijacking)

### Mô tả
Phân tích bài đang viral → Viết bài tương tự hoặc chuyên sâu hơn

### Luồng hoạt động

```
┌─────────────────────────────────────────────────────────────────────┐
│                      HOT POST ANALYZER FLOW                          │
└─────────────────────────────────────────────────────────────────────┘

👤 User: "Phân tích post này: [link]" 
         hoặc "Tìm trend về AI tuần này"
                    ↓
┌─────────────────────────────────────────────────────────────────────┐
│ BƯỚC 1: SCRAPE & EXTRACT                                            │
│ ├── Firecrawl/Playwright lấy nội dung                               │
│ ├── Extract: text, images, engagement metrics                       │
│ └── Lưu raw data                                                     │
└─────────────────────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────────────────────┐
│ BƯỚC 2: AI ANALYSIS                                                  │
│ ├── Phân tích tại sao bài này viral                                 │
│ ├── Xác định: hook, format, emotional triggers                      │
│ ├── Đánh giá độ sâu nội dung                                        │
│ └── Tìm gaps (thiếu sót trong bài gốc)                              │
└─────────────────────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────────────────────┐
│ BƯỚC 3: CONTENT STRATEGY                                            │
│ User chọn:                                                           │
│ ├── Option A: SIMILAR - Viết bài tương tự, góc nhìn khác            │
│ ├── Option B: DEEP DIVE - Viết chuyên sâu hơn bài gốc               │
│ ├── Option C: COUNTER - Viết bài phản biện/góc nhìn đối lập         │
│ └── Option D: SERIES - Tạo series nhiều bài từ chủ đề               │
└─────────────────────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────────────────────┐
│ BƯỚC 4: GENERATE CONTENT                                            │
│ ├── AI viết nội dung theo strategy đã chọn                          │
│ ├── Tạo hook mạnh (học từ bài gốc)                                  │
│ ├── Thêm data, ví dụ, insights mới                                  │
│ └── Format phù hợp platform                                          │
└─────────────────────────────────────────────────────────────────────┘
```

### Công cụ cần thiết

| Công cụ | Vai trò |
|---------|---------|
| **Firecrawl** | Scrape web content (có API) |
| **Playwright** | Browser automation (backup) |
| **Gemini** | Phân tích & viết content |
| **Serper API** | Tìm trending topics |

### Ví dụ sử dụng

```
👤: Phân tích post này và viết bài hay hơn: [LinkedIn link]

🤖: 📊 PHÂN TÍCH BÀI GỐC:
    
    📈 Engagement: 5.2K likes, 342 comments
    🎯 Hook: "Tôi đã mất 3 năm để học điều này..."
    💡 Nội dung: 5 tips về AI productivity
    ⚠️ Gaps: 
       - Thiếu ví dụ cụ thể
       - Không có data backup
       - Tips quá chung chung
    
    Bạn muốn:
    1️⃣ Viết bài tương tự (góc nhìn khác)
    2️⃣ Viết chuyên sâu hơn (thêm case studies)
    3️⃣ Tạo series 5 bài chi tiết

👤: 2

🤖: ✅ Đã tạo bài viết chuyên sâu!
    
    📝 Title: "10 AI Tools Tôi Dùng Hàng Ngày (Với Data Thực Tế)"
    📊 Độ dài: 2,500 từ
    🖼️ Kèm 8 hình minh họa
    
    [Preview bài viết...]
    
    Đăng lên kênh nào?
```

---

## 4️⃣ VIRTUAL KOL (AI Influencer)

### Mô tả
Tạo một nhân vật ảo với khuôn mặt AI cố định, sử dụng video body doubles, đăng bài định kỳ như người thật

### Kiến trúc

```
┌─────────────────────────────────────────────────────────────────────┐
│                      VIRTUAL KOL SYSTEM                              │
└─────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────┐
│ IDENTITY LAYER (Nhận diện thương hiệu)                              │
│ ├── AI Generated Face (cố định)                                     │
│ ├── Persona: tên, tính cách, style nói                              │
│ ├── Voice: clone voice riêng                                        │
│ └── Visual style: màu sắc, filter, aesthetic                        │
└─────────────────────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────────────────────┐
│ CONTENT LIBRARY (Thư viện nội dung gốc)                             │
│ ├── Dancing videos (người thật làm mẫu)                             │
│ ├── Talking head templates                                          │
│ ├── Daily life clips (đi cafe, làm việc, workout...)                │
│ └── Reaction clips                                                   │
└─────────────────────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────────────────────┐
│ FACE SWAP ENGINE                                                     │
│ ├── Option 1: HeyGen (Cloud API) ⭐                                 │
│ ├── Option 2: D-ID (Cloud API)                                      │
│ ├── Option 3: DeepFaceLive (Local, free)                            │
│ └── Option 4: Roop/FaceFusion (Local, free)                         │
└─────────────────────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────────────────────┐
│ CONTENT GENERATION                                                   │
│ ├── AI viết script (Gemini)                                         │
│ ├── Voice synthesis (TTS + Voice Clone)                             │
│ ├── Lip sync (nếu có dialog)                                        │
│ └── Background music/effects                                         │
└─────────────────────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────────────────────┐
│ SCHEDULING & POSTING                                                 │
│ ├── Content calendar (tự động lên lịch)                             │
│ ├── Status posts (AI viết)                                          │
│ ├── Story/Reel posts                                                 │
│ ├── Engagement (reply comments - tùy chọn)                          │
│ └── Analytics tracking                                               │
└─────────────────────────────────────────────────────────────────────┘
```

### Công cụ Face Swap

| Công cụ | Loại | Giá | Chất lượng |
|---------|------|-----|------------|
| **HeyGen** | Cloud | $$$ | ⭐⭐⭐⭐⭐ |
| **D-ID** | Cloud | $$ | ⭐⭐⭐⭐ |
| **DeepFaceLive** | Local | Free | ⭐⭐⭐⭐ |
| **Roop/FaceFusion** | Local | Free | ⭐⭐⭐ |
| **Akool AI** | Cloud | $$ | ⭐⭐⭐⭐ |

### Loại content cho Virtual KOL

| Loại | Mô tả | Độ khó |
|------|-------|--------|
| **Status text** | Caption + ảnh AI | 🟢 Dễ |
| **Photo posts** | Ảnh AI generated | 🟢 Dễ |
| **Talking head** | Video nói chuyện | 🟡 Trung bình |
| **Dance/Trend** | Face swap lên video nhảy | 🟡 Trung bình |
| **Daily vlog** | Ghép mặt vào hoạt động | 🔴 Khó |
| **Live stream** | Real-time face swap | 🔴 Rất khó |

### Ví dụ Calendar KOL

```
┌─────────────────────────────────────────────────────────────────────┐
│                    WEEKLY CONTENT CALENDAR                           │
├─────────────────────────────────────────────────────────────────────┤
│ THỨ 2: Status buổi sáng + ảnh cafe                                  │
│ THỨ 3: Video tips ngắn (30s talking head)                           │
│ THỨ 4: Story behind-the-scenes                                      │
│ THỨ 5: Reel dance/trend                                             │
│ THỨ 6: Post chia sẻ kiến thức                                       │
│ THỨ 7: Video dài (3-5 phút)                                         │
│ CN:    Status cuối tuần + tương tác followers                       │
└─────────────────────────────────────────────────────────────────────┘
```

### Workflow trong n8n

```
[Schedule Trigger: 8:00 AM hàng ngày]
            ↓
[Check content calendar: Hôm nay đăng gì?]
            ↓
[Gemini: Viết caption/script phù hợp ngày]
            ↓
[Chọn video template từ library]
            ↓
[Face Swap API: Gắn mặt AI vào video]
            ↓
[TTS: Tạo voice (nếu cần)]
            ↓
[FFmpeg: Ghép hoàn chỉnh]
            ↓
[Upload lên platform]
            ↓
[Telegram: Thông báo đã đăng]
```

---

## 5️⃣ AI VIDEO GENERATION (Google Veo 3)

### Mô tả
Tạo video AI từ text prompt hoặc image bằng Google Veo 3, tự động bypass reCaptcha

### Nguồn tham khảo
- Workflow: [workflowfree.com](https://workflowfree.com/quy-trinh-tu-dong-hoa-text-to-video-veo-3-1-mien-phi-tu-dong-giai-recaptcha-google/)
- Template: [Download JSON](https://drive.google.com/file/d/14IAKYYPC7l62ufqcROZvCALZo4nVsmO4/view)

### 📦 Workflow JSON Mẫu Có Sẵn

Trong thư mục dự án đã có 2 file workflow JSON sẵn sàng import:

#### 1️⃣ `Lấy authorization Flow.json`

**Mục đích:** Lấy Google Authorization token để sử dụng cho Veo 3

**Luồng xử lý:**
```
[Webhook POST /get-authorization]
        ↓
[Edit Fields] - Trích xuất: name, email, expires, Authorization
        ↓
[Google Sheets Append] - Lưu token vào bảng tính
```

**Cách sử dụng:**
1. Import workflow vào n8n
2. Cài extension [Multi Webhook Sender](https://chromewebstore.google.com/detail/multi-webhook-sender-send/kbkfglmdbbkppnmojdmpndadegmlhhkb)
3. Truy cập: https://labs.google/fx/api/auth/session
4. Dùng extension gửi data về webhook n8n
5. Token được lưu vào Google Sheets

**Sheet mẫu:** [Tại đây](https://docs.google.com/spreadsheets/d/1_egUcHLDKNJdw0LFg4eoRetwCvvR3tG4SV8vZFvXQzQ/edit)

---

#### 2️⃣ `nanoai.pics pass captcha text to video 3.1 (update 26.12).json`

**Mục đích:** Tạo video với Google Veo 3, bypass reCaptcha qua NanoAI

**Setup cần thiết:**
| Parameter | Mô tả |
|-----------|-------|
| `projectId` | Project ID từ Google Cloud |
| `flow_auth_token` | Authorization token (từ workflow trên) |
| `prompt` | Mô tả video muốn tạo |
| `Token Apikey nanoai` | API key từ nanoai.pics |

**Models & Aspect Ratios:**

| Loại tài khoản | Model | Aspect Ratio |
|----------------|-------|--------------|
| **Gemini PRO - Landscape** | `veo_3_1_t2v_fast` | `VIDEO_ASPECT_RATIO_LANDSCAPE` |
| **Gemini PRO - Portrait** | `veo_3_1_t2v_fast_portrait` | `VIDEO_ASPECT_RATIO_PORTRAIT` |
| **Gemini ULTRA - Landscape** | `veo_3_1_t2v_fast_ultra` | `VIDEO_ASPECT_RATIO_LANDSCAPE` |
| **Gemini ULTRA - Portrait** | `veo_3_1_t2v_fast_portrait_ultra` | `VIDEO_ASPECT_RATIO_PORTRAIT` |

**Luồng xử lý:**
```
[Manual Trigger]
        ↓
[Setup First] - Nhập projectId, token, prompt, model, aspectRatio
        ↓
[HTTP Request2] - Gửi request tạo video đến NanoAI API
        ↓
[HTTP Request3] - Lấy task status
        ↓
[If1] - Kiểm tra message = "successfully"?
  ├── Yes → [HTTP Request4] - Gọi Google API kiểm tra status
  └── No  → [Wait] → Loop lại HTTP Request3
        ↓
[Wait1 - 15s] - Chờ video render
        ↓
[Switch] - Kiểm tra status
  ├── FAILED → [Stop and Error]
  ├── SUCCESSFUL → [HTTP Request5] - Download video
  └── ACTIVE → Loop lại HTTP Request4
        ↓
[Edit Fields1] - Lấy remainingCredits
        ↓
[Merge] - Gộp video + credits info
```

**Status codes:**
- `MEDIA_GENERATION_STATUS_ACTIVE` - Đang xử lý
- `MEDIA_GENERATION_STATUS_SUCCESSFUL` - Thành công
- `MEDIA_GENERATION_STATUS_FAILED` - Thất bại

---

### Hướng dẫn lấy Authorization & Project ID

> Xem chi tiết: [workflowfree.com/huong-dan-lay-authorization](https://workflowfree.com/huong-dan-lay-authorization-va-project_id-cho-quy-trinh-tu-dong-hoa-tao-video-voi-google-veo-3-1/)

### Công cụ sử dụng

| Công cụ | Vai trò | Chi phí |
|---------|---------|---------|
| **n8n** | Điều phối workflow | Free (self-host) |
| **NanoAI API** | Bypass reCaptcha Google | ~50đ/video |
| **Google Veo 3** | AI tạo video | Free (qua NanoAI) |

### Luồng hoạt động

```
┌─────────────────────────────────────────────────────────────────────┐
│                    TEXT-TO-VIDEO VEO 3 FLOW                          │
└─────────────────────────────────────────────────────────────────────┘

👤 User: "Tạo video: Một người đang code n8n workflow"
                    ↓
┌─────────────────────────────────────────────────────────────────────┐
│ BƯỚC 1: SETUP PARAMETERS                                            │
│ ├── projectId (từ Google Cloud)                                     │
│ ├── Token (từ nanoai.pics)                                          │
│ └── prompt (mô tả video muốn tạo)                                   │
└─────────────────────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────────────────────┐
│ BƯỚC 2: GỬI YÊU CẦU TẠO VIDEO                                       │
│ ├── HTTP Request → NanoAI API                                       │
│ ├── NanoAI tự động bypass reCaptcha (90%+ success rate)             │
│ └── Nhận video generation ID                                         │
└─────────────────────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────────────────────┐
│ BƯỚC 3: POLLING STATUS                                              │
│ ├── Loop: Kiểm tra trạng thái video                                 │
│ ├── Nếu processing → chờ → kiểm tra lại                             │
│ └── Nếu success → lấy URL video                                      │
└─────────────────────────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────────────────────────┐
│ BƯỚC 4: OUTPUT                                                       │
│ ├── Download video từ URL                                            │
│ ├── Upload lên Google Drive/Storage                                  │
│ └── Gửi link về Telegram                                             │
└─────────────────────────────────────────────────────────────────────┘
```

### Cách lấy Token NanoAI

1. Tạo tài khoản: https://nanoai.pics
2. Truy cập: https://nanoai.pics/account
3. Copy token từ trang account
4. Dán vào node "Setup First" trong n8n

### Workflow nodes

```
[Manual Trigger]
      ↓
[Setup First] ─── projectId, Token, prompt
      ↓
[HTTP Request2] ─── Gửi yêu cầu tạo video
      ↓
[HTTP Request3] ─── Lấy trạng thái
      ↓
[If] ─── Kiểm tra success?
  ├── Yes → [HTTP Request5] → Lấy URL video
  └── No  → [Wait] → [HTTP Request4] → Loop lại
```

### Ví dụ sử dụng

```
👤: Tạo video AI: "Một cô gái đang làm việc với laptop trong quán cafe, 
     ánh nắng chiếu qua cửa sổ, cinematic style"

🤖: 🎬 Đang tạo video với Veo 3...
    ⏳ Ước tính: 2-5 phút
    
    ... (2 phút sau) ...
    
    ✅ Video đã sẵn sàng!
    📎 Link: [Google Drive URL]
    ⏱️ Độ dài: 8 giây
    🎥 Chất lượng: 1080p
    
    Bạn muốn:
    1️⃣ Tạo thêm video khác
    2️⃣ Thêm nhạc nền
    3️⃣ Ghép với video khác
```

### Tích hợp với các chức năng khác

| Kết hợp với | Use case |
|-------------|----------|
| **Video Remake** | Tạo video mới từ script đã viết lại |
| **Virtual KOL** | Tạo background/b-roll cho video KOL |
| **Hot Post** | Tạo video minh họa cho bài viết |
| **TTS** | Kết hợp Veo video + voice-over tiếng Việt |

### Chi phí ước tính

| Số lượng | Chi phí NanoAI |
|----------|----------------|
| 10 video/ngày | ~500đ/ngày |
| 100 video/tháng | ~5,000đ/tháng |
| 1000 video/tháng | ~50,000đ/tháng |

> [!TIP]
> Chi phí rất rẻ so với các dịch vụ AI video khác (Runway, Pika thường $10-50/tháng)

---

### 🚀 AUTO_VEO3 - Workflow Nâng Cao (162K+ stars)

Workflow tự động hóa hoàn chỉnh với nhiều tính năng nâng cao:

#### Yêu cầu chuẩn bị:
1. **Kiểm tra FFmpeg** đã cài đặt
2. **Tạo thư mục** `/files/outputvideo` (lưu video về VPS)
3. **Copy Sheet mẫu** từ template có sẵn

#### Luồng xử lý chi tiết:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         AUTO_VEO3 COMPLETE WORKFLOW                          │
└─────────────────────────────────────────────────────────────────────────────┘

[Schedule Trigger] → [Thiết Lập] → [Limit] → [Set Cookie] → [Create Token]
                                                                    ↓
                                                            [Check Token]
                                                                    ↓
[Create Project] → [Update Queue] → [Create Folder] → [Check prompt]
                                                                    ↓
┌─────────────────────────────────────────────────────────────────────────────┐
│                        AI AGENT (Google Gemini)                              │
│  ├── Tách Scene (chia nhỏ nội dung)                                         │
│  ├── Tạo Scenario (kịch bản từng cảnh)                                      │
│  ├── Tổng hợp Input (gộp thông tin)                                         │
│  └── Tách Input (chuẩn bị cho loop)                                         │
└─────────────────────────────────────────────────────────────────────────────┘
                                    ↓
┌─────────────────────────────────────────────────────────────────────────────┐
│                           LOOP GENERATION                                    │
│  [Loop Over Items] ──────────────────────────────────────────────────       │
│        ↓                                                                     │
│  [Nếu "Create"] → [Check Status] → [STATUS_SUCCESS?]                        │
│        ↓                    ↓              ↓                                 │
│  [Upload Prompt Veo]   [Wait 10s]    [IFS → Set id file]                    │
│                                            ↓                                 │
│                              [Split Out4] → [HTTP Request9]                  │
│                                            ↓                                 │
│                              [Upload file] → [Thành Công ✅]                 │
└─────────────────────────────────────────────────────────────────────────────┘
                                    ↓
┌─────────────────────────────────────────────────────────────────────────────┐
│                            MERGE VIDEO (FFmpeg)                              │
│  [IF2] → [Read/Write Files from Disk] → [Execute Command]                   │
│                                            ↓                                 │
│                [Read/Write Files] → [Upload file] → [Update link]           │
│                                            ↓                                 │
│                                      [Delete mp4] (cleanup)                  │
└─────────────────────────────────────────────────────────────────────────────┘
```

#### Tính năng nổi bật:

| Tính năng | Mô tả |
|-----------|-------|
| **AI Scene Splitting** | Gemini tự động chia prompt thành nhiều scene |
| **Auto Token Management** | Tạo và refresh token tự động |
| **Batch Generation** | Loop tạo nhiều video clips |
| **Status Polling** | Kiểm tra đến khi thành công |
| **Video Merging** | FFmpeg ghép nhiều clips thành 1 video |
| **Auto Upload** | Upload lên storage sau khi hoàn thành |
| **Auto Cleanup** | Xóa file tạm sau khi upload |
| **Schedule Trigger** | Chạy tự động theo lịch |

#### Use case:

```
👤: "Tạo video dài 1 phút về hành trình học n8n"

🤖: AI Agent tự động:
    1. Chia thành 8 scenes (mỗi scene ~8 giây)
    2. Tạo prompt chi tiết cho từng scene
    3. Loop tạo 8 video clips
    4. Ghép thành 1 video hoàn chỉnh
    5. Upload & gửi link
```

---

## 📊 Tổng Hợp Công Cụ Mới Cần Thêm

| Công cụ | Vai trò | Loại | Ưu tiên |
|---------|---------|------|---------|
| **yt-dlp** | Download video | Local | 🔴 Cao |
| **Whisper** | Transcribe audio | Local/API | 🔴 Cao |
| **NanoAI API** | Bypass reCaptcha + Veo 3 | API | 🔴 Cao |
| **Firecrawl** | Scrape web | API | 🟡 Trung bình |
| **HeyGen/D-ID** | Face swap | API | 🟡 Trung bình |
| **DeepFaceLive** | Face swap local | Local | 🟢 Thấp |
| **Serper API** | Search trends | API | 🟢 Thấp |

---

## ⚠️ Lưu Ý Pháp Lý & Đạo Đức

> [!CAUTION]
> **Virtual KOL và Face Swap:**
> - Không sử dụng khuôn mặt người thật mà không có sự đồng ý
> - Tạo AI face riêng hoặc dùng face có license
> - Cân nhắc về tính minh bạch với followers
> - Tuân thủ terms of service của các platform

> [!WARNING]
> **Content Remake:**
> - Không copy nguyên văn nội dung
> - Luôn thêm giá trị mới, góc nhìn riêng
> - Cân nhắc về copyright khi dùng hình ảnh gốc
