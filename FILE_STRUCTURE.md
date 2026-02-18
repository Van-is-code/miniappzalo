# 📁 Cấu Trúc File Project - SmartDoor Mini App

```
smartdoor-zalo-mini-app/
│
├── 📄 index.html                    ⭐ FILE CHÍNH - Ứng dụng hoàn chỉnh
│   ├─ HTML5 structure
│   ├─ CSS (dark theme + animations)
│   └─ JavaScript (API integration)
│
├── 📋 app.json                      ⭐ CẦN EDIT - Cấu hình Zalo Mini App
│   ├─ appId (CẦN NHẬP APP_ID)
│   ├─ appName, appDescription
│   ├─ serverDomain (API whitelist)
│   └─ pages, icons, etc
│
├── 📦 package.json                  Node.js dependencies & scripts
│   ├─ npm start (local testing)
│   ├─ vercel deploy scripts
│   └─ dependencies info
│
├── 🔧 vercel.json                   Vercel deployment config
│   ├─ Routes config
│   ├─ CORS headers
│   └─ Build settings
│
├── 🚀 QUICK_START.md                ⭐ BẮT ĐẦU - 5 phút deploy
│   ├─ 3 bước nhanh nhất
│   ├─ Checklist
│   └─ FAQ
│
├── 📤 DEPLOYMENT.md                 Hướng dẫn phát hành chi tiết
│   ├─ Vercel, GitHub Pages, Server
│   ├─ Checklist trước submit
│   └─ Troubleshooting
│
├── 🎯 ZALO_LAUNCH_GUIDE_VI.md       Hướng dẫn Zalo Developer chi tiết
│   ├─ Đăng ký tài khoản
│   ├─ Tạo ứng dụng mini app
│   ├─ Submit lên store
│   ├─ Screenshots & metadata
│   └─ Monitoring & updates
│
├── 🌐 CORS_SETUP.md                 Cấu hình CORS & Backend API
│   ├─ Express, Nginx, Django, ASP.NET
│   ├─ Security best practices
│   ├─ Testing & debugging
│   └─ Common issues
│
├── 📖 README.md                     Project overview (English)
│   ├─ Features
│   ├─ Quick start
│   ├─ API docs
│   ├─ Contributing
│   └─ Support
│
├── .env.example                     Environment variables template
│   ├─ Zalo credentials
│   ├─ API endpoints
│   └─ Deployment URLs
│
├── .gitignore                       Git ignore rules
│   ├─ node_modules
│   ├─ .env
│   ├─ .vercel
│   └─ Temp files
│
└── 📂 (Optional - chưa tạo)
    ├─ /assets                      Ảnh, icon, fonts
    ├─ /public                      Static files
    ├─ /docs                        Extra documentation
    └─ /tests                       Test files
```

---

## 📝 Mô Tả Chi Tiết Từng File

### **1. `index.html` ⭐⭐⭐ (QUAN TRỌNG NHẤT)**
**Chức năng**: Ứng dụng hoàn chỉnh (single-file app)

**Nội dung**:
```html
<!-- HTML: 5 trang (Login, Home, Schedule, History, Profile) -->
<!-- CSS: Tất cả styles (dark theme, animations) -->
<!-- JavaScript: API calls, state management, UI logic -->
```

**Không chỉnh sửa**: Chỉ cần có nó, bạn không cần chỉnh HTML code

**Nếu cần thay đổi API URL**:
```javascript
// Tìm dòng ~242
const API_BASE = "https://nguyenthanhvan.software/rolldingdoor/api";
const AUTH_BASE = "https://nguyenthanhvan.software/rolldingdoor";
// Thay URL tại đây
```

---

### **2. `app.json` ⭐⭐⭐ (PHẢI CHỈNH SỬA)**
**Chức năng**: Cấu hình cho Zalo Mini App Platform

**Phải chỉnh sửa**:
```json
"appId": "YOUR_APP_ID_HERE"  // ← Dán APP_ID từ Zalo Developer Portal tại đây
```

**Lựa chọn chỉnh sửa thêm**:
```json
"appIcon": "https://yourdomain.com/icon.png"      // Icon app
"serverDomain": ["https://your-api.com"]          // API domain whitelist
```

**Không chỉnh sửa**: appName, appTitle (nếu không muốn đổi tên)

---

### **3. `package.json` ⭐⭐**
**Chức năng**: Quản lý dependencies & scripts cho Node.js

**Khi nào cần dùng**: 
- Deploy lên Vercel: `npm vercel`
- Test local: `npm start`

**Chỉnh sửa tùy ý**:
```json
"name": "smartdoor-zalo-mini-app"   // Tên project
"version": "1.0.0"                  // Phiên bản
"author": "Your Name"               // Tác giả
"repository": { "url": "github repo URL" }
```

---

### **4. `vercel.json` ⭐⭐**
**Chức năng**: Cấu hình Vercel deployment

**Auto**: Vercel tự xử lý, không cần chỉnh

**Tùy chỉnh nếu cần**:
```json
"routes": [...]        // URL routes
"headers": [...]       // CORS headers
```

---

