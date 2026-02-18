# 🚀 SmartDoor Zalo Mini App - Hướng Dẫn Phát Hành

## 📋 Yêu Cầu Trước Khi Phát Hành

### 1. **Chuẩn Bị Trên Zalo Developer Portal**
- Đăng ký tài khoản Zalo Developer: https://developers.zalo.me
- Tạo ứng dụng mini app mới
- Get **APP_ID** từ Zalo Developer Portal

### 2. **Cập Nhật `app.json`**
```json
{
  "app": {
    "appId": "YOUR_APP_ID",  // ← Thay thế bằng APP_ID từ Zalo
    "appName": "SmartDoor",
    ...
  }
}
```

### 3. **Config API Domain**
Cập nhật `serverDomain` trong `app.json`:
```json
"serverDomain": [
  "https://nguyenthanhvan.software"
]
```

## 🌐 Deploy Ứng Dụng

### **Option 1: Host trên Vercel (Recommended)**
```bash
# 1. Cài đặt Vercel CLI
npm install -g vercel

# 2. Trong thư mục mini app
cd "c:\Users\thanh\Downloads\mini app"

# 3. Deploy
vercel

# 4. Sao chép URL được cấp
```

### **Option 2: Host trên GitHub Pages**
```bash
# 1. Tạo GitHub repo
git init
git add .
git commit -m "Initial commit"
git push origin main

# 2. Enable GitHub Pages ở Settings
# Chọn branch: main
# Folder: / (root)
```

### **Option 3: Host trên Server Riêng (Nginx)**
```nginx
server {
    listen 443 ssl http2;
    server_name app.yourdomain.com;

    root /var/www/smartdoor-mini-app;

    # Enable CORS cho API calls
    add_header 'Access-Control-Allow-Origin' 'https://nguyenthanhvan.software' always;
    add_header 'Access-Control-Allow-Methods' 'GET, POST, PUT, DELETE, OPTIONS' always;
    add_header 'Access-Control-Allow-Headers' 'Content-Type, Authorization' always;

    location / {
        try_files $uri /index.html;
    }

    ssl_certificate /path/to/cert.crt;
    ssl_certificate_key /path/to/key.key;
}
```

## ✅ Checklist Trước Submit

- [ ] `app.json` có đúng APP_ID
- [ ] `serverDomain` trỏ đúng backend API
- [ ] Ứng dụng hỗ trợ HTTPS (bắt buộc)
- [ ] Icon 144x144px (hoặc 512x512px)
- [ ] Thumbnail 256x256px
- [ ] Thử login & các chức năng chính
- [ ] Test trên thiết bị Zalo thực tế

## 📤 Phát Hành Trên Zalo Developer Portal

### 1. **Upload Ứng Dụng**
```
Zalo Developer Portal → Mini App → Versions → Create New Version
```

### 2. **Cung Cấp Thông Tin**
- **Bundle URL**: https://yourdomain.com/index.html
- **Config URL**: https://yourdomain.com/app.json
- **Category**: Nhà Thông Minh / Smart Home
- **Description**: Mô tả ứng dụng (tiếng Việt)
- **Privacy Policy**: URL chính sách quyền riêng tư
- **Support Email**: Email hỗ trợ

### 3. **Nộp Review**
Zalo Team sẽ review trong 1-3 ngày

### 4. **Công Khai**
Sau khi duyệt, ứng dụng sẽ có sẵn trên Zalo Mini App Store

## 🔧 Cập Nhật Zalo SDK (Optional)

Nếu muốn dùng thêm Zalo SDK features (share, user info, etc):

```html
<script>
// Thêm vào cuối file index.html trước tag </body>
if (window.ZaloSDK) {
  ZaloSDK.getAccessToken(function(access_token) {
    console.log('Token:', access_token);
  });
}
</script>
```

## 🐛 Troubleshooting

### "CORS Error"
→ Cấu hình `serverDomain` trong `app.json`
→ Enable CORS trên backend API

### "WHITE_LIST Error"
→ Cập nhật `navigateWhiteList` với domain backend

### "App không tải"
→ Kiểm tra Bundle URL đúng không
→ Ensure app.json đúng format JSON

## 📱 Test Trên Zalo (Local)

```html
<!-- Thêm vào index.html để test local -->
<script src="https://sp.zaloapp.com/plugins/sdk.js"></script>
```

Sau đó mở Zalo → QR Code → Scan để test

## 📞 Hỗ Trợ

- Zalo Developer Docs: https://developers.zalo.me/docs
- Email: support@nguyenthanhvan.software

---

**Created**: Feb 19, 2026
**Version**: 1.0.0
