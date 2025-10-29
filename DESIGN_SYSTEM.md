# Proximol - Design System

## Brand Identity

**Mission**: Empower developers to build web applications through natural conversation with AI.

**Visual Theme**: Modern, clean, professional with a focus on **blue** as the primary brand color - representing trust, intelligence, and innovation.

---

## Color Palette

### Primary Colors (Blue-based)

```css
:root {
  /* Primary Blue Scale */
  --color-primary-50: #eff6ff;   /* Lightest blue - backgrounds */
  --color-primary-100: #dbeafe;  /* Very light blue - hover states */
  --color-primary-200: #bfdbfe;  /* Light blue - borders */
  --color-primary-300: #93c5fd;  /* Medium light blue - disabled states */
  --color-primary-400: #60a5fa;  /* Medium blue - secondary elements */
  --color-primary-500: #3b82f6;  /* Core brand blue - PRIMARY */
  --color-primary-600: #2563eb;  /* Dark blue - hover on primary */
  --color-primary-700: #1d4ed8;  /* Darker blue - active states */
  --color-primary-800: #1e40af;  /* Very dark blue - text on light */
  --color-primary-900: #1e3a8a;  /* Darkest blue - emphasis */

  /* Accent Blue (Cyan) */
  --color-accent-50: #ecfeff;
  --color-accent-100: #cffafe;
  --color-accent-200: #a5f3fc;
  --color-accent-300: #67e8f9;
  --color-accent-400: #22d3ee;
  --color-accent-500: #06b6d4;  /* Accent color */
  --color-accent-600: #0891b2;
  --color-accent-700: #0e7490;
  --color-accent-800: #155e75;
  --color-accent-900: #164e63;
}
```

### Neutral Colors

```css
:root {
  /* Grays */
  --color-gray-50: #f9fafb;
  --color-gray-100: #f3f4f6;
  --color-gray-200: #e5e7eb;
  --color-gray-300: #d1d5db;
  --color-gray-400: #9ca3af;
  --color-gray-500: #6b7280;
  --color-gray-600: #4b5563;
  --color-gray-700: #374151;
  --color-gray-800: #1f2937;
  --color-gray-900: #111827;

  /* True blacks and whites */
  --color-white: #ffffff;
  --color-black: #000000;
}
```

### Semantic Colors

```css
:root {
  /* Success - Green */
  --color-success-50: #f0fdf4;
  --color-success-500: #22c55e;
  --color-success-600: #16a34a;
  --color-success-700: #15803d;

  /* Warning - Amber */
  --color-warning-50: #fffbeb;
  --color-warning-500: #f59e0b;
  --color-warning-600: #d97706;
  --color-warning-700: #b45309;

  /* Error - Red */
  --color-error-50: #fef2f2;
  --color-error-500: #ef4444;
  --color-error-600: #dc2626;
  --color-error-700: #b91c1c;

  /* Info - Blue (same as primary) */
  --color-info-50: var(--color-primary-50);
  --color-info-500: var(--color-primary-500);
  --color-info-600: var(--color-primary-600);
  --color-info-700: var(--color-primary-700);
}
```

### Dark Mode Colors

```css
:root[data-theme='dark'] {
  /* Dark mode adjustments */
  --bg-primary: #0f172a;        /* Dark blue-gray */
  --bg-secondary: #1e293b;
  --bg-tertiary: #334155;

  --text-primary: #f1f5f9;
  --text-secondary: #cbd5e1;
  --text-tertiary: #94a3b8;

  /* Primary blue remains vibrant in dark mode */
  --color-primary: #3b82f6;
  --color-accent: #06b6d4;
}
```

---

## Typography

### Font Families

```css
:root {
  /* Primary font for UI */
  --font-sans: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;

  /* Monospace for code */
  --font-mono: 'JetBrains Mono', 'Fira Code', 'Consolas', monospace;

  /* Display font for headings */
  --font-display: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
}
```

