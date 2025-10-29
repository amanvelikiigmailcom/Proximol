# Proximol

<div align="center">

![Proximol Logo](https://via.placeholder.com/200x200/3b82f6/ffffff?text=Proximol)

**AI-Powered Web Application Builder**

Build production-ready web applications through natural conversation with AI

[Features](#features) • [Quick Start](#quick-start) • [Documentation](#documentation) • [Roadmap](#roadmap)

</div>

---

## Overview

Proximol is an innovative AI-powered platform that enables developers to create full-stack web applications using natural language. Inspired by Lovable, Proximol takes it further with a unique blue-themed design and enhanced developer experience.

### What Makes Proximol Special?

- **Conversational Development**: Build apps by chatting with AI
- **Live Preview**: See your changes in real-time
- **Code Ownership**: Export clean, production-ready code
- **GitHub Integration**: Automatic version control
- **One-Click Deploy**: Ship to production instantly
- **Beautiful Design**: Modern blue-themed interface

---

## Features

### Core Features

- **AI Code Generation**: Generate React, TypeScript, and Tailwind CSS code from natural language
- **Interactive Chat**: Iteratively refine your application through conversation
- **Live Preview**: Real-time preview with hot module replacement
- **Code Editor**: Built-in Monaco editor with syntax highlighting
- **File Management**: Create, edit, and organize project files
- **Project Templates**: Start quickly with pre-built templates

### Advanced Features

- **Multi-File Generation**: Generate complete features across multiple files
- **Component Library**: Reusable components with blue theme
- **Asset Management**: Upload and manage images and assets
- **GitHub Sync**: Automatic repository creation and commits
- **Deployment**: One-click deploy to Vercel, Netlify, or custom hosting
- **Collaboration**: Share projects and collaborate with team members

---

## Tech Stack

### Frontend
- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript
- **Styling**: Tailwind CSS (Blue theme)
- **Editor**: Monaco Editor
- **Icons**: Lucide React
- **State**: Zustand

### Backend
- **Runtime**: Node.js 20+
- **Database**: Supabase (PostgreSQL)
- **Authentication**: Supabase Auth
- **AI**: Anthropic Claude 3.5 Sonnet
- **Storage**: Supabase Storage
- **Cache**: Redis

### Infrastructure
- **Hosting**: Vercel
- **CDN**: Cloudflare
- **Monitoring**: Sentry
- **Analytics**: PostHog

---

## Quick Start

### Prerequisites

- Node.js 20+
- Supabase account
- Anthropic API key

### Installation

```bash
# Clone repository
git clone https://github.com/yourusername/proximol.git
cd proximol

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env.local
# Edit .env.local with your credentials

# Run database migrations
npx supabase db push

# Start development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to see the app.

For detailed setup instructions, see [QUICKSTART.md](./QUICKSTART.md)

---

## Documentation

- **[QUICKSTART.md](./QUICKSTART.md)** - Get started in 10 minutes
- **[ARCHITECTURE.md](./ARCHITECTURE.md)** - System architecture and design
- **[DESIGN_SYSTEM.md](./DESIGN_SYSTEM.md)** - Blue-themed design system
- **[AI_PROMPTS.md](./AI_PROMPTS.md)** - AI prompts and templates
- **[ROADMAP.md](./ROADMAP.md)** - Development roadmap (16 weeks)

---

## Roadmap

### Phase 1: MVP (Weeks 1-4) ✅
- [x] Project setup and infrastructure
- [x] Authentication and user management
- [x] Basic project creation
- [x] Simple AI code generation
- [ ] Start implementation

### Phase 2: Core Features (Weeks 5-8)
- [ ] Live preview system
- [ ] Code editor integration
- [ ] GitHub integration
- [ ] Project templates

### Phase 3: Advanced Features (Weeks 9-12)
- [ ] Multi-file generation
- [ ] Asset management
- [ ] Deployment integration
- [ ] Collaboration features

### Phase 4: Polish & Launch (Weeks 13-16)
- [ ] Performance optimization
- [ ] Advanced UI/UX
- [ ] Analytics and monitoring
- [ ] Documentation and launch

See [ROADMAP.md](./ROADMAP.md) for the complete plan.

---

## Screenshots

### Chat Interface
```
┌─────────────────────────────────────────────────────┐
│  New Project - Chat with AI                         │
├─────────────────────────────────────────────────────┤
│                                                      │
│  You: Create a landing page with a hero section    │
│                                                      │
│  AI: I'll create a beautiful landing page with:    │
│      - Hero section with blue gradient             │
│      - CTA buttons                                  │
│      - Responsive design                            │
│                                                      │
│  [Generated Files]                                  │
│  - src/pages/Home.tsx                              │
│  - src/components/Hero.tsx                         │
│                                                      │
└─────────────────────────────────────────────────────┘
```

### Code Editor with Preview
```
┌──────────┬──────────────────────────────────────────┐
│ Files    │  Editor                │  Preview       │
├──────────┼──────────────────────────────────────────┤
│ src/     │ import React from...   │  [Live App]    │
│ ├─ App   │                        │                 │
│ ├─ Hero  │ export function Hero() │  ┌───────────┐ │
│ └─ CTA   │   return (             │  │   Hero    │ │
│          │     <div className=    │  │  Section  │ │
│          │       "bg-blue-500"    │  │           │ │
│          │     >                  │  │  [Button] │ │
└──────────┴──────────────────────────────────────────┘
```

---

## Design Philosophy

Proximol embraces **blue** as its primary brand color, representing:

- **Trust**: Reliable AI-powered code generation
- **Intelligence**: Advanced Claude AI integration
- **Innovation**: Cutting-edge development experience
- **Professionalism**: Production-ready output

The design is clean, modern, and developer-focused with smooth animations and intuitive interactions.

---

## Use Cases

### 1. Rapid Prototyping
Build MVPs and prototypes in minutes instead of hours.

### 2. Learning
Learn React, TypeScript, and modern web development by seeing how AI builds applications.

### 3. Component Libraries
Generate reusable components for your design system.

### 4. Landing Pages
Create beautiful landing pages with conversion-optimized designs.

### 5. Dashboards
Build admin dashboards and data visualization tools.

### 6. Portfolios
Generate personal portfolio websites with unique designs.

---

## Examples

### Example 1: Create a Button Component

**Prompt:**
```
Create a blue primary button with hover effects and loading state
```

**Generated Code:**
```typescript
interface ButtonProps {
  children: React.ReactNode;
  onClick?: () => void;
  loading?: boolean;
}

export function Button({ children, onClick, loading }: ButtonProps) {
  return (
    <button
      onClick={onClick}
      disabled={loading}
      className="bg-blue-500 hover:bg-blue-600 text-white px-6 py-3
                 rounded-lg font-medium transition-all duration-200
                 shadow-md hover:shadow-lg disabled:opacity-50"
    >
      {loading ? 'Loading...' : children}
    </button>
  );
}
```

### Example 2: Create a Complete Landing Page

**Prompt:**
```
Create a landing page for a SaaS product with:
- Hero section with blue gradient background
- Features section with 3 cards
- Pricing table with 3 tiers
- CTA section
- Footer
```

**Result:** Complete multi-file landing page with all sections, fully responsive.

---

## API Reference

### POST `/api/generate`

Generate code from natural language prompt.

**Request:**
```json
{
  "prompt": "Create a blue button component",
  "projectId": "uuid",
  "context": {
    "files": [...],
    "framework": "react"
  }
}
```

**Response:**
```json
{
  "success": true,
  "files": [
    {
      "path": "src/components/Button.tsx",
      "content": "...",
      "action": "create"
    }
  ],
  "explanation": "Created a reusable button component..."
}
```

See full API documentation in [ARCHITECTURE.md](./ARCHITECTURE.md)

---

## Contributing

We welcome contributions! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines

- Follow TypeScript best practices
- Use the blue color theme from design system
- Write tests for new features
- Update documentation

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgments

- Inspired by [Lovable](https://lovable.dev)
- Powered by [Anthropic Claude](https://anthropic.com)
- Built with [Next.js](https://nextjs.org)
- Database by [Supabase](https://supabase.com)

---

## Contact

- **GitHub**: [@yourusername](https://github.com/yourusername)
- **Twitter**: [@proximol](https://twitter.com/proximol)
- **Email**: hello@proximol.dev

---

<div align="center">

**Built with ❤️ and AI**

[⭐ Star us on GitHub](https://github.com/yourusername/proximol)

</div>
