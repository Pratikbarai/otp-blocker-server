# GitHub Hosting Guide - OTP Server

## Overview

This guide explains how to host your OTP server on GitHub and use it to deliver OTPs to clients. GitHub provides several hosting options that are perfect for OTP delivery:

- **GitHub Pages** - Static website hosting
- **GitHub Actions** - Automated deployment
- **GitHub API** - Programmatic access

## 🚀 Quick Start

### 1. Create GitHub Repository

```bash
# Create a new repository on GitHub
# Name it: otp-blocker-server
# Make it public for GitHub Pages
```

### 2. Upload Files

Upload these files to your repository:

```
otp-blocker-server/
├── web_otp_server.html      # Main OTP server
├── .github/
│   └── workflows/
│       └── deploy-otp-server.yml  # GitHub Actions
├── README.md                # Repository documentation
└── index.html              # Redirect to main server
```

### 3. Enable GitHub Pages

1. Go to repository **Settings**
2. Scroll to **Pages** section
3. Select **Source**: "Deploy from a branch"
4. Select **Branch**: "gh-pages" (created by GitHub Actions)
5. Click **Save**

Your OTP server will be available at:
`https://your-username.github.io/otp-blocker-server/`

## 📁 File Structure

### Core Files

#### `web_otp_server.html`
- **Purpose**: Main OTP server with web interface
- **Features**: 
  - Real-time TOTP generation
  - 30-second countdown timer
  - Multiple delivery methods
  - API endpoints for external access
  - Responsive design

#### `.github/workflows/deploy-otp-server.yml`
- **Purpose**: Automated deployment workflow
- **Triggers**: Push to main branch
- **Actions**: Deploy to GitHub Pages, Vercel, Netlify

#### `github_otp_client.c`
- **Purpose**: C client to fetch OTPs from GitHub server
- **Features**: HTTP client, OTP validation, driver integration

## 🔧 Configuration

### Update Client Configuration

Edit `github_otp_client.c`:

```c
#define GITHUB_SERVER_URL "your-username.github.io"
#define GITHUB_REPO_NAME "otp-blocker-server"
```

### Update Server Configuration

Edit `web_otp_server.html`:

```javascript
// Update these values in the JavaScript section
const SERVER_CONFIG = {
    name: "Your OTP Server",
    description: "Custom OTP Blocker Server",
    contact: "your-email@example.com"
};
```

## 🌐 Deployment Options

### 1. GitHub Pages (Free)

**Pros:**
- Completely free
- Automatic HTTPS
- Custom domain support
- Integrated with GitHub

**Cons:**
- Static content only
- No server-side processing

**Setup:**
```yaml
# .github/workflows/deploy-otp-server.yml
- name: Deploy to GitHub Pages
  uses: peaceiris/actions-gh-pages@v3
  with:
    github_token: ${{ secrets.GITHUB_TOKEN }}
    publish_dir: ./dist
```

### 2. Vercel (Free Tier)

**Pros:**
- Serverless functions
- Global CDN
- Automatic deployments
- Custom domains

**Setup:**
```yaml
- name: Deploy to Vercel
  uses: amondnet/vercel-action@v25
  with:
    vercel-token: ${{ secrets.VERCEL_TOKEN }}
    vercel-org-id: ${{ secrets.VERCEL_ORG_ID }}
    vercel-project-id: ${{ secrets.VERCEL_PROJECT_ID }}
```

### 3. Netlify (Free Tier)

**Pros:**
- Form handling
- Serverless functions
- Custom domains
- Easy setup

**Setup:**
```yaml
- name: Deploy to Netlify
  uses: nwtgck/actions-netlify@v2.0
  with:
    publish-dir: './dist'
    production-branch: main
```

## 🔌 API Integration

### Web Server API

The web server exposes these API endpoints:

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

### HTTP API Endpoints

```bash
# Get current OTP (JSON)
GET https://your-username.github.io/otp-blocker-server/api/otp

# Generate new OTP
POST https://your-username.github.io/otp-blocker-server/api/generate

# Get server status
GET https://your-username.github.io/otp-blocker-server/api/status
```

## 📱 Client Integration

### C Client Usage

```bash
# Build the client
build_github_client.bat

# Run the client
github_otp_client.exe
```

### Web Client Usage

```html
<!DOCTYPE html>
<html>
<head>
    <title>OTP Client</title>
</head>
<body>
    <h1>OTP from GitHub Server</h1>
    <div id="otp">Loading...</div>
    
    <script>
        // Fetch OTP from GitHub server
        fetch('https://your-username.github.io/otp-blocker-server/api/otp')
            .then(response => response.json())
            .then(data => {
                document.getElementById('otp').textContent = data.otp;
            });
    </script>
</body>
</html>
```

