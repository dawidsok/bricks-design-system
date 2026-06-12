# Bricks Design System

A brutalist, instrument-panel design system extracted from the [Sunny 16](https://github.com/dawidsok/sunny-16) film photography exposure calculator.

The system starts as **tokens + guidelines**, not a component library. Components are specified as reusable styling rules first, so other apps and agents can recreate the look without inheriting Sunny 16 app logic.

## Status

- OSS-ready public repository scaffold
- Design tokens in JSON and CSS variable formats
- Agent styling guidelines for AI coding assistants
- Component guidelines/specs, not implementations

## Design principles

1. **Legibility over decoration** — this UI must survive bright sunlight, small screens, and quick glances.
2. **Brutalist instrument language** — square edges, hairline rules, monospace type, uppercase labels, no cosmetic chrome.
3. **Monochrome by default** — black/white/stone neutrals carry the interface; orange is reserved for warnings or off-target states.
4. **Token-first styling** — use semantic tokens before literal colors or arbitrary values.
5. **Components as behavior-agnostic guidelines** — a drum, badge, readout, or control may be implemented in any framework if it follows the same visual contract.

## Repository structure

```text
tokens/
  bricks.tokens.json   # canonical design tokens
styles/
  tokens.css                    # CSS custom properties generated/maintained from tokens
  tailwind-v4.css               # optional Tailwind v4 theme aliases
guidelines/
  agent-styling.md              # instructions for AI agents creating UI
  components.md                 # component-level visual contracts
  style-principles.md           # human-readable system rules
docs/
  extraction-notes.md           # mapping from Sunny 16 app styles to this system
examples/
  css-usage.html                # minimal no-build example
```

## Quick start

### Use CSS variables

Copy or import `styles/tokens.css`:

```css
@import "./styles/tokens.css";

.app {
  background: var(--bricks-color-surface);
  color: var(--bricks-color-text-primary);
  font-family: var(--bricks-font-family-mono);
}
```

Enable dark mode by adding either `.dark` or `data-theme="dark"` to the document root:

```html
<html class="dark">
```

### Use Tailwind v4 aliases

Copy or import `styles/tailwind-v4.css` after Tailwind is available:

```css
@import "tailwindcss";
@import "./styles/tailwind-v4.css";
```

Then use the CSS variables directly in utilities:

```tsx
<main className="min-h-screen bg-[var(--bricks-color-surface)] text-[var(--bricks-color-text-primary)] font-mono">
  <h1 className="text-sm uppercase tracking-[var(--bricks-letter-spacing-wordmark)] text-[var(--bricks-color-text-secondary)]">
    App Name
  </h1>
</main>
```

## Token formats

- `tokens/bricks.tokens.json` is the canonical source.
- `styles/tokens.css` is the practical runtime format for web apps.
- `styles/tailwind-v4.css` exposes theme aliases for Tailwind v4 projects.

## Agent usage

When asking an AI coding agent to style an app with this system, include:

```text
Follow Bricks Design System. Read guidelines/agent-styling.md first.
Use tokens from styles/tokens.css. Do not introduce rounded corners, shadows,
gradients, proportional fonts, or extra accent colors. Components are guidelines,
not imported implementations.
```

See [`guidelines/agent-styling.md`](guidelines/agent-styling.md).

## Package policy

This repo is intentionally lightweight. It is safe to vendor/copy files directly until a published package is needed.

## Author

[Dawid Sokół](https://github.com/dawidsok) · <dave@okhy.pl>

## License

MIT © Dawid Sokół
