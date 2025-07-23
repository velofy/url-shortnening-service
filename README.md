# URL Shortening Service

A robust, enterprise-ready URL shortening service built with Django that can be easily integrated into any platform or enterprise software. Transform long URLs into short, manageable links with comprehensive analytics and customization options.

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Django](https://img.shields.io/badge/Django-4.2%2B-green)
![License](https://img.shields.io/badge/License-MIT-yellow)
![Build Status](https://img.shields.io/badge/Build-Passing-brightgreen)

## 🌟 Features

- **URL Shortening**: Convert long URLs into short, memorable links
- **Custom Aliases**: Create branded short URLs with custom aliases
- **Analytics Dashboard**: Comprehensive click tracking and analytics
- **Enterprise Integration**: RESTful API for seamless integration
- **User Management**: Multi-user support with role-based access
- **Link Expiration**: Set expiration dates for temporary links
- **QR Code Generation**: Generate QR codes for shortened URLs
- **Bulk Operations**: Create and manage multiple URLs at once
- **Rate Limiting**: Built-in protection against abuse
- **Custom Domains**: Support for branded domains
- **Link Preview**: Safe link preview before redirection
- **Detailed Reporting**: Export analytics data in various formats

## 🚀 Tech Stack

### Core Technologies
- **Backend**: Python 3.8+ with Django 4.2+
- **Database**: PostgreSQL (production) / SQLite (development)
- **API**: Django REST Framework
- **Authentication**: JWT with Django Simple JWT

### Additional Tools & Libraries
- **Caching**: Redis for high-performance caching
- **Task Queue**: Celery with Redis broker for background tasks
- **Web Server**: Gunicorn with Nginx (production)
- **Monitoring**: Django Debug Toolbar (development)
- **Testing**: pytest with coverage reporting
- **Documentation**: Django REST Swagger/OpenAPI
- **Deployment**: Docker & Docker Compose
- **CI/CD**: GitHub Actions
- **Analytics**: Custom analytics engine with Chart.js
- **QR Codes**: qrcode library
- **URL Validation**: validators library
- **Environment Management**: python-decouple
- **CORS**: django-cors-headers
- **Rate Limiting**: django-ratelimit

## 📋 Prerequisites

- Python 3.8 or higher
- pip (Python package manager)
- PostgreSQL (for production)
- Redis (for caching and task queue)
- Git

## 🛠️ Installation

### 1. Clone the Repository
```bash
git clone https://github.com/Velofy/url-shortnening-service.git
cd url-shortnening-service
```

### 2. Create Virtual Environment
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Environment Configuration
```bash
cp .env.example .env
# Edit .env file with your configuration
```

### 5. Database Setup
```bash
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
```

### 6. Run Development Server
```bash
python manage.py runserver
```

Visit `http://localhost:8000` to access the application.

## 🐳 Docker Installation

### Quick Start with Docker Compose
```bash
docker-compose up -d
```

### Manual Docker Setup
```bash
# Build the image
docker build -t url-shortener .

# Run with environment variables
docker run -p 8000:8000 --env-file .env url-shortener
```

## 🔧 Configuration

### Environment Variables
Create a `.env` file in the root directory:

```env
# Django Settings
SECRET_KEY=your-secret-key-here
DEBUG=False
ALLOWED_HOSTS=localhost,127.0.0.1,yourdomain.com

# Database Configuration
DATABASE_URL=postgresql://user:password@localhost:5432/urlshortener
REDIS_URL=redis://localhost:6379/0

# Domain Settings
BASE_URL=https://yourdomain.com
SHORT_URL_LENGTH=6

# Analytics
ENABLE_ANALYTICS=True
ANALYTICS_RETENTION_DAYS=365

# Rate Limiting
RATE_LIMIT_ENABLED=True
RATE_LIMIT_PER_MINUTE=60

# Email Configuration (for notifications)
EMAIL_BACKEND=django.core.mail.backends.smtp.EmailBackend
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USE_TLS=True
EMAIL_HOST_USER=your-email@gmail.com
EMAIL_HOST_PASSWORD=your-app-password
```

## 📖 API Documentation

### Authentication
```bash
# Get JWT Token
POST /api/auth/login/
{
    "username": "your_username",
    "password": "your_password"
}
```

### Core Endpoints

#### Shorten URL
```bash
POST /api/shorten/
Authorization: Bearer <token>
Content-Type: application/json

{
    "original_url": "https://example.com/very/long/url",
    "custom_alias": "custom-name",  # Optional
    "expires_at": "2024-12-31T23:59:59Z"  # Optional
}
```

#### Get URL Details
```bash
GET /api/urls/{id}/
Authorization: Bearer <token>
```

#### Redirect to Original URL
```bash
GET /{short_code}/
```

#### Analytics
```bash
GET /api/urls/{id}/analytics/
Authorization: Bearer <token>
```

#### Bulk Operations
```bash
POST /api/bulk-shorten/
Authorization: Bearer <token>
Content-Type: application/json

{
    "urls": [
        {"original_url": "https://example1.com"},
        {"original_url": "https://example2.com"}
    ]
}
```

## 🏢 Enterprise Integration

### SDK/Client Libraries
```python
# Python SDK Example
from url_shortener_client import URLShortenerClient

client = URLShortenerClient(
    api_url="https://your-domain.com/api",
    api_key="your-api-key"
)

# Shorten a URL
result = client.shorten("https://example.com/long-url")
print(f"Short URL: {result.short_url}")
```

### Webhook Integration
```bash
# Configure webhooks for real-time notifications
POST /api/webhooks/
{
    "url": "https://your-app.com/webhook-endpoint",
    "events": ["url_created", "url_clicked", "url_expired"]
}
```

## 📊 Analytics & Reporting

- **Real-time Click Tracking**: Monitor URL performance in real-time
- **Geographic Analytics**: See where your clicks are coming from
- **Device & Browser Stats**: Understand your audience
- **Referrer Tracking**: Know which platforms drive traffic
- **Export Options**: CSV, JSON, PDF reports
- **Custom Date Ranges**: Flexible reporting periods

## 🔒 Security Features

- **Rate Limiting**: Prevent abuse with configurable limits
- **URL Validation**: Malicious URL detection and blocking
- **Access Control**: Role-based permissions
- **Audit Logs**: Complete activity tracking
- **HTTPS Enforcement**: Secure connections only
- **CORS Configuration**: Cross-origin request management
- **SQL Injection Protection**: Built-in Django security

## 🧪 Testing

### Run Tests
```bash
# Run all tests
python manage.py test

# Run with coverage
coverage run --source='.' manage.py test
coverage html
```

### API Testing
```bash
# Install pytest
pip install pytest pytest-django

# Run API tests
pytest tests/api/
```

## 🚀 Deployment

### Production Checklist
- [ ] Set `DEBUG=False`
- [ ] Configure secure `SECRET_KEY`
- [ ] Set up PostgreSQL database
- [ ] Configure Redis for caching
- [ ] Set up SSL certificates
- [ ] Configure domain and DNS
- [ ] Set up monitoring and logging
- [ ] Configure backup strategy

### Docker Production Deployment
```bash
docker-compose -f docker-compose.prod.yml up -d
```

### Traditional Server Deployment
```bash
# Install dependencies
pip install -r requirements.txt

# Collect static files
python manage.py collectstatic

# Run with Gunicorn
gunicorn url_shortener.wsgi:application --bind 0.0.0.0:8000
```

## 📈 Performance Optimization

- **Database Indexing**: Optimized for fast lookups
- **Redis Caching**: Frequently accessed data cached
- **CDN Support**: Static files served via CDN
- **Database Connection Pooling**: Efficient database connections
- **Async Task Processing**: Background job processing with Celery

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Setup
```bash
# Install development dependencies
pip install -r requirements-dev.txt

# Run pre-commit hooks
pre-commit install

# Run linting
flake8 .
black .
```

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🐛 Support & Issues

- **Bug Reports**: [GitHub Issues](https://github.com/Velofy/url-shortnening-service/issues)
- **Feature Requests**: [GitHub Discussions](https://github.com/Velofy/url-shortnening-service/discussions)
- **Documentation**: [Wiki](https://github.com/Velofy/url-shortnening-service/wiki)
- **Email Support**: support@yourdomain.com

## 🛣️ Roadmap

- [ ] **v2.0**: GraphQL API support
- [ ] **v2.1**: Mobile SDK (iOS/Android)
- [ ] **v2.2**: Advanced analytics with ML insights
- [ ] **v2.3**: Multi-tenant architecture
- [ ] **v2.4**: Plugin system for custom integrations
- [ ] **v2.5**: Real-time collaboration features

## 👥 Authors

- **Your Name** - *Initial work* - [@yourusername](https://github.com/yourusername)

## 🙏 Acknowledgments

- Django community for the excellent framework
- Contributors and beta testers
- Open source libraries that make this project possible

---

**Made with ❤️ for the enterprise community**