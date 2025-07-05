# GestSup Mobile App 📱

A complete mobile application solution for GestSup ticket management system with real-time WebSocket notifications and push notifications.

## 🎯 Project Overview

This project extends the existing [GestSup](https://doc.gestsup.fr/) system with:
- **Mobile API Layer** - RESTful APIs optimized for mobile consumption
- **WebSocket Plugin** - Real-time notifications for ticket events
- **Push Notifications** - Firebase Cloud Messaging integration
- **Mobile App** - Cross-platform mobile application

## 🚀 Quick Start

### Prerequisites
- Docker & Docker Compose
- Node.js 18+ (for local development)
- Git

### 1. Clone Repository
```bash
git clone https://github.com/otmanebaraka/gestsup-mobile-app.git
cd gestsup-mobile-app
```

### 2. Environment Setup
```bash
cp .env.example .env
# Edit .env file with your configurations
```

### 3. Start Services
```bash
# Start all services with Docker Compose
docker-compose up -d

# Check service status
docker-compose ps

# View logs
docker-compose logs -f
```

### 4. GestSup Installation
1. Access GestSup at http://localhost:80
2. Follow the web installation wizard
3. Use database credentials from .env file
4. Complete the setup

## 📦 Services

- **GestSup Web**: http://localhost:80 (PHP/Apache)
- **Mobile API**: http://localhost:3000 (Node.js/Express)
- **WebSocket Server**: http://localhost:3001 (Socket.IO)
- **Database**: localhost:3306 (MariaDB)

## 🔌 API Endpoints

### Authentication
- `POST /api/v1/auth/login` - User login
- `POST /api/v1/auth/refresh` - Refresh JWT token

### Tickets
- `GET /api/v1/tickets` - List tickets
- `POST /api/v1/tickets` - Create ticket
- `PUT /api/v1/tickets/:id/assign` - Assign ticket
- `PUT /api/v1/tickets/:id/status` - Update status

### Real-time Events
- `ticket_created` - New ticket notification
- `ticket_assigned` - Assignment notification
- `ticket_status_changed` - Status change notification

## 📱 Mobile Features

- ✅ Live push notifications
- ✅ Real-time ticket updates via WebSocket
- ✅ Ticket creation and management
- ✅ Technician assignment
- ✅ Status updates
- ✅ Offline support

## 📖 Documentation

- [GestSup Installation](https://doc.gestsup.fr/install/)
- [Project Setup](./docs/setup.md)
- [API Documentation](./docs/api.md)
- [Mobile App Guide](./docs/mobile.md)

## 🤝 Contributing

1. Fork the repository
2. Create feature branch
3. Commit changes
4. Open Pull Request

---
**Built for GestSup community** 🎯