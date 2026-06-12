# Color Reference: Dim Sum

Bricks uses [Dim Sum](https://github.com/dawidsok/dim-sum-theme) as its color reference library.

This does **not** mean Bricks imports every Dim Sum color into product UI. Bricks remains a strict, brutalist, instrument-panel system: monochrome surfaces, monospace type, square geometry, and very limited accent use.

Dim Sum provides the broader color vocabulary and mood reference for future Bricks palette work.

## Relationship

| System | Role |
|---|---|
| Bricks | Product/UI design-system tokens, component styling rules, agent guidance |
| Dim Sum | Reference palette family for color taste, warmth, neutral ramps, and optional future variants |

## Current Bricks color stance

Bricks core tokens are intentionally stricter than Dim Sum:

- Core dark surface is pure black: `#000000`.
- Core dark text is pure white: `#ffffff`.
- Core light surface is stone/paper-like: `#f5f5f4`.
- Orange remains the only accent and is reserved for alert/off-target states.

This keeps Bricks suitable for field tools, meters, calculators, dashboards, and other high-legibility interfaces.

## Dim Sum variants to reference

When expanding Bricks color tokens, use these Dim Sum variants as references:

| Need | Dim Sum reference | Why |
|---|---|---|
| Strict dark monochrome | `dim-sum-mono` | Greyscale dark UI ramp without hue noise |
| Warm dark neutrals | `dim-sum` | Calm, barely warm dark surfaces |
| Light paper surface | `dim-sum-paper` | Soft off-white paper background and ink foreground |
| Warmer alert/accent direction | `dim-sum-sunset` or default `dim-sum` orange | Muted warmth instead of saturated app colors |
| Experimental atmospheric variant | `dim-sum-wave` | Ink/wave mood, only for future opt-in themes |

## Reference values

These are Dim Sum values that may inform future Bricks tokens. They are **not** all active Bricks tokens today.

### Dim Sum Mono

From `dawidsok/dim-sum-theme/scheme/dim-sum-mono.json`:

| Role | Value |
|---|---|
| `bg` | `#0f0f0f` |
| `bg1` | `#181818` |
| `bg2` | `#222222` |
| `bg3` | `#2e2e2e` |
| `dim` | `#5e5e5e` |
| `mid` | `#8a8a8a` |
| `fg` | `#d0d0d0` |
| `white` | `#f2f2f2` |

### Dim Sum Paper

From `dawidsok/dim-sum-theme/scheme/dim-sum-paper.json`:

| Role | Value |
|---|---|
| `bg` | `#f7f6f1` |
| `bg1` | `#efede7` |
| `bg2` | `#e6e2d9` |
| `bg3` | `#d8d3c8` |
| `dim` | `#a09a8f` |
| `mid` | `#767168` |
| `fg` | `#4b4740` |
| `white` | `#24231f` |

### Dim Sum default orange

From `dawidsok/dim-sum-theme/scheme/dim-sum.json`:

| Role | Value |
|---|---|
| `orange` | `#b77a4a` |
| `brightYellow` | `#c4a55a` |
| `red` | `#a85f59` |

Bricks currently uses a stronger Tailwind-derived orange for exposure/alert legibility. If Bricks adds a softer theme later, Dim Sum orange should be the first accent candidate.

## Rules for agents

When asked to add colors to Bricks or a Bricks-styled app:

1. Check this document first.
2. Prefer existing Bricks semantic tokens.
3. If a new color is required, look for a Dim Sum reference value before inventing one.
4. Add the color as a semantic Bricks token; do not paste raw Dim Sum colors into components.
5. Preserve Bricks meaning: orange/accent is still alert/off-target unless a documented variant says otherwise.

## Dependency policy

Bricks does not depend on Dim Sum at runtime. The reference is conceptual and documented, not an import chain.

If generated color syncing is introduced later, it should be opt-in and preserve committed CSS outputs for downstream stability.
