<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/b22f9561-d977-40cf-b6c2-4164c50399f5" /># Krapto Technologies - API Documentation

## 🌐 Live Documentation
**URL:** [https://kraptotech.github.io/krapto-api-docs/](https://aryanbarde80.github.io/Krapto-Swagger)

## 📚 API Endpoints
The documentation includes all endpoints for the horizontally scaled backend:

### Health & Monitoring
- `/health` - Instance health check
- `/health/all` - All 10 instances health
- `/metrics` - Prometheus metrics
- `/metrics/prometheus` - Prometheus endpoint

### Authentication
- `/auth/login` - User login
- `/auth/register` - User registration
- `/auth/refresh` - Token refresh

### User Management
- `/users` - List/Create users
- `/users/{id}` - Get/Update/Delete user

### Content Management
- `/content` - List/Create content

### Analytics
- `/analytics/overview` - System analytics
- `/analytics/requests` - Request analytics

### Job Management (BullMQ)
- `/jobs/queues` - Queue status
- `/jobs/{queue}/retry-failed` - Retry failed jobs

### System Admin
- `/admin/instances` - All instance status
- `/admin/cache/clear` - Clear Redis cache

## 🔗 Connect to Backend Instances
The backend is horizontally scaled across 10 instances:

| Instance | URL | Region |
|----------|-----|--------|
| Instance 1 | https://krapto-backend-server-instance-1.onrender.com | Singapore |
| Instance 2 | https://krapto-backend-server-instance-2.onrender.com | Singapore |
| Instance 3 | https://krapto-backend-server-instance-3.onrender.com | Oregon, USA |
| Instance 4 | https://krapto-backend-server-instance-4.onrender.com | Oregon, USA |
| Instance 5 | https://krapto-backend-server-instance-5.onrender.com | Frankfurt, EU |
| Instance 6 | https://krapto-backend-server-instance-6.onrender.com | Frankfurt, EU |
| Instance 7 | https://krapto-backend-server-instance-7.onrender.com | Ohio, USA |
| Instance 8 | https://krapto-backend-server-instance-8.onrender.com | Ohio, USA |
| Instance 9 | https://krapto-backend-server-instance-9.onrender.com | Virginia, USA |
| Instance 10 | https://krapto-backend-server-instance-10.onrender.com | Virginia, USA |

## 🚀 Quick Test
```bash
# Health check on Instance 1
curl https://krapto-backend-server-instance-1.onrender.com/health

# Test with Swagger UI
# Visit: https://kraptotech.github.io/krapto-api-docs/
