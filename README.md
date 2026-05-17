# Language Practice AI

An AI-powered language learning application similar to Voca AI, enabling users to practice speaking skills through interactive conversations with an AI tutor.

## Features

- 🎤 **Real-time Speaking Practice**: Engage in conversations with AI tutor in realistic scenarios
- 🎯 **Instant Feedback**: Get immediate feedback on pronunciation, grammar, and fluency
- 📚 **Personalized Learning Paths**: Lessons adapted to your proficiency level
- 🌍 **Multi-language Support**: English, Spanish, Japanese, Portuguese, and more
- 📱 **Cross-platform**: Web and iOS support
- 🔐 **Secure**: User data protection and authentication

## Project Structure

```
language-practice-ai/
├── backend/              # Node.js/Express backend server
├── web/                  # React web application
├── mobile/               # React Native iOS application
├── docs/                 # Documentation
└── README.md
```

## Tech Stack

### Frontend (Web)
- React 18+
- TypeScript
- Vite (build tool)
- Tailwind CSS
- Zustand (state management)
- React Query (data fetching)

### Mobile (iOS)
- React Native
- TypeScript
- React Navigation
- Zustand (state management)
- React Query

### Backend
- Node.js + Express
- MongoDB
- OpenAI API
- JWT Authentication
- TypeScript

## Getting Started

### Prerequisites
- Node.js 18+
- npm or yarn
- MongoDB (local or cloud)
- OpenAI API key

### Setup

#### Backend Setup
```bash
cd backend
npm install
cp .env.example .env
# Edit .env with your configuration
npm run dev
```

#### Web Setup
```bash
cd web
npm install
npm run dev
```

#### Mobile Setup (iOS)
```bash
cd mobile
npm install
cd ios && pod install && cd ..
npm run ios
```

## API Documentation

See [API.md](./docs/API.md) for complete API documentation.

## Architecture

See [ARCHITECTURE.md](./docs/ARCHITECTURE.md) for system architecture and design decisions.

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md) for contribution guidelines.

## License

MIT License

## Support

For issues and questions, please open an issue on GitHub.
