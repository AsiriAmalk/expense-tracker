# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev      # Start dev server at http://localhost:5173
npm run build    # Production build
npm run lint     # Run ESLint
npm run preview  # Preview production build
```

**Note:** Requires Node.js 20.19+ or 22.12+. If using nvm: `nvm use 22`.

## Architecture

This is a single-file React app — all logic and UI lives in `src/App.jsx`. There are no separate components, routing, or state management libraries.

- `src/App.jsx` — entire app: transaction state, filtering, summary calculations, form handling, and JSX
- `src/App.css` — component styles
- `src/index.css` — global styles
- `src/main.jsx` — React root mount

### Known issues (intentional for the course)
- `amount` is stored as a string, causing string concatenation instead of numeric addition in `totalIncome`/`totalExpenses`
- The "Freelance Work" transaction is marked as `type: "expense"` but categorized as `"salary"`
- UI is intentionally minimal/unstyled
