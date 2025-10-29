# Proximol - Architecture Plan

## Overview
Proximol is an AI-powered web application builder that generates production-ready code from natural language descriptions. Users can create, iterate, and deploy full-stack web applications through conversational interactions.

## Core Features

### 1. AI-Powered Code Generation
- Natural language to code conversion
- Support for React, TypeScript, Tailwind CSS
- Iterative refinement through chat
- Context-aware code modifications

### 2. Live Preview
- Real-time preview of generated applications
- Hot module replacement
- Instant visual feedback
- Multi-device preview (desktop, tablet, mobile)

### 3. Version Control Integration
- Automatic GitHub repository creation
- Commit history tracking
- Branch management
- Code ownership (users own their code)

### 4. Deployment
- One-click deployment to production
- Multiple hosting options (Vercel, Netlify, custom)
- Environment variable management
- SSL certificates

### 5. Project Management
- Multiple projects per user
- Project templates
- Asset management (images, fonts, etc.)
- Export/import functionality

## System Architecture

### High-Level Components

```
┌─────────────────────────────────────────────────────────────┐
│                        Frontend (React)                      │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │   Chat UI    │  │ Code Editor  │  │Live Preview  │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                     API Gateway (Next.js)                    │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │  Auth Routes │  │Project Routes│  │  AI Routes   │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└─────────────────────────────────────────────────────────────┘
                              │
              ┌───────────────┼───────────────┐
              ▼               ▼               ▼
    ┌─────────────┐  ┌─────────────┐  ┌─────────────┐
    │  AI Engine  │  │  Database   │  │   GitHub    │
    │  (Claude)   │  │ (Supabase)  │  │     API     │
    └─────────────┘  └─────────────┘  └─────────────┘
              │               │               │
              ▼               ▼               ▼
    ┌─────────────┐  ┌─────────────┐  ┌─────────────┐
    │Code Generator│  │File Storage │  │Git Hosting  │
    └─────────────┘  └─────────────┘  └─────────────┘
```

### Technology Stack

#### Frontend
- **Framework**: Next.js 14+ (App Router)
- **UI Library**: React 18+
- **Styling**: Tailwind CSS
- **State Management**: Zustand / React Context
- **Code Editor**: Monaco Editor (VS Code engine)
- **Preview**: iframe-based sandboxed preview
- **Real-time**: WebSockets (Socket.io)

#### Backend
- **Runtime**: Node.js 20+
- **Framework**: Next.js API Routes
- **Database**: Supabase (PostgreSQL)
- **Authentication**: Supabase Auth / NextAuth.js
- **File Storage**: Supabase Storage / AWS S3
- **AI Provider**: Anthropic Claude API
- **Queue**: Bull / BullMQ (for long-running tasks)
- **Cache**: Redis

#### Infrastructure
- **Hosting**: Vercel / Railway
- **CDN**: Cloudflare
- **Monitoring**: Sentry
- **Analytics**: PostHog / Mixpanel

## Database Schema

### Users Table
```sql
users (
  id UUID PRIMARY KEY,
  email TEXT UNIQUE NOT NULL,
  name TEXT,
  avatar_url TEXT,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),
  subscription_tier TEXT DEFAULT 'free'
)
```

### Projects Table
```sql
projects (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES users(id),
  name TEXT NOT NULL,
  description TEXT,
  github_repo_url TEXT,
  github_branch TEXT DEFAULT 'main',
  deploy_url TEXT,
  status TEXT DEFAULT 'active',
  framework TEXT DEFAULT 'react',
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
)
```

### Messages Table (Chat History)
```sql
messages (
  id UUID PRIMARY KEY,
  project_id UUID REFERENCES projects(id),
  role TEXT NOT NULL, -- 'user' or 'assistant'
  content TEXT NOT NULL,
  metadata JSONB, -- additional context
  created_at TIMESTAMP DEFAULT NOW()
)
```

### Files Table
```sql
files (
  id UUID PRIMARY KEY,
  project_id UUID REFERENCES projects(id),
  path TEXT NOT NULL,
  content TEXT,
  language TEXT,
  size INTEGER,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),
  UNIQUE(project_id, path)
)
```

