# Extraction Notes

This design system was extracted from the Sunny 16 film photography exposure calculator.

## Source material

Primary source files in the original app:

- `style.md` — original app-specific style guidelines.
- `src/App.tsx` — page shell, theme toggle, install control, mode switch.
- `src/components/DrumWheel.tsx` — instrument row, horizontal drum, lock control.
- `src/components/EVDisplay.tsx` — numeric EV readout and alert color usage.
- `src/components/LightMeter.tsx` — camera frame, target overlay, capture action.
- `src/components/MeteredBadge.tsx` — captured reading badge.
- `docs/superpowers/specs/*` — feature design specs and rationale.

## Important changes during extraction

### From app-specific to reusable

The original Sunny 16 styles referenced photography labels and exposure-specific behavior. This repository keeps the reusable visual language and moves domain behavior out of scope.

Examples:

| Sunny 16 app | Design-system abstraction |
|---|---|
| EV display | Readout |
| Condition/aperture/shutter/ISO wheel | Drum / Roller |
| Lock button | Square Control Button |
| Metered EV row | Badge / Measurement Strip |
| Lightmeter video | Camera / Meter Frame |
| Build hash | Metadata Hash |

### From Tailwind literals to semantic tokens

The app uses Tailwind utilities such as:

```text
bg-stone-100 dark:bg-black
text-black dark:text-white
text-black/40 dark:text-white/40
border-black/30 dark:border-white/30
text-orange-500 dark:text-orange-400
```

The design system maps these into semantic CSS variables:

```text
--bricks-color-surface
--bricks-color-text-primary
--bricks-color-text-secondary
--bricks-color-border-muted
--bricks-color-text-alert
```

### Dark-first heritage, light-compatible tokens

The first Sunny 16 style guide was dark-only: black background, white text, orange alert. The app later gained a light theme. This design system preserves both:

- dark mode as the canonical field/instrument look
- light mode as a tokenized counterpart for apps that need system theme support

### Component implementation deferred

The design system intentionally does not ship React components yet. Component behavior in Sunny 16 is app-specific and should not leak into downstream apps. Each component is documented as a visual contract in `guidelines/components.md`.

## Original value references

| Role | Original value | Token |
|---|---|---|
| Dark background | `#000000` / `bg-black` | `--bricks-color-surface` in dark |
| Light background | `#f5f5f4` / `bg-stone-100` | `--bricks-color-surface` in light |
| Dark primary text | `#ffffff` / `text-white` | `--bricks-color-text-primary` in dark |
| Light primary text | `#000000` / `text-black` | `--bricks-color-text-primary` in light |
| Secondary text | 40% foreground | `--bricks-color-text-secondary` |
| Tertiary text | 20% foreground | `--bricks-color-text-tertiary` |
| Muted/inactive | 30% foreground | `--bricks-color-text-muted`, `--bricks-opacity-inactive` |
| Alert dark | Tailwind `orange-400` / `#fb923c` | `--bricks-color-text-alert` in dark |
| Alert light | Tailwind `orange-500` / `#f97316` | `--bricks-color-text-alert` in light |
| Track height | `h-14` / `56px` | `--bricks-size-wheel-track-height` |
| Control size | `w-8 h-8` / `32px` | `--bricks-size-control` |
| Label width | `w-10` / `40px` | `--bricks-size-wheel-label-width` |
| Max stack width | `max-w-sm` / `24rem` | `--bricks-size-container-sm` |
| Snap duration | `150ms` | `--bricks-motion-duration-fast` |
| Drag threshold | `5px` | `--bricks-interaction-drag-threshold` |

## Open questions for future versions

- Should this become an npm package with generated outputs?
- Should tokens be generated from JSON into CSS automatically?
- Should component examples be framework-specific or stay platform-neutral?
- Should focus-ring tokens be added for stronger keyboard accessibility guidance?
- Should non-orange semantic states exist, or should the system stay strict monochrome + alert?
