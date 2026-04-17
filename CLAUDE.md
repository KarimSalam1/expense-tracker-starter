# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install       # Install dependencies
npm run dev       # Start dev server at http://localhost:3000
npm run build     # Production build
npm run lint      # Run ESLint
npm run preview   # Preview production build
```

## Architecture

This is a single-component React app (Vite + React 19). All logic lives in `src/App.jsx` — there are no sub-components, routing, or external state management.

**State in `App.jsx`:**
- `transactions` — array of `{ id, description, amount, type, category, date }`. `amount` is stored as a string (known bug — causes incorrect arithmetic in totals).
- `filterType` / `filterCategory` — control which transactions are shown in the table.

**Data flow:** all transaction CRUD and filtering happens inline in `App.jsx`. There is no persistence; data resets on page refresh.

**Known issues (intentional for the course):**
- `amount` is stored as a string instead of a number, causing incorrect income/expense totals.
- UI styling needs improvement.
- Code structure is monolithic and could be split into components.
