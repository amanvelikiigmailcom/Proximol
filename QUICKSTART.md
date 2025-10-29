# Proximol - Quick Start Guide

## Getting Started in 10 Minutes

This guide will help you set up Proximol locally and understand the core architecture.

---

## Prerequisites

- Node.js 20+ installed
- npm or pnpm
- Supabase account (free tier)
- Anthropic API key
- Git

---

## Step 1: Initial Setup (2 minutes)

### Clone and Install

```bash
# Clone repository
git clone https://github.com/yourusername/proximol.git
cd proximol

# Install dependencies
npm install

# Or with pnpm (recommended for faster installs)
pnpm install
```

---

## Step 2: Environment Configuration (3 minutes)

### Create `.env.local`

```bash
cp .env.example .env.local
```

### Configure Environment Variables

```env
# App Configuration
NEXT_PUBLIC_APP_URL=http://localhost:3000
NODE_ENV=development

# Supabase Configuration
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key

# Anthropic Claude API
ANTHROPIC_API_KEY=sk-ant-api03-...

# GitHub OAuth (optional for MVP)
GITHUB_CLIENT_ID=your-github-client-id
GITHUB_CLIENT_SECRET=your-github-client-secret

# Redis (optional for caching)
REDIS_URL=redis://localhost:6379
```

---

## Step 3: Database Setup (2 minutes)

### Set up Supabase

