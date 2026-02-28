<p align="center">
  <h1 align="center">Starter</h1>
  <p align="center">A minimal, opinionated monorepo starter kit.</p>
</p>

<p align="center">
  <strong>pnpm workspaces</strong> &bull; <strong>Biome</strong> &bull; <strong>TypeScript</strong> &bull; <strong>Vitest</strong>
</p>

---

## Structure

```
├── apps/
│   └── web/               # Next.js 15 application
├── libs/
│   ├── shared/            # Shared utility library
│   └── tsconfig/          # Shared TypeScript configurations
├── roadmap/               # Project roadmap
├── biome.json             # Linting, formatting & import sorting
├── vitest.config.ts       # Root test configuration
└── package.json           # Root scripts and shared dev dependencies
```

| Directory          | Purpose                                          |
| ------------------ | ------------------------------------------------ |
| `apps/web`         | Next.js 15 app with App Router                   |
| `libs/shared`      | Shared utilities consumed by apps                |
| `libs/tsconfig`    | Shared TypeScript configs (base, lib, Next.js)   |

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

### Test

```bash
pnpm test         # Run all tests
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

### Vitest

Testing is configured with [Vitest](https://vitest.dev/). Each testable package has its own `vitest.config.ts` that extends the root config.

## License

MIT
