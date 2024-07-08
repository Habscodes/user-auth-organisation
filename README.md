# User Authentication and Organization Management API

## Overview
This API provides endpoints for user registration, login, and organization management. It supports the following functionalities:
- User Registration
- User Login
- Fetching User Data
- Fetching Organization Data
- Adding Users to Organizations

## Base URL

https://user-auth-organisation-xi.vercel.app



## Endpoints

### User Registration
#### POST `/auth/register`
Registers a new user.

##### Request
- **URL**: `/auth/register`
- **Method**: `POST`
- **Headers**: `Content-Type: application/json`
- **Body**:
  ```json
  {
    "username": "newuser",
    "email": "newuser@example.com",
    "password": "securepassword",
    "confirmPassword": "securepassword",
    "firstName": "New",
    "lastName": "User"
  }
  ```

Response
Success:
Status: 201 Created
Body
```
{
  "message": "User registered successfully",
  "user": {
    "id": "unique_user_id",
    "username": "newuser",
    "email": "newuser@example.com",
    "firstName": "New",
    "lastName": "User"
  }
}
```
Error:
Status: 400 Bad Request
Body





User Login
POST /auth/login
Logs in a user.

Request
URL: /auth/login
Method: POST
Headers: Content-Type: application/json
```
{
  "email": "newuser@example.com",
  "password": "securepassword"
}
```
Response
Success:
Status: 200 OK
```
{
  "message": "Login successful",
  "token": "jwt_token"
}
```

Error:
Status: 401 Unauthorized
Body

```
{
  "message": "Invalid email or password"
}
```



Fetch User Data
GET /api/users/:id
Fetches user data by user ID.

Request
URL: /api/users/:id
Method: GET
Headers: Authorization: Bearer <jwt_token>
Response
Success:
Status: 200 OK

```
{
  "id": "unique_user_id",
  "username": "newuser",
  "email": "newuser@example.com",
  "firstName": "New",
  "lastName": "User"
}
```

Error:
Status: 404 Not Found
```
{
  "message": "User not found"
}
```



Fetch Organization Data
GET /api/organisations/:id
Fetches organization data by organization ID.

Request
URL: /api/organisations/:id
Method: GET
Headers: Authorization: Bearer <jwt_token>
Response
Success:
Status: 200 OK
Body:
json
Copy code
{
  "id": "unique_org_id",
  "name": "Organization Name",
  "users": [
    {
      "id": "unique_user_id",
      "username": "newuser",
      "email": "newuser@example.com",
      "firstName": "New",
      "lastName": "User"
    }
  ]
}
Error:
Status: 404 Not Found
Body:
json
Copy code
{
  "message": "Organization not found"
}
Add User to Organization
POST /api/organisations/:id/users
Adds a user to an organization.

Request
URL: /api/organisations/:id/users
Method: POST
Headers: Authorization: Bearer <jwt_token>
Body:
json
Copy code
{
  "userId": "unique_user_id"
}
Response
Success:
Status: 200 OK
Body:
json
Copy code
{
  "message": "User added to organization successfully"
}
Error:
Status: 404 Not Found
Body:
json
Copy code
{
  "message": "Organization or user not found"
}
Error Handling
All error responses follow the structure:

json
Copy code
{
  "error": {
    "message": "Error message",
    "details": [
      {
        "field": "field_name",
        "message": "Error message for the specific field"
      }
    ]
  }
}
Authentication
All protected endpoints require a JWT token in the Authorization header:

makefile
Copy code
Authorization: Bearer <jwt_token>
Example Usage
Register a New User
sh
Copy code
curl -X POST https://user-auth-organisation-xi.vercel.app/auth/register \
-H "Content-Type: application/json" \
-d '{
  "username": "newuser",
  "email": "newuser@example.com",
  "password": "securepassword",
  "confirmPassword": "securepassword",
  "firstName": "New",
  "lastName": "User"
}'
Log in with a User
sh
Copy code
curl -X POST https://user-auth-organisation-xi.vercel.app/auth/login \
-H "Content-Type: application/json" \
-d '{
  "email": "newuser@example.com",
  "password": "securepassword"
}'
Fetch User Data
sh
Copy code
curl -X GET https://user-auth-organisation-xi.vercel.app/api/users/<user_id> \
-H "Authorization: Bearer <jwt_token>"
Fetch Organization Data
sh
Copy code
curl -X GET https://user-auth-organisation-xi.vercel.app/api/organisations/<org_id> \
-H "Authorization: Bearer <jwt_token>"
Add User to Organization
sh
Copy code
curl -X POST https://user-auth-organisation-xi.vercel.app/api/organisations/<org_id>/users \
-H "Authorization: Bearer <jwt_token>" \
-H "Content-Type: application/json" \
-d '{
  "userId": "unique_user_id"
}'
