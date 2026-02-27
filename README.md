# 🚪 SmartDoor - Zalo Mini App

**Hệ Thống Điều Khiển Cửa Thông Minh** cho Zalo Mini App

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Platform](https://img.shields.io/badge/platform-Zalo%20Mini%20App-yellow)

## ✨ Tính Năng

### 🏠 **Trang Chủ - Điều Khiển Cửa**
- Control cửa garage: Mở, Đóng, Dừng
- View trạng thái realtime
- Hiển thị thông tin hệ thống (Online status, Temp)
- Animated UI với hiệu ứng neon

### ⏱️ **Hẹn Giờ Tự Động**
- Tạo lịch mở/đóng cửa
- Chọn ngày lặp lại trong tuần
- Bật/tắt nhanh lịch
- Xóa lịch không cần

### 📋 **Lịch Sử Hoạt Động**
- Xem toàn bộ nhật ký hành động
- Lọc theo loại (Mở/Đóng/Dừng)
- Hiển thị thời gian & nguồn (APP/AUTO/SENSOR)
- Group by date

### 👤 **Hồ Sơ Người Dùng**
- Thông tin tài khoản
- Thống kê: tổng lượt, thiết bị, lịch hẹn
- Settings: Thông báo, Bảo mật
- Đăng xuất

## 🚀 Quick Start

### Prerequisites
- Node.js 14+ (optional, for local testing)
- Modern browser with HTTPS support
- Zalo account

### Local Testing
```bash
# 1. Clone repo
git clone https://github.com/yourusername/smartdoor-zalo-mini-app
cd smartdoor-zalo-mini-app

# 2. Install http-server (optional)
npm install -g http-server

# 3. Start server
http-server -p 8080

# 4. Open browser
# http://localhost:8080
```

### Deploy to Zalo

#### **Option 1: Vercel (Easiest)**
```bash
npm install -g vercel
vercel login
vercel
# Follow prompts, get URL
```

#### **Option 2: GitHub Pages**
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/yourusername/smartdoor-zalo-mini-app
git push -u origin main
# Enable Pages in GitHub Settings
```

See [DEPLOYMENT.md](./DEPLOYMENT.md) for detailed instructions

## 🔑 API Integration

### Backend Required Endpoints
```
POST /auth/login
  - Email & Password authentication
  - Returns: { token, user }

POST /api/command
  - Body: { action: "OPEN" | "CLOSE" | "STOP" }
  - Auth: Bearer token
  - Returns: { message, status }

GET /api/logs
  - Auth: Bearer token
  - Returns: [ { id, action, source, timestamp } ]

GET /api/schedules
  - Auth: Bearer token
  - Returns: [ { id, action, cronTime, isActive } ]

POST /api/schedules
  - Auth: Bearer token
  - Body: { action, cronTime }
  - Returns: { id, action, cronTime }

DELETE /api/schedules/:id
  - Auth: Bearer token
  - Returns: { message }
```

## 📁 File Structure

```
.
├── index.html              # Main app (all-in-one HTML)
├── app.json               # Zalo Mini App config (IMPORTANT!)
├── package.json           # Node dependencies
├── vercel.json           # Vercel deployment config
├── DEPLOYMENT.md         # Detailed deployment guide
├── .env.example          # Environment variables template
├── .gitignore            # Git ignore rules
└── README.md             # This file
```

## ⚙️ Configuration

### Update `app.json`
```json
{
  "app": {
    "appId": "YOUR_APP_ID",          // ← Get from Zalo Developer Portal
    "appName": "SmartDoor",
    "serverDomain": [
      "https://nguyenthanhvan.software"
    ],
    ...
  }
}
```

### API Endpoints
Edit in `index.html` (lines ~242-243):
```javascript
const API_BASE = "https://your-api.com/api";
const AUTH_BASE = "https://your-api.com";
```

## 🎨 UI/UX Features

- **Dark Modern Design**: GitHub dark theme colors
- **Responsive Layout**: Optimized for mobile
- **Smooth Animations**: Spring animations, transitions
- **Glass Morphism**: Frosted glass effects
- **Neon Glow**: Glowing reactor core logo
- **Real-time Clock**: System clock display
- **Haptic Feedback Ready**: Good for vibration support

## 🔒 Security

✅ Token-based authentication (Bearer)
✅ localStorage for session persistence
✅ HTTPS enforced (Zalo requirement)
✅ CORS configured for API calls
✅ No sensitive data in code

⚠️ **Note**: Keep API credentials secure, use environment variables in backend

## 📱 Browser Support

| Browser | Version | Status |
|---------|---------|--------|
| Zalo | Latest | ✅ Full Support |
| Chrome | 90+ | ✅ Full Support |
| Safari | 14+ | ✅ Full Support |
| Firefox | 88+ | ✅ Full Support |

## 🧪 Testing

### Manual Testing Checklist
- [ ] Login with correct/wrong credentials
- [ ] Door control buttons (Open/Close/Stop)
- [ ] Add/delete schedules
- [ ] Filter history logs
- [ ] Navigate between pages
- [ ] Check responsive on mobile
- [ ] Test logout

### Browser DevTools
```javascript
// Check token
localStorage.getItem('authToken')

// Clear cache
localStorage.clear()

// Check API calls
// Open Console → Network tab
```

## 🐛 Troubleshooting

### "401 Unauthorized"
→ Token expired or invalid
→ Clear localStorage and re-login

### "CORS Error"
→ Backend needs CORS headers
→ Check `serverDomain` in app.json

### "White screen"
→ JavaScript error in console
→ Check network tab for failed requests
→ Verify API_BASE URL

### "App loads but buttons don't work"
→ Check token with `localStorage.getItem('authToken')`
→ Verify API endpoints
→ Check browser console for errors

## 📊 Analytics (Optional)

```javascript
// Add Zalo Analytics if needed
if (window.ZaloSDK) {
  ZaloSDK.trackEvent('door_opened');
}
```

## 🤝 Contributing

Contributions welcome! Please:
1. Fork repo
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

## 📄 License

This project is licensed under the MIT License - see [LICENSE](LICENSE) file for details.

## 📞 Support & Contact

- **Issues**: GitHub Issues
- **Email**: support@nguyenthanhvan.software
- **Docs**: [DEPLOYMENT.md](./DEPLOYMENT.md)

## 🙏 Credits

- **UI Design**: Dark Modern + Neon aesthetic
- **Backend API**: SmartDoor IoT System
- **Zalo Platform**: Mini App Framework

## 📈 Roadmap

- [ ] Push notifications
- [ ] Multiple device support
- [ ] Voice control (Zalo Voice)
- [ ] Energy analytics
- [ ] Sharing access with family
- [ ] Dark/Light theme toggle
- [ ] Multilingual support

## 🎯 Version History

**v1.0.0** (Feb 19, 2026)
- Initial release
- Core features: Control, Schedule, History, Profile
- Zalo Mini App integration

---

**Made with ❤️ for Smart Home Automation**

Last Updated: February 19, 2026
