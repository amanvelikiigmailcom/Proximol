# Proximol - UI Components & Functionality

Полное описание функционала всех элементов интерфейса

---

## 1. Главная страница (Landing Page)

### Навигация (Header)

```
┌─────────────────────────────────────────────────────────┐
│ [Proximol Logo]    Features  Pricing  Docs   [Sign In] │
│                                              [Sign Up → ]│
└─────────────────────────────────────────────────────────┘
```

#### Кнопки:
- **[Proximol Logo]** - Возврат на главную страницу
- **Features** - Прокрутка к секции с возможностями
- **Pricing** - Прокрутка к тарифным планам
- **Docs** - Переход к документации
- **[Sign In]** - Открывает модальное окно входа
- **[Sign Up →]** - Открывает модальное окно регистрации (голубая кнопка)

### Hero Section

```
┌─────────────────────────────────────────────────────────┐
│         Build Web Apps with AI Conversation              │
│    Create production-ready applications in minutes       │
│                                                           │
│   [Start Building Free →]  [Watch Demo ▶]               │
│                                                           │
│         [Live Preview Animation]                         │
└─────────────────────────────────────────────────────────┘
```

#### Кнопки:
- **[Start Building Free →]**
  - Действие: Переход к регистрации → создание первого проекта
  - Стиль: Большая голубая кнопка с градиентом
  - Hover: Увеличение тени, эффект свечения
  - Клик: Анимация нажатия, переход на /signup

- **[Watch Demo ▶]**
  - Действие: Открывает видео демонстрацию в модальном окне
  - Стиль: Прозрачная кнопка с голубой обводкой
  - Hover: Голубой фон с прозрачностью

---

## 2. Страница входа (Login Page)

```
┌─────────────────────────────────────────────────────────┐
│                    Welcome back                          │
│                                                           │
│  Email:    [_____________________________]              │
│  Password: [_____________________________] [👁]          │
│                                                           │
│  [Sign In →]                     [Forgot Password?]     │
│                                                           │
│  ──────────── or ────────────                           │
│                                                           │
│  [Continue with GitHub 🐙]                               │
│  [Continue with Google 🔍]                               │
│                                                           │
│  Don't have an account? [Sign Up]                       │
└─────────────────────────────────────────────────────────┘
```

#### Функционал:

**Input поля:**
- **Email input**
  - Валидация: проверка формата email
  - Автофокус при загрузке
  - Автокомплит включен

- **Password input**
  - Валидация: минимум 8 символов
  - **[👁]** - Показать/скрыть пароль
  - Enter = отправка формы

**Кнопки:**
- **[Sign In →]**
  - Действие: Аутентификация через Supabase
  - Состояния: Normal / Loading / Error
  - Loading: Показывает спиннер, текст "Signing in..."
  - Success: Редирект на /dashboard
  - Error: Красная обводка полей, сообщение об ошибке

- **[Forgot Password?]**
  - Действие: Открывает модальное окно восстановления пароля
  - Запрашивает email
  - Отправляет письмо для сброса

- **[Continue with GitHub]**
  - Действие: OAuth через GitHub
  - Открывает popup окно GitHub
  - После авторизации: создает профиль и редирект на /dashboard

- **[Continue with Google]**
  - Действие: OAuth через Google
  - Аналогично GitHub

- **[Sign Up]**
  - Действие: Переход на /signup

---

## 3. Dashboard (Главная после входа)

```
┌─────────────────────────────────────────────────────────┐
│ [☰] Proximol    [🔍 Search projects...]    [👤] [🔔]   │
├─────────────────────────────────────────────────────────┤
│                                                           │
│  My Projects                              [+ New Project]│
│                                                           │
│  ┌───────────┐  ┌───────────┐  ┌───────────┐          │
│  │ Landing   │  │ Dashboard │  │ E-commerce│          │
│  │ Page      │  │ App       │  │ Site      │          │
│  │           │  │           │  │           │          │
│  │ [Open]    │  │ [Open]    │  │ [Open]    │          │
│  │ [⚙️] [🗑]   │  │ [⚙️] [🗑]   │  │ [⚙️] [🗑]   │          │
│  └───────────┘  └───────────┘  └───────────┘          │
│                                                           │
│  Recent Activity                                         │
│  • Updated Landing Page - 2 hours ago                   │
│  • Created Dashboard App - 1 day ago                    │
│  • Deployed E-commerce Site - 3 days ago               │
└─────────────────────────────────────────────────────────┘
```

