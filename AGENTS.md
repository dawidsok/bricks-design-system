# Repository Guidelines

## Critical styling rules

- Read `guidelines/agent-styling.md` before changing UI guidance or examples.
- Use tokens from `tokens/sunny-brutalist.tokens.json` and `styles/tokens.css`; do not invent component-local colors.
- Preserve the brutalist contract: monospace only, square corners, hairline borders, no shadows, no gradients, no blur.
- Orange is reserved for alert/off-target states only.
- Components are guidelines/specs first. Do not add framework-specific component implementations unless explicitly requested.

## Project structure

- `tokens/` — canonical design-token source.
- `styles/` — CSS-variable and Tailwind-facing token files.
- `guidelines/` — human/agent rules and component visual contracts.
- `docs/` — rationale and extraction notes.
- `examples/` — tiny examples that demonstrate token usage.

## Validation

This repo currently has no build step. Before finishing changes:

```sh
python3 -m json.tool tokens/sunny-brutalist.tokens.json >/dev/null
```

Also manually scan examples/guidelines for forbidden styles:

```text
rounded, shadow, gradient, blur, font-sans, font-serif, text-blue, text-green, text-purple
```

## Commit style

Use short imperative commit messages, for example:

```text
Add initial Sunny Brutalist tokens
Document drum wheel visual contract
```

## Ownership

Author identity for this repo:

- Dawid Sokół
- dave@okhy.pl
- https://github.com/dawidsok
