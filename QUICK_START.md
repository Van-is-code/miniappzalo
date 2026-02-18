# ⚡ Quick Start - Deploy Lên Zalo Trong 5 Phút

## 🎯 3 Bước Nhanh Nhất

### **Bước 1: Deploy Lên Vercel** (2 phút)

```bash
# 1️⃣ Cài npm
# → Download từ nodejs.org

# 2️⃣ Mở PowerShell
npm install -g vercel
vercel login
cd "c:\Users\thanh\Downloads\mini app"
vercel

# 3️⃣ Nhấn Enter, chọn defaults
# → Bạn sẽ nhận URL như: https://smartdoor-xxx.vercel.app
```

✅ **Dễ nhất, free, HTTPS tự động**

---

### **Bước 2: Đăng Ký APP_ID Trên Zalo** (2 phút)

```
1. Truy cập: https://developers.zalo.me
2. Đăng nhập / Đăng ký
3. Tạo Mini App mới
4. Điền tên: "SmartDoor"
5. Lưu APP_ID
```

---

### **Bước 3: Submit Lên Zalo** (1 phút)

```
1. Cập nhật APP_ID vào app.json
2. Dia → Mini Apps → Create Version
3. Bundle URL: https://your-vercel-url/index.html
4. Config URL: https://your-vercel-url/app.json
5. Submit Review
```

✅ **Done! Chờ duyệt 1-3 ngày**

---

## 📋 Checklist

```
□ Cài Vercel
□ Deploy thành công (có URL)
□ Đăng ký Zalo Developer
□ Cuốu nhận APP_ID
□ Cập nhật app.json
□ Submit lên Zalo
```

---

## 🔧 Cập Nhật app.json - Cần Làm Gì?

Mở file `c:\Users\thanh\Downloads\mini app\app.json`

Tìm dòng này:
```json
"appId": "YOUR_APP_ID_HERE",
```

Thay thế:
```json
"appId": "123456789abcdef",  // ← Dán APP_ID Zalo tại đây
```

**Lưu file** → Ctrl + S

---

## ❓ Thắc Mắc Thường Gặp

### Q: Deploy lên đâu?
**A**: Dùng **Vercel** (cái dễ nhất) hoặc GitHub Pages

### Q: Cần APP_ID từ đâu?
**A**: Zalo Developer Portal → Tạo mini app → Lấy APP_ID

### Q: Chuẩn bị gì trước submit?
**A**: 
- URL bundle (từ Vercel)
- 3 screenshot (phone 1080x1920)
- Icon 144x144
- Mô tả, email liên hệ

### Q: Duyệt bao lâu?
**A**: 1-3 ngày, Zalo sẽ notify qua email

### Q: Sau khi duyệt thì sao?
**A**: Tự động public trên Zalo Mini App Store, người dùng tìm kiếm "SmartDoor" sẽ thấy

---

## 🚨 Gặp Lỗi?

### "CORS Error" hoặc "API không hoạt động"
👉 Xem [CORS_SETUP.md](./CORS_SETUP.md)

### "App không tải"
👉 Kiểm tra Bundle URL hợp lệ
👉 Verify `app.json` format

### "rejected by Zalo"
👉 Xem lý do reject từ Zalo email
👉 Fix & resubmit

---

## 📚 Links Hữu Ích

| Nội Dung | Link |
|---------|------|
| Zalo Developer | https://developers.zalo.me |
| Vercel | https://vercel.com |
| Full Guides | [DEPLOYMENT.md](./DEPLOYMENT.md) |
| CORS Setup | [CORS_SETUP.md](./CORS_SETUP.md) |
| Zalo Launch | [ZALO_LAUNCH_GUIDE_VI.md](./ZALO_LAUNCH_GUIDE_VI.md) |

---

**🎉 Vậy là bạn đã sẵn sàng phát hành!**

Last updated: Feb 19, 2026
