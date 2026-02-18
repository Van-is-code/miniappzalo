# 🎯 Hướng Dẫn Đăng Ký & Phát Hành Trên Zalo Mini App

## 📝 Bước 1: Đăng Ký Tài Khoản Zalo Developer

### 1.1 Truy Cập Zalo Developer Portal
```
👉 Đi tới: https://developers.zalo.me
```

### 1.2 Đăng Nhập / Đăng Ký
- Nhấn **"Đăng Ký"** nếu chưa có tài khoản
- Hoặc **"Đăng Nhập"** với tài khoản Zalo hiện tại
- Hoàn thành xác minh 2 lớp (2FA)

---

## 🔐 Bước 2: Tạo Ứng Dụng Mini App

### 2.1 Dashboard Developer
```
Zalo Developer Portal 
  → Ứng dụng của tôi (sidebar trái)
  → Tạo ứng dụng mới
```

### 2.2 Điền Thông Tin Ứng Dụng
| Field | Giá Trị | Ghi Chú |
|-------|--------|--------|
| **Tên Ứng Dụng** | SmartDoor | Hiển thị trên Zalo |
| **Slug** | smartdoor | URL-friendly name |
| **Loại** | Mini App | Quan trọng! |
| **Trang Web** | https://your-domain.com | Trang chủ ứng dụng |
| **Mô Tả** | Ứng dụng điều khiển cửa thông minh | Max 160 ký tự |
| **Loại**: | Nhà thông minh / Smart Home | Chọn category |

### 2.3 Upload Icon & Thumbnail
- **Icon**: 144x144px hoặc 512x512px (Square)
- **Thumbnail**: 256x256px (cho Mini App Store)
- Format: PNG hoặc JPG
- Min size: 50KB

**Tạo icon nhanh**:
```html
<!-- Lưu dưới dạng PNG -->
<svg viewBox="0 0 144 144" xmlns="http://www.w3.org/2000/svg">
  <rect fill="#38bdf8" width="144" height="144"/>
  <text x="50%" y="50%" font-size="80" fill="white" text-anchor="middle" dominant-baseline="middle">🚪</text>
</svg>
```

### 2.4 Nhấn "Tạo"
Bạn sẽ nhận được:
- ✅ **APP_ID** (lưu lại)
- ✅ **APP_SECRET** (lưu bảo mật)

**⚠️ LƯU GHI CHÚNG RA!**
```
APP_ID: xxxxxxxxxxxxxxxx
APP_SECRET: xxxxxxxxxxxxxxxxxxxxxxxx
```

---

## 🚀 Bước 3: Chuẩn Bị Bundle Ứng Dụng

### 3.1 Cập Nhật `app.json`
```json
{
  "app": {
    "appId": "YOUR_APP_ID_HERE",    // ← Dán APP_ID tại đây
    "appName": "SmartDoor",
    "appTitle": "SmartDoor - Hệ Thống Điều Khiển Cửa",
    "appDescription": "Ứng dụng điều khiển cửa garage thông minh",
    "appIcon": "https://your-domain.com/icon.png",
    "minPlatformVersion": "1.0.0",
    "serverDomain": [
      "https://nguyenthanhvan.software"  // ← Thay bằng API domain của bạn
    ]
  }
}
```

### 3.2 Deploy Ứng Dụng

#### **Cách 1: Dùng Vercel (Dễ Nhất)** ⭐
```bash
# Cài đặt Vercel CLI
npm install -g vercel

# Trong folder mini app
cd "c:\Users\thanh\Downloads\mini app"

# Deploy
vercel login   # Đăng nhập GitHub account
vercel         # Chọn import từ current directory

# Sẽ hiển thị: https://smartdoor-xxx.vercel.app
```
✅ Lợi: Tự động HTTPS, CDN nhanh, free
❌ Nhược: Miễn phí cho public projects

#### **Cách 2: GitHub Pages**
```bash
# Tạo repo trên GitHub
# Bật Settings → Pages
# Chọn branch: main, folder: /

# Deploy với git
git push origin main
# URL: https://yourusername.github.io/smartdoor-zalo-mini-app
```
✅ Lợi: Hoàn toàn free + GitHub
❌ Nhược: Cần SSH keys setup

#### **Cách 3: Server Riêng (Nginx)**
```bash
# Upload files lên server
scp -r ./* user@server:/var/www/smartdoor

# Cấu hình Nginx (HTTPS bắt buộc!)
sudo nano /etc/nginx/sites-available/smartdoor

# Enable site
sudo ln -s /etc/nginx/sites-available/smartdoor /etc/nginx/sites-enabled/

# Reload
sudo systemctl reload nginx
```

---

## 📤 Bước 4: Submit Lên Zalo Mini App Store

### 4.1 Trên Zalo Developer Portal
```
Ứng dụng của tôi 
  → SmartDoor (select)
  → Mini App
  → Create New Version
```

### 4.2 Điền Thông Tin Version
| Field | Ví Dụ |
|-------|-------|
| **Version** | 1.0.0 |
| **Bundle URL** | https://yourdomain.com/index.html |
| **Config URL** | https://yourdomain.com/app.json |
| **Release Notes** | Phiên bản đầu tiên |

### 4.3 Cấu Hình Metadata
- **Tiêu đề**: SmartDoor - Điều Khiển Cửa
- **Mô tả ngắn**: Ứng dụng điều khiển cửa garage thông minh có hẹn giờ tự động
- **Mô tả đầy đủ**: 
```
SmartDoor là ứng dụng điều khiển cửa garage thông minh. 
Bạn có thể:
✓ Mở, đóng cửa từ xa
✓ Hẹn giờ tự động mở/đóng
✓ Xem lịch sử hoạt động
✓ Theo dõi trạng thái realtime

Tính năng:
- Giao diện hiện đại, dễ sử dụng
- Hoạt động offline-ready
- Tích hợp Zalo, không cần app riêng
- Bảo mật với token authentication

Yêu cầu: Kết nối internet, tài khoản SmartDoor
```
- **Danh mục**: Nhà Thông Minh
- **Hình ảnh**: Ít nhất 3 screenshot
- **URL Chính Sách Quyền Riêng Tư**: https://yourdomain.com/privacy.html

