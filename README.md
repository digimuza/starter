<p align="center">
  <h1 align="center">Starter</h1>
  <p align="center">A minimal, opinionated monorepo starter kit.</p>
</p>

<p align="center">
  <strong>pnpm workspaces</strong> &nbsp;&bull;&nbsp; <strong>Biome</strong> &nbsp;&bull;&nbsp; <strong>TypeScript</strong>
</p>

---

## Structure

```
├── apps/          # Deployable applications
├── libs/          # Shared libraries and packages
├── biome.json     # Linting, formatting & import sorting
└── package.json   # Root scripts and shared dev dependencies
```

| Directory | Purpose |
|-----------|---------|
| `apps/*`  | Each sub-folder is a standalone, deployable application |
| `libs/*`  | Shared code consumed by apps (utilities, configs, UI kits, etc.) |

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) v22+
- [pnpm](https://pnpm.io/) v10+

### Install

```bash
pnpm install
```

### Develop

```bash
pnpm dev          # Run all apps in parallel
```

### Build

```bash
pnpm build        # Build all apps
```

### Lint & Format

```bash
pnpm lint         # Check for issues
pnpm format       # Auto-fix and format
```

### Type Check

```bash
pnpm typecheck    # Run tsc --noEmit across all packages
```

## Adding a New App

```bash
mkdir apps/my-app
cd apps/my-app
pnpm init
```

Then add your framework of choice and start building.

## Adding a Shared Library

```bash
mkdir libs/my-lib
cd libs/my-lib
pnpm init
```

Name it with a scope (e.g. `@starter/my-lib`) and reference it from any app:

```bash
pnpm --filter my-app add @starter/my-lib --workspace
```

## Tooling

### Biome

This repo uses [Biome](https://biomejs.dev/) for linting, formatting, and import sorting — no Prettier or ESLint needed.

Key config choices:
- **Tabs** for indentation
- **Double quotes** for strings
- **Auto-sorted** imports, object keys, interface members, and Tailwind classes
- **Cognitive complexity** capped at 25

VS Code will auto-format on save with the included `.vscode/settings.json`.

## License

MIT
