# TeamSync API Documentation

## Overview

The TeamSync API provides endpoints for interacting with the project management and collaboration system. This documentation covers version 1 (v1) of the API. Versioning allows for changes and updates while maintaining backward compatibility.

## API Endpoints

### **1. User Management**

#### **1.1 Register User**

**Endpoint**: `POST /api/v1/users/register`

**Description**: Registers a new user in the system.

**Request Payload**:

```json
{
  "name": "John Doe",
  "email": "john.doe@example.com",
  "password": "password123",
  "role": "Member"
}
```

**Response**:

**_Success_** :

```json
{
  "message": "User registered successfully",
  "userId": 1
}
```

**_Error_** :

```json
{
  "error": "Email already in use"
}
```

#### **1.2 Login User**

**Endpoint**: `POST api/v1/users/login`

**Description**: Authenticates a user and returns a JWT token.

**Request Payload**:

```json
{
  "email": "john.doe@example.com",
  "password": "password123"
}
```

**Response**:

**_Success_** :

```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTY3ODkwMjAwLCJleHBpcmVkX3N0YXR1cyI6IkF1dG9tYXRpb25zIn0.S4K-5mPzi7z4UtpQkUdW-XLV8P9lc7L5v8_gFO5E9dA"
}
```

**_Error_** :

```json
{
  "error": "Invalid credentials"
}
```

### **2. Project Management**

#### **2.1 Create Project**

**Endpoint**: `POST /api/v1/projects`

**Description**: Creates a new project.

**Request Payload**:

```json
{
  "name": "New Project",
  "description": "A detailed description of the new project.",
  "ownerId": 1,
  "startDate": "2024-07-01",
  "endDate": "2024-12-31"
}
```

**Response**:

**_Success_** :

```json
{
  "message": "Project created successfully",
  "projectId": 1
}
```

**_Error_** :

```json
{
  "error": "Project creation failed"
}
```

#### **2.2 Update Project**

**Endpoint**: `PUT /api/v1/projects/:id`

**Description**: Updates an existing project.

**Request Payload**:

```json
{
  "name": "Updated Project Name",
  "description": "Updated description of the project.",
  "startDate": "2024-07-01",
  "endDate": "2024-12-31"
}
```

**Response**:

**_Success_** :

```json
{
  "message": "Project updated successfully"
}
```

**_Error_** :

```json
{
  "error": "Project update failed"
}
```
