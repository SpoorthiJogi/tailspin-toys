---
description: 'Central UI strategy and component development philosophy'
---

# UI Component Strategy

This file defines the central UI development strategy for Tailspin Toys. Technology-specific guidance is in separate instruction files.

## Component Architecture

### Technology Separation

- **Astro** (`.astro` files): Pages, layouts, components, routing, and static content. The site is fully prerendered (`output: 'static'`), so components render to HTML at build time.
- **Tailwind CSS** (utility classes): Styling
- **Astro `<script>`**: Reach for a small client-side script only when genuine interactivity is required — there is no client-side UI framework.

Refer to technology-specific instruction files:
- [`astro.instructions.md`](astro.instructions.md) - Astro pages, layouts, and components
- [`style.instructions.md`](style.instructions.md) - Tailwind CSS styling patterns

## Core Principles

### Comments and Documentation

- Comment intent, constraints, and non-obvious decisions — explain *why* the code exists rather than restating *what* the code already says.
- Prefer clear names and simple structure over comments that narrate straightforward mechanics.
- Keep comments next to the behavior they explain. Update or remove comments in the same change as the related code; an outdated comment is a bug.
- Use TSDoc/JSDoc for exported APIs and component contracts. Document the purpose, parameters, and return value where applicable.

### TypeScript Formatting

- Use single quotes for TypeScript strings, terminate statements with semicolons, and include trailing commas in multiline collections and parameter lists.
- Use spaces inside object braces (`{ value }`) and keep formatting consistent with the ESLint rules in `eslint.config.js`.
- Run `npm run lint` before submitting changes; do not bypass formatting errors with disable comments.

### Testability

- Every interactive element MUST include a `data-testid` attribute
- Use descriptive test IDs that identify the element's purpose and context
- Examples: `data-testid="game-card-{game.id}"`, `data-testid="submit-button"`, `data-testid="nav-home"`

### Accessibility

- Use semantic HTML elements (`<nav>`, `<main>`, `<article>`, `<button>`)
- Provide ARIA labels and roles where semantic HTML isn't sufficient
- Use plain `<nav>` with `<a>`/`<button>` elements for site navigation — do **not** add `role="menu"`. Reserve `role="menu"` / `role="menuitem"` for true application-style menus that implement full composite keyboard semantics (arrow-key roving focus, Home/End, type-ahead)
- Loading states should use `role="status"` and `aria-live="polite"` for screen reader announcements
- Include Escape key handlers for dismissible elements (menus, modals)
- Ensure keyboard navigation works for all interactive elements, with proper focus management
- Include visible focus states: `focus:ring-2 focus:ring-blue-500 focus:outline-none`
- Maintain sufficient color contrast (especially in dark theme)

### Design Consistency

- Dark theme throughout the application
- Modern, clean UI with rounded corners and smooth transitions
- Consistent spacing and visual hierarchy
- Responsive design that works on mobile, tablet, and desktop

### Component Reusability

- Create reusable components for common UI patterns
- Keep components focused on a single responsibility
- Use props for configuration, not duplication
- Document component APIs with a typed `Props` interface and a short description of each non-obvious prop

## Development Workflow

1. **Choose the right tool**: 
   - Content & structure → Astro components/pages
   - Styling → Tailwind
   - Client interactivity (rare) → a scoped Astro `<script>`

2. **Follow technology-specific patterns**: 
   - Refer to the appropriate instruction file

3. **Ensure testability**: 
   - Add `data-testid` to all interactive elements

4. **Verify accessibility**: 
   - Test keyboard navigation
   - Check focus states
   - Validate semantic structure