### **5. `QUICK_START.md` (ĐỌCM ĐẦU TIÊN)**
**Nội dung**: 
- 5 phút deploy lên Zalo
- 3 bước chính
- FAQ nhanh

**Khi nào đọc**: Lần đầu tiên setup, muốn deploy nhanh

---

### **6. `DEPLOYMENT.md`**
**Nội dung**:
- 3 cách deploy (Vercel, GitHub Pages, Server)
- Checklist trước submit
- Troubleshooting

**Khi nào đọc**: Cần chi tiết cách deploy

---

### **7. `ZALO_LAUNCH_GUIDE_VI.md` (DÀNH CHO ZALO)**
**Nội dung**:
- Đăng ký developer Zalo
- Tạo mini app
- Submit review
- Screenshots & metadata
- Monitoring sau publish

**Khi nào đọc**: Sắp submit lên Zalo Mini App Store

---

### **8. `CORS_SETUP.md`**
**Nội dung**:
- CORS configuration (Express, Nginx, Django, ASP.NET)
- Security best practices
- Debugging CORS errors

**Khi nào đọc**: Gặp CORS error hoặc cần setup backend

---

### **9. `README.md`**
**Nội dung**:
- Overview project (tiếng Anh)
- Features, API docs
- Contributing guide
- Support links

**Khi nào đọc**: GitHub repo documentation

---

### **10. `.env.example`**
**Chức năng**: Template cho environment variables

**Khi nào dùng**:
1. Copy thành `.env`
2. Điền giá trị

```bash
cp .env.example .env
```

---

### **11. `.gitignore`**
**Chức năng**: Bảo vệ sensitive files trên GitHub

**Auto**: Git sẽ skip những file trong .gitignore

**Files được ignore**:
```
node_modules/      // Dependencies (download lại từ package.json)
.env               // Credentials (KHÔNG push lên GitHub)
.vercel/           // Vercel local config
*.log              // Log files
```

---

## 🚀 Workflow - Từ Lần Đầu Đến Deploy

### **Lần Đầu Tiên** (5 phút)
```
1. Đọc: QUICK_START.md
2. Deploy: Vercel (2 phút)
3. Nhận: URL từ Vercel
4. Edit: app.json (add APP_ID)
5. Submit: Zalo Developer
```

### **Lần Cập Nhật** (5 phút)
```
1. Chỉnh sửa: index.html (code changes)
2. Push: git push
3. Vercel: Auto-deploy (nó sẽ auto update)
```

### **Debug Issues** (Tìm kiếm file)
```
CORS Error?          → CORS_SETUP.md
Deploy Problem?      → DEPLOYMENT.md
Zalo Submit?         → ZALO_LAUNCH_GUIDE_VI.md
API Error?           → index.html (API_BASE URL)
```

---

## 📊 File Size & Load Time

| File | Size | Load Time |
|------|------|-----------|
| index.html | ~150KB | <1s |
| app.json | <2KB | <100ms |
| Total | ~150KB | <2s (on 4G) |

✅ Rất nhẹ, load nhanh

---

## 🔐 Files Cần Bảo Mật

### **KHÔNG PUSH LÊN GITHUB**
- `.env` (nếu có credentials)
- `*.key` files (private keys)
- Passwords, API secrets

### **OK ĐỂ PUBLIC**
- `index.html`
- `app.json`
- `.env.example` (template)
- Docs, README

---

## 📱 Mobile-First Design

**index.html** được design cho mobile:
- 390px width (iPhone X)
- 844px height
- Responsive ngay trên mọi thiết bị

Không cần media queries, là responsive intrin

sic!

---

## 🔄 Version Control (Git)

### First Time Setup:
```bash
git init
git add .
git commit -m "Initial commit: SmartDoor Mini App"
git remote add origin https://github.com/yourusername/smartdoor
git push -u origin main
```

### Every Update:
```bash
git add .
git commit -m "Update: [describe changes]"
git push
```

Vercel sẽ auto-deploy khi detect new push!

---

## 🆘 Help Guide

| Vấn đề | Xem File |
|-------|---------|
| Không biết bắt đầu từ đâu | **QUICK_START.md** |
| Deploy lên Vercel | **DEPLOYMENT.md** → Option 1 |
| Deploy lên GitHub Pages | **DEPLOYMENT.md** → Option 2 |
| Deploy lên Server riêng | **DEPLOYMENT.md** → Option 3 |
| Cấu hình Zalo Developer | **ZALO_LAUNCH_GUIDE_VI.md** |
| CORS Error | **CORS_SETUP.md** |
| Chỉnh sửa API URL | **index.html** (Line ~242) |
| Thay APP_ID | **app.json** (Line ~3) |

---

## ✅ Setup Checklist

```
□ Đọc QUICK_START.md
□ Deploy lên Vercel (có URL)
□ Cập nhật app.json (APP_ID)
□ Đăng ký Zalo Developer
□ Submit lên Zalo
□ Chờ approve (1-3 ngày)
□ Publish (auto public)
□ Share link với bạn bè!
```

---

**🎉 Enjoy your SmartDoor Mini App on Zalo!**

Last updated: Feb 19, 2026