### Type Scale

```css
:root {
  /* Font sizes */
  --text-xs: 0.75rem;      /* 12px */
  --text-sm: 0.875rem;     /* 14px */
  --text-base: 1rem;       /* 16px */
  --text-lg: 1.125rem;     /* 18px */
  --text-xl: 1.25rem;      /* 20px */
  --text-2xl: 1.5rem;      /* 24px */
  --text-3xl: 1.875rem;    /* 30px */
  --text-4xl: 2.25rem;     /* 36px */
  --text-5xl: 3rem;        /* 48px */
  --text-6xl: 3.75rem;     /* 60px */

  /* Line heights */
  --leading-none: 1;
  --leading-tight: 1.25;
  --leading-snug: 1.375;
  --leading-normal: 1.5;
  --leading-relaxed: 1.625;
  --leading-loose: 2;

  /* Font weights */
  --font-normal: 400;
  --font-medium: 500;
  --font-semibold: 600;
  --font-bold: 700;
  --font-extrabold: 800;
}
```

### Typography Usage

| Element | Size | Weight | Color |
|---------|------|--------|-------|
| H1 | 3xl-4xl | Bold | primary-900 |
| H2 | 2xl-3xl | Semibold | primary-800 |
| H3 | xl-2xl | Semibold | primary-700 |
| H4 | lg-xl | Medium | primary-700 |
| Body | base | Normal | gray-700 |
| Small | sm | Normal | gray-600 |
| Caption | xs | Normal | gray-500 |
| Code | sm | Mono | primary-600 |

---

## Spacing

```css
:root {
  --space-0: 0;
  --space-1: 0.25rem;   /* 4px */
  --space-2: 0.5rem;    /* 8px */
  --space-3: 0.75rem;   /* 12px */
  --space-4: 1rem;      /* 16px */
  --space-5: 1.25rem;   /* 20px */
  --space-6: 1.5rem;    /* 24px */
  --space-8: 2rem;      /* 32px */
  --space-10: 2.5rem;   /* 40px */
  --space-12: 3rem;     /* 48px */
  --space-16: 4rem;     /* 64px */
  --space-20: 5rem;     /* 80px */
  --space-24: 6rem;     /* 96px */
}
```

---

## Border Radius

```css
:root {
  --radius-none: 0;
  --radius-sm: 0.125rem;   /* 2px */
  --radius-base: 0.25rem;  /* 4px */
  --radius-md: 0.375rem;   /* 6px */
  --radius-lg: 0.5rem;     /* 8px */
  --radius-xl: 0.75rem;    /* 12px */
  --radius-2xl: 1rem;      /* 16px */
  --radius-3xl: 1.5rem;    /* 24px */
  --radius-full: 9999px;
}
```

---

## Shadows

```css
:root {
  /* Blue-tinted shadows */
  --shadow-sm: 0 1px 2px 0 rgba(59, 130, 246, 0.05);
  --shadow-base: 0 1px 3px 0 rgba(59, 130, 246, 0.1), 0 1px 2px -1px rgba(59, 130, 246, 0.1);
  --shadow-md: 0 4px 6px -1px rgba(59, 130, 246, 0.1), 0 2px 4px -2px rgba(59, 130, 246, 0.1);
  --shadow-lg: 0 10px 15px -3px rgba(59, 130, 246, 0.1), 0 4px 6px -4px rgba(59, 130, 246, 0.1);
  --shadow-xl: 0 20px 25px -5px rgba(59, 130, 246, 0.1), 0 8px 10px -6px rgba(59, 130, 246, 0.1);
  --shadow-2xl: 0 25px 50px -12px rgba(59, 130, 246, 0.25);

  /* Inner shadow */
  --shadow-inner: inset 0 2px 4px 0 rgba(59, 130, 246, 0.05);

  /* Glow effect for primary elements */
  --shadow-glow: 0 0 20px rgba(59, 130, 246, 0.3);
}
```

