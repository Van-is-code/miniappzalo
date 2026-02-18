# 🔐 Cấu Hình CORS & Backend API cho Zalo Mini App

## ⚠️ Vấn Đề Phổ Biến: CORS Error

Khi chạy mini app, bạn có thể gặp lỗi:
```
Access to XMLHttpRequest at 'https://nguyenthanhvan.software/...'
from origin 'https://app.zaloapp.com' has been blocked by CORS policy
```

**Nguyên nhân**: Browser chặn request từ domain khác

---

## ✅ Giải Pháp: Enable CORS Trên Backend

### 🔧 Cách 1: Express.js (Node.js)

```javascript
const express = require('express');
const cors = require('cors');

const app = express();

// Enable CORS cho tất cả Zalo requests
app.use(cors({
  origin: [
    'https://app.zaloapp.com',
    'https://sp.zaloapp.com',
    'http://localhost:8080',      // For local testing
    'http://localhost:3000'
  ],
  credentials: true,
  methods: ['GET', 'POST', 'PUT', 'DELETE', 'OPTIONS'],
  allowedHeaders: ['Content-Type', 'Authorization'],
  maxAge: 86400  // cache preflight for 24h
}));

// HOẶC Chi tiết hơn cho từng route:
app.post('/api/command', (req, res) => {
  res.header('Access-Control-Allow-Origin', 'https://app.zaloapp.com');
  res.header('Access-Control-Allow-Methods', 'POST, OPTIONS');
  res.header('Access-Control-Allow-Headers', 'Content-Type, Authorization');
  // ... rest of logic
});

app.listen(3000);
```

**Install package**:
```bash
npm install cors
```

### 🔧 Cách 2: Nginx (Reverse Proxy)

```nginx
server {
    listen 443 ssl http2;
    server_name nguyenthanhvan.software;

    # SSL certificates
    ssl_certificate /path/to/cert.crt;
    ssl_certificate_key /path/to/key.key;

    # CORS Headers
    add_header 'Access-Control-Allow-Origin' 'https://app.zaloapp.com' always;
    add_header 'Access-Control-Allow-Methods' 'GET, POST, PUT, DELETE, OPTIONS' always;
    add_header 'Access-Control-Allow-Headers' 'Content-Type, Authorization, Accept' always;
    add_header 'Access-Control-Allow-Credentials' 'true' always;
    add_header 'Access-Control-Max-Age' '86400' always;

    # Handle OPTIONS preflight
    if ($request_method = 'OPTIONS') {
        return 204;
    }

    # Proxy requests
    location /rolldingdoor/api/ {
        proxy_pass http://localhost:5000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

**Reload Nginx**:
```bash
sudo systemctl reload nginx
```

### 🔧 Cách 3: Django (Python)

```python
# settings.py
INSTALLED_APPS = [
    ...
    'corsheaders',
]

MIDDLEWARE = [
    'corsheaders.middleware.CorsMiddleware',
    'django.middleware.common.CommonMiddleware',
    ...
]

CORS_ALLOWED_ORIGINS = [
    "https://app.zaloapp.com",
    "https://sp.zaloapp.com",
    "http://localhost:8080",
    "http://localhost:3000",
]

CORS_ALLOW_CREDENTIALS = True
CORS_ALLOW_HEADERS = [
    'content-type',
    'authorization',
]
```

**Install**:
```bash
pip install django-cors-headers
```

### 🔧 Cách 4: ASP.NET Core (C#)

```csharp
// Startup.cs hoặc Program.cs
public void ConfigureServices(IServiceCollection services)
{
    services.AddCors(options =>
    {
        options.AddPolicy("AllowZalo", builder =>
        {
            builder
                .WithOrigins(
                    "https://app.zaloapp.com",
                    "https://sp.zaloapp.com",
                    "http://localhost:3000")
                .AllowAnyMethod()
                .AllowAnyHeader()
                .AllowCredentials();
        });
    });
    
    services.AddControllers();
}

public void Configure(IApplicationBuilder app)
{
    app.UseCors("AllowZalo");
    app.UseRouting();
    app.UseEndpoints(endpoints => endpoints.MapControllers());
}
```

---

## 🌐 Zalo Mini App - Whitelist Domains

Zalo sẽ **chỉ cho phép** kết nối tới các domain trong `serverDomain` (app.json)

```json
{
  "app": {
    "serverDomain": [
      "https://nguyenthanhvan.software",
      "https://api.yourdomain.com"
    ],
    "navigateWhiteList": [
      "https://nguyenthanhvan.software"
    ]
  }
}
```

**Quan trọng**:
- ✅ Phải là **HTTPS** (không http)
- ✅ Không có `/api/` path, chỉ domain
- ✅ Max 5 domains
- ✅ Zalo sẽ validate certificate
- ✅ Domain phải public accessible

---

## 🧪 Test CORS Trước Submit

### Method 1: Browser Console
```javascript
// Test trong console Zalo Mini App
const response = await fetch('https://nguyenthanhvan.software/rolldingdoor/api/logs', {
  method: 'GET',
  headers: {
    'Authorization': 'Bearer YOUR_TOKEN',
    'Content-Type': 'application/json'
  }
});

