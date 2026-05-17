# Language Practice AI - System Architecture

## Overview

This document describes the architecture of the Language Practice AI application.

## System Components

### 1. Frontend (Web)
- **Framework**: React 18 with TypeScript
- **Build Tool**: Vite
- **Styling**: Tailwind CSS
- **State Management**: Zustand
- **API Communication**: React Query + Axios

#### Key Pages
- Authentication (Login/Sign Up)
- Dashboard
- Conversation Interface
- Progress/Stats
- Settings

### 2. Mobile (iOS)
- **Framework**: React Native with TypeScript
- **Navigation**: React Navigation
- **State Management**: Zustand
- **API Communication**: React Query + Axios

#### Key Screens
- Splash Screen
- Authentication
- Dashboard
- Conversation Screen
- Recording & Playback
- Progress Screen

### 3. Backend API
- **Framework**: Express.js
- **Language**: TypeScript
- **Database**: MongoDB
- **Authentication**: JWT
- **External Services**: OpenAI API, Speech-to-Text, Text-to-Speech

#### Core Endpoints
- `POST /auth/register` - User registration
- `POST /auth/login` - User login
- `POST /api/conversations/start` - Start conversation
- `POST /api/conversations/{id}/message` - Send message in conversation
- `GET /api/conversations/{id}/history` - Get conversation history
- `POST /api/feedback` - Get AI feedback
- `GET /api/progress` - Get user progress

## Data Flow

### Conversation Flow

1. User initiates conversation
2. Backend generates initial prompt/scenario
3. TTS (Text-to-Speech) converts AI response to audio
4. Client plays audio
5. User records response
6. STT (Speech-to-Text) converts audio to text
7. Backend sends to OpenAI API for analysis
8. AI provides feedback on pronunciation, grammar, fluency
9. Cycle repeats

## Authentication

- JWT-based authentication
- Access token stored in secure storage (mobile) / localStorage (web)
- Refresh token for session management
- Role-based access control (user, admin)

## Database Schema

### Users
```
{
  _id: ObjectId,
  email: String (unique),
  passwordHash: String,
  username: String,
  profile: {
    nativeLanguage: String,
    targetLanguage: String,
    proficiencyLevel: String,
  },
  createdAt: Date,
  updatedAt: Date
}
```

### Conversations
```
{
  _id: ObjectId,
  userId: ObjectId (ref: Users),
  topic: String,
  language: String,
  difficulty: String,
  messages: [{
    role: String,
    content: String,
    timestamp: Date,
    feedback: {
      pronunciation: Number,
      grammar: Number,
      fluency: Number,
      suggestions: [String]
    }
  }],
  startedAt: Date,
  endedAt: Date,
  duration: Number,
  stats: {
    totalMessages: Number,
    avgPronunciation: Number,
    avgGrammar: Number,
    avgFluency: Number
  }
}
```

## Security

- HTTPS/TLS for all communications
- JWT tokens with expiration
- Password hashing with bcrypt
- Input validation and sanitization
- Rate limiting on API endpoints
- CORS configuration

## Deployment

### Backend
- Deployed on Node.js hosting (e.g., Heroku, AWS, DigitalOcean)
- MongoDB Atlas for database
- Environment variables for configuration

### Web
- Static hosting (Vercel, Netlify, AWS S3)
- CDN for assets

### iOS
- TestFlight for beta testing
- App Store for production

## Performance Considerations

- Lazy loading for images and components
- Memoization for React components
- Request debouncing/throttling
- Caching strategies for API responses
- Web Worker support for heavy computation
- Code splitting for optimal bundle size