### Top Navigation

**Левая сторона:**
- **[☰]** - Меню (открывает/закрывает sidebar)
  - Клик: Анимация slide-in/out sidebar
  - Mobile: Overlay sidebar

- **Proximol** - Логотип
  - Клик: Возврат на dashboard

- **[🔍 Search projects...]** - Поиск
  - Действие: Фильтрация проектов в реальном времени
  - Поддержка: Поиск по названию, описанию, тегам
  - Shortcut: Cmd/Ctrl + K открывает command palette

**Правая сторона:**
- **[👤]** - Профиль пользователя
  - Клик: Открывает dropdown меню
    - Profile Settings
    - Billing
    - API Keys
    - Sign Out

- **[🔔]** - Уведомления
  - Клик: Открывает панель уведомлений
  - Badge: Показывает количество непрочитанных
  - Типы уведомлений:
    - Deployment successful
    - Build failed
    - Collaboration invite
    - Usage limit warning

### Project Cards

**Элементы карточки проекта:**
- **Thumbnail** - Скриншот/превью проекта
  - Hover: Небольшое увеличение (scale 1.05)
  - Клик: Открывает проект

- **Название проекта**
  - Клик: Открывает проект
  - Double-click: Редактирование названия inline

- **Метаданные**
  - Framework badge (React/Vue/etc)
  - Last updated timestamp
  - Status indicator (Active/Draft/Archived)

- **[Open]** - Основная кнопка
  - Действие: Открывает проект в редакторе (/projects/{id})
  - Стиль: Голубая кнопка
  - Hover: Более темный голубой

- **[⚙️]** - Настройки проекта
  - Клик: Открывает dropdown меню
    - Rename
    - Duplicate
    - Export to GitHub
    - Deploy
    - Archive
    - Delete

- **[🗑]** - Удалить проект
  - Клик: Открывает confirmation dialog
  - Dialog: "Are you sure? This action cannot be undone."
  - Buttons: [Cancel] [Delete Forever]

### Action Buttons

- **[+ New Project]**
  - Действие: Открывает modal создания проекта
  - Стиль: Голубая кнопка с градиентом
  - Hover: Эффект свечения

**Modal "New Project":**
```
┌─────────────────────────────────────────────────────────┐
│  Create New Project                               [✕]   │
├─────────────────────────────────────────────────────────┤
│                                                           │
│  Start from:                                             │
│  ○ Blank Project                                         │
│  ○ Template                                              │
│  ○ Import from GitHub                                   │
│                                                           │
│  [Template Gallery ▼]                                   │
│  ┌────┐ ┌────┐ ┌────┐ ┌────┐                          │
│  │Land│ │Blog│ │Dash│ │Shop│                          │
│  │ing │ │    │ │board│ │    │                          │
│  └────┘ └────┘ └────┘ └────┘                          │
│                                                           │
│  Project Name: [_____________________________]          │
│  Description:  [_____________________________]          │
│                                                           │
│              [Cancel]  [Create Project →]               │
└─────────────────────────────────────────────────────────┘
```

**Кнопки в модале:**
- **[✕]** - Закрыть modal (ESC также работает)
- **Radio buttons** - Выбор способа создания
- **[Template Gallery ▼]** - Dropdown с шаблонами
- **Template cards** - Клик выбирает шаблон
- **[Cancel]** - Закрывает modal
- **[Create Project →]** - Создает проект и открывает редактор

---

## 4. Project Editor (Главный интерфейс разработки)

