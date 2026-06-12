# Bricks Brutalist Style Principles

## The contract

Bricks Brutalist is a design language for small, focused tools that should feel like physical instruments: camera dials, labels etched into a panel, measurement readouts, and sparse controls.

It is not generic minimalism. It is deliberately strict.

## Non-negotiables

1. **Monospace only**
   - Use the system monospace stack for every text element.
   - No proportional display font, no serif, no UI default sans.

2. **No rounded corners**
   - Border radius is always `0`.
   - Controls, badges, frames, overlays, and panels are square.

3. **No decorative depth**
   - No shadows.
   - No gradients.
   - No blur/frosted glass.
   - No neumorphism.

4. **Monochrome first**
   - Use semantic foreground/background/border tokens.
   - Orange is the only accent and is reserved for alert/off-target states.
   - Do not add blue links, green success, red error, purple focus, etc. unless this design system explicitly grows those tokens later.

5. **Hairline geometry**
   - Borders and divider rules are normally `1px`.
   - A `2px` border is reserved for metering/target overlays or deliberate focus-like instrumentation.

6. **Uppercase instrumentation labels**
   - Labels are short, uppercase, letter-spaced.
   - Prefer `ISO`, `EV`, `COND`, `APT`, `SHUT`, `ZONE`, `CAPTURE` over prose.

7. **Low-chrome controls**
   - Controls may be bordered, but should not look like app-store buttons.
   - Primary actions can be stark, not colorful.
   - Disabled or inactive states use opacity, not a separate color family.

## Theme model

The system supports light and dark themes, with dark preserving the original Sunny 16 high-contrast field-use look.

- Light surface: `#f5f5f4`
- Dark surface: `#000000`
- Light primary text: `#000000`
- Dark primary text: `#ffffff`

Use `.dark` or `[data-theme="dark"]` on a root element to switch CSS variables.

## Palette discipline

Bricks uses [Dim Sum](../docs/color-reference.md) as the broader color reference library, but Bricks core remains stricter than a terminal/editor theme. Product UI should use Bricks semantic tokens first; Dim Sum is consulted when expanding the palette, not when styling one-off components.

| Role | Token | Usage |
|---|---|---|
| Surface | `--bricks-color-surface` | Page/app background |
| Primary text | `--bricks-color-text-primary` | Selected values, critical readouts |
| Secondary text | `--bricks-color-text-secondary` | Labels, low-priority controls |
| Tertiary text | `--bricks-color-text-tertiary` | Metadata/version hashes |
| Muted text | `--bricks-color-text-muted` | Inactive wheel items, faint UI |
| Subtle text | `--bricks-color-text-subtle` | Supporting details |
| Alert text | `--bricks-color-text-alert` | Off-target measurement, warning, exposure mismatch |
| Hairline border | `--bricks-color-border-hairline` | Badges, secondary buttons |
| Strong border | `--bricks-color-border-strong` | Locked/active square controls |

## Typographic rhythm

- Wordmark/title: small, uppercase, wide tracking.
- Labels: extra small, uppercase, wide tracking.
- Readouts: larger, bold, tabular numbers where numeric.
- Metadata: tiny, low opacity.

Recommended CSS patterns:

```css
.bricks-wordmark {
  font-family: var(--bricks-font-family-mono);
  font-size: var(--bricks-font-size-sm);
  text-transform: uppercase;
  letter-spacing: var(--bricks-letter-spacing-wordmark);
  color: var(--bricks-color-text-secondary);
}

.bricks-readout {
  font-family: var(--bricks-font-family-mono);
  font-size: var(--bricks-font-size-xl);
  font-weight: var(--bricks-font-weight-bold);
  letter-spacing: var(--bricks-letter-spacing-readout);
  font-variant-numeric: tabular-nums;
}
```

## Layout rhythm

- Full-screen tools are centered columns.
- Outer padding: `--bricks-space-4`, adjusted for safe areas on mobile.
- Major vertical gaps: `--bricks-space-8`.
- Repeated rows: `--bricks-space-6`.
- Inline row control gaps: `--bricks-space-2`.
- Narrow tool column: `--bricks-size-container-sm` (`24rem`).

## Motion

Motion should communicate mechanical snap or state change only.

Allowed:

- `150ms` opacity transitions
- `150ms` strip/position snap transitions
- simple color transition on hover/focus

Avoid:

- bouncing/spring effects
- entrance animations
- background animation
- loading shimmer

## Accessibility expectations

- High contrast must be preserved.
- Controls require accessible names.
- Do not rely on orange alone; pair alert color with signed text or explicit label.
- Use large enough hit targets for mobile (`2rem` minimum, larger if space allows).
- Preserve `prefers-reduced-motion` when adding any optional motion.
