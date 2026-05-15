# @dcrgll/lint

Pinned Biome and Ultracite presets for dcrgll projects.

The goal is to install one lint package and choose the closest preset instead of starting from a generic base and patching it locally.

## Installation

```sh
npm install --save-dev @dcrgll/lint
```

## Presets

- `@dcrgll/lint/core` for Node or non-React TypeScript packages
- `@dcrgll/lint/react` for React packages
- `@dcrgll/lint/next` for Next.js apps

`core` contains the shared formatting and lint choices: tabs, 100-character lines, single quotes, semicolons as needed, no trailing commas, sorted attributes/properties/keys, the project import groups, and `a11y.useKeyWithClickEvents` as an error.

`react` and `next` are framework layers. Use them with the earlier layers rather than by themselves.

## Usage

Node or non-React TypeScript package:

```json
{
  "$schema": "https://biomejs.dev/schemas/2.4.15/schema.json",
  "extends": ["@dcrgll/lint/core"],
  "root": true
}
```

React package:

```json
{
  "$schema": "https://biomejs.dev/schemas/2.4.15/schema.json",
  "extends": ["@dcrgll/lint/core", "@dcrgll/lint/react"],
  "root": true
}
```

Next.js app:

```json
{
  "$schema": "https://biomejs.dev/schemas/2.4.15/schema.json",
  "extends": [
    "@dcrgll/lint/core",
    "@dcrgll/lint/react",
    "@dcrgll/lint/next"
  ],
  "root": true
}
```

## Scripts

Add scripts like these to consuming projects:

```json
{
  "scripts": {
    "lint": "biome check .",
    "lint:fix": "biome check --write ."
  }
}
```

## Commits

This repo uses Conventional Commits so releases can infer the next version.

Use the guided commit prompt:

```sh
npm run commit
```

Commit messages and PR titles must use the same format:

```text
feat: add next preset
fix: adjust import groups
docs: update usage
```

## Publishing

This package is configured for public npm publishing:

```sh
npm publish --access public
```