### Python Client

```python
import requests
import json

def fetch_otp_from_github():
    url = "https://your-username.github.io/otp-blocker-server/api/otp"
    response = requests.get(url)
    if response.status_code == 200:
        data = response.json()
        return data['otp']
    return None

# Usage
otp = fetch_otp_from_github()
print(f"Current OTP: {otp}")
```

## 🔒 Security Considerations

### HTTPS Only
- GitHub Pages provides automatic HTTPS
- All communications are encrypted
- No sensitive data in URLs

### Rate Limiting
```javascript
// Implement rate limiting in web server
const rateLimit = {
    maxRequests: 10,
    windowMs: 60000, // 1 minute
    requests: new Map()
};
```

### CORS Configuration
```html
<!-- Add CORS headers for cross-origin requests -->
<meta http-equiv="Access-Control-Allow-Origin" content="*">
<meta http-equiv="Access-Control-Allow-Methods" content="GET, POST, OPTIONS">
```

## 🚀 Advanced Features

### 1. WebSocket Support

For real-time OTP updates:

```javascript
// WebSocket connection for live updates
const ws = new WebSocket('wss://your-websocket-server.com');
ws.onmessage = function(event) {
    const otp = JSON.parse(event.data).otp;
    updateOTPDisplay(otp);
};
```

### 2. Service Worker

For offline support:

```javascript
// Register service worker
if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('/sw.js')
        .then(registration => {
            console.log('Service Worker registered');
        });
}
```

### 3. Push Notifications

For mobile notifications:

```javascript
// Request notification permission
if ('Notification' in window) {
    Notification.requestPermission().then(permission => {
        if (permission === 'granted') {
            // Send push notification with OTP
        }
    });
}
```

## 🔧 Troubleshooting

### Common Issues

**GitHub Pages Not Loading:**
- Check repository settings
- Verify branch name (gh-pages)
- Check for build errors in Actions

**Client Can't Connect:**
- Verify URL in client configuration
- Check network connectivity
- Ensure HTTPS is used

**OTP Not Updating:**
- Check browser cache
- Verify JavaScript is enabled
- Check console for errors

### Debug Information

Enable debug logging:

```javascript
// In web_otp_server.html
const DEBUG = true;

if (DEBUG) {
    console.log('OTP Server initialized');
    console.log('Current OTP:', currentOTP);
}
```

## 📊 Monitoring

### GitHub Actions Logs
- Check Actions tab in repository
- Monitor deployment status
- View build logs

### Web Analytics
```html
<!-- Add Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_MEASUREMENT_ID');
</script>
```

## 🔄 Continuous Deployment

### Automatic Updates

The GitHub Actions workflow automatically:
1. Builds the application
2. Runs tests
3. Deploys to multiple platforms
4. Sends notifications

### Manual Deployment

```bash
# Manual deployment
git add .
git commit -m "Update OTP server"
git push origin main
```

## 📈 Scaling

### Multiple Instances

For high availability:

```yaml
# Deploy to multiple regions
- name: Deploy to US East
  run: deploy-to-region us-east-1
  
- name: Deploy to EU West
  run: deploy-to-region eu-west-1
  
- name: Deploy to Asia Pacific
  run: deploy-to-region ap-southeast-1
```

### Load Balancing

```javascript
// Round-robin load balancing
const servers = [
    'https://server1.github.io/otp-blocker-server/',
    'https://server2.github.io/otp-blocker-server/',
    'https://server3.github.io/otp-blocker-server/'
];

let currentServer = 0;
function getNextServer() {
    const server = servers[currentServer];
    currentServer = (currentServer + 1) % servers.length;
    return server;
}
```

## 💰 Cost Analysis

### Free Tier Limits

| Service | Free Tier | Paid Plans |
|---------|-----------|------------|
| GitHub Pages | Unlimited | N/A |
| Vercel | 100GB bandwidth | $20/month |
| Netlify | 100GB bandwidth | $19/month |

### Recommended Setup

For most use cases:
1. **GitHub Pages** - Primary hosting (free)
2. **Vercel** - Backup/fallback (free tier)
3. **Custom domain** - Professional appearance ($10-15/year)

## 🎯 Best Practices

### 1. Security
- Use HTTPS only
- Implement rate limiting
- Validate all inputs
- Log security events

### 2. Performance
- Minimize JavaScript bundle size
- Use CDN for static assets
- Implement caching
- Optimize images

### 3. Reliability
- Deploy to multiple platforms
- Implement health checks
- Monitor uptime
- Have fallback servers

### 4. User Experience
- Responsive design
- Fast loading times
- Clear error messages
- Intuitive interface

This GitHub hosting solution provides a robust, scalable, and cost-effective way to deliver OTPs to your clients while maintaining all your specified constraints! 