```
┌─────────────────────────────────────────────────────────┐
│ [←] Landing Page        [💾] [▶️] [🚀]    [👤] [⚙️]     │
├──────┬────────────────────────────┬─────────────────────┤
│ 📁   │                            │                     │
│ src/ │  // Code Editor            │   [Live Preview]    │
│ ├─App│  import React...           │                     │
│ ├─Hero│                           │   ┌───────────────┐ │
│ ├─CTA│  export function Hero() {  │   │   Your App    │ │
│ │     │    return (               │   │   Running     │ │
│ │     │      <div className=      │   │   Here        │ │
│ │ 💬  │        "bg-blue-500"      │   │               │ │
│ Chat │      >                     │   │  [Button]     │ │
│      │        Hero Section        │   │               │ │
│      │      </div>                │   └───────────────┘ │
├──────┤    )                       │                     │
│ User:│  }                         │  [Desktop▼] [🔄]   │
│ Make │                            │                     │
│ button│  [Problems] [Console]     │                     │
│ blue │                            │                     │
└──────┴────────────────────────────┴─────────────────────┘
```

### Top Toolbar

**Левая сторона:**
- **[←]** - Назад к dashboard
  - Действие: Возврат на /dashboard
  - Если есть несохраненные изменения: показывает warning dialog

- **Project Name** - "Landing Page"
  - Клик: Inline редактирование
  - Auto-save после изменения

**Центр:**
- **[💾]** - Save
  - Действие: Сохраняет все файлы в БД
  - Shortcut: Cmd/Ctrl + S
  - Состояния:
    - Normal: Серая иконка
    - Saving: Крутящийся спиннер
    - Saved: Зеленая галочка на 2 сек
  - Auto-save: Каждые 30 секунд если есть изменения

- **[▶️]** - Preview
  - Действие: Обновляет preview панель
  - Auto-refresh при сохранении
  - Если есть ошибки: показывает error overlay

- **[🚀]** - Deploy
  - Клик: Открывает deployment wizard
  - Состояния: Ready / Building / Deploying / Deployed
  - Показывает прогресс

**Правая сторона:**
- **[👤]** - Пользователь (как на dashboard)
- **[⚙️]** - Настройки проекта
  - Project Settings
  - Environment Variables
  - Build Settings
  - GitHub Settings
  - Danger Zone

---

## 5. File Tree Panel (Левая панель)

```
┌──────────────┐
│ 📁 src/      │
│   ├─📄 App.tsx
│   ├─📁 components/
│   │  ├─📄 Hero.tsx
│   │  ├─📄 Button.tsx
│   │  └─📄 Footer.tsx
│   ├─📁 pages/
│   └─📄 main.tsx
│ 📁 public/
│ 📄 package.json
│              │
│ [+ New File] │
└──────────────┘
```

### Функционал File Tree

**Элементы дерева:**
- **📁 Folder** - Клик: раскрыть/свернуть
  - Right-click: Context menu
    - New File
    - New Folder
    - Rename
    - Delete Folder
    - Reveal in Terminal

- **📄 File** - Клик: открыть в редакторе
  - Right-click: Context menu
    - Rename
    - Duplicate
    - Delete
    - Copy Path
    - Download

- **Active file** - Подсвечен голубым цветом
- **Modified file** - Белая точка рядом с именем

**Действия:**
- **Drag & Drop** - Перемещение файлов между папками
- **Multi-select** - Shift+Click для выбора нескольких
- **Search** - Cmd/Ctrl + P для поиска файлов

**Кнопки:**
- **[+ New File]**
  - Клик: Создает новый файл в текущей папке
  - Inline input для названия
  - Enter: создает файл
  - ESC: отменяет

---

## 6. Code Editor (Monaco Editor)

```
┌────────────────────────────────────────────────┐
│ [App.tsx ✕] [Hero.tsx ✕] [Button.tsx ✕]      │
├────────────────────────────────────────────────┤
│ 1  import React from 'react';                 │
│ 2  import { Hero } from './components/Hero';  │
│ 3                                              │
│ 4  export function App() {                    │
│ 5    return (                                  │
│ 6      <div className="min-h-screen">         │
│ 7        <Hero />                             │
│ 8      </div>                                  │
│ 9    )                                         │
│10  }                                           │
│                                                │
│ [Problems: 0] [Console] [Output]              │
└────────────────────────────────────────────────┘
```

### File Tabs

**Элементы табов:**
- **File name** - Клик: переключение между файлами
- **[✕]** - Закрыть таб
  - Клик: Закрывает файл
  - Если modified: показывает warning
  - Middle-click: Закрывает без предупреждения
- **Modified indicator** - Белая точка если файл изменен

