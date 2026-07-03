# Frontend Standards

- **Framework**: React + Vite
- **UI/UX Framework:** Shadcn
- **Template**: [natiq-frontend](https://github.com/natiq-foundation/natiq-frontend)

## Naming

- Use restProps, not props

## imports periority

1. React, Next
2. other Deps
3. Yakad(lib, ui, x, symbol)
4. @/localfolders
5. ./localfiles
6. styles

## Structure

src
│
├─ assets
│ └─ svg
│ └─ IconName.tsx
│ - default export
│ - simple arrow function
│
├─ components (NO Default Export / ForwardRef / don't design pages here)
│
│ ├─ ui (Original shadcn components)
│ │ ├─ button.tsx
│ │ ├─ input.tsx
│ │ ├─ dialog.tsx
│ │ └─ ...
│ │
│ ├─ specified (Project‑specific components)
│ │ ├─ HeroBanner.tsx
│ │ ├─ LandingCard.tsx
│ │ └─ ...
│ │
│ ├─ features (Active components with logic)
│ │
│ │ ├─ darkMode
│ │ │ ├─ DarkModeToggle.tsx
│ │ │ ├─ useDarkMode.ts
│ │ │ └─ index.ts
│ │ │
│ │ ├─ user
│ │ │ ├─ UserFetcher.tsx
│ │ │ ├─ useUser.ts
│ │ │ └─ index.ts
│ │ │
│ │ └─ ...
│ │
│ └─ modules (Large UI blocks)
│
│ ├─ auth
│ │ ├─ LoginForm.tsx
│ │ ├─ RegisterForm.tsx
│ │ └─ index.ts
│ │
│ ├─ dashboard
│ │ ├─ Sidebar.tsx
│ │ ├─ Navbar.tsx
│ │ └─ index.ts
│ │
│ └─ ...
│
├─ layouts
│ ├─ AppLayout.tsx
│ ├─ AuthLayout.tsx
│ └─ ...
│
├─ routes (Page layout and composition only)
│
│ ├─ Dashboard
│ │ ├─ index.tsx (default export)
│ │ ├─ AppBarWrapper.tsx
│ │ ├─ IntroSection.tsx
│ │ ├─ StatsSection.tsx
│ │ └─ ...
│ │
│ └─ ...
│
├─ hooks (Reusable React hooks)
│ ├─ useMediaQuery.ts
│ ├─ useDebounce.ts
│ ├─ useLocalStorage.ts
│ └─ ...
│
├─ store (Global state management)
│ ├─ themeStore.ts
│ ├─ authStore.ts
│ ├─ userStore.ts
│ └─ ...
│
├─ context (React providers / dependency injection)
│ ├─ ThemeContext.tsx
│ ├─ AuthContext.tsx
│ ├─ QueryProvider.tsx
│ └─ ...
│
├─ lib (Framework or library helpers)
│ ├─ api.ts
│ ├─ fetcher.ts
│ ├─ cn.ts
│ └─ ...
│
├─ utils (Pure utility functions / no React)
│ ├─ format.ts
│ ├─ validators.ts
│ ├─ date.ts
│ ├─ numbers.ts
│ └─ string.ts
│
├─ globals.css
├─ router.tsx
├─ app.tsx
└─ main.tsx
