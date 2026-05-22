# Student Grade Management System

## 📚 Project Overview

A comprehensive full-stack student grade management system built with Vue.js, Node.js, Express, and MongoDB.

## ✨ Features

- 👤 **User Authentication**: Registration, login with JWT authentication
- 👨‍🎓 **Student Management**: Add, update, delete, and manage student information
- 📚 **Course Management**: Create and manage courses with enrollment
- 📊 **Grade Management**: Record, update, and analyze grades
- 📈 **Statistics & Analytics**: Grade analysis, GPA calculation, distribution analysis
- 🔐 **Role-Based Access Control**: Admin, Teacher, and Student roles
- ✅ **Comprehensive Testing**: Jest for backend, Vitest for frontend

## 🛠 Tech Stack

### Frontend
- Vue 3
- Vue Router
- Pinia (State Management)
- Element Plus UI
- Axios
- Vitest & @vue/test-utils

### Backend
- Node.js
- Express.js
- MongoDB with Mongoose
- JWT Authentication
- Jest Testing Framework

## 🚀 Quick Start

### Prerequisites
- Node.js >= 16
- MongoDB >= 4.4
- Docker & Docker Compose (optional)

### Backend Setup

```bash
cd server
npm install
cp .env.example .env
npm run dev
```

### Frontend Setup

```bash
cd client
npm install
npm run dev
```

Visit http://localhost:3000 in your browser.

### Docker Setup (Recommended)

```bash
docker-compose up -d
```

## 📖 Documentation

- [Getting Started Guide](./GETTING_STARTED.md) - Detailed setup and usage instructions
- [API Documentation](./docs/API.md) - Complete API reference
- [Architecture](./docs/ARCHITECTURE.md) - System architecture and design

## 📁 Project Structure

```
├── server/                  # Backend (Node.js + Express)
│   ├── src/
│   │   ├── models/         # MongoDB schemas
│   │   ├── controllers/    # Business logic
│   │   ├── routes/         # API routes
│   │   ├── middleware/     # Express middleware
│   │   └── app.js
│   ├── tests/              # Jest test files
│   └── package.json
├── client/                  # Frontend (Vue 3)
│   ├── src/
│   │   ├── views/          # Page components
│   │   ├── components/     # Reusable components
│   │   ├── stores/         # Pinia stores
│   │   ├── router/         # Vue Router config
│   │   ├── api/            # API client
│   │   └── main.js
│   ├── tests/              # Vitest test files
│   └── package.json
└── docker-compose.yml      # Docker configuration
```

## 🔑 Key Modules

### Authentication
- User registration and login
- JWT token management
- Password encryption with bcryptjs

### Student Management
- CRUD operations for students
- Pagination and filtering
- Student status management

### Grade Management
- Record and update grades
- Automatic GPA calculation
- Grade statistics and analysis

### Course Management
- Create and maintain courses
- Student enrollment management
- Course capacity control

## 🧪 Testing

### Backend Tests
```bash
cd server
npm test
npm run test:watch
```

### Frontend Tests
```bash
cd client
npm test
npm run coverage
```

## 📊 API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - User login
- `GET /api/auth/profile` - Get user profile

### Students
- `GET /api/students` - Get students list
- `POST /api/students` - Create student
- `PUT /api/students/:id` - Update student
- `DELETE /api/students/:id` - Delete student

### Grades
- `GET /api/grades` - Get grades list
- `POST /api/grades` - Create grade
- `PUT /api/grades/:id` - Update grade
- `DELETE /api/grades/:id` - Delete grade
- `GET /api/grades/statistics/summary` - Get statistics
- `GET /api/grades/student/:studentId` - Get student grades

### Courses
- `GET /api/courses` - Get courses list
- `POST /api/courses` - Create course
- `PUT /api/courses/:id` - Update course
- `DELETE /api/courses/:id` - Delete course

## 👥 User Roles

| Feature | Admin | Teacher | Student |
|---------|-------|---------|---------|
| View Grades | ✓ | ✓ | ✓ |
| Record Grades | ✓ | ✓ | ✗ |
| Manage Students | ✓ | ✓ | ✗ |
| Manage Courses | ✓ | ✓ | ✗ |
| Delete Grades | ✓ | ✗ | ✗ |

## 🔐 Security

- Password hashing with bcryptjs
- JWT authentication
- CORS protection
- Input validation
- Error message sanitization

## 📝 Default Test Account

- Username: `admin`
- Password: `password123`
- Role: `admin`

## 🐳 Docker Support

```bash
# Build images
docker-compose build

# Start containers
docker-compose up -d

# View logs
docker-compose logs -f

# Stop containers
docker-compose down
```

## 📦 Environment Variables

### Backend (.env)
```
PORT=5000
MONGODB_URI=mongodb://localhost:27017/grade-management
JWT_SECRET=your_secret_key
NODE_ENV=development
```

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 💡 Support

For support, please open an issue or contact the development team.

---

**Last Updated**: 2024
**Version**: 1.0.0