**Действия:**
- **Drag tabs** - Изменение порядка табов
- **Ctrl+Tab** - Переключение между табами
- **Ctrl+W** - Закрыть текущий таб

### Editor Features

**Функционал редактора:**
- **Syntax highlighting** - Подсветка синтаксиса
- **Auto-completion** - Автодополнение (Ctrl+Space)
- **IntelliSense** - Подсказки TypeScript
- **Error highlighting** - Красное подчеркивание ошибок
- **Quick fixes** - Лампочка 💡 для быстрых исправлений
- **Format document** - Shift+Alt+F
- **Go to definition** - F12
- **Find & Replace** - Ctrl+F / Ctrl+H
- **Multi-cursor** - Alt+Click
- **Comment line** - Ctrl+/

**Context menu (Right-click):**
- Cut / Copy / Paste
- Format Document
- Go to Definition
- Find All References
- Rename Symbol
- AI: Explain this code
- AI: Optimize this code
- AI: Add comments

### Bottom Panel

**Tabs:**
- **[Problems]** - Список ошибок и предупреждений
  - Клик на ошибку: переход к строке
  - Фильтры: Errors / Warnings / Info

- **[Console]** - Консоль из preview
  - console.log() из приложения
  - Clear button
  - Filter level (log/warn/error)

- **[Output]** - Build логи
  - Vite dev server output
  - Build errors
  - Deployment logs

---

## 7. Chat Panel (AI Assistant)

```
┌─────────────────────────────┐
│ 💬 AI Assistant       [─][✕]│
├─────────────────────────────┤
│                             │
│ You: Create a blue button  │
│                             │
│ AI: I'll create a button   │
│     component for you...   │
│                             │
│     [📄 Button.tsx created] │
│     [View Code →]           │
│                             │
│ You: Add loading state     │
│                             │
│ AI: Adding loading state..  │
│     [Loading ⚡]             │
│                             │
├─────────────────────────────┤
│ [Type message...]      [🎤] │
│                        [📎] │
└─────────────────────────────┘
```

### Chat Messages

**User Message (Справа, голубой фон):**
```
┌─────────────────────┐
│ Create a blue button│ You
└─────────────────────┘
```
- Text: Сообщение пользователя
- Timestamp: Hover показывает время
- Edit: Double-click для редактирования

**AI Message (Слева, белый фон):**
```
┌─────────────────────────┐
AI │ I'll create a button   │
   │ component with:        │
   │ • Blue color scheme    │
   │ • Hover effects        │
   │ • Loading state        │
   │                        │
   │ [📄 Button.tsx]        │
   │ [View Code →]          │
   │ [Apply Changes]        │
   └─────────────────────────┘
```

**Элементы AI сообщения:**
- **Markdown text** - Форматированный текст
- **Code blocks** - С подсветкой синтаксиса и кнопкой Copy
- **File badges** - Показывают созданные/измененные файлы
- **[View Code →]** - Открывает файл в редакторе
- **[Apply Changes]** - Применяет изменения к проекту
- **[Regenerate 🔄]** - Генерирует другой вариант

**Loading State:**
```
AI │ Generating code...    │
   │ [⚡⚡⚡ Animating]      │
```

### Input Area

**Элементы:**
- **Text input** - Многострочный input
  - Placeholder: "Describe what you want to build..."
  - Auto-resize при вводе
  - Shift+Enter: новая строка
  - Enter: отправка

- **[🎤]** - Voice input
  - Клик: Начинает запись голоса
  - Recording: Показывает wave animation
  - Stop: Преобразует в текст и отправляет

- **[📎]** - Attach file
  - Клик: Открывает file picker
  - Поддержка: Images, mockups, sketches
  - AI анализирует изображение

**Shortcuts:**
- Enter: Отправить сообщение
- Shift+Enter: Новая строка
- ↑: Редактировать предыдущее сообщение
- ESC: Очистить input

### Panel Controls

- **[─]** - Minimize panel
  - Сворачивает до маленькой иконки
  - Клик на иконку: разворачивает обратно

- **[✕]** - Close panel
  - Закрывает чат
  - Можно открыть снова через меню

---

## 8. Preview Panel (Правая панель)