### 4.4 Upload Screenshots (Bắt Buộc)
Cần 3-5 screenshots:
1. **Trang Login** (màn hình đăng nhập)
2. **Trang Chủ** (điều khiển chính)
3. **Hẹn Giờ** (scheduling page)
4. **Lịch Sử** (history page)
5. **Hồ Sơ** (profile page)

Kích thước: 1080x1920px (ratio 9:16)

### 4.5 Cấu Hình Quyền Hạn
```
Quyền được phép truy cập:
☑ Thông tin người dùng (email)
☑ Lưu trữ dữ liệu (localStorage)
☑ Mạng (API calls)
```

### 4.6 Thông Tin Liên Hệ
- **Email hỗ trợ**: support@your-company.com
- **Số điện thoại**: +84-xxx-xxxx-xxxx
- **Website**: https://yourdomain.com

### 4.7 Submit Review
👉 Nhấn **"Submit for Review"**

---

## ⏳ Bước 5: Chờ Duyệt

### Timeline
| Giai Đoạn | Thời Gian | Ghi Chú |
|-----------|----------|--------|
| **Initial Review** | 1-2 ngày | Kiểm tra cơ bản |
| **Functional Test** | 1-2 ngày | Test chức năng |
| **Security Review** | 1-2 ngày | Kiểm tra bảo mật |
| **Approved/Rejected** | Thông báo ngay | Email + Alert |

### Trạng Thái Có Thể Gặp
- ✅ **APPROVED**: Đã duyệt, sẽ public trong 24h
- ⏳ **IN_REVIEW**: Đang review
- ❌ **REJECTED**: Bị từ chối, xem feedback
- 🔄 **NEED_INFO**: Cần bổ sung thông tin

---

## 🛠️ Bước 6: Publish Lên Zalo Mini App Store

### 6.1 Sau Khi Approved
```
Zalo Developer Portal 
  → SmartDoor 
  → Mini App 
  → Version → Publish
```

### 6.2 Người Dùng Có Thể Tìm
```
Zalo 
  → Khám Phá 
  → Mini Apps 
  → Tìm "SmartDoor"
  → Nhấn "Cài đặt"
```

---

## ✅ Checklist Trước Submit

### Technical
- [ ] URL Bundle có HTTPS (bắt buộc)
- [ ] `app.json` JSON hợp lệ
- [ ] API servers trong whitelist
- [ ] Icons/thumbnails kích thước đúng
- [ ] Thử toàn bộ chức năng trên Zalo

### Content
- [ ] Mô tả không quá dài (max 500 ký tự)
- [ ] Screenshots rõ ràng, professional
- [ ] Privacy policy hoàn chỉnh
- [ ] Không có typo, lỗi chính tả

### Compliance
- [ ] Không spam, adware, malware
- [ ] Không vi phạm bản quyền
- [ ] Tuân thủ T&C của Zalo
- [ ] Có support email hợp lệ

---

## 🐛 Nếu Bị Reject

### Lý Do Phổ Biến

1. **"Bundle URL không hoạt động"**
   → Kiểm tra URL có tồn tại
   → Ensure HTTPS hoạt động
   → Thêm URL vào whitelist

2. **"app.json format sai"**
   → Kiểm tra JSON trên jsonlint.com
   → Đảm bảo appId đúng

3. **"Privacy Policy không được chấp nhận"**
   → Thêm mục "Dữ liệu được thu thập"
   → Giải thích cách dùng token
   → Add "Liên hệ" & "GDPR"

4. **"Icon chất lượng thấp"**
   → Tăng độ phân giải lên 512x512px
   → Đảm bảo PNG background transparent
   → Không nên blur hoặc mờ

### Cách Fix
1. Xem feedback từ Zalo team
2. Cập nhật thông tin / code
3. Nhấn "Resubmit"
4. Chờ duyệt lại (thường 1 ngày)

---

## 📊 Sau Khi Publish

### Monitoring
```
Zalo Developer Portal 
  → SmartDoor 
  → Analytics
```

Theo dõi:
- Số lượt cài
- Số người dùng hoạt động
- Crash reports
- User feedback

### Updates
Để phát hành phiên bản mới:
1. Update code trên server
2. Deploy lên Vercel/GitHub
3. Zalo Developer → Create New Version
4. Submit for Review
5. Chờ approve & publish

---

## 🆘 Support & Liên Hệ

### Zalo Developer Support
- **Forum**: https://developers.zalo.me/docs
- **Email**: dev-support@zalo.me
- **Response Time**: 24-48 hours

### Your Support
- **Email**: support@your-company.com
- **Phone**: +84-xxx-xxxx-xxxx
- **Website**: https://yourdomain.com

---

## 📚 Tài Liệu Tham Khảo

1. **Zalo Mini App Docs**
   https://developers.zalo.me/docs

2. **CORS Configuration**
   https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS

3. **HTTPS Setup**
   https://letsencrypt.org/ (free SSL certificates)

4. **Vercel Deployment**
   https://vercel.com/docs

---

**🎉 Chúc mừng! SmartDoor sẽ sớm xuất hiện trên Zalo Mini App Store!**

---

**Cập nhật**: Feb 19, 2026
**Phiên bản**: 1.0.0
