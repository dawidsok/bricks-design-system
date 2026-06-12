# Contributing

Thanks for improving Sunny 16 Design System.

## Scope

This project is currently token- and guideline-first. Good contributions include:

- clearer design-token names
- improved CSS variable coverage
- component visual contracts
- accessibility improvements that preserve the brutalist style
- examples that use existing tokens

Out of scope unless discussed first:

- framework component packages
- broad color palettes
- rounded or soft visual variants
- decorative animation systems

## Local checks

Validate token JSON:

```sh
python3 -m json.tool tokens/sunny-brutalist.tokens.json >/dev/null
```

Search for forbidden styling drift before opening a PR:

```sh
grep -RniE "rounded|shadow|gradient|blur|font-sans|font-serif|text-blue|text-green|text-purple" . \
  --exclude-dir=.git
```

Some occurrences are allowed in documentation when listed as forbidden examples.

## Commit messages

Use short imperative messages:

```text
Add alert color token
Document badge visual contract
```

## License

By contributing, you agree that your contribution is licensed under the MIT License.