```
┌─────────────────────────────┐
│ [Desktop ▼] [🔄] [⚡] [📱] │
├─────────────────────────────┤
│ ┌─────────────────────────┐ │
│ │                         │ │
│ │   Your App Preview      │ │
│ │                         │ │
│ │   [Button Component]    │ │
│ │                         │ │
│ │   Live updating...      │ │
│ │                         │ │
│ └─────────────────────────┘ │
│                             │
│ http://localhost:3000       │
└─────────────────────────────┘
```

### Preview Toolbar

**Кнопки:**
- **[Desktop ▼]** - Device selector
  - Dropdown menu:
    - 💻 Desktop (1920x1080)
    - 💻 Laptop (1440x900)
    - 📱 Tablet (768x1024)
    - 📱 Mobile (375x667)
    - 📱 Mobile Large (414x896)
    - Custom size...
  - Клик: Меняет размер preview

- **[🔄]** - Refresh
  - Действие: Перезагружает preview
  - Shortcut: Cmd/Ctrl + R
  - Auto-refresh: При сохранении файлов

- **[⚡]** - Open in new window
  - Действие: Открывает preview в отдельном окне браузера
  - URL: localhost:3000 или custom dev URL
  - Полезно для тестирования на реальном размере экрана

- **[📱]** - Toggle rotation (для mobile)
  - Переключает portrait ↔ landscape
  - Только для mobile/tablet режимов

### Preview Frame

**Функционал:**
- **Live reload** - Автоматическое обновление при изменениях
- **Hot module replacement** - Обновление без перезагрузки страницы
- **Error overlay** - Показывает ошибки компиляции
- **Console integration** - Логи видны в Editor Console
- **Click-to-inspect** - Cmd+Click элемента открывает компонент в редакторе

**States:**
- **Loading** - Показывает spinner и "Building..."
- **Running** - Нормальный preview
- **Error** - Красный overlay с описанием ошибки и стеком
- **Offline** - Серый экран "Preview server stopped"

---

## 9. Settings Modal

### Project Settings

```
┌─────────────────────────────────────────────────────────┐
│ Project Settings                                  [✕]   │
├─────────────────────────────────────────────────────────┤
│ [General] [Build] [Environment] [GitHub] [Danger Zone]  │
├─────────────────────────────────────────────────────────┤
│ General Settings                                         │
│                                                           │
│ Project Name:  [Landing Page________________]           │
│ Description:   [My awesome landing page_____]           │
│ Framework:     [React ▼]                                │
│ Visibility:    ○ Private  ● Public                      │
│                                                           │
│              [Cancel]  [Save Changes]                   │
└─────────────────────────────────────────────────────────┘
```

**Tabs:**

### [General] Tab
- **Project Name** - Input для имени
- **Description** - Textarea для описания
- **Framework** - Dropdown (React/Vue/Svelte)
- **Visibility** - Radio buttons (Private/Public)
- **[Save Changes]** - Сохраняет настройки

### [Build] Tab
```
Build Command:     [npm run build_________]
Output Directory:  [dist__________________]
Install Command:   [npm install__________]

[Preview Build] [Reset to Defaults]
```

- **Build settings** - Custom build configuration
- **[Preview Build]** - Тестовый запуск build
- **[Reset to Defaults]** - Сброс к стандартным настройкам

### [Environment] Tab
```
Environment Variables

Development:
KEY                      VALUE                    [🗑]
API_URL                  http://localhost:3000    [🗑]
[+ Add Variable]

Production:
KEY                      VALUE                    [🗑]
API_URL                  https://api.prod.com     [🗑]
[+ Add Variable]
```

- **Environment tabs** - Dev/Staging/Production
- **Variables table** - Key-value пары
- **[+ Add Variable]** - Добавить новую переменную
- **[🗑]** - Удалить переменную
- **[Save]** - Сохраняет env variables

### [GitHub] Tab
```
GitHub Integration

Status: ✅ Connected to yourusername/landing-page

Repository:     yourusername/landing-page
Branch:         main
Auto-commit:    ☑ Enabled
Commit message: [AI-generated changes____________]

[Disconnect] [Open on GitHub →]
```

- **Connection status** - Показывает статус связи с GitHub
- **[Disconnect]** - Отключает репозиторий
- **[Open on GitHub →]** - Открывает repo в новой вкладке
- **Auto-commit checkbox** - Включает автоматические коммиты

