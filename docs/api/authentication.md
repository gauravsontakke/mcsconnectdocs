# Authentication API

## Register a new user
`POST /api/auth/register`

### Request
```json
{
  "username": "john_doe",
  "email": "john@example.com",
  "password": "securePassword123",
  "contact": "9876543210",
  "first_name": "John",
  "last_name": "Doe"
}
```

### Response
```json
{
  "success": true,
  "message": "User registered successfully",
  "user": {
    "id": 1,
    "username": "john_doe",
    "email": "john@example.com"
  }
}
```

## User login
`POST /api/auth/login`

### Request
```json
{
  "username": "john_doe",
  "password": "securePassword123"
}
```

### Response
```json
{
  "token": "jwt_token_here",
  "user": {
    "id": 1,
    "username": "john_doe",
    "email": "john@example.com"
  }
}
```

## User logout
`POST /api/auth/logout`

### Headers
```
Authorization: Bearer <token>
```

### Response
```json
{
  "message": "User logged out successfully"
}
```

## Request password reset
`POST /api/auth/forgot-password`

### Request
```json
{
  "email": "john@example.com"
}
```

### Response
```json
{
  "message": "Password reset link sent to email"
}
```

## Reset password
`POST /api/auth/reset-password`

### Request
```json
{
  "token": "reset_token_here",
  "new_password": "newSecurePassword123"
}
```

### Response
```json
{
  "message": "Password has been reset successfully"
}
```

## Get current user profile
`GET /api/users/me`

### Headers
```
Authorization: Bearer <token>
```

### Response
```json
{
  "id": 1,
  "username": "john_doe",
  "email": "john@example.com",
  "first_name": "John",
  "last_name": "Doe",
  "contact": "9876543210"
}
```

## Update user profile
`PUT /api/users/me`

### Headers
```
Authorization: Bearer <token>
```

### Request
```json
{
  "username": "john_doe",
  "email": "john@example.com",
  "first_name": "Johnny",
  "last_name": "Doe",
  "contact": "9876543210"
}
```

### Response
```json
{
  "message": "Profile updated successfully"
}