const data = await response.json();
console.log(data);
```

### Method 2: curl Command
```bash
curl -X GET https://nguyenthanhvan.software/rolldingdoor/api/logs \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Origin: https://app.zaloapp.com" \
  -H "Content-Type: application/json" \
  -v
```

Check response headers:
```
Access-Control-Allow-Origin: https://app.zaloapp.com ✅
Access-Control-Allow-Methods: GET, POST, OPTIONS ✅
```

### Method 3: Online CORS Checker
https://www.test-cors.org/

---

## 🔒 Security Best Practices

### 1. **Token Validation**
```javascript
// Backend - Validate token before processing
const token = req.headers.authorization?.split(' ')[1];
if (!token || !validateToken(token)) {
  return res.status(401).json({ message: 'Unauthorized' });
}
```

### 2. **Rate Limiting**
```javascript
// Prevent abuse
const rateLimit = require('express-rate-limit');

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000,  // 15 minutes
  max: 100,                   // Limit each IP to 100 requests
  keyGenerator: (req) => req.user.id // per user, not per IP
});

app.use('/api/', limiter);
```

### 3. **HTTPS Certificate**
```bash
# Use Let's Encrypt (FREE)
certbot certonly --standalone -d nguyenthanhvan.software

# Auto-renew
sudo certbot renew --dry-run
```

### 4. **Input Validation**
```javascript
// Validate all inputs
const { body, validationResult } = require('express-validator');

app.post('/api/command', [
  body('action').isIn(['OPEN', 'CLOSE', 'STOP']),
  body('deviceId').isLength({ min: 1 })
], (req, res) => {
  const errors = validationResult(req);
  if (!errors.isEmpty()) {
    return res.status(400).json({ errors: errors.array() });
  }
  // Process...
});
```

### 5. **Logging & Monitoring**
```javascript
// Log all API calls
app.use((req, res, next) => {
  console.log(`${new Date().toISOString()} ${req.method} ${req.path} - ${req.user?.id}`);
  next();
});
```

---

## 🚨 Common CORS Issues & Solutions

| Error | Cause | Solution |
|-------|-------|----------|
| **"blocked by CORS policy"** | Origin not in whitelist | Add to `Access-Control-Allow-Origin` |
| **"preflight request failed"** | OPTIONS method rejected | Allow OPTIONS in CORS config |
| **"credentials mode is 'include'"** | Missing `Allow-Credentials` | Set `Access-Control-Allow-Credentials: true` |
| **"method not allowed"** | POST/DELETE not allowed | Include in `Access-Control-Allow-Methods` |
| **"header not allowed"** | Authorization header missing | Add `Authorization` to `Allow-Headers` |

---

## 📊 Testing Checklist

- [ ] Login API works
- [ ] Door control API responds
- [ ] Schedule CRUD operations work
- [ ] History logs load without CORS error
- [ ] No 401/403 errors on authenticated calls
- [ ] Tokens refresh properly
- [ ] Error handling working (4xx, 5xx)

---

## 🆘 Debug Mode

### Enable Debug Logging In Mini App
```javascript
// Add to index.html
const originalFetch = window.fetch;
window.fetch = function(...args) {
  console.log('🔵 FETCH:', args[0], args[1]);
  return originalFetch.apply(this, args)
    .then(res => {
      console.log('✅ RESPONSE:', res.status);
      return res.clone();
    })
    .catch(err => {
      console.error('❌ ERROR:', err);
      throw err;
    });
};
```

### Dev Tools
```bash
# Check network requests
# Phone: Hold Zalo app → Dev Tools → Network tab
```

---

## 📝 Final Checklist Before Submit to Zalo

- [ ] CORS headers tested
- [ ] SSL/HTTPS certificate valid
- [ ] Domains in whitelist match API endpoints
- [ ] Token auth working
- [ ] Error messages display properly
- [ ] No CORS errors in network tab
- [ ] App loads & functions on Zalo platform

---

**✅ Nếu làm đúng các bước trên, không sẽ gặp CORS issues!**

Created: Feb 19, 2026
