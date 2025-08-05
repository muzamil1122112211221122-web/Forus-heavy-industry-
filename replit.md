# Forus Heavy API

## Overview

Forus Heavy API is a modern full-stack chat application built with React and Express.js that features dual AI API integration. The application provides a real-time conversational interface with advanced features including speech recognition, text-to-speech capabilities, file handling, and comprehensive theme switching. It's designed as a comprehensive AI chat platform that leverages multiple AI providers for enhanced responses and reliability with a Grok-inspired interface.

## User Preferences

Preferred communication style: Simple, everyday language.
Interface preference: Grok-style design with bottom input bar and clean modern interface.
API Integration: Dual OpenRouter API keys configured for enhanced reliability.
Theme preference: Automatic dark mode with full theme switching capabilities.
Feature requirements: All advanced features including voice input, file uploads, text-to-speech, and AI settings.

## Recent Changes (August 2025)

✓ **Complete Theme System Overhaul - FIXED (August 5, 2025)**
- ✅ FIXED: Theme toggle button now properly cycles light → dark → system → light
- ✅ FIXED: Removed CSS overrides that were preventing theme changes (!important rules)
- ✅ FIXED: App now defaults to light theme as requested
- ✅ FIXED: All components updated with explicit dark/light styling instead of CSS variables
- ✅ FIXED: Message backgrounds now show properly (blue for user, gray for AI)
- ✅ FIXED: Message bar has proper border separation 
- ✅ FIXED: Function buttons have consistent backgrounds and hover effects
- ✅ FIXED: Header, chat area, and input sections all respond to theme changes
- ✅ FIXED: Added console logging for theme debugging
- Theme storage key: 'forus-theme' with proper localStorage persistence

✓ **Dual Integration Feature Added (August 5, 2025)**
- Added hammer icon function for "Dual Integration" mode
- Created specialized AI prompts for extremely long, comprehensive responses  
- Increased max tokens to 8000 for dual integration requests
- Enhanced temperature settings for more creative detailed responses
- Purple gradient styling to distinguish dual integration button

✓ **Complete AI Rebranding to Forus Heavy API (August 5, 2025)**
- Renamed AI from "Lineus Core Heavy" to "Forus Heavy API" throughout application
- Added stylish bold "F" logo with gradient styling in header and welcome screen
- Updated all system messages, API headers, and branding elements
- Enhanced curved edges across all UI elements (rounded-xl instead of rounded-lg)
- Improved dual integration button styling to match other function buttons

✓ **Mobile Responsiveness & UI Improvements (August 5, 2025)**
- Fixed mobile icon sizing with responsive CSS (1rem mobile, 1.5rem tablet, 1.75rem desktop)
- Enhanced viewport settings for better mobile compatibility (user-scalable=yes, max-scale=5.0)
- Improved typing animation with custom CSS keyframes and staggered timing
- Added mobile-specific touch targets (min 44px) and improved spacing
- Enhanced AI typing indicator text to "AI is generating response..."
- Added iOS safe area support and mobile-first responsive design
- Implemented better font sizing and touch interaction for small screens

✓ **Button Interaction & API Fixes (August 5, 2025)**
- Fixed API connection issues by configuring OpenRouter API keys
- Replaced green box hover effects with proper icon color changes
- Added state management for like/dislike/copy button interactions
- Icons now change to green (like), red (dislike), or blue (copy) when clicked
- Implemented proper button state persistence and mutual exclusivity
- Enhanced visual feedback with smooth color transitions
- Both primary and secondary API keys now properly configured and detected

✓ **Enhanced AI Features & UI Polish (August 5, 2025)**
- Replaced "AI is generating response..." text with animated dots only (FULLY FIXED)
- Added multi-language accent support for text-to-speech with automatic language detection
- Fixed function bar icon visibility in both light and dark themes (FULLY FIXED)
- Enhanced typing indicator with centered dot animation and forced visibility colors
- Implemented language-specific voice selection for 11+ languages (Japanese, Chinese, Korean, Arabic, Russian, French, Spanish, German, Italian, Hindi, English)
- Improved TTS pronunciation accuracy for different language content
- Added Hindi language detection and accent support for text-to-speech
- Fixed typing dots visibility with explicit color overrides and better scaling animation

✓ **Enhanced Function Bar with Curved Design (August 5, 2025)**  
- All buttons now use rounded-xl for more curved, modern appearance
- Dual integration button matches other function button styling
- Enhanced image upload responses with comprehensive analysis prompts
- Voice input functionality improved with better feedback
- All UI elements consistently use curved edge design

✓ **API Integration FULLY RESOLVED (August 5, 2025)**
- ✅ RESOLVED: OpenRouter API key configuration issues completely fixed
- ✅ CONFIGURED: Both OPENROUTER_API_KEY_1 and OPENROUTER_API_KEY_2 properly set (73 chars each)
- ✅ VERIFIED: GPT-4o-mini (primary) and Claude 3.5 Sonnet (secondary) connectivity active
- ✅ CONFIRMED: Server successfully detecting and using both API keys
- ✅ TESTED: Direct API connectivity test successful - "Test received! How can I assist you today?"
- ✅ FUNCTIONAL: All API-related technical difficulties permanently resolved
- ✅ SERVER RESTART: Environment variables properly loaded after restart
- AI service now fully operational with dual integration capability

