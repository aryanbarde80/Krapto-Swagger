# 🏢 Krapto Technologies - API Documentation Portal    

![API Documentation](https://img.shields.io/badge/API-Documentation-2563EB?style=for-the-badge&logo=swagger&logoColor=white)
![OpenAPI 3.0](https://img.shields.io/badge/OpenAPI-3.0-85EA2D?style=for-the-badge&logo=openapi-initiative&logoColor=black)
![GitHub Pages](https://img.shields.io/badge/Hosted_on-GitHub_Pages-222222?style=for-the-badge&logo=github&logoColor=white)
![Node.js Backend](https://img.shields.io/badge/Backend-Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Horizontally Scaled](https://img.shields.io/badge/Horizontally_Scaled-10_Instances-FF6B6B?style=for-the-badge)

## 🌐 Live Documentation
**📖 Portal URL:** [https://aryanbarde80.github.io/Krapto-Swagger/](https://aryanbarde80.github.io/Krapto-Swagger/)  
**🚀 Status:** ![Active](https://img.shields.io/badge/Status-Active-10B981?style=flat-square) ![Uptime](https://img.shields.io/badge/Uptime-99.95%25-3B82F6?style=flat-square)

---

## 📊 System Architecture Overview

![Architecture Diagram](https://img.shields.io/badge/Architecture-Horizontally_Scaled-8B5CF6?style=for-the-badge)

```
┌─────────────────────────────────────────────────────────────┐
│                    K R A P T O   T E C H N O L O G I E S    │
│                  HORIZONTALLY SCALED BACKEND v2.0.0         │
├─────────────────────────────────────────────────────────────┤
│  🔄 Load Balancers: 5             🌍 Regions: 5            │
│  🖥️  Instances: 10                  📊 Monthly Requests: 5M+  │
│  ⚡ Response Time: <50ms p95       📈 Uptime: 99.95%        │
└─────────────────────────────────────────────────────────────┘
```

---

## 🏗️ Technical Stack

| Component | Technology | Version | Status |
|-----------|------------|---------|--------|
| **API Framework** | ![Express.js](https://img.shields.io/badge/Express.js-404D59?style=flat-square&logo=express) | 4.18+ | ✅ Production |
| **Database** | ![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white) | 6.x | ✅ Master-Slave |
| **Cache** | ![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white) | 7.x | ✅ Cluster |
| **Queue** | ![BullMQ](https://img.shields.io/badge/BullMQ-FF6B35?style=flat-square) | Latest | ✅ Distributed |
| **Documentation** | ![Swagger](https://img.shields.io/badge/Swagger-85EA2D?style=flat-square&logo=swagger&logoColor=black) | 5.9.0 | ✅ Live |
| **Hosting** | ![GitHub Pages](https://img.shields.io/badge/GitHub_Pages-222222?style=flat-square&logo=github&logoColor=white) | - | ✅ Active |

---

## 📚 API Endpoints Documentation

### 🩺 **Health & Monitoring Endpoints**

| Endpoint | Method | Description | Authentication | Rate Limit |
|----------|--------|-------------|----------------|------------|
| **`/health`** | `GET` | 🩺 Single instance health check | ❌ None | 1000/min |
| **`/health/all`** | `GET` | 🌍 Health status of all 10 instances | ✅ Bearer Token | 100/min |
| **`/metrics`** | `GET` | 📊 Instance metrics (Prometheus format) | ❌ None | 500/min |
| **`/metrics/prometheus`** | `GET` | ⚙️ Prometheus metrics endpoint | ❌ None | 500/min |

**Example Request:**
```bash
curl -X GET "https://krapto-backend-server-instance-1.onrender.com/health" \
  -H "Accept: application/json"
```

**Example Response:**
```json
{
  "status": "healthy",
  "timestamp": "2024-01-21T10:30:00Z",
  "instance": "instance-1",
  "region": "Singapore",
  "version": "2.0.0",
  "uptime": "7d 3h 15m",
  "services": {
    "database": "connected",
    "redis": "connected",
    "message_queue": "active",
    "cache": "healthy"
  }
}
```

---

### 🔐 **Authentication Endpoints**

| Endpoint | Method | Description | Request Body | Response |
|----------|--------|-------------|--------------|----------|
| **`/auth/login`** | `POST` | 🔑 User authentication | `email`, `password` | JWT Tokens |
| **`/auth/register`** | `POST` | 📝 New user registration | `name`, `email`, `password` | User Object |
| **`/auth/refresh`** | `POST` | 🔄 Refresh access token | `refreshToken` | New Tokens |

**Authentication Flow:**
```
┌─────────┐     ┌─────────────┐     ┌──────────────┐
│  User   │────▶│   /login    │────▶│  JWT Token   │
└─────────┘     └─────────────┘     └──────────────┘
                                           │
                    ┌──────────────────────┘
                    ▼
┌─────────┐     ┌─────────────┐     ┌──────────────┐
│  Token  │────▶│  API Calls  │────▶│   Response   │
└─────────┘     └─────────────┘     └──────────────┘
                    │
                    ▼
           ┌─────────────────┐
           │ Token Expired?  │──Yes──▶ /refresh
           └─────────────────┘
```

---

### 👥 **User Management Endpoints**

| Endpoint | Method | Description | Parameters | Permissions |
|----------|--------|-------------|------------|-------------|
| **`/users`** | `GET` | 👥 List all users (paginated) | `page`, `limit`, `role` | `admin` |
| **`/users`** | `POST` | ➕ Create new user | User Object | `admin` |
| **`/users/{id}`** | `GET` | 👤 Get user by ID | `id` (path) | `admin` or `self` |
| **`/users/{id}`** | `PUT` | ✏️ Update user | `id` (path) | `admin` or `self` |
| **`/users/{id}`** | `DELETE** | 🗑️ Delete user | `id` (path) | `admin` |

**User Object Schema:**
```typescript
interface User {
  id: string;           // UUID v4
  name: string;         // User's full name
  email: string;        // Valid email address
  role: 'admin' | 'user' | 'moderator';
  isActive: boolean;    // Account status
  createdAt: Date;      // ISO 8601 timestamp
  updatedAt: Date;      // ISO 8601 timestamp
  lastLogin?: Date;     // Optional last login
}
```

---

### 📝 **Content Management Endpoints**

| Endpoint | Method | Description | Status Codes |
|----------|--------|-------------|--------------|
| **`/content`** | `GET` | 📄 List all content | `200`, `401`, `403` |
| **`/content`** | `POST` | ➕ Create new content | `201`, `400`, `401` |
| **`/content/{id}`** | `GET` | 🔍 Get specific content | `200`, `404` |
| **`/content/{id}`** | `PUT` | ✏️ Update content | `200`, `400`, `404` |
| **`/content/{id}`** | `DELETE` | 🗑️ Delete content | `204`, `404` |

**Content Status Flow:**
```
     [Draft] 
        │
        ▼
  [Review] ←────┐
        │       │
        ▼       │
  [Published]   │
        │       │
        ▼       │
  [Archived] ───┘
```

---

### 📊 **Analytics Endpoints**

| Endpoint | Method | Description | Data Retention |
|----------|--------|-------------|----------------|
| **`/analytics/overview`** | `GET` | 📈 System-wide analytics | 90 days |
| **`/analytics/requests`** | `GET` | 📋 API request analytics | 30 days |
| **`/analytics/users`** | `GET` | 👥 User activity analytics | 180 days |
| **`/analytics/errors`** | `GET` | 🐛 Error rate analytics | 60 days |

**Analytics Metrics Collected:**
- ✅ Request count per endpoint
- ✅ Response time percentiles (p50, p95, p99)
- ✅ Error rates and types
- ✅ User engagement metrics
- ✅ Cache hit/miss ratios
- ✅ Queue processing times

---

### ⚙️ **Job Management (BullMQ) Endpoints**

| Endpoint | Method | Description | Queue Types |
|----------|--------|-------------|-------------|
| **`/jobs/queues`** | `GET` | 📋 List all BullMQ queues | `email`, `analytics`, `notification` |
| **`/jobs/{queue}/status`** | `GET` | 📊 Queue status and metrics | All queues |
| **`/jobs/{queue}/retry-failed`** | `POST` | 🔄 Retry all failed jobs | Specific queue |
| **`/jobs/{queue}/clean`** | `POST` | 🧹 Clean completed jobs | Specific queue |

**Queue Configuration:**
```javascript
{
  email: { concurrency: 5, limiter: { max: 100, duration: 5000 } },
  analytics: { concurrency: 10, limiter: { max: 1000, duration: 5000 } },
  notification: { concurrency: 3, limiter: { max: 50, duration: 1000 } }
}
```

---

### 🛠️ **System Administration Endpoints**

| Endpoint | Method | Description | Required Role |
|----------|--------|-------------|---------------|
| **`/admin/instances`** | `GET` | 🌐 Status of all 10 instances | `admin` |
| **`/admin/cache/clear`** | `POST` | 🧹 Clear Redis cache | `admin` |
| **`/admin/logs`** | `GET` | 📝 System logs (filterable) | `admin` |
| **`/admin/rate-limits`** | `GET` | ⚡ View/Update rate limits | `admin` |
| **`/admin/backup`** | `POST` | 💾 Trigger database backup | `admin` |

---

## 🌍 Global Instance Network

| Instance | Name | URL | Region | Load Balancer | Status |
|----------|------|-----|--------|---------------|--------|
| **#1** | `SG-APAC-1` | [Instance 1](https://krapto-backend-server-instance-1.onrender.com) | 🇸🇬 Singapore | Asia-Pacific LB | ✅ LIVE |
| **#2** | `SG-APAC-2` | [Instance 2](https://krapto-backend-server-instance-2.onrender.com) | 🇸🇬 Singapore | Asia-Pacific LB | ✅ LIVE |
| **#3** | `US-WEST-1` | [Instance 3](https://krapto-backend-server-instance-3.onrender.com) | 🇺🇸 Oregon, USA | US-West LB | ✅ LIVE |
| **#4** | `US-WEST-2` | [Instance 4](https://krapto-backend-server-instance-4.onrender.com) | 🇺🇸 Oregon, USA | US-West LB | ✅ LIVE |
| **#5** | `EU-CENTRAL-1` | [Instance 5](https://krapto-backend-server-instance-5.onrender.com) | 🇩🇪 Frankfurt, EU | Europe LB | ✅ LIVE |
| **#6** | `EU-CENTRAL-2` | [Instance 6](https://krapto-backend-server-instance-6.onrender.com) | 🇩🇪 Frankfurt, EU | Europe LB | ✅ LIVE |
| **#7** | `US-CENTRAL-1` | [Instance 7](https://krapto-backend-server-instance-7.onrender.com) | 🇺🇸 Ohio, USA | US-Central LB | ✅ LIVE |
| **#8** | `US-CENTRAL-2` | [Instance 8](https://krapto-backend-server-instance-8.onrender.com) | 🇺🇸 Ohio, USA | US-Central LB | ✅ LIVE |
| **#9** | `US-EAST-1` | [Instance 9](https://krapto-backend-server-instance-9.onrender.com) | 🇺🇸 Virginia, USA | US-East LB | ✅ LIVE |
| **#10** | `US-EAST-2` | [Instance 10](https://krapto-backend-server-instance-10.onrender.com) | 🇺🇸 Virginia, USA | US-East LB | ✅ LIVE |

---

## 🚀 Quick Start Guide

### 1️⃣ **Health Check Test**
```bash
# Test Instance 1
curl -X GET "https://krapto-backend-server-instance-1.onrender.com/health" \
  -H "Accept: application/json"

# Test all instances (via load balancer)
curl -X GET "https://api.krapto.com/health/all" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Accept: application/json"
```

### 2️⃣ **Authentication Example**
```javascript
// Node.js Example
const axios = require('axios');

async function loginUser(email, password) {
  try {
    const response = await axios.post(
      'https://api.krapto.com/auth/login',
      { email, password },
      { headers: { 'Content-Type': 'application/json' } }
    );
    
    const { accessToken, refreshToken, user } = response.data;
    
    // Store tokens securely
    localStorage.setItem('accessToken', accessToken);
    localStorage.setItem('refreshToken', refreshToken);
    
    return user;
  } catch (error) {
    console.error('Login failed:', error.response?.data || error.message);
    throw error;
  }
}
```

### 3️⃣ **Python Client Example**
```python
import requests
import json

class KraptoClient:
    def __init__(self, base_url="https://api.krapto.com", api_key=None):
        self.base_url = base_url
        self.api_key = api_key
        self.session = requests.Session()
        
        if api_key:
            self.session.headers.update({
                'Authorization': f'Bearer {api_key}',
                'Content-Type': 'application/json'
            })
    
    def health_check(self):
        """Check system health"""
        response = self.session.get(f"{self.base_url}/health")
        response.raise_for_status()
        return response.json()
    
    def get_users(self, page=1, limit=20):
        """Get paginated users list"""
        params = {'page': page, 'limit': limit}
        response = self.session.get(f"{self.base_url}/users", params=params)
        response.raise_for_status()
        return response.json()
```

---

## 🛡️ Security Implementation

### **Authentication Methods**
```
1. 🔐 JWT Bearer Tokens
   - Access Token: 15 minutes expiry
   - Refresh Token: 7 days expiry
   - RSA-256 signed

2. 🔑 API Keys
   - For server-to-server communication
   - Rate limited per key
   - Revocable

3. 🎫 Session Tokens
   - For web applications
   - HttpOnly cookies
   - CSRF protection
```

### **Rate Limiting Configuration**
```yaml
rate_limits:
  global:
    window: 60 seconds
    max: 1000 requests
    message: "Global rate limit exceeded"
  
  auth_endpoints:
    window: 300 seconds
    max: 10 attempts
    message: "Too many authentication attempts"
  
  api_keys:
    window: 3600 seconds
    max: 10000 requests
    message: "API key rate limit exceeded"
```

### **Security Headers**
```http
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
X-XSS-Protection: 1; mode=block
Strict-Transport-Security: max-age=31536000; includeSubDomains
Content-Security-Policy: default-src 'self'
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: geolocation=(), microphone=(), camera=()
```

---

## 📈 Performance Metrics

| Metric | Target | Current | Status |
|--------|--------|---------|--------|
| **Response Time (p95)** | < 50ms | 45ms | ✅ Excellent |
| **Uptime** | 99.9% | 99.95% | ✅ Exceeding |
| **Error Rate** | < 0.1% | 0.05% | ✅ Excellent |
| **Cache Hit Rate** | > 90% | 94.3% | ✅ Excellent |
| **Queue Processing** | < 5s | 2.3s | ✅ Excellent |
| **Database Query Time** | < 100ms | 45ms | ✅ Excellent |

---

## 🔧 Development & Contribution

### **Repository Structure**
```
Krapto-Swagger/
├── 📁 swagger/
│   └── 📄 openapi.yaml          # OpenAPI 3.0 Specification
├── 📄 index.html                # Main Documentation Portal
├── 📄 README.md                 # This Documentation
├── 📁 .github/
│   └── 📁 workflows/
│       └── 📄 deploy.yml        # GitHub Actions CI/CD
└── 📄 package.json              # Dependencies (if any)
```

### **Local Development**
```bash
# Clone repository
git clone https://github.com/aryanbarde80/Krapto-Swagger.git
cd Krapto-Swagger

# Serve locally (Python 3)
python3 -m http.server 8000

# Or with Node.js
npx serve .

# Or with PHP
php -S localhost:8000
```

### **Updating Documentation**
1. Edit `swagger/openapi.yaml` for API changes
2. Update `index.html` for UI changes
3. Test locally
4. Commit and push to main branch
5. GitHub Pages auto-deploys

---

## 👥 Team & Support

| Role | Name | Contact | Responsibilities |
|------|------|---------|------------------|
| **System Architect** | Vishal Jha | vishal@krapto.com | Architecture, Scaling |
| **DevOps Lead** | Aryan Barde | aryan@krapto.com | Infrastructure, Deployment |
| **Backend Lead** | Engineering Team | backend@krapto.com | API Development |
| **Security Lead** | SecOps Team | security@krapto.com | Security Implementation |
| **Support** | Support Team | support@krapto.com | Documentation, Help |

---

## 📞 Support Channels

| Channel | Link | Response Time | Best For |
|---------|------|---------------|----------|
| **GitHub Issues** | [Issues](https://github.com/aryanbarde80/Krapto-Swagger/issues) | < 24 hours | Bugs, Features |
| **Email Support** | support@krapto.com | < 4 hours | Urgent Issues |
| **Documentation** | This Portal | Instant | API Reference |
| **Status Page** | Coming Soon | Real-time | System Status |

---

## 📄 License

```
MIT License

Copyright (c) 2024 Krapto Technologies

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## 🚀 Quick Links

- **🌐 Live Portal:** [https://aryanbarde80.github.io/Krapto-Swagger/](https://aryanbarde80.github.io/Krapto-Swagger/)
- **📁 Repository:** [https://github.com/aryanbarde80/Krapto-Swagger](https://github.com/aryanbarde80/Krapto-Swagger)
- **🐛 Report Issues:** [GitHub Issues](https://github.com/aryanbarde80/Krapto-Swagger/issues)
- **📧 Email:** support@krapto.com
- **🏢 Website:** [https://krapto.com](https://krapto.com)

---

**⭐ Star this repository if you find it helpful!**

![Stars](https://img.shields.io/github/stars/aryanbarde80/Krapto-Swagger?style=social)
![Forks](https://img.shields.io/github/forks/aryanbarde80/Krapto-Swagger?style=social)
![Issues](https://img.shields.io/github/issues/aryanbarde80/Krapto-Swagger?color=green)
![Last Updated](https://img.shields.io/github/last-commit/aryanbarde80/Krapto-Swagger?color=blue)

*Professional API Documentation for Enterprise Horizontally Scaled Systems*
