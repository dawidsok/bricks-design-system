# Component Guidelines

This repository defines component **visual contracts**, not component implementations. Use these guidelines to recreate the components in React, Vue, Svelte, native mobile, or plain HTML.

## Shared component rules

All components must follow:

- Monospace typography.
- Square corners.
- Hairline borders unless specified.
- Token-based color.
- No shadows, gradients, blur, or decorative animation.
- Accessible names for interactive controls.

## App Shell

A single-purpose tool should use a full-screen centered column.

### Contract

- Minimum height: full viewport.
- Background: `--bricks-color-surface`.
- Text: `--bricks-color-text-primary`.
- Layout: centered flex column.
- Section gap: `--bricks-space-8`.
- Padding: `--bricks-space-4`; use safe-area padding on mobile.
- Max content width for control stacks: `--bricks-size-container-sm`.

### CSS sketch

```css
.bricks-app-shell {
  min-height: 100svh;
  background: var(--bricks-color-surface);
  color: var(--bricks-color-text-primary);
  font-family: var(--bricks-font-family-mono);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: var(--bricks-space-8);
  padding: var(--bricks-space-4);
}
```

## Wordmark / Tool Title

A quiet uppercase title, not a marketing masthead.

### Contract

- Font size: `--bricks-font-size-sm`.
- Uppercase.
- Letter spacing: `--bricks-letter-spacing-wordmark`.
- Color: `--bricks-color-text-secondary`.
- Centered when used in the app shell.

### Example text

```text
SUNNY 16
FIELD METER
EXPOSURE LOG
```

## Readout

A permanent measurement/status line.

### Contract

- Always visible.
- Centered.
- Bold monospace.
- Tabular numeric alignment.
- Correct/neutral state uses `--bricks-color-text-primary`.
- Alert/off-target state uses `--bricks-color-text-alert`.
- Include sign or label in text; do not rely on color alone.

### Example

```text
0 EV
+1.3 EV
-0.7 EV
```

### CSS sketch

```css
.bricks-readout {
  font-size: var(--bricks-font-size-xl);
  font-weight: var(--bricks-font-weight-bold);
  letter-spacing: var(--bricks-letter-spacing-readout);
  font-variant-numeric: tabular-nums;
}

.bricks-readout[data-state="alert"] {
  color: var(--bricks-color-text-alert);
}
```

## Instrument Row

A horizontal row combining a terse label, an interactive/mechanical region, and an optional square control.

### Contract

- Display: flex row, center aligned.
- Gap: `--bricks-space-2`.
- Label width: `--bricks-size-wheel-label-width`.
- Label text: uppercase, extra small, secondary color.
- Main region stretches.
- Optional trailing control is square `--bricks-size-control`.

## Drum / Roller Guideline

A horizontal scroll strip with a fixed center selection point.

### Contract

- Track height: `--bricks-size-wheel-track-height` (`3.5rem`).
- Overflow hidden.
- Center pointer: vertical `1px` rule at 50% width using `--bricks-color-rule-center`.
- Item strip translates horizontally until selected item aligns with center pointer.
- Default item slot width: `--bricks-size-wheel-item-default` (`5rem`).
- Compact item slot width: `--bricks-size-wheel-item-compact` (`2rem`).
- Long/condition item slot width: `--bricks-size-wheel-item-condition` (`6rem`).
- Selected item opacity: `1`.
- Non-selected item opacity: `0.3`.
- Snap transition: `150ms` on release; no transition during drag.
- Touch action: `none` for the draggable track.

### Interaction contract

- Drag horizontally to move between values.
- Click/tap a non-selected item to snap to it.
- Gestures below `--bricks-interaction-drag-threshold` may be treated as click.
- Locked state: track ignores pointer input but remains visually readable.

### Accessibility contract

- If implemented as a custom control, expose a label and current value.
- Support keyboard increment/decrement where practical.
- Lock button must have an accessible `Lock` / `Unlock` name.

## Square Control Button

Used for lock, theme, install, close, capture-adjacent controls, and icon-only utility actions.

### Contract

- Width/height: `--bricks-size-control` (`2rem`).
- Border: `1px solid --bricks-color-border-muted`.
- Text/icon color: `--bricks-color-text-secondary`.
- Hover: border `--bricks-color-border-hover`, text `--bricks-color-text-subtle`.
- Active/locked state: border and text `--bricks-color-border-strong` / primary.
- No border radius.
- No filled background unless documented for a future variant.

### Allowed glyph examples

```text
🔒 🔓 ○ ● ⊕ ✕
```

Use glyphs sparingly; a text label is better when space allows.

## Text Action Button

Used for secondary actions such as switching modes.

### Contract

- Monospace, extra small.
- Uppercase.
- Wide tracking.
- Hairline border.
- Horizontal padding: `--bricks-space-4`.
- Vertical padding: `--bricks-space-2`.
- Secondary color by default.
- No accent color unless action is explicitly alert/off-target.

## Badge / Measurement Strip

A compact bordered row that communicates a captured reading or current mode.

### Contract

- Full width of the control stack.
- Border: hairline.
- Padding: `--bricks-space-4` horizontal, `--bricks-space-3` vertical.
- Layout: flex, space-between, center aligned.
- Label: uppercase, tracking, secondary/subtle text.
- Value: primary text, slightly larger or bold.
- Clear/remove action: low-contrast square/text control.

### Example

```text
METERED EV 15        [trash]
```

## Camera / Meter Frame

A rectangular preview region used for metering or visual targeting.

### Contract

- Aspect ratio: `16 / 9` by default.
- Background: black.
- Media fills frame with `object-fit: cover`.
- Center spot indicator: square overlay.
- Spot size: `--bricks-size-meter-spot`.
- Spot border: `--bricks-border-width-spot` solid white at roughly 60% opacity.
- No rounded video corners.

## Metadata Hash

Tiny fixed-position technical metadata such as a build hash.

### Contract

- Position: bottom-left.
- Font size: `--bricks-font-size-metadata`.
- Color: `--bricks-color-text-tertiary`.
- Monospace.

## Empty / Permission Message

A rare prose pattern.

### Contract

- Font size: small.
- Text color: `--bricks-color-text-subtle`.
- Center aligned if replacing primary content.
- Keep the wording direct and utilitarian.

### Example

```text
Camera permission denied. Grant camera access to use lightmeter mode.
```

## Variant policy

Do not create variants casually. A new variant must answer:

1. What existing guideline fails?
2. Which token does it use?
3. Is it required for accessibility or product meaning?
4. Does it preserve square, monochrome, instrument-panel aesthetics?

If the answer is mostly visual preference, do not add it.
