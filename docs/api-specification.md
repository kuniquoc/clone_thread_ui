# Threads App API Specification

## 1. Authentication Module

### 1.1. Login
POST: /api/auth/login
Body: 
```json
{
"username": "string",
"password": "string"
}
Response:
```json
{
    "token": "string",
    "user": {
        "id": "string",
        "username": "string",
        "avatar": "string",
        "isVerified": "boolean"
    }
}
```
### 1.2. Register
POST: /api/auth/register
Body: 
```json
{
    "username": "string",
    "email": "string",
    "password": "string"
}
```
Response:
```json
{
    "success": "boolean",
    "message": "string"
}
```

### 1.3. Logout
POST: /api/auth/logout
Response:
```json
{
    "success": "boolean",
    "message": "string"
}
```

## 2. Profile Module
### 2.1. Get Profile
GET: /api/profile/:username
Response:
```json
{
    "id": "string",
    "username": "string",
    "avatar": "string",
    "isVerified": "boolean",
    "stats": {
        "posts": "number",
        "replies": "number",
        "followers": "number",
        "following": "number"
    }
}
```

### 2.2. Update Profile
PUT: /api/profile
Body:
```json
{
    "username": "string",
    "bio": "string",
    "avatar": "string"
}
```
Response:
```json
{
    "success": "boolean",
    "user": {
        "id": "string",
        "username": "string",
        "bio": "string",
        "avatar": "string",
        "isVerified": "boolean"
    }
}
```
### 2.3. Change Password
PUT: /api/profile/password
Body:
```json
{
    "currentPassword": "string",
    "newPassword": "string",
    "confirmPassword": "string"
}
```
Response:
```json
{
    "success": "boolean",
    "message": "string"
}
```

### 2.4. Update Profile Settings
PUT: /api/profile/settings
Body:
```json
{
    "emailNotifications": "boolean",
    "privateAccount": "boolean",
    "language": "string",
    "theme": "string"
}
```
Response:
```json
{
    "success": "boolean",
    "settings": {
        "emailNotifications": "boolean",
        "privateAccount": "boolean",
        "language": "string",
        "theme": "string"
    }
}
```
### 2.5. Delete Account
DELETE: /api/profile
Body:
```json
{
    "password": "string",
    "confirmDelete": "boolean"
}
```
Response:
```json
{
    "success": "boolean",
    "message": "string"
}
```

## 3. Posts Module
### 3.1. Get Posts
GET: /api/posts
GET: /api/posts
Query Parameters:
- page: number
- limit: number
- userId: string (optional)

Response:
```json
{
    "posts": [{
        "id": "string",
        "author": {
            "username": "string",
            "avatar": "string",
            "isVerified": "boolean"
        },
        "content": "string",
        "media": ["string"],
        "publishTime": "string",
        "stats": {
            "likes": "number",
            "replies": "number"
        },
        "isReposted": "boolean",
        "repostedBy": "string"
    }],
    "pagination": {
        "currentPage": "number",
        "totalPages": "number",
        "hasMore": "boolean"
    }
}
```

### 3.2. Create Post
POST: /api/posts
Body: 
```json
{
    "content": "string",
    "media": ["string"]
}
```
Response:
```json
{
    "id": "string",
    "content": "string",
    "media": ["string"],
    "publishTime": "string"
}
```

### 3.3. Like Post
POST: /api/posts/:postId/like
Response:
```json
{
    "success": "boolean",
    "message": "string"
}
```

### 3.4. Unlike Post
POST: /api/posts/:postId/unlike
Response:
```json
{
    "success": "boolean",
    "message": "string"
}
```

### 3.5. Repost Post
POST: /api/posts/:postId/repost

Response:
```json
{
    "success": "boolean",
    "message": "string"
}
```

### 3.6. Delete Post
DELETE: /api/posts/:postId
Response:
```json
{
    "success": "boolean",
    "message": "string",
}
```

## 4. Replies Module
### 4.1. Get Replies
GET: /api/replies/:postId
Query Parameters:
- page: number
- limit: number

Response:
```json
{
    "replies": [{
        "id": "string",
        "originalPost": {
            "id": "string",
            "content": "string",
            "author": {
                "username": "string",
                "avatar": "string",
                "isVerified": "boolean"
            }
        },
        "reply": {
            "content": "string",
            "publishTime": "string",
            "stats": {
                "likes": "number",
                "replies": "number"
            },
            "isLiked": "boolean",
            "repliedByMutual": {
                "avatar": "string"
            }
        }
    }],
    "pagination": {
        "currentPage": "number",
        "totalPages": "number",
        "hasMore": "boolean"
    }
}
```

### 4.2. Create Reply
POST: /api/posts/:postId/replies
Body: 
```json
{
    "content": "string"
}
```
Response:
```json
{
    "id": "string",
    "content": "string",
    "publishTime": "string",
    "stats": {
        "likes": 0,
        "replies": 0
    }
}
```

### 4.3. Like Reply
POST: /api/replies/:replyId/like
Response:
```json
{
    "success": "boolean",
    "message": "string"
}
```

### 4.4. Unlike Reply
POST: /api/replies/:replyId/unlike
Response:
```json
{
    "success": "boolean",
    "message": "string"
}
```

### 4.5. Delete Reply
DELETE: /api/replies/:replyId
Response:
```json
{
    "success": "boolean",
    "message": "string"
}
```

## 5. Error Response Format
```json
{
    "error": {
        "code": "string",
        "message": "string"
    }
}


