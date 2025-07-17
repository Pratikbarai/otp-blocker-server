# 🔐 OTP Blocker - GitHub Hosted Server

A complete OTP (One-Time Password) delivery system hosted on GitHub Pages, designed to work with the OTP Blocker Windows kernel driver.

## 🌟 Features

- **Real-time TOTP Generation** - 30-second rotating OTPs
- **Multiple Delivery Methods** - Email, SMS, Push notifications, Webhook
- **User Registration System** - Complete user management
- **Secure Authentication** - Password protection with social login
- **Responsive Design** - Works on desktop, tablet, and mobile
- **Free Hosting** - Completely hosted on GitHub Pages

## 🚀 Quick Start

### 1. Access the OTP Server
Visit: `https://your-username.github.io/otp-blocker-server/`

### 2. Register for OTP Delivery
- Click "Register Account" on the main page
- Fill in your details and select delivery methods
- Create a secure password
- Start receiving OTPs!

### 3. Use with Windows Driver
- Install the OTP Blocker driver on your Windows system
- Use the C client to fetch OTPs from the server
- Submit OTPs to unlock CMD and PowerShell

## 📱 OTP Delivery Methods

| Method | Description | Requirements |
|--------|-------------|--------------|
| 📧 **Email** | OTPs sent to your email | Valid email address |
| 📱 **SMS** | OTPs sent via text message | Phone number |
| 🔔 **Push** | Browser notifications | Browser permission |
| 🌐 **Webhook** | HTTP POST to your server | Webhook URL |

## 🔧 OTP Constraints

- **Length**: 3 characters
- **Maximum Numbers**: 2
- **Must Include**: Uppercase, lowercase, special character, number
- **Valid For**: 30 seconds
- **Session**: 5 minutes after validation

## 🏗️ System Architecture

```
GitHub Pages (Frontend)
├── OTP Generation Server
├── User Registration System
├── Authentication System
└── User Dashboard

Windows Driver (Backend)
├── Process Interception
├── OTP Validation
└── CMD/PowerShell Blocking
```

## 📁 File Structure

```
otp-blocker-server/
├── index.html                    # Landing page
├── web_otp_server.html          # Main OTP server
├── user_registration.html       # User registration
├── user_login.html             # User login
├── user_dashboard.html         # User dashboard
├── README.md                   # This file
├── GITHUB_HOSTING_GUIDE.md     # Hosting setup guide
├── USER_REGISTRATION_GUIDE.md  # User registration guide
└── .github/
    └── workflows/
        └── deploy-otp-server.yml  # Auto-deployment
```

## 🔐 Security Features

- **HTTPS Encryption** - All communications encrypted
- **Strong Passwords** - Enforced password requirements
- **Session Management** - Secure user sessions
- **Rate Limiting** - Protection against abuse
- **Data Privacy** - GDPR compliant data handling

## 🛠️ Technical Details

### Frontend Technologies
- **HTML5** - Semantic markup
- **CSS3** - Modern styling with gradients
- **JavaScript** - Real-time OTP generation
- **LocalStorage** - User data persistence

### Backend Integration
- **GitHub Pages** - Static hosting
- **GitHub Actions** - Automated deployment
- **Local Storage** - User data (client-side)

### Driver Integration
- **Windows Kernel Driver** - Process interception
- **IOCTL Commands** - OTP validation
- **C Client** - HTTP communication

## 📊 Usage Statistics

- **OTP Generation**: Every 30 seconds
- **Session Timeout**: 5 minutes
- **Delivery Methods**: 4 options
- **User Management**: Complete registration system

## 🔗 API Endpoints

### Web Server API
```javascript
// Get current OTP
window.OTPAPI.getCurrentOTP()

// Generate new OTP
window.OTPAPI.generateOTP()

// Reset OTP session
window.OTPAPI.resetOTP()

// Get server status
window.OTPAPI.getStatus()
```

### HTTP API (Future)
```bash
# Get current OTP
GET /api/otp

# Generate new OTP
POST /api/generate

# Get server status
GET /api/status
```

## 🚀 Deployment

### GitHub Pages (Current)
- **URL**: `https://your-username.github.io/otp-blocker-server/`
- **Branch**: `gh-pages` (auto-generated)
- **Deployment**: Automatic on push to main

### Alternative Hosting
- **Vercel**: Serverless functions
- **Netlify**: Custom domains
- **Self-hosted**: Full control

## 📖 Documentation

- **[GitHub Hosting Guide](GITHUB_HOSTING_GUIDE.md)** - Complete setup instructions
- **[User Registration Guide](USER_REGISTRATION_GUIDE.md)** - User management details
- **[Driver Documentation](Driver.c)** - Windows driver source code

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🆘 Support

- **Issues**: Create an issue on GitHub
- **Documentation**: Check the guides in this repository
- **Email**: Contact through the registration form

## 🔮 Roadmap

- [ ] Two-factor authentication
- [ ] API access for developers
- [ ] Mobile application
- [ ] Enterprise features
- [ ] Advanced analytics
- [ ] Multi-language support

## ⚡ Quick Links

- **[Live Demo](https://your-username.github.io/otp-blocker-server/)**
- **[Register Account](https://your-username.github.io/otp-blocker-server/user_registration.html)**
- **[User Dashboard](https://your-username.github.io/otp-blocker-server/user_dashboard.html)**
- **[Documentation](GITHUB_HOSTING_GUIDE.md)**

---

**🔐 Secure • 🚀 Fast • 🌐 Free • 📱 Responsive**

Built with ❤️ for secure OTP delivery 