### [Danger Zone] Tab
```
⚠️ Danger Zone

Archive Project
Archive this project. It will be hidden but not deleted.
[Archive Project]

Delete Project
Permanently delete this project. This cannot be undone.
[Delete Project]
```

- **[Archive Project]** - Архивирует проект (можно восстановить)
- **[Delete Project]** - Удаляет навсегда
  - Требует подтверждения: "Type project name to confirm"

---

## 10. Deployment Wizard

```
┌─────────────────────────────────────────────────────────┐
│ Deploy to Production                              [✕]   │
├─────────────────────────────────────────────────────────┤
│ Step 1: Choose Platform                                 │
│                                                           │
│ ┌────────────┐  ┌────────────┐  ┌────────────┐        │
│ │   Vercel   │  │  Netlify   │  │   Custom   │        │
│ │   [✓]      │  │            │  │            │        │
│ └────────────┘  └────────────┘  └────────────┘        │
│                                                           │
│ Step 2: Configuration                                   │
│                                                           │
│ Project Name:    [landing-page_____________]            │
│ Domain:          [landing-page.vercel.app__]            │
│ Build Command:   [npm run build___________]            │
│                                                           │
│ Step 3: Environment Variables                           │
│ ☑ Use production environment variables                 │
│                                                           │
│              [Back]  [Deploy Now →]                     │
└─────────────────────────────────────────────────────────┘
```

### Wizard Steps

**Step 1: Platform Selection**
- **Platform cards** - Клик выбирает платформу
- Показывает лого и информацию о платформе
- Recommended badge на лучшем варианте

**Step 2: Configuration**
- **Project name** - Автозаполняется из проекта
- **Domain** - Предлагает доступный домен
- **Build settings** - Показывает команды

**Step 3: Environment**
- **Checkbox** - Использовать prod env variables
- **Review** - Список env переменных

**Progress:**
```
Deploying...

✓ Building project
✓ Running tests
⏳ Deploying to Vercel
  Uploading assets...

[View Logs]
```

**Success:**
```
🎉 Deployment Successful!

Your site is live at:
https://landing-page.vercel.app

[Visit Site →]  [Copy URL]  [Share]
```

**Buttons:**
- **[Back]** - Предыдущий шаг
- **[Deploy Now →]** - Начинает деплой
- **[View Logs]** - Показывает логи деплоя
- **[Visit Site →]** - Открывает сайт
- **[Copy URL]** - Копирует URL
- **[Share]** - Открывает меню шаринга

---

## 11. Command Palette

```
┌─────────────────────────────────────────────────────────┐
│ [🔍 Type a command or search...]                        │
├─────────────────────────────────────────────────────────┤
│ > new                                                    │
│                                                           │
│ 📄 New File                               Ctrl+N        │
│ 📁 New Folder                             Ctrl+Shift+N  │
│ 📦 New Project                            Ctrl+Shift+P  │
│ 💬 New Chat Message                       Ctrl+/        │
│                                                           │
└─────────────────────────────────────────────────────────┘
```

**Открытие:** Cmd/Ctrl + K

**Категории команд:**

### File Operations
- `New File` - Создать файл
- `New Folder` - Создать папку
- `Open File` - Открыть файл (fuzzy search)
- `Save All` - Сохранить все
- `Close All` - Закрыть все табы

### AI Commands
- `Ask AI` - Начать чат с AI
- `Generate Component` - Сгенерировать компонент
- `Explain Code` - Объяснить выделенный код
- `Optimize Code` - Оптимизировать код
- `Add Tests` - Добавить тесты
- `Fix Errors` - Исправить ошибки

### Git Commands
- `Commit Changes` - Коммит
- `Push to GitHub` - Push
- `Pull from GitHub` - Pull
- `View History` - История коммитов

### Project Commands
- `Deploy` - Деплой
- `Settings` - Настройки
- `Preview` - Preview в новом окне
- `Export` - Экспорт проекта

### Navigation
- `Go to File` - Переход к файлу
- `Go to Line` - Переход к строке
- `Go to Symbol` - Переход к символу

**Функционал:**
- **Fuzzy search** - Нечеткий поиск команд
- **Keyboard navigation** - ↑↓ для выбора, Enter для выполнения
- **Recent commands** - Показывает последние команды
- **Shortcuts** - Отображает keyboard shortcuts

