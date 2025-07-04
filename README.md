# 💬 Study Buddy - AI Learning Assistant
**Ứng dụng chatbot AI hỗ trợ học tập với khả năng xử lý tài liệu thông minh và hệ thống xác thực người dùng**

## ✨ Tính năng chính

### 🔐 Hệ thống Authentication
- Đăng ký/Đăng nhập với Supabase
- Mã hóa mật khẩu với bcrypt
- Validation dữ liệu đầu vào
- Row Level Security (RLS)

### 🤖 AI Chat
- Hỗ trợ Local LLM qua LM Studio (miễn phí, offline)
- Chat thông thường với AI assistant
- Giao diện Streamlit tương tự ChatGPT

### 📄 Xử lý tài liệu
- **Định dạng**: PDF, DOCX, TXT, MD
- **OCR PDF**: Mistral OCR cho PDF có hình ảnh
- **Tóm tắt tự động**: AI tóm tắt nội dung
- **Câu hỏi gợi ý**: Tự động tạo câu hỏi liên quan

### 🎯 RAG (Retrieval-Augmented Generation)
- Trả lời câu hỏi dựa trên tài liệu
- Tìm kiếm thông tin chính xác
- Carousel câu hỏi tương tác

### 💾 Lưu trữ và Quản lý
- Database PostgreSQL qua Supabase
- Lưu trữ tài liệu theo session
- Lịch sử chat và tài liệu cá nhân

## 🛠️ Cấu trúc dự án

```
Study Buddy/
├── app.py                      # Entry point chính
├── requirements.txt            # Python dependencies
├── database_schema.sql         # Schema database
├── README.md                   # Tài liệu dự án
├── .gitignore                  # Git ignore rules
├── assets/
│   └── styles/
│       └── style.css          # CSS tùy chỉnh
├── src/
│   ├── __init__.py
│   ├── config/
│   │   ├── __init__.py
│   │   └── constants.py       # Cấu hình hằng số
│   ├── pages/
│   │   ├── __init__.py
│   │   ├── login_page.py      # Trang đăng nhập/đăng ký
│   │   └── home_page.py       # Trang chính
│   └── utils/
│       ├── __init__.py
│       ├── chat_handler.py    # Xử lý Local LLM
│       ├── chat_persistence.py # Lưu trữ chat
│       ├── document_processor.py # Xử lý tài liệu + RAG
│       ├── error_handler.py   # Xử lý lỗi
│       ├── ui_components.py   # Components giao diện
│       └── validators.py      # Validation dữ liệu
└── tests/
    └── test_validators.py     # Unit tests
```

## 🚀 Hướng dẫn cài đặt

### 1. Yêu cầu hệ thống
- **Python**: 3.8+
- **Hệ điều hành**: Windows, macOS, hoặc Linux
- **RAM**: Tối thiểu 8GB, khuyến nghị 16GB+
- **GPU** (khuyến nghị): NVIDIA GPU (6GB VRAM+) hoặc Apple Silicon
- **Dung lượng**: 5-20GB cho LLM models

### 2. Cài đặt LM Studio

#### Tải và cài đặt
1. Vào [lmstudio.ai](https://lmstudio.ai/)
2. Tải phiên bản phù hợp với hệ điều hành
3. Cài đặt theo hướng dẫn

#### Tải mô hình LLM
1. Mở LM Studio → Search models
2. Tải mô hình khuyến nghị:
   - **Llama-3.1-8B-Instruct** (Q4_K_M)
   - **Mistral-7B-Instruct** (Q4_K_M)
3. Chờ tải hoàn tất

#### Kích hoạt API Server
1. Vào tab **Developer** trong LM Studio
2. Bật **Enable API Server**
3. Ghi nhớ endpoint: `http://localhost:1234/v1`
4. Test API:
   ```bash
   curl http://localhost:1234/v1/models
   ```

### 3. Cài đặt Database (Supabase)

#### Tạo dự án Supabase
1. Vào [supabase.com](https://supabase.com)
2. Tạo tài khoản và dự án mới
3. Lấy **URL** và **anon key** từ Settings → API

#### Chạy database schema
1. Vào Supabase → SQL Editor
2. Copy nội dung file `database_schema.sql`
3. Chạy script để tạo tables và functions

#### Cấu hình kết nối
Cập nhật thông tin Supabase trong `src/pages/login_page.py`:
```python
SUPABASE_URL = "your-project-url"
SUPABASE_KEY = "your-anon-key"
```

### 4. Chạy ứng dụng

#### Cài đặt dependencies
```bash
pip install -r requirements.txt
```

#### Khởi động ứng dụng
```bash
streamlit run app.py
```

Ứng dụng sẽ chạy tại: `http://localhost:8501`

## 📋 Hướng dẫn sử dụng

### Đăng ký tài khoản
1. Mở ứng dụng → Tab "Đăng ký"
2. Điền thông tin (username, email, password)
3. Nhấn "Tạo tài khoản"

### Đăng nhập
1. Tab "Đăng nhập"
2. Nhập username và password
3. Nhấn "Đăng nhập"

### Sử dụng AI Chat
1. Sau khi đăng nhập → Giao diện chat chính
2. Gõ câu hỏi và nhấn Enter
3. AI sẽ trả lời qua Local LLM

### Upload và xử lý tài liệu
1. Sử dụng file uploader
2. Chọn file PDF, DOCX, TXT, MD
3. Đợi xử lý và tóm tắt
4. Đặt câu hỏi về nội dung tài liệu

## 🔧 Configuration

### Environment Variables
Tạo file `.env` (tùy chọn):
```env
SUPABASE_URL=your-project-url
SUPABASE_KEY=your-anon-key
LM_STUDIO_URL=http://localhost:1234/v1
```

### LM Studio Settings
- Model: Llama-3.1-8B-Instruct hoặc Mistral-7B-Instruct
- Context Length: 4096-8192 tokens
- Temperature: 0.7
- Max Tokens: 1024

## 🧪 Testing

Chạy unit tests:
```bash
python -m pytest tests/ -v
```

Test validators:
```bash
python -m pytest tests/test_validators.py -v
```

## 🐛 Troubleshooting

### Lỗi kết nối LM Studio
- Kiểm tra LM Studio đã bật API Server
- Verify endpoint: `http://localhost:1234/v1`
- Restart LM Studio nếu cần

### Lỗi database
- Kiểm tra Supabase URL và key
- Verify database schema đã được tạo
- Check network connection

### Lỗi upload tài liệu
- Kiểm tra định dạng file (PDF, DOCX, TXT, MD)
- Verify file size < 200MB
- Check file permissions

## 💡 Tính năng nổi bật

- ✅ **Miễn phí hoàn toàn** với Local LLM
- ✅ **Chạy offline**, bảo mật cao
- ✅ **Hỗ trợ tiếng Việt** tốt
- ✅ **Xử lý tài liệu** thông minh
- ✅ **Authentication** secure
- ✅ **Database** persistent
- ✅ **RAG** chính xác

## 🤝 Contributing

1. Fork repository
2. Tạo feature branch: `git checkout -b feature/amazing-feature`
3. Commit changes: `git commit -m 'Add amazing feature'`
4. Push branch: `git push origin feature/amazing-feature`
5. Tạo Pull Request

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

## 📞 Contact

- **Developer**: Nhóm 6
- **Email**: [ 22010201@st.phenikaa-uni.edu.vn, 22010449@st.phenikaa-uni.edu.vn, 22010032@st.phenikaa-uni.edu.vn ]

---

**Khuyến nghị**: Sử dụng với LM Studio để có trải nghiệm tốt nhất! 🚀
