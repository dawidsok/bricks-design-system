# Agent Styling Guidelines

These instructions are for AI coding agents implementing UI with Bricks Brutalist.

## Read this first

Before changing UI code:

1. Read `README.md`.
2. Read `styles/tokens.css`.
3. Read `guidelines/style-principles.md`.
4. If touching a reusable UI pattern, read `guidelines/components.md`.

## Prime directive

**Keep the UI looking like a monochrome physical instrument, not a modern SaaS dashboard.**

If a styling choice makes the UI softer, friendlier, glossy, colorful, or card-like, it is probably wrong.

## Required implementation rules

### Use tokens

Prefer CSS variables from `styles/tokens.css`:

```css
color: var(--bricks-color-text-primary);
border-color: var(--bricks-color-border-muted);
font-family: var(--bricks-font-family-mono);
```

Tailwind arbitrary values are acceptable when they reference tokens:

```tsx
className="bg-[var(--bricks-color-surface)] text-[var(--bricks-color-text-primary)]"
```

Avoid hard-coded colors unless you are updating the design-system token files themselves.

### Use monospace everywhere

Every component and page shell must inherit or explicitly set:

```css
font-family: var(--bricks-font-family-mono);
```

Do not introduce app-default sans-serif type.

### Keep shape square

Use:

```css
border-radius: var(--bricks-border-radius-none);
```

Do not use:

- `rounded`
- `rounded-md`
- `rounded-full`
- pill buttons
- circular icon buttons unless the shape is a glyph itself, not a container

### Keep depth flat

Never add:

- `box-shadow`
- drop shadows
- gradients
- backdrop blur
- translucent glass panels

### Protect accent color meaning

Orange means an alert, mismatch, warning, or off-target reading.

Do not use orange for:

- brand decoration
- normal primary buttons
- selected tabs
- links
- success states

### Use opacity for hierarchy

Use semantic text tokens or opacity for inactive/secondary states. Do not invent gray scales per component.

Common hierarchy:

- selected/critical: primary text
- labels: secondary text
- metadata: tertiary text
- inactive items: opacity `0.3`

### Use terse uppercase labels

Prefer short instrument labels:

| Prefer | Avoid |
|---|---|
| `EV` | `Exposure Value` in primary UI |
| `ISO` | `Film speed setting` |
| `COND` | `Lighting condition` |
| `CAPTURE` | `Capture reading now` |
| `ZONE` | `Exposure zone adjustment` |

Longer explanatory text is allowed in empty states, permission messages, docs, and onboarding.

## Tailwind guidance

When using Tailwind, prefer these patterns:

```tsx
// Page shell
<main className="min-h-screen bg-[var(--bricks-color-surface)] text-[var(--bricks-color-text-primary)] font-mono flex flex-col items-center justify-center gap-8 p-4" />

// Label
<span className="text-xs uppercase tracking-[var(--bricks-letter-spacing-label)] text-[var(--bricks-color-text-secondary)]" />

// Square control
<button className="w-8 h-8 border border-[var(--bricks-color-border-muted)] text-[var(--bricks-color-text-secondary)] hover:border-[var(--bricks-color-border-hover)] hover:text-[var(--bricks-color-text-subtle)] transition-colors" />

// Alert readout
<div className="text-2xl font-bold tracking-[var(--bricks-letter-spacing-readout)] tabular-nums text-[var(--bricks-color-text-alert)]" />
```

Avoid these classes:

```text
rounded rounded-* shadow shadow-* drop-shadow bg-gradient-* from-* to-* blur backdrop-blur
font-sans font-serif text-blue-* text-green-* text-purple-* ring-* animate-bounce animate-pulse
```

`ring-*` may be used only if mapped to an explicit accessibility focus token in a future version. Until then, use a square border/outline.

## Component creation workflow

When asked to create a component:

1. Identify the closest component guideline in `guidelines/components.md`.
2. Implement the smallest semantic HTML structure that matches the guideline.
3. Apply tokens and strict square geometry.
4. Add accessible names and keyboard behavior where interactive.
5. Check against the forbidden class/property list.
6. Do not add a new component variant unless the design system needs it.
7. If a new variant is unavoidable, document it in `guidelines/components.md` before or with implementation.

## Review checklist

Before finalizing UI work, answer yes/no:

- Does every visible element use monospace?
- Are all corners square?
- Are there zero shadows, gradients, and blur effects?
- Is orange used only for alert/off-target states?
- Are labels uppercase and terse?
- Are borders hairline unless there is a specific instrument reason?
- Are inactive states low-opacity instead of new colors?
- Are numeric readouts tabular where alignment matters?
- Are interactive controls accessible by keyboard and screen reader?
- Did I avoid inventing component-local style values?

## If requirements conflict

Choose in this order:

1. Accessibility and legibility
2. Existing tokens
3. Existing component guidelines
4. Visual novelty

If a user requests a visual style that violates this system, explain the conflict and offer a token-compatible alternative.