---

## Components

### Buttons

#### Primary Button
```css
.btn-primary {
  background: linear-gradient(135deg, var(--color-primary-500), var(--color-primary-600));
  color: white;
  padding: 0.75rem 1.5rem;
  border-radius: var(--radius-lg);
  font-weight: var(--font-medium);
  box-shadow: var(--shadow-md);
  transition: all 0.2s ease;
}

.btn-primary:hover {
  background: linear-gradient(135deg, var(--color-primary-600), var(--color-primary-700));
  box-shadow: var(--shadow-lg), var(--shadow-glow);
  transform: translateY(-1px);
}

.btn-primary:active {
  transform: translateY(0);
  box-shadow: var(--shadow-sm);
}
```

#### Secondary Button
```css
.btn-secondary {
  background: white;
  color: var(--color-primary-600);
  border: 2px solid var(--color-primary-200);
  padding: 0.75rem 1.5rem;
  border-radius: var(--radius-lg);
  font-weight: var(--font-medium);
  transition: all 0.2s ease;
}

.btn-secondary:hover {
  background: var(--color-primary-50);
  border-color: var(--color-primary-300);
}
```

#### Ghost Button
```css
.btn-ghost {
  background: transparent;
  color: var(--color-primary-600);
  padding: 0.75rem 1.5rem;
  border-radius: var(--radius-lg);
  font-weight: var(--font-medium);
  transition: all 0.2s ease;
}

.btn-ghost:hover {
  background: var(--color-primary-50);
}
```

### Input Fields

```css
.input {
  width: 100%;
  padding: 0.75rem 1rem;
  background: white;
  border: 2px solid var(--color-gray-200);
  border-radius: var(--radius-lg);
  font-size: var(--text-base);
  transition: all 0.2s ease;
}

.input:focus {
  outline: none;
  border-color: var(--color-primary-500);
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
}

.input::placeholder {
  color: var(--color-gray-400);
}
```

### Cards

```css
.card {
  background: white;
  border: 1px solid var(--color-gray-200);
  border-radius: var(--radius-xl);
  padding: var(--space-6);
  box-shadow: var(--shadow-base);
  transition: all 0.2s ease;
}

.card:hover {
  box-shadow: var(--shadow-md);
  border-color: var(--color-primary-200);
}

.card-header {
  border-bottom: 1px solid var(--color-gray-100);
  padding-bottom: var(--space-4);
  margin-bottom: var(--space-4);
}
```

### Chat Interface

```css
.chat-container {
  display: flex;
  flex-direction: column;
  height: 100vh;
  background: linear-gradient(to bottom, var(--color-primary-50), white);
}

.message-user {
  background: var(--color-primary-500);
  color: white;
  padding: var(--space-4);
  border-radius: var(--radius-xl);
  border-bottom-right-radius: var(--radius-sm);
  max-width: 70%;
  margin-left: auto;
  box-shadow: var(--shadow-md);
}

.message-assistant {
  background: white;
  color: var(--color-gray-800);
  padding: var(--space-4);
  border: 1px solid var(--color-primary-100);
  border-radius: var(--radius-xl);
  border-bottom-left-radius: var(--radius-sm);
  max-width: 70%;
  margin-right: auto;
  box-shadow: var(--shadow-sm);
}
```

### Code Editor Theme

```css
.code-editor {
  background: #0f172a;  /* Dark blue-gray */
  border: 1px solid var(--color-primary-800);
  border-radius: var(--radius-lg);
  padding: var(--space-4);
  font-family: var(--font-mono);
}

/* Syntax highlighting with blue accents */
.token.keyword { color: #3b82f6; }  /* Blue keywords */
.token.string { color: #22d3ee; }   /* Cyan strings */
.token.function { color: #60a5fa; } /* Light blue functions */
.token.comment { color: #64748b; }  /* Gray comments */
.token.number { color: #93c5fd; }   /* Light blue numbers */
```

