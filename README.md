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

Commit messages should use the same format:

```text
feat: add next preset
fix: adjust import groups
docs: update usage
```

## Publishing

This package is configured as a two-step release:

1. `release.yml` runs `release-it` on `main` to create the version commit, tag, changelog, and GitHub release.
2. `publish.yml` runs after the release workflow completes, checks out the release tag, and publishes that exact package version to npm using Trusted Publishing.

On npmjs.com, configure the package trusted publisher with:

- Publisher: GitHub Actions
- Organization or user: `dcrgll`
- Repository: `lint`
- Workflow filename: `publish.yml`

The release workflow uses GitHub OIDC, so it does not need an `NPM_TOKEN` secret and will not prompt for a one-time password.

If CI fails with `ENEEDAUTH`, npm is not matching the workflow to the trusted publisher. Check that the npm package settings exactly match the repository and workflow filename above, including the `.yml` extension.

If a release exists but was not published, run the `Publish` workflow manually and provide the release tag, for example `v0.2.0`.
