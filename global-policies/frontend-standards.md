# Frontend Standards

- **Framework**: React (PWA/TS) + Vite
- **UI/UX Framework:** shadcn
- **API SDK:** nq-sdk
- **Template**: [natiq-frontend](https://github.com/natiq-foundation/natiq-frontend)

## Naming

- Use restProps, not props
- Separate JSON files for every lang in app translations (i18n)

## Imports Priority

1. React, Next
2. Other dependencies
3. Yakad(lib, ui, x, symbol)
4. @/localfolders
5. ./localfiles
6. styles

## URL

- **Root path**: Omit the language code (`/`).
- **Content paths**: Include the language code (e.g., `/en/...`, `/fa/...`) as they require multilingual SEO.
- **Technical paths**: Language code is optional; the priority is to omit it.
- **Note**: The user's selected language is stored in cross-domain cookies, not in the URL.

### URL Strategy

| Scenario                                                        | Action                                                                                                             |
| :-------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------- |
| **Cookie exists**                                               | Use the cookie language.                                                                                           |
| **No cookie, but URL has langCode**                             | Use the URL language (for SEO and initial context). Save this to the cookie.                                       |
| **No cookie, no URL langCode**                                  | Fall back to browser language (`Accept-Language`). **Do not** save this to the cookie.                             |
| **Cookie conflicts with URL langCode**                          | Cookie wins (render in cookie language). Show a prompt offering the user the option to switch to the URL language. |
| **User explicitly selects a language** (via switcher or prompt) | Save the selected language to the cookie.                                                                          |

## Structure

```
src
│
├─ assets
│ ├─ svg
│ └─ IconName.tsx
│ - default export
│ - simple arrow function
│
├─ components (NO default export / don't design pages here)
│ │
│ ├─ ui (Standard UI components)
│ │ ├─ button
│ │ ├─ input
│ │ ├─ dialog
│ │ ├─ Card
│ │ ├─ Footer
│ │ └─ ...
│ │
│ ├─ specified (Project‑specific/Wrapped UI components)
│ │ ├─ SerachInput (Specified UI SearchInput for this project)
│ │ ├─ CardWrapped (Wrapped from Yakad or ex.)
│ │ ├─ FooterWrapped
│ │ └─ ...
│ │
│ └─ features (Active components with logic)
│   ├─ darkMode
│   │ ├─ DarkModeToggle.tsx
│   │ └─ useDarkMode.ts (Save data on cookie)
│   ├─ SearchBar
│   │ ├─ SearchBar.tsx
│   │ ├─ api.ts (Get search result from api)
│   │ └─ forward.ts (Forward to selected item)
│   ├─ user
│   │ ├─ User.tsx (Profile Button on corner)
│   │ └─ useUser.ts
│   └─ ...
│
├─ layouts
│ ├─ AppLayout.tsx
│ ├─ AuthLayout.tsx
│ └─ ...
│
├─ routes (Page content)
│ ├─ Intro
│ │ ├─ index.tsx (default export)
│ │ ├─ AppBarWrapper.tsx
│ │ ├─ IntroSection.tsx
│ │ ├─ StatsSection.tsx
│ │ └─ ...
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
│ ├─ sdk.ts
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
```