---

## 12. Component Library Panel

```
┌─────────────────────────────────────────────────────────┐
│ Component Library                                 [✕]   │
├─────────────────────────────────────────────────────────┤
│ [🔍 Search components...]     [All ▼] [Sort ▼]         │
├─────────────────────────────────────────────────────────┤
│                                                           │
│ Buttons                                                  │
│ ┌──────────┐  ┌──────────┐  ┌──────────┐              │
│ │[Primary] │  │[Secondary│  │ [Ghost]  │              │
│ │  Button  │  │  Button] │  │  Button  │              │
│ │ [Use]    │  │ [Use]    │  │ [Use]    │              │
│ └──────────┘  └──────────┘  └──────────┘              │
│                                                           │
│ Forms                                                    │
│ ┌──────────┐  ┌──────────┐                             │
│ │ Input    │  │ Select   │                             │
│ │ Field    │  │ Dropdown │                             │
│ │ [Use]    │  │ [Use]    │                             │
│ └──────────┘  └──────────┘                             │
└─────────────────────────────────────────────────────────┘
```

**Функционал:**

### Search & Filter
- **[🔍 Search]** - Поиск по названию/тегам
- **[All ▼]** - Фильтр по категории
  - All Components
  - Buttons
  - Forms
  - Layout
  - Navigation
  - Data Display
  - Feedback
- **[Sort ▼]** - Сортировка
  - Most Used
  - Alphabetical
  - Recent

### Component Cards
- **Preview** - Миниатюра компонента
- **Name** - Название компонента
- **[Use]** - Кнопка использования
  - Клик: Открывает insert dialog
  - Dialog: Выбор куда вставить компонент
  - Варианты:
    - Insert in current file
    - Create new file
    - Add to imports only

**Component Actions (Right-click):**
- View Code
- Copy Code
- Customize
- Add to Favorites
- Report Issue

---

## 13. Collaboration Features

### Share Modal

```
┌─────────────────────────────────────────────────────────┐
│ Share Project                                     [✕]   │
├─────────────────────────────────────────────────────────┤
│                                                           │
│ Share link:                                              │
│ https://proximol.dev/share/abc123  [Copy Link]         │
│                                                           │
│ Access:  ○ View only  ● Can edit                        │
│                                                           │
│ Invite by email:                                         │
│ [email@example.com______________] [Invite]              │
│                                                           │
│ Collaborators:                                           │
│                                                           │
│ 👤 John Doe (You)          Owner                        │
│ 👤 Jane Smith              Editor        [Remove]       │
│ 👤 Bob Johnson             Viewer        [Remove]       │
│                                                           │
│                          [Done]                          │
└─────────────────────────────────────────────────────────┘
```

**Кнопки:**
- **[Copy Link]** - Копирует ссылку для шаринга
- **Access radio** - Выбор уровня доступа
- **[Invite]** - Отправляет приглашение на email
- **[Remove]** - Удаляет collaborator
- **[Done]** - Закрывает modal

### Live Collaboration Indicators

```
Editor with cursors:
┌────────────────────────────────────────────────┐
│ 1  import React from 'react';                 │
│ 2  |Jane                                       │
│ 3  export function Button()█Bob {             │
│ 4    return <button>Click</button>            │
```

**Элементы:**
- **Colored cursor** - Курсор другого пользователя
- **Name label** - Имя пользователя над курсором
- **Selection highlight** - Выделенный текст других пользователей
- **Typing indicator** - Мигающий курсор

**Presence avatars (Top right):**
```
[👤Jane] [👤Bob] [+2]
```
- Клик на аватар: Показывает что делает пользователь
- `[+2]`: Показывает сколько еще пользователей

---

## 14. Notifications Panel

