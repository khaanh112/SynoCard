# SynoCard - Smart Digital Business Card Platform

A modern platform for creating smart digital business cards with QR codes and personal profile websites.

🌐 **Live Demo**: [https://synocard.vercel.app/](https://synocard.vercel.app/)

## 🚀 Quick Start

### Prerequisites

- Docker & Docker Compose installed
- Node.js 20+ (for local development outside Docker)
- Git

### Setup Instructions

1. **Clone the repository**
   ```bash
   git clone https://github.com/khaanh112/SynoCard.git
   cd SynoCard
   ```

2. **Set up environment file**
   
   The `.env` file is already configured with default values. Update if needed for production.

3. **Start all services**
   ```bash
   docker-compose up
   ```

4. **Access the application**
   - Frontend: http://localhost:5173
   - Backend API: http://localhost:3000
   - API Docs: http://localhost:3000/api/v1/docs
   - pgAdmin: http://localhost:5050
   - Health Check: http://localhost:3000/health

### Development Workflow

#### Backend Development

```bash
cd backend
npm install
npm run dev
```

#### Frontend Development

```bash
cd frontend
npm install
npm run dev
```

#### Database Migrations

```bash
cd backend
npx prisma migrate dev
npx prisma generate
```

#### Database Seeding

```bash
cd backend
npx prisma db seed
```

### Docker Commands

```bash
# Start services
docker-compose up

# Start in background
docker-compose up -d

# Stop services
docker-compose down

# View logs
docker-compose logs -f

# Rebuild containers
docker-compose up --build

# Remove volumes (careful - deletes data!)
docker-compose down -v
```

## 📁 Project Structure

```
├── backend/              # Express.js API
│   ├── src/
│   │   ├── routes/      # API routes (auth, profile, analytics)
│   │   ├── controllers/ # Request handlers
│   │   ├── middleware/  # Auth & rate limiting
│   │   ├── utils/       # JWT, QR code, validation
│   │   ├── lib/         # Prisma client
│   │   └── config/      # Swagger configuration
│   ├── prisma/          # Database schema & migrations
│   │   ├── schema.prisma
│   │   ├── seed.js
│   │   └── migrations/
│   ├── uploads/         # File uploads (avatars, QR codes)
│   └── package.json
│
├── frontend/            # React + Vite SPA
│   ├── src/
│   │   ├── components/  # React components
│   │   │   ├── analytics/  # Profile analytics
│   │   │   └── wizard/     # Profile creation wizard
│   │   ├── pages/       # Page components
│   │   │   ├── public/     # Public profile view
│   │   │   ├── CreateProfileWizard.jsx
│   │   │   ├── Dashboard.jsx
│   │   │   └── EditProfile.jsx
│   │   ├── themes/      # Profile themes
│   │   ├── store/       # Zustand state management
│   │   ├── config/      # API configuration
│   │   └── utils/       # Validation schemas
│   └── package.json
│
└── docker-compose.yml   # Docker orchestration
```

## 🛠️ Tech Stack

### Frontend
- React 18+ (JavaScript/ES6+)
- Vite (Build tool)
- Tailwind CSS (Styling)
- React Router v6 (Routing)
- React Hook Form + Yup (Forms & Validation)
- Zustand (State management)
- Axios (HTTP client)

### Backend
- Node.js 20+ (JavaScript/ES6+)
- Express.js (Web framework)
- Prisma (ORM)
- PostgreSQL 15 (Database)
- JWT (Authentication)
- Swagger/OpenAPI (API documentation)
- QRCode (QR code generation)
- Express Rate Limit (API protection)
- Multer (File uploads)

### DevOps & Deployment
- Docker & Docker Compose
- Vercel (Frontend hosting)
- Railway (Backend hosting - optional)

## 📚 API Documentation

Once the backend is running, visit:
- **Swagger UI**: http://localhost:3000/api/v1/docs - Interactive API documentation with request/response examples
- **Health Check**: http://localhost:3000/health - API health status and service dependencies

### Available Endpoints

#### Authentication
- `POST /api/v1/auth/register` - Register new user
- `POST /api/v1/auth/login` - Login with email/password
- `POST /api/v1/auth/refresh` - Refresh access token
- `POST /api/v1/auth/logout` - Logout and invalidate tokens
- `GET /api/v1/auth/me` - Get current user (protected)

#### Profile Management
- `POST /api/v1/profile` - Create profile
- `GET /api/v1/profile/:username` - Get profile by username
- `PUT /api/v1/profile/:id` - Update profile
- `DELETE /api/v1/profile/:id` - Delete profile

#### Analytics
- `POST /api/v1/analytics/profile-view` - Track profile view
- `GET /api/v1/analytics/profile/:profileId` - Get profile analytics

The Swagger documentation provides detailed information about:
- Request/response schemas
- Authentication requirements (JWT Bearer tokens)
- Example requests and responses
- Error codes and messages

## 🧪 Testing

```bash
# Backend tests
cd backend
npm test
npm run test:watch
npm run test:coverage

# Frontend tests
cd frontend
npm test
npm run test:e2e
```

## 🔧 Configuration

### pgAdmin Setup

1. Access pgAdmin at http://localhost:5050
2. Login with credentials from `.env`:
   - Email: admin@smartcard.com
   - Password: admin
3. Add server:
   - Name: SmartCard Local
   - Host: postgres
   - Port: 5432
   - Username: postgres
   - Password: (from .env)

## 🎯 Features

- **User Authentication**: Secure JWT-based authentication with refresh tokens
- **Profile Creation Wizard**: Step-by-step guide to create professional profiles
- **QR Code Generation**: Automatic QR code generation for each profile
- **Profile Analytics**: Track profile views and engagement
- **Responsive Design**: Mobile-first design with Tailwind CSS
- **File Upload**: Avatar and image upload support
- **Public Profile Pages**: Shareable profile URLs (e.g., `/profile/:username`)
- **Dashboard**: Manage multiple profiles and view analytics

## 🚢 Deployment

### Frontend (Vercel)
The frontend is deployed on Vercel at [https://synocard.vercel.app/](https://synocard.vercel.app/)

### Backend (Local/Railway)
Backend can be deployed to Railway or any Node.js hosting platform. Update the `BACKEND_URL` in frontend configuration.

## 🤝 Contributing

1. Create feature branch
2. Make changes
3. Write tests
4. Submit pull request

## 📄 License

MIT License

## 👥 Author

- GitHub: [khaanh112](https://github.com/khaanh112)
- Project: SynoCard - Smart Digital Business Card Platform

## 🐛 Troubleshooting

### Port already in use
```bash
# Check what's using the port
netstat -ano | findstr :3000
# Kill the process
taskkill /PID <pid> /F
```

### Docker container won't start
```bash
docker-compose down
docker-compose up --build
```

### Database connection issues
```bash
# Check if postgres is running
docker-compose ps
# View postgres logs
docker-compose logs postgres
```

### Reset everything
```bash
docker-compose down -v
docker-compose up --build
```
