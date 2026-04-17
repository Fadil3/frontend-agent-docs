---
tags:
  - engineering
  - frontend
  - standards
  - guidelines
date: 2026-04-17
---

# Frontend Engineering Standards

This document serves as the ground truth for Hermes Agent during automated development. Hermes will read this file before starting any coding task to ensure compliance with our architecture and style preferences.

## 1. Core Principles
- **Type Safety:** TypeScript is mandatory. Strict mode must remain enabled. No `any`.
- **Component Architecture:** Functional components only. Atomic design pattern (Atoms -> Molecules -> Organisms).
- **Styling:** [Insert Standard: e.g., Tailwind CSS, CSS Modules, or Styled Components].
- **State Management:** [Insert Standard: e.g., Zustand, React Query/TanStack Query].

## 2. Testing Standards
- **Framework:** [e.g., Vitest + React Testing Library]
- **Coverage:** Minimum 80% coverage on new logic.
- **Approach:** Focus on accessibility roles (`getByRole`) over `data-testid` where possible.
- **Integration:** All components must be tested for interactions (clicks, input changes) and state transitions.

## 3. Workflow & Best Practices
- **PR Structure:** Automated via GitLab MCP. Description must include the Notion task link and a summary of changes.
- **Naming Conventions:** PascalCase for components, camelCase for variables/functions.
- **Review Pipeline:**
    1. `npm run typecheck`
    2. `npm run lint`
    3. `npm run test`
    4. Automated review by Hermes (via `requesting-code-review` skill).

## 4. Specific Patterns (Project-Specific)
- [Insert any project-specific constraints: e.g., "Always use `framer-motion` for animations", "Do not import CSS directly in TSX files"]

---

## 🛠 Automated Verification (Hermes Checklist)
*Hermes is instructed to run this checklist before every push.*
- [ ] TypeScript check pass
- [ ] ESLint clean
- [ ] All unit tests passing
- [ ] Accessibility check (A11y)
- [ ] Guidelines compliance check