### Navigation

```css
.navbar {
  background: white;
  border-bottom: 1px solid var(--color-primary-100);
  padding: var(--space-4) var(--space-6);
  box-shadow: var(--shadow-sm);
}

.nav-link {
  color: var(--color-gray-600);
  padding: var(--space-2) var(--space-4);
  border-radius: var(--radius-md);
  transition: all 0.2s ease;
}

.nav-link:hover {
  color: var(--color-primary-600);
  background: var(--color-primary-50);
}

.nav-link.active {
  color: var(--color-primary-700);
  background: var(--color-primary-100);
  font-weight: var(--font-medium);
}
```

### Sidebar

```css
.sidebar {
  width: 280px;
  background: linear-gradient(to bottom, var(--color-primary-600), var(--color-primary-800));
  color: white;
  padding: var(--space-6);
  box-shadow: var(--shadow-xl);
}

.sidebar-item {
  padding: var(--space-3) var(--space-4);
  border-radius: var(--radius-lg);
  transition: all 0.2s ease;
  color: var(--color-primary-100);
}

.sidebar-item:hover {
  background: rgba(255, 255, 255, 0.1);
  color: white;
}

.sidebar-item.active {
  background: rgba(255, 255, 255, 0.2);
  color: white;
  font-weight: var(--font-medium);
}
```

### Modal

```css
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(15, 23, 42, 0.75);
  backdrop-filter: blur(4px);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal {
  background: white;
  border-radius: var(--radius-2xl);
  max-width: 600px;
  width: 90%;
  padding: var(--space-8);
  box-shadow: var(--shadow-2xl);
  border: 1px solid var(--color-primary-200);
}

.modal-header {
  color: var(--color-primary-800);
  font-size: var(--text-2xl);
  font-weight: var(--font-bold);
  margin-bottom: var(--space-4);
}
```

### Loading States

```css
.spinner {
  width: 40px;
  height: 40px;
  border: 4px solid var(--color-primary-100);
  border-top-color: var(--color-primary-600);
  border-radius: 50%;
  animation: spin 0.8s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

.skeleton {
  background: linear-gradient(
    90deg,
    var(--color-gray-200) 25%,
    var(--color-primary-100) 50%,
    var(--color-gray-200) 75%
  );
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
  border-radius: var(--radius-md);
}

@keyframes shimmer {
  0% { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}
```

### Toast Notifications

```css
.toast {
  background: white;
  border-left: 4px solid var(--color-primary-500);
  padding: var(--space-4);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-lg);
  display: flex;
  align-items: center;
  gap: var(--space-3);
}

.toast.success {
  border-left-color: var(--color-success-500);
}

.toast.error {
  border-left-color: var(--color-error-500);
}

.toast.warning {
  border-left-color: var(--color-warning-500);
}

.toast.info {
  border-left-color: var(--color-primary-500);
}
```

---

## Animations

```css
/* Fade in */
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Slide in from right */
@keyframes slideInRight {
  from {
    opacity: 0;
    transform: translateX(20px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

/* Pulse (for attention) */
@keyframes pulse {
  0%, 100% {
    opacity: 1;
  }
  50% {
    opacity: 0.7;
  }
}

/* Glow effect */
@keyframes glow {
  0%, 100% {
    box-shadow: 0 0 20px rgba(59, 130, 246, 0.3);
  }
  50% {
    box-shadow: 0 0 30px rgba(59, 130, 246, 0.5);
  }
}
```

---

## Layout Patterns

### Dashboard Layout

```
┌─────────────────────────────────────────────────────┐
│  Navbar (white bg, blue accents)                    │
├──────────┬──────────────────────────────────────────┤
│          │                                           │
│ Sidebar  │  Main Content Area                       │
│ (blue    │  (light blue gradient background)        │
│ gradient)│                                           │
│          │  ┌────────────────────────────┐          │
│          │  │  Cards with blue borders   │          │
│          │  └────────────────────────────┘          │
│          │                                           │
└──────────┴──────────────────────────────────────────┘
```

