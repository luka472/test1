# Grade Management System API Documentation

## Base URL

```
http://localhost:5000/api
```

## Authentication

All endpoints (except `/auth/register` and `/auth/login`) require JWT token in header:

```
Authorization: Bearer {token}
```

## Endpoints

### Authentication

#### Register
```
POST /auth/register
Content-Type: application/json

{
  "username": "student",
  "email": "student@example.com",
  "password": "password123",
  "name": "John Doe",
  "role": "student"
}

Response: 201 Created
{
  "success": true,
  "message": "User registered successfully",
  "user": {
    "id": "...",
    "username": "student",
    "email": "student@example.com",
    "role": "student"
  }
}
```

#### Login
```
POST /auth/login
Content-Type: application/json

{
  "username": "admin",
  "password": "password123"
}

Response: 200 OK
{
  "success": true,
  "message": "Login successful",
  "token": "eyJhbGciOiJIUzI1NiIs...",
  "user": {
    "id": "...",
    "username": "admin",
    "email": "admin@example.com",
    "role": "admin",
    "name": "Admin User"
  }
}
```

#### Get Profile
```
GET /auth/profile
Headers: Authorization: Bearer {token}

Response: 200 OK
{
  "success": true,
  "user": { ... }
}
```

### Students

#### Get Students List
```
GET /students?page=1&limit=10
Headers: Authorization: Bearer {token}

Response: 200 OK
{
  "success": true,
  "data": [ ... ],
  "pagination": {
    "total": 50,
    "page": 1,
    "pages": 5
  }
}
```

#### Get Single Student
```
GET /students/{id}
Headers: Authorization: Bearer {token}

Response: 200 OK
{
  "success": true,
  "data": { ... }
}
```

#### Create Student
```
POST /students
Headers: Authorization: Bearer {token}
Content-Type: application/json

{
  "studentId": "STU001",
  "name": "John Doe",
  "email": "john@example.com",
  "className": "Class A",
  "major": "Computer Science",
  "phone": "1234567890"
}

Response: 201 Created
```

#### Update Student
```
PUT /students/{id}
Headers: Authorization: Bearer {token}
Content-Type: application/json

{
  "name": "Jane Doe",
  "status": "active"
}

Response: 200 OK
```

#### Delete Student
```
DELETE /students/{id}
Headers: Authorization: Bearer {token}

Response: 200 OK
```

### Grades

#### Get All Grades
```
GET /grades?page=1&limit=10
Headers: Authorization: Bearer {token}

Response: 200 OK
{
  "success": true,
  "data": [ ... ],
  "pagination": { ... }
}
```

#### Get Student Grades
```
GET /grades/student/{studentId}
Headers: Authorization: Bearer {token}

Response: 200 OK
{
  "success": true,
  "data": [ ... ],
  "gpa": 3.5
}
```

#### Create Grade
```
POST /grades
Headers: Authorization: Bearer {token}
Content-Type: application/json

{
  "student": "student_mongodb_id",
  "course": "course_mongodb_id",
  "score": 85,
  "remarks": "Good performance"
}

Response: 201 Created
{
  "success": true,
  "message": "Grade created successfully",
  "data": {
    "_id": "...",
    "student": { ... },
    "course": { ... },
    "score": 85,
    "grade": "B",
    "gradePoint": 2.7
  }
}
```

#### Update Grade
```
PUT /grades/{id}
Headers: Authorization: Bearer {token}
Content-Type: application/json

{
  "score": 90
}

Response: 200 OK
```

#### Delete Grade
```
DELETE /grades/{id}
Headers: Authorization: Bearer {token}

Response: 200 OK
```

#### Get Grade Statistics
```
GET /grades/statistics/summary
Headers: Authorization: Bearer {token}

Response: 200 OK
{
  "success": true,
  "data": {
    "totalGrades": 150,
    "averageScore": 78.5,
    "gradeDistribution": [
      { "_id": "A+", "count": 10 },
      { "_id": "A", "count": 15 },
      ...
    ]
  }
}
```

### Courses

#### Get All Courses
```
GET /courses?page=1&limit=10
Headers: Authorization: Bearer {token}

Response: 200 OK
```

#### Create Course
```
POST /courses
Headers: Authorization: Bearer {token}
Content-Type: application/json

{
  "courseCode": "CS101",
  "name": "Introduction to Computer Science",
  "credits": 3,
  "capacity": 30,
  "semester": "2024-Spring",
  "schedule": "Mon-Wed 10:00-11:30",
  "classroom": "Room 101"
}

Response: 201 Created
```

## Grade Calculation

Grades are automatically calculated based on score:

| Score | Grade | Grade Point |
|-------|-------|-------------|
| 90-100 | A+ | 4.0 |
| 87-89 | A | 3.7 |
| 84-86 | A- | 3.3 |
| 81-83 | B+ | 3.0 |
| 78-80 | B | 2.7 |
| 75-77 | B- | 2.3 |
| 72-74 | C+ | 2.0 |
| 69-71 | C | 1.7 |
| 66-68 | C- | 1.3 |
| 63-65 | D+ | 1.0 |
| 60-62 | D | 0.7 |
| <60 | F | 0 |

## GPA Calculation

GPA = (Sum of (Grade Point × Credits)) / Total Credits

## Role Permissions

| Action | Admin | Teacher | Student |
|--------|-------|---------|---------|
| View Grades | ✓ | ✓ | ✓ |
| Record Grades | ✓ | ✓ | ✗ |
| Manage Students | ✓ | ✓ | ✗ |
| Manage Courses | ✓ | ✓ | ✗ |
| Delete Grades | ✓ | ✗ | ✗ |

## Error Responses

```json
{
  "success": false,
  "message": "Error description",
  "error": "Detailed error message"
}
```

Common Status Codes:
- 200: OK
- 201: Created
- 400: Bad Request
- 401: Unauthorized
- 403: Forbidden
- 404: Not Found
- 500: Internal Server Error
