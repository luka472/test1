# Getting Started Guide

## Prerequisites

- Node.js >= 16.x
- MongoDB >= 4.4
- Docker & Docker Compose (optional)

## Project Structure

```
test1/
├── server/                 # Backend (Node.js + Express)
│   ├── src/
│   │   ├── models/        # MongoDB schemas
│   │   ├── routes/        # API routes
│   │   ├── middleware/    # Auth middleware
│   │   └── app.js         # Express app
│   ├── tests/             # Jest tests
│   ├── package.json
│   ├── .env.example
│   └── Dockerfile
├── client/                # Frontend (Vue 3)
│   ├── src/
│   │   ├── views/         # Page components
│   │   ├── stores/        # Pinia state
│   │   ├── router/        # Vue Router
│   │   └── main.js
│   ├── tests/             # Vitest tests
│   ├── package.json
│   └── Dockerfile
├── docker-compose.yml     # Docker setup
└── README.md
```

## Local Development Setup

### 1. Backend Setup

```bash
cd server

# Install dependencies
npm install

# Create .env file
cp .env.example .env

# Start MongoDB (if not running as service)
# You can use Docker: docker run -d -p 27017:27017 mongo

# Run development server
npm run dev

# Run tests
npm test
npm run test:coverage
```

The backend will run on `http://localhost:5000`

### 2. Frontend Setup

In a new terminal:

```bash
cd client

# Install dependencies
npm install

# Start development server
npm run dev

# Run tests
npm test
npm run coverage
```

The frontend will run on `http://localhost:3000`

## Docker Setup (Recommended)

### Build and Start

```bash
# Build all services
docker-compose build

# Start all services
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down
```

### Access Points

- Frontend: http://localhost:3000
- Backend: http://localhost:5000
- MongoDB: localhost:27017

## Testing

### Backend Tests

```bash
cd server

# Run all tests
npm test

# Watch mode
npm run test:watch

# Coverage report
npm run test:coverage
```

### Frontend Tests

```bash
cd client

# Run all tests
npm test

# Coverage report
npm run coverage
```

## Default Test Account

- **Username**: admin
- **Password**: password123
- **Role**: admin

## Common Tasks

### Create New Database User

```javascript
// Run this in MongoDB shell
db.createUser({
  user: "admin",
  pwd: "password123",
  roles: [
    { role: "readWrite", db: "grade-management" }
  ]
})
```

### Reset Database

```bash
# Delete all data
docker-compose exec mongodb mongosh mongodb://admin:password123@localhost:27017/grade-management --authenticationDatabase admin

# In MongoDB shell
db.dropDatabase()
```

### View MongoDB Data

```bash
docker-compose exec mongodb mongosh mongodb://admin:password123@localhost:27017/grade-management --authenticationDatabase admin

# Show collections
show collections

# View documents
db.students.find()
db.grades.find()
db.courses.find()
```

## Environment Variables

### Backend (.env)

```
PORT=5000
MONGODB_URI=mongodb://admin:password123@localhost:27017/grade-management?authSource=admin
JWT_SECRET=your_jwt_secret_key_change_in_production
NODE_ENV=development
```

### Frontend (.env.local)

```
VITE_API_URL=http://localhost:5000/api
```

## Troubleshooting

### MongoDB Connection Error

If you get a MongoDB connection error:

1. Ensure MongoDB is running
2. Check connection string in `.env`
3. Verify credentials if using authentication

```bash
# Test connection
docker-compose exec mongodb mongosh --version
```

### Port Already in Use

If port 5000 or 3000 is already in use:

```bash
# Find process using port
lsof -i :5000
lsof -i :3000

# Kill process
kill -9 <PID>
```

### Module Not Found

If you get "module not found" errors:

```bash
# Clear node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
```

## Development Tips

1. **Hot Reload**: Both frontend and backend support hot reload in development
2. **API Documentation**: See `docs/API.md` for complete API reference
3. **VS Code**: Install recommended extensions for Vue and Node.js development
4. **Testing**: Write tests as you develop features

## Performance Tips

- Use pagination for large datasets
- Index frequently queried fields in MongoDB
- Cache API responses on the frontend when appropriate
- Use lazy loading for routes

## Security Checklist

- [ ] Change JWT_SECRET in production
- [ ] Use strong database passwords
- [ ] Enable CORS restrictions in production
- [ ] Validate and sanitize all inputs
- [ ] Use HTTPS in production
- [ ] Keep dependencies updated

## Next Steps

1. Review API documentation in `docs/API.md`
2. Explore the codebase structure
3. Run tests to verify everything works
4. Start building new features

## Support

For issues or questions, check the README.md or create an issue in the repository.