### Chat Layout

```
┌─────────────────────────────────────────────────────┐
│  Header (project name, actions)                     │
├──────────┬──────────────────────────────────────────┤
│          │  Messages Area                            │
│ File     │  (gradient blue to white background)     │
│ Tree     │                                           │
│ (left    │  ┌──────────────────────────┐            │
│ panel)   │  │  User message (blue)     │            │
│          │  └──────────────────────────┘            │
│          │  ┌──────────────────────────┐            │
│          │  │ AI message (white/border)│            │
│          │  └──────────────────────────┘            │
├──────────┴──────────────────────────────────────────┤
│  Input Area (white with blue focus)                 │
└─────────────────────────────────────────────────────┘
```

---

## Accessibility

### Color Contrast
- All text meets WCAG 2.1 AA standards (4.5:1 for normal text, 3:1 for large)
- Primary blue (#3b82f6) on white: 4.53:1 ✓
- White on primary blue (#3b82f6): 4.53:1 ✓
- Always test color combinations

### Focus States
```css
:focus-visible {
  outline: 2px solid var(--color-primary-500);
  outline-offset: 2px;
}
```

### Screen Reader Support
- Use semantic HTML
- Add ARIA labels where needed
- Ensure keyboard navigation works
- Provide alternative text for images

---

## Responsive Design

### Breakpoints
```css
:root {
  --breakpoint-sm: 640px;   /* Mobile */
  --breakpoint-md: 768px;   /* Tablet */
  --breakpoint-lg: 1024px;  /* Desktop */
  --breakpoint-xl: 1280px;  /* Large Desktop */
  --breakpoint-2xl: 1536px; /* Extra Large */
}
```

### Mobile-First Approach
- Design for mobile first
- Add complexity for larger screens
- Use responsive typography
- Stack elements vertically on mobile
- Use hamburger menu for navigation

---

## Icon System

**Library**: Lucide React

**Colors**:
- Primary actions: `var(--color-primary-600)`
- Secondary actions: `var(--color-gray-600)`
- Success: `var(--color-success-500)`
- Error: `var(--color-error-500)`
- Warning: `var(--color-warning-500)`

**Sizes**:
- Small: 16px
- Medium: 20px
- Large: 24px
- XLarge: 32px

---

## Logo & Branding

### Logo Concept
- Modern geometric design
- Incorporates shades of blue
- Works in both light and dark modes
- Scalable (SVG format)

### Brand Voice
- Professional yet approachable
- Empowering and innovative
- Clear and concise
- Encouraging experimentation

---

## Implementation Example

### Tailwind Config
```javascript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#eff6ff',
          100: '#dbeafe',
          200: '#bfdbfe',
          300: '#93c5fd',
          400: '#60a5fa',
          500: '#3b82f6',  // Main brand color
          600: '#2563eb',
          700: '#1d4ed8',
          800: '#1e40af',
          900: '#1e3a8a',
        },
        accent: {
          50: '#ecfeff',
          500: '#06b6d4',
          600: '#0891b2',
        }
      },
      fontFamily: {
        sans: ['Inter', 'sans-serif'],
        mono: ['JetBrains Mono', 'monospace'],
      },
      boxShadow: {
        'glow': '0 0 20px rgba(59, 130, 246, 0.3)',
        'glow-lg': '0 0 30px rgba(59, 130, 246, 0.5)',
      }
    },
  },
}
```

---

## Design Principles

1. **Clarity First**: Every element should have a clear purpose
2. **Consistency**: Use the design system throughout
3. **Blue as Identity**: Blue should be prominent but not overwhelming
4. **Responsive**: Works on all device sizes
5. **Accessible**: Meets WCAG 2.1 AA standards
6. **Performance**: Fast loading and smooth animations
7. **Delightful**: Subtle animations and transitions create joy
