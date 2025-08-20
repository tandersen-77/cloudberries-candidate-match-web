# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Project Overview

This is a React + TypeScript + Vite frontend application for candidate matching at Cloudberries. It's a modern single-page application using Material-UI components that displays candidate cards with match percentages and connects to a backend health service.

## Common Development Commands

### Development Server
```bash
npm run dev
# Starts Vite dev server on port 5174
```

### Build and Deployment
```bash
npm run build
# TypeScript compilation followed by Vite production build

npm run preview
# Preview the production build locally
```

### Code Quality
```bash
npm run lint
# Run ESLint to check for code issues
```

### Docker Development
```bash
npm run docker:dev
# Build and run the application in Docker container
# Maps container port 80 to host port 8080
```

## Architecture Overview

### Application Structure
- **Single Page Application**: No routing, displays one main candidate list page
- **Component-Based**: Uses React functional components with TypeScript
- **Material-UI Design System**: Consistent theming and components throughout
- **Mock Data**: Currently uses static mock data for candidates

### Key Components
- `App.tsx`: Root component with theme provider and main layout
- `CandidateListPage.tsx`: Main page displaying header and candidate grid
- `CandidateCard.tsx`: Individual candidate display with match percentage circular progress
- `Header.tsx`: Application header with health status monitoring and branding

### Data Flow
- Mock candidate data is imported from `src/data/mockCandidates.ts`
- Health service (`src/services/healthService.ts`) polls backend at `http://localhost:8080/api/health`
- Health status updates every 30 seconds and displays real-time system status

### Styling Approach
- Material-UI theme system with custom color palette
- Roboto font family loaded via `@fontsource`
- Custom styling using `sx` prop for component-specific overrides
- Consistent spacing and color scheme throughout

## Development Environment Setup

### Prerequisites
- Node.js 20.x (as specified in GitHub Actions)
- npm for package management

### Local Development
The Vite config is optimized for Docker development:
- Server runs on host `true` for container port mapping
- Uses polling for file watching in Docker environments
- Port 5174 for development server

### Backend Integration
- Health service expects backend on `localhost:8080`
- API endpoint: `/api/health`
- Returns structured health data for database, flowcase, and GenAI services

## CI/CD Pipeline

The project includes automated CI with Gemini AI code review:
- Runs linting and build checks on all pushes
- Performs AI-powered code review using Gemini API on pull requests
- Follows frontend-specific review criteria focusing on React/TypeScript best practices
- Comments review results directly on pull requests

## Key Files to Monitor

- `package.json`: Dependencies and scripts
- `vite.config.ts`: Development server and build configuration
- `src/data/mockCandidates.ts`: Data structure definitions
- `src/services/healthService.ts`: Backend integration point
- `.github/workflows/frontend-ci.yml`: CI/CD configuration
