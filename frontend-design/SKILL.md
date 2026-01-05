# Frontend Design Skill

Generate modern, accessible, and responsive frontend code with consistent design patterns.

## Trigger

Activated when user asks for:
- UI components (buttons, cards, modals, forms)
- Page layouts
- Styling/CSS work
- React/Vue/Svelte components with styling
- Design system implementation

## Design Principles

### 1. Accessibility First (WCAG AA)

- Minimum contrast ratio: 4.5:1 for text, 3:1 for large text
- All interactive elements must be keyboard accessible
- Use semantic HTML (`<button>`, `<nav>`, `<main>`, `<article>`)
- Include `aria-label` for icon-only buttons
- Focus states must be visible
- Never rely on color alone to convey information

### 2. Color Palette

**Dark Theme (default)**:
```css
--bg-primary: #000000;      /* Pure black background */
--bg-secondary: #111111;    /* Elevated surfaces */
--bg-tertiary: #1a1a1a;     /* Cards, modals */
--text-primary: #ffffff;    /* Main text */
--text-secondary: #a0a0a0;  /* Secondary text */
--accent: #3b82f6;          /* Blue accent */
--accent-hover: #2563eb;    /* Accent hover state */
--success: #22c55e;         /* Green */
--warning: #f59e0b;         /* Amber */
--error: #ef4444;           /* Red */
--border: #333333;          /* Borders */
```

**Light Theme**:
```css
--bg-primary: #ffffff;
--bg-secondary: #f5f5f5;
--bg-tertiary: #e5e5e5;
--text-primary: #000000;
--text-secondary: #666666;
```

### 3. Typography

```css
--font-sans: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
--font-mono: 'JetBrains Mono', 'Fira Code', monospace;

--text-xs: 0.75rem;    /* 12px */
--text-sm: 0.875rem;   /* 14px */
--text-base: 1rem;     /* 16px */
--text-lg: 1.125rem;   /* 18px */
--text-xl: 1.25rem;    /* 20px */
--text-2xl: 1.5rem;    /* 24px */
--text-3xl: 1.875rem;  /* 30px */

--leading-tight: 1.25;
--leading-normal: 1.5;
--leading-relaxed: 1.75;
```

### 4. Spacing System (8px base)

```css
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
```

### 5. Border Radius

```css
--radius-sm: 0.25rem;   /* 4px - inputs, small buttons */
--radius-md: 0.5rem;    /* 8px - cards, modals */
--radius-lg: 0.75rem;   /* 12px - large cards */
--radius-xl: 1rem;      /* 16px - hero sections */
--radius-full: 9999px;  /* Pills, avatars */
```

### 6. Shadows

```css
--shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
--shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
--shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
--shadow-xl: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
```

## Layout Preferences

### Grid vs Flexbox

- **CSS Grid**: Card grids, page layouts, two-dimensional layouts
- **Flexbox**: Navigation, single-row/column alignment, centering

### Responsive Breakpoints

```css
--screen-sm: 640px;   /* Mobile landscape */
--screen-md: 768px;   /* Tablet */
--screen-lg: 1024px;  /* Desktop */
--screen-xl: 1280px;  /* Large desktop */
--screen-2xl: 1536px; /* Extra large */
```

### Container

```css
.container {
  width: 100%;
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 1rem;
}

@media (min-width: 640px) {
  .container { padding: 0 1.5rem; }
}

@media (min-width: 1024px) {
  .container { padding: 0 2rem; }
}
```

## Component Patterns

### Buttons

```css
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  padding: 0.5rem 1rem;
  font-size: 0.875rem;
  font-weight: 500;
  border-radius: 0.5rem;
  transition: all 150ms ease;
  cursor: pointer;
}

.btn:focus-visible {
  outline: 2px solid var(--accent);
  outline-offset: 2px;
}

.btn-primary {
  background: var(--accent);
  color: white;
}

.btn-primary:hover {
  background: var(--accent-hover);
}

.btn-secondary {
  background: transparent;
  border: 1px solid var(--border);
  color: var(--text-primary);
}

.btn-secondary:hover {
  background: var(--bg-secondary);
}
```

### Cards

```css
.card {
  background: var(--bg-tertiary);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  padding: var(--space-6);
}

.card-hover {
  transition: transform 150ms ease, box-shadow 150ms ease;
}

.card-hover:hover {
  transform: translateY(-2px);
  box-shadow: var(--shadow-lg);
}
```

### Forms

```css
.input {
  width: 100%;
  padding: 0.5rem 0.75rem;
  background: var(--bg-secondary);
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  color: var(--text-primary);
  font-size: 0.875rem;
}

.input:focus {
  outline: none;
  border-color: var(--accent);
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
}

.input::placeholder {
  color: var(--text-secondary);
}

.label {
  display: block;
  margin-bottom: 0.5rem;
  font-size: 0.875rem;
  font-weight: 500;
  color: var(--text-primary);
}
```

## Constraints / NEVER

- NEVER use gradients unless explicitly requested
- NEVER use `#1a1a1a` for dark backgrounds - use `#000` or `#111`
- NEVER use inline styles in React/Vue components
- NEVER use `!important` unless absolutely necessary
- NEVER use pixel values for font sizes (use rem)
- NEVER use `outline: none` without providing alternative focus indicator
- NEVER use color alone to indicate state (add icons/text)
- NEVER nest more than 3 levels in CSS/SCSS

## Preferences

- Prefer CSS custom properties (variables) over hardcoded values
- Prefer `gap` over margins for spacing flex/grid children
- Prefer `min-height: 100dvh` over `100vh` for mobile
- Prefer CSS Grid for card layouts (auto-fill/auto-fit)
- Prefer native CSS over utility frameworks when possible
- Prefer `clamp()` for fluid typography
- Prefer semantic class names over utility classes

## Animation Guidelines

```css
/* Subtle, professional animations */
--transition-fast: 150ms ease;
--transition-base: 200ms ease;
--transition-slow: 300ms ease;

/* Respect user preferences */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

## Framework-Specific

### React

- Use CSS Modules or styled-components
- Component file structure: `ComponentName/index.tsx`, `styles.module.css`
- Export types separately when needed

### Tailwind (if requested)

- Use `@apply` sparingly - prefer component extraction
- Custom colors in `tailwind.config.js`, not inline
- Use `cn()` utility for conditional classes

## Output Format

When generating components, always include:

1. **Component code** (JSX/HTML)
2. **Styles** (CSS/SCSS/CSS Modules)
3. **Usage example**
4. **Accessibility notes** (if relevant)