### Generations Table (AI Generation History)
```sql
generations (
  id UUID PRIMARY KEY,
  project_id UUID REFERENCES projects(id),
  message_id UUID REFERENCES messages(id),
  prompt TEXT NOT NULL,
  files_changed JSONB, -- list of files modified
  tokens_used INTEGER,
  duration_ms INTEGER,
  status TEXT DEFAULT 'pending',
  error TEXT,
  created_at TIMESTAMP DEFAULT NOW()
)
```

## AI Engine Architecture

### Prompt Pipeline

```
User Input → Context Builder → Prompt Constructor → Claude API → Code Parser → File System Writer
```

### Context Builder
- Collects project structure
- Gathers relevant file contents
- Includes previous conversation history
- Adds framework-specific templates

### Code Parser
- Extracts code blocks from AI response
- Validates syntax
- Organizes files by path
- Detects dependencies

### Safety Layer
- Code review for malicious patterns
- XSS prevention
- SQL injection checks
- Sensitive data detection

## API Endpoints

### Authentication
- `POST /api/auth/signup` - User registration
- `POST /api/auth/login` - User login
- `POST /api/auth/logout` - User logout
- `GET /api/auth/me` - Get current user

### Projects
- `GET /api/projects` - List all projects
- `POST /api/projects` - Create new project
- `GET /api/projects/:id` - Get project details
- `PUT /api/projects/:id` - Update project
- `DELETE /api/projects/:id` - Delete project

### AI Generation
- `POST /api/generate` - Generate code from prompt
- `POST /api/chat` - Chat with AI about project
- `GET /api/chat/:projectId/history` - Get chat history

### Files
- `GET /api/projects/:id/files` - List all files
- `GET /api/projects/:id/files/:path` - Get file content
- `PUT /api/projects/:id/files/:path` - Update file
- `DELETE /api/projects/:id/files/:path` - Delete file

### Preview
- `GET /api/preview/:projectId` - Get preview URL
- `POST /api/preview/:projectId/build` - Trigger build

### Deployment
- `POST /api/deploy/:projectId` - Deploy to production
- `GET /api/deploy/:projectId/status` - Get deployment status

## Security Considerations

### Authentication & Authorization
- JWT-based authentication
- Row-level security (RLS) in Supabase
- API rate limiting
- CORS configuration

### Code Generation Safety
- Sandboxed preview environment
- Content Security Policy (CSP)
- No server-side code execution from user input
- Dependency vulnerability scanning

### Data Protection
- Encrypted data at rest
- HTTPS only
- Input validation and sanitization
- SQL injection prevention
- XSS protection

## Performance Optimization

### Caching Strategy
- Redis cache for:
  - User sessions
  - Project metadata
  - Frequently accessed files
  - AI responses (when appropriate)

### Code Generation
- Incremental updates (only changed files)
- Parallel file writing
- Background job processing for large generations

### Preview System
- CDN for static assets
- Build caching
- Lazy loading of preview iframe

## Scalability Considerations

### Horizontal Scaling
- Stateless API design
- Load balancing
- Database connection pooling
- Distributed caching

### Queue System
- Background jobs for:
  - Code generation
  - GitHub operations
  - Deployment tasks
  - Email notifications

## Monitoring & Observability

### Metrics to Track
- API response times
- AI generation duration
- Error rates
- User engagement
- Token usage
- Deployment success rate

### Logging
- Structured logging (JSON)
- Log levels (debug, info, warn, error)
- Correlation IDs for request tracing
- Sensitive data redaction

## Development Phases

### Phase 1: MVP (Weeks 1-4)
- Basic authentication
- Single project creation
- Simple code generation (React components)
- Text-based chat interface
- File viewer (read-only)

### Phase 2: Core Features (Weeks 5-8)
- Live preview system
- File editing
- GitHub integration
- Project templates
- Better AI prompts

### Phase 3: Advanced Features (Weeks 9-12)
- Multi-file generation
- Component library
- Asset management
- Deployment integration
- Collaborative editing

### Phase 4: Polish & Scale (Weeks 13-16)
- Performance optimization
- Advanced UI/UX
- Analytics
- Subscription tiers
- Documentation