1. Go to [supabase.com](https://supabase.com)
2. Create a new project
3. Copy the URL and anon key
4. Run migrations:

```bash
# If using Supabase CLI
npx supabase db push

# Or manually copy SQL from supabase/migrations/
```

### Initial Database Schema

```sql
-- Run this in Supabase SQL Editor

-- Enable UUID extension
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";

-- Profiles table
CREATE TABLE profiles (
  id UUID REFERENCES auth.users PRIMARY KEY,
  email TEXT,
  full_name TEXT,
  avatar_url TEXT,
  subscription_tier TEXT DEFAULT 'free',
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Projects table
CREATE TABLE projects (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  user_id UUID REFERENCES auth.users NOT NULL,
  name TEXT NOT NULL,
  description TEXT,
  framework TEXT DEFAULT 'react',
  status TEXT DEFAULT 'active',
  github_repo_url TEXT,
  deploy_url TEXT,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Files table
CREATE TABLE files (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  project_id UUID REFERENCES projects(id) ON DELETE CASCADE,
  path TEXT NOT NULL,
  content TEXT,
  language TEXT,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),
  UNIQUE(project_id, path)
);

-- Messages table (chat history)
CREATE TABLE messages (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  project_id UUID REFERENCES projects(id) ON DELETE CASCADE,
  role TEXT NOT NULL, -- 'user' or 'assistant'
  content TEXT NOT NULL,
  metadata JSONB,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Generations table (AI generation tracking)
CREATE TABLE generations (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  project_id UUID REFERENCES projects(id) ON DELETE CASCADE,
  message_id UUID REFERENCES messages(id),
  prompt TEXT NOT NULL,
  files_changed JSONB,
  tokens_used INTEGER,
  duration_ms INTEGER,
  status TEXT DEFAULT 'pending',
  error TEXT,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Row Level Security (RLS)
ALTER TABLE profiles ENABLE ROW LEVEL SECURITY;
ALTER TABLE projects ENABLE ROW LEVEL SECURITY;
ALTER TABLE files ENABLE ROW LEVEL SECURITY;
ALTER TABLE messages ENABLE ROW LEVEL SECURITY;
ALTER TABLE generations ENABLE ROW LEVEL SECURITY;

-- Policies
CREATE POLICY "Users can view own profile"
  ON profiles FOR SELECT
  USING (auth.uid() = id);

CREATE POLICY "Users can update own profile"
  ON profiles FOR UPDATE
  USING (auth.uid() = id);

CREATE POLICY "Users can view own projects"
  ON projects FOR SELECT
  USING (auth.uid() = user_id);

CREATE POLICY "Users can create own projects"
  ON projects FOR INSERT
  WITH CHECK (auth.uid() = user_id);

CREATE POLICY "Users can update own projects"
  ON projects FOR UPDATE
  USING (auth.uid() = user_id);

CREATE POLICY "Users can delete own projects"
  ON projects FOR DELETE
  USING (auth.uid() = user_id);

-- Similar policies for files, messages, generations
CREATE POLICY "Users can manage files in own projects"
  ON files FOR ALL
  USING (
    EXISTS (
      SELECT 1 FROM projects
      WHERE projects.id = files.project_id
      AND projects.user_id = auth.uid()
    )
  );
```

---

## Step 4: Run Development Server (1 minute)

```bash
npm run dev
# or
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## Step 5: Test the Setup (2 minutes)

1. **Sign Up**: Create a new account
2. **Create Project**: Click "New Project"
3. **Test AI Generation**: Try generating a simple component

Example prompt:
```
Create a blue button component with hover effects
```

Expected output:
```typescript
// src/components/Button.tsx
interface ButtonProps {
  children: React.ReactNode;
  onClick?: () => void;
  variant?: 'primary' | 'secondary';
}

export function Button({ children, onClick, variant = 'primary' }: ButtonProps) {
  const baseStyles = "px-6 py-3 rounded-lg font-medium transition-all duration-200";
  const variants = {
    primary: "bg-blue-500 hover:bg-blue-600 text-white shadow-md hover:shadow-lg",
    secondary: "bg-white border-2 border-blue-500 text-blue-600 hover:bg-blue-50"
  };

  return (
    <button
      onClick={onClick}
      className={`${baseStyles} ${variants[variant]}`}
    >
      {children}
    </button>
  );
}
```

---

## Project Structure

```
proximol/
├── src/
│   ├── app/                          # Next.js App Router
│   │   ├── (auth)/                   # Auth pages
│   │   │   ├── login/page.tsx
│   │   │   └── signup/page.tsx
│   │   ├── (dashboard)/              # Protected pages
│   │   │   ├── dashboard/page.tsx
│   │   │   └── projects/[id]/page.tsx
│   │   ├── api/                      # API routes
│   │   │   ├── auth/
│   │   │   ├── projects/
│   │   │   ├── generate/route.ts
│   │   │   └── chat/route.ts
│   │   ├── layout.tsx                # Root layout
│   │   └── page.tsx                  # Home page
│   ├── components/                   # React components
│   │   ├── ui/                       # Base UI components
│   │   │   ├── Button.tsx
│   │   │   ├── Input.tsx
│   │   │   ├── Card.tsx
│   │   │   └── Modal.tsx
│   │   ├── auth/                     # Auth components
│   │   ├── chat/                     # Chat interface
│   │   ├── editor/                   # Code editor
│   │   ├── preview/                  # Preview system
│   │   └── projects/                 # Project management
│   ├── lib/                          # Utilities
│   │   ├── supabase/
│   │   │   ├── client.ts             # Client-side Supabase
│   │   │   └── server.ts             # Server-side Supabase
│   │   ├── ai/
│   │   │   ├── claude.ts             # Claude API client
│   │   │   ├── prompts.ts            # Prompt templates
│   │   │   └── parser.ts             # Code parser
│   │   └── utils.ts                  # Helper functions
│   ├── hooks/                        # Custom React hooks
│   │   ├── useAuth.ts
│   │   ├── useProject.ts
│   │   └── useGeneration.ts
│   ├── store/                        # Zustand stores
│   │   ├── authStore.ts
│   │   ├── projectStore.ts
│   │   └── editorStore.ts
│   ├── types/                        # TypeScript types
│   │   ├── database.ts
│   │   ├── project.ts
│   │   └── ai.ts
│   └── styles/
│       └── globals.css               # Global styles + Tailwind
├── public/                           # Static assets
├── supabase/
│   ├── migrations/                   # Database migrations
│   └── seed.sql                      # Seed data
├── .env.example                      # Environment template
├── .env.local                        # Your local environment
├── next.config.js                    # Next.js config
├── tailwind.config.js                # Tailwind config (blue theme)
├── tsconfig.json                     # TypeScript config
└── package.json                      # Dependencies
```

---

## Core Files to Understand

### 1. Supabase Client (`src/lib/supabase/client.ts`)

```typescript
import { createClient } from '@supabase/supabase-js';

export const supabase = createClient(
  process.env.NEXT_PUBLIC_SUPABASE_URL!,
  process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!
);
```

### 2. Claude API Client (`src/lib/ai/claude.ts`)

```typescript
import Anthropic from '@anthropic-ai/sdk';

const anthropic = new Anthropic({
  apiKey: process.env.ANTHROPIC_API_KEY,
});

export async function generateCode(prompt: string, context: string) {
  const response = await anthropic.messages.create({
    model: 'claude-3-5-sonnet-20241022',
    max_tokens: 4096,
    messages: [
      {
        role: 'user',
        content: `${context}\n\nUser request: ${prompt}`,
      },
    ],
  });

  return response.content[0].text;
}
```

### 3. Main Code Generation Route (`src/app/api/generate/route.ts`)

```typescript
import { NextRequest, NextResponse } from 'next/server';
import { generateCode } from '@/lib/ai/claude';
import { parseCodeResponse } from '@/lib/ai/parser';

export async function POST(request: NextRequest) {
  try {
    const { prompt, projectId, context } = await request.json();

    // Generate code with Claude
    const response = await generateCode(prompt, context);

    // Parse response to extract files
    const files = parseCodeResponse(response);

    // Save to database
    // ... database operations

    return NextResponse.json({ success: true, files });
  } catch (error) {
    return NextResponse.json(
      { error: 'Generation failed' },
      { status: 500 }
    );
  }
}
```

### 4. Tailwind Config with Blue Theme (`tailwind.config.js`)

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    './src/pages/**/*.{js,ts,jsx,tsx,mdx}',
    './src/components/**/*.{js,ts,jsx,tsx,mdx}',
    './src/app/**/*.{js,ts,jsx,tsx,mdx}',
  ],
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#eff6ff',
          100: '#dbeafe',
          200: '#bfdbfe',
          300: '#93c5fd',
          400: '#60a5fa',
          500: '#3b82f6',   // Main brand blue
          600: '#2563eb',
          700: '#1d4ed8',
          800: '#1e40af',
          900: '#1e3a8a',
        },
        accent: {
          500: '#06b6d4',   // Cyan accent
        },
      },
      fontFamily: {
        sans: ['Inter', 'sans-serif'],
        mono: ['JetBrains Mono', 'monospace'],
      },
      boxShadow: {
        glow: '0 0 20px rgba(59, 130, 246, 0.3)',
      },
    },
  },
  plugins: [],
};
```

---

## Common Development Tasks

### Adding a New Component

```bash
# Create component file
touch src/components/ui/MyComponent.tsx
```

```typescript
// src/components/ui/MyComponent.tsx
interface MyComponentProps {
  // Props
}

export function MyComponent({ }: MyComponentProps) {
  return (
    <div className="bg-primary-50 p-4 rounded-lg">
      {/* Component content */}
    </div>
  );
}
```

### Creating a New API Route

```bash
# Create route file
mkdir -p src/app/api/my-route
touch src/app/api/my-route/route.ts
```

```typescript
// src/app/api/my-route/route.ts
import { NextRequest, NextResponse } from 'next/server';

export async function GET(request: NextRequest) {
  return NextResponse.json({ message: 'Hello' });
}

export async function POST(request: NextRequest) {
  const body = await request.json();
  return NextResponse.json({ received: body });
}
```

### Adding a Database Table

```sql
-- Create migration file: supabase/migrations/YYYYMMDD_table_name.sql

CREATE TABLE my_table (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  user_id UUID REFERENCES auth.users NOT NULL,
  data TEXT,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Enable RLS
ALTER TABLE my_table ENABLE ROW LEVEL SECURITY;

-- Create policy
CREATE POLICY "Users can manage own data"
  ON my_table FOR ALL
  USING (auth.uid() = user_id);
```

---

## Testing

### Run Unit Tests

```bash
npm run test
# or
pnpm test
```

### Run E2E Tests

```bash
npm run test:e2e
# or
pnpm test:e2e
```

### Test Code Generation Locally

```typescript
// Test in Node.js REPL or create a test file
import { generateCode } from './src/lib/ai/claude';

const prompt = 'Create a blue button component';
const context = 'Project uses React, TypeScript, and Tailwind CSS';

const result = await generateCode(prompt, context);
console.log(result);
```

---

## Debugging

### Enable Debug Logs

```env
# .env.local
DEBUG=true
LOG_LEVEL=debug
```

### Common Issues

#### 1. Supabase Connection Error
```
Error: Invalid Supabase URL
```
**Solution**: Check that `NEXT_PUBLIC_SUPABASE_URL` is correct

#### 2. Claude API Error
```
Error: Invalid API key
```
**Solution**: Verify `ANTHROPIC_API_KEY` in `.env.local`

#### 3. Build Errors
```
Error: Module not found
```
**Solution**:
```bash
rm -rf .next
rm -rf node_modules
npm install
npm run dev
```

---

## Deployment

### Deploy to Vercel

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel

# Set environment variables in Vercel dashboard
# - NEXT_PUBLIC_SUPABASE_URL
# - NEXT_PUBLIC_SUPABASE_ANON_KEY
# - SUPABASE_SERVICE_ROLE_KEY
# - ANTHROPIC_API_KEY
```

### Environment Variables for Production

Make sure to set all environment variables in your hosting platform:
- Vercel: Project Settings → Environment Variables
- Netlify: Site Settings → Build & Deploy → Environment

---

## Development Workflow

### 1. Feature Branch

```bash
git checkout -b feature/my-feature
```

### 2. Make Changes

```bash
# Make your changes
# Test locally
npm run dev
```

### 3. Commit

```bash
git add .
git commit -m "feat: add my feature"
```

### 4. Push and Create PR

```bash
git push origin feature/my-feature
# Create PR on GitHub
```

---

## Performance Tips

### 1. Use React.memo for Expensive Components

```typescript
export const ExpensiveComponent = React.memo(({ data }) => {
  // Component logic
});
```

### 2. Lazy Load Heavy Components

```typescript
const MonacoEditor = dynamic(
  () => import('@monaco-editor/react'),
  { ssr: false }
);
```

### 3. Optimize Images

```typescript
import Image from 'next/image';

<Image
  src="/image.png"
  width={500}
  height={300}
  alt="Description"
/>
```

---

## Security Best Practices

### 1. Never Expose API Keys in Client

```typescript
// ❌ Bad
const apiKey = process.env.NEXT_PUBLIC_SECRET_KEY;

// ✅ Good - use server-side only
const apiKey = process.env.SECRET_KEY; // Only in API routes
```

### 2. Validate User Input

```typescript
import { z } from 'zod';

const schema = z.object({
  name: z.string().min(1).max(100),
  email: z.string().email(),
});

const validated = schema.parse(userInput);
```

### 3. Use Row Level Security in Supabase

Always enable RLS and create appropriate policies for each table.

---

## Useful Commands

```bash
# Development
npm run dev              # Start dev server
npm run build            # Build for production
npm run start            # Start production server
npm run lint             # Lint code
npm run format           # Format with Prettier

# Database
npx supabase db push     # Push migrations
npx supabase db reset    # Reset database
npx supabase gen types   # Generate TypeScript types

# Testing
npm run test             # Run unit tests
npm run test:watch       # Watch mode
npm run test:e2e         # E2E tests

# Deployment
vercel                   # Deploy to Vercel
vercel --prod            # Deploy to production
```

---

## Next Steps

1. ✅ Complete this quick start
2. 📖 Read [ARCHITECTURE.md](./ARCHITECTURE.md) for system design
3. 🎨 Review [DESIGN_SYSTEM.md](./DESIGN_SYSTEM.md) for UI guidelines
4. 🤖 Study [AI_PROMPTS.md](./AI_PROMPTS.md) for AI integration
5. 🗺️ Follow [ROADMAP.md](./ROADMAP.md) for development plan
6. 🚀 Start building!

---

## Getting Help

- 📚 Documentation: See other .md files in this repo
- 🐛 Issues: Create an issue on GitHub
- 💬 Discussions: Join discussions on GitHub

---

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Write tests
5. Submit a pull request

---

Happy coding! 🚀