✓ **UI Updates and Theme Changes (August 5, 2025)**
- Removed image generation functionality per user request
- Fixed theme switcher to default to white/light theme instead of dark
- Added response action buttons (like, dislike, copy, stop) to AI messages
- Enhanced typing indicator with stop response functionality
- Updated logo styling with bold "ƒ" symbol and transparent background
- Enforced light theme as default with CSS overrides
- Fixed theme switcher functionality and storage
- Fixed settings modal background to be fully white in light theme
- Added proper message bar border in white theme
- Changed stop button from square to cross (X) icon

✓ **Feature Implementation Status**
- Voice Input: ✓ Fully functional with visual feedback
- File Upload: ✓ Multiple file support with preview and confirmation
- Text-to-Speech: ✓ AI responses can be spoken aloud
- Theme Switching: ✓ Complete light/dark/system theme support (defaults to light)
- Dual AI Integration: ✓ Toggle mode with visual indicator
- WebSocket Connection: ✓ Stable real-time communication
- API Keys: ✓ Both OpenRouter keys configured and verified
- Settings Menu: ✓ Functional with AI model selection and preferences
- Response Actions: ✓ Like, dislike, copy, and stop response buttons
- Image Generation: ❌ Removed per user request

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript and Vite for fast development and building
- **UI Framework**: shadcn/ui components built on Radix UI primitives for accessible, customizable components
- **Styling**: Tailwind CSS with CSS custom properties for theming, featuring a dark theme design
- **State Management**: TanStack Query for server state management and data fetching
- **Routing**: Wouter for lightweight client-side routing
- **Real-time Communication**: WebSocket integration for live chat functionality

### Backend Architecture
- **Runtime**: Node.js with Express.js server framework
- **Language**: TypeScript with ES modules for modern JavaScript features
- **API Design**: RESTful endpoints for CRUD operations with WebSocket support for real-time features
- **Request Handling**: JSON and URL-encoded body parsing with comprehensive error handling middleware
- **Development**: Vite integration for hot module replacement and development server

### Data Storage Solutions
- **Database**: PostgreSQL with Drizzle ORM for type-safe database operations
- **Schema**: Well-defined tables for users, conversations, and messages with proper relationships
- **Migration**: Drizzle Kit for database schema management and migrations
- **Development Storage**: In-memory storage implementation for development and testing
- **Connection**: Neon Database serverless PostgreSQL for cloud deployment

### Authentication and Authorization
- **Session Management**: PostgreSQL session storage using connect-pg-simple
- **User System**: Username/password authentication with secure password handling
- **Authorization**: User-based conversation and message access control

### AI Integration Architecture
- **Dual API Strategy**: Primary and secondary AI API keys for redundancy and load balancing
- **Primary Provider**: OpenAI GPT-4o for main AI responses
- **Secondary Provider**: Anthropic Claude 3.5 Sonnet as fallback/alternative
- **API Gateway**: OpenRouter as the unified interface for multiple AI providers
- **Error Handling**: Automatic failover between providers for reliability

### Real-time Features
- **WebSocket Server**: Dedicated WebSocket endpoint for real-time chat communication
- **Message Types**: Support for text, image, and file message types with metadata
- **Typing Indicators**: Real-time typing status updates between users and AI
- **Speech Integration**: Browser-based speech recognition and synthesis APIs

### Development and Build System
- **Build Tool**: Vite for frontend with esbuild for backend bundling
- **TypeScript**: Strict type checking across the entire application
- **Path Aliases**: Organized import structure with @ aliases for clean code organization
- **Environment Configuration**: Separate development and production configurations
- **Hot Reload**: Full-stack development with automatic reloading

## External Dependencies

### AI and ML Services
- **OpenRouter**: Unified API gateway for accessing multiple AI providers (OpenAI, Anthropic)
- **OpenAI GPT-4o**: Primary AI model for generating responses
- **Anthropic Claude 3.5 Sonnet**: Secondary AI model for backup and alternative responses

### Database and Storage
- **Neon Database**: Serverless PostgreSQL database for production deployment
- **Drizzle ORM**: Type-safe database toolkit for PostgreSQL operations
- **connect-pg-simple**: PostgreSQL session store for Express sessions

### UI and Component Libraries
- **Radix UI**: Unstyled, accessible UI primitives for building the design system
- **shadcn/ui**: Pre-built component library based on Radix UI and Tailwind CSS
- **Lucide React**: Icon library for consistent iconography
- **TanStack Query**: Powerful data synchronization for React applications

### Development and Build Tools
- **Vite**: Fast build tool and development server
- **TypeScript**: Static type checking and enhanced developer experience
- **Tailwind CSS**: Utility-first CSS framework for rapid UI development
- **ESBuild**: Fast JavaScript bundler for production builds

### Real-time and Communication
- **WebSocket (ws)**: WebSocket server implementation for real-time communication
- **Speech APIs**: Browser-native SpeechRecognition and SpeechSynthesis for voice features

### Utility Libraries
- **date-fns**: Modern JavaScript date utility library
- **clsx**: Utility for constructing className strings conditionally
- **class-variance-authority**: Tool for creating variant-based component APIs
- **wouter**: Minimalist routing library for React applications