```
┌─────────────────────────────────────────────────────────┐
│ Notifications                    [Mark all read] [✕]   │
├─────────────────────────────────────────────────────────┤
│                                                           │
│ ● Deployment successful                    2 min ago    │
│   Your site is live at landing-page.vercel.app          │
│   [View Site] [Dismiss]                                 │
│                                                           │
│ ● Jane Smith invited you to collaborate   5 min ago    │
│   Project: E-commerce Dashboard                         │
│   [Accept] [Decline]                                    │
│                                                           │
│   Build failed                            10 min ago    │
│   TypeError in Hero.tsx line 23                         │
│   [View Logs] [Dismiss]                                 │
│                                                           │
│   Usage warning                            1 hour ago   │
│   You've used 80% of your monthly AI credits            │
│   [Upgrade] [Dismiss]                                   │
│                                                           │
└─────────────────────────────────────────────────────────┘
```

**Типы уведомлений:**

### Success (Зеленый)
- Deployment successful
- Build completed
- Invite accepted

### Info (Голубой)
- Collaboration invite
- New feature announcement
- Update available

### Warning (Желтый)
- Usage limit warning
- Deprecated API usage
- Security advisory

### Error (Красный)
- Build failed
- Deployment failed
- API error

**Actions:**
- **[Mark all read]** - Отмечает все как прочитанные
- **Notification item** - Клик открывает детали
- **Action buttons** - Специфичные для каждого типа
- **[Dismiss]** - Удаляет уведомление

---

## 15. Context Menus

### File Tree Context Menu
```
Right-click on file:
┌──────────────────┐
│ Open             │
│ Rename       F2  │
│ Duplicate        │
│ ─────────────── │
│ Copy Path        │
│ Copy Relative... │
│ ─────────────── │
│ AI Actions    ►  │
│ ─────────────── │
│ Delete      Del  │
└──────────────────┘
```

**AI Actions submenu:**
```
┌──────────────────┐
│ Explain Code     │
│ Add Comments     │
│ Optimize         │
│ Generate Tests   │
│ Refactor         │
└──────────────────┘
```

### Editor Context Menu
```
Right-click in editor:
┌──────────────────────┐
│ Cut           Ctrl+X │
│ Copy          Ctrl+C │
│ Paste         Ctrl+V │
│ ─────────────────── │
│ Format Document     │
│ ─────────────────── │
│ Go to Definition F12│
│ Find References     │
│ Rename Symbol   F2  │
│ ─────────────────── │
│ AI Assistant     ►  │
└──────────────────────┘
```

---

## 16. Keyboard Shortcuts

### Global
- `Cmd/Ctrl + K` - Command Palette
- `Cmd/Ctrl + S` - Save
- `Cmd/Ctrl + /` - Toggle Comment
- `Cmd/Ctrl + P` - Quick Open File
- `Cmd/Ctrl + Shift + P` - New Project
- `Cmd/Ctrl + B` - Toggle Sidebar

### Editor
- `Cmd/Ctrl + F` - Find
- `Cmd/Ctrl + H` - Replace
- `Cmd/Ctrl + D` - Select Next Occurrence
- `Cmd/Ctrl + Shift + L` - Select All Occurrences
- `Alt + ↑/↓` - Move Line Up/Down
- `Shift + Alt + ↑/↓` - Copy Line Up/Down
- `Cmd/Ctrl + /` - Toggle Comment
- `Shift + Alt + F` - Format Document
- `F12` - Go to Definition
- `Alt + F12` - Peek Definition

### Navigation
- `Ctrl + Tab` - Next Editor
- `Ctrl + Shift + Tab` - Previous Editor
- `Cmd/Ctrl + W` - Close Editor
- `Cmd/Ctrl + \` - Split Editor

### AI
- `Cmd/Ctrl + I` - Inline AI Chat
- `Cmd/Ctrl + Shift + I` - AI Sidebar
- `Cmd/Ctrl + .` - Quick Fix / AI Suggestions

---

## Резюме функционала

Все кнопки и элементы в Proximol имеют четкое назначение:

✅ **Визуальный feedback** - Hover, active, loading states
✅ **Keyboard shortcuts** - Быстрый доступ ко всем функциям
✅ **Context menus** - Дополнительные действия по правому клику
✅ **Tooltips** - Подсказки при наведении
✅ **Confirmation dialogs** - Для деструктивных действий
✅ **Loading states** - Для асинхронных операций
✅ **Error handling** - Информативные сообщения об ошибках
✅ **Accessibility** - ARIA labels, keyboard navigation

Голубая тема применяется ко всем интерактивным элементам для создания единого фирменного стиля! 💙
