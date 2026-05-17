# Language Practice AI - API Documentation

## Base URL

```
https://api.language-practice-ai.com/api
```

## Authentication

All protected endpoints require a Bearer token in the Authorization header:

```
Authorization: Bearer <access_token>
```

## Endpoints

### Authentication

#### Register User
```
POST /auth/register
```

Request:
```json
{
  "email": "user@example.com",
  "password": "securePassword123",
  "username": "username",
  "nativeLanguage": "English",
  "targetLanguage": "Spanish"
}
```

Response:
```json
{
  "success": true,
  "user": {
    "id": "userId",
    "email": "user@example.com",
    "username": "username"
  },
  "tokens": {
    "accessToken": "...",
    "refreshToken": "..."
  }
}
```

#### Login
```
POST /auth/login
```

Request:
```json
{
  "email": "user@example.com",
  "password": "securePassword123"
}
```

Response: (Same as Register)

#### Refresh Token
```
POST /auth/refresh
```

Request:
```json
{
  "refreshToken": "..."
}
```

Response:
```json
{
  "accessToken": "..."
}
```

### Conversations

#### Start Conversation
```
POST /conversations/start
```

Headers:
```
Authorization: Bearer <access_token>
```

Request:
```json
{
  "topic": "restaurant",
  "language": "Spanish",
  "difficulty": "intermediate"
}
```

Response:
```json
{
  "conversationId": "convId123",
  "aiMessage": "Hola, bienvenido al restaurante. ¿Qué deseas ordenar?",
  "audioUrl": "https://..."
}
```

#### Send Message
```
POST /conversations/{conversationId}/message
```

Headers:
```
Authorization: Bearer <access_token>
```

Request:
```json
{
  "userMessage": "Quisiera una mesa para dos personas",
  "audioData": "base64_encoded_audio"
}
```

Response:
```json
{
  "aiMessage": "Perfecto, aquí está su mesa...",
  "audioUrl": "https://...",
  "feedback": {
    "pronunciation": 8.5,
    "grammar": 9.0,
    "fluency": 8.0,
    "suggestions": [
      "Try using 'gustería' for 'I would like'"
    ]
  }
}
```

#### Get Conversation History
```
GET /conversations/{conversationId}/history
```

Headers:
```
Authorization: Bearer <access_token>
```

Response:
```json
{
  "conversationId": "convId123",
  "messages": [
    {
      "role": "ai",
      "content": "Hola, bienvenido...",
      "timestamp": "2024-01-10T10:00:00Z"
    },
    {
      "role": "user",
      "content": "Quisiera una mesa...",
      "feedback": {},
      "timestamp": "2024-01-10T10:05:00Z"
    }
  ]
}
```

#### End Conversation
```
POST /conversations/{conversationId}/end
```

Headers:
```
Authorization: Bearer <access_token>
```

Response:
```json
{
  "success": true,
  "sessionStats": {
    "duration": 300,
    "messagesCount": 5,
    "avgPronunciation": 8.5,
    "avgGrammar": 8.8,
    "avgFluency": 8.2
  }
}
```

### Progress

#### Get User Progress
```
GET /progress
```

Headers:
```
Authorization: Bearer <access_token>
```

Response:
```json
{
  "totalConversations": 42,
  "totalMinutes": 840,
  "currentStreak": 7,
  "languages": [
    {
      "language": "Spanish",
      "conversations": 30,
      "avgScore": 8.2,
      "lastPracticed": "2024-01-10T10:00:00Z"
    }
  ],
  "weeklyStats": {}
}
```

### User Settings

#### Get User Profile
```
GET /user/profile
```

Headers:
```
Authorization: Bearer <access_token>
```

#### Update User Profile
```
PUT /user/profile
```

Headers:
```
Authorization: Bearer <access_token>
```

Request:
```json
{
  "nativeLanguage": "English",
  "targetLanguage": "Japanese",
  "proficiencyLevel": "beginner"
}
```

## Error Responses

All errors follow this format:

```json
{
  "error": "Error message",
  "code": "ERROR_CODE",
  "details": {}
}
```

### Common Error Codes
- `UNAUTHORIZED` - 401: Invalid or expired token
- `FORBIDDEN` - 403: Access denied
- `NOT_FOUND` - 404: Resource not found
- `VALIDATION_ERROR` - 400: Invalid request data
- `INTERNAL_ERROR` - 500: Server error
