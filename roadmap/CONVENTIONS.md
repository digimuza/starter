# Project Conventions

Rules the AI must follow when executing sprints. These are non-negotiable.

---

## Monorepo Structure

```
starter/
├── apps/           # Deployable applications
│   └── web/        # Next.js app
├── libs/           # Shared libraries and configs
│   ├── shared/     # Shared utilities and types
│   └── tsconfig/   # Shared TypeScript configs
├── roadmap/        # Sprint planning and tracking
├── biome.json      # Linter and formatter config
└── package.json    # Root workspace config
```

## Package Manager

- Use `pnpm`. Never use `npm` or `yarn`.
- Workspace protocol for internal deps: `"@starter/shared": "workspace:*"`

## Code Style

- Formatting and linting: Biome (`pnpm lint`, `pnpm format`).
- No ESLint, no Prettier. Biome handles both.
- Run `pnpm lint` before marking any task complete.

## TypeScript

- Strict mode everywhere.
- Run `pnpm typecheck` before marking any task complete.
- Shared configs live in `libs/tsconfig/`.

## Testing

- Vitest for all tests.
- Run `pnpm test` before marking any task complete.

## Secrets

- Infisical for secrets management.
- Never hardcode secrets. Use environment variables.
- `.infisical.json` at root for project binding.

## Git

- Each sprint produces exactly one pull request.
- Branch naming: `sprint/S001-short-name`
- Commit messages: conventional commits (`feat:`, `fix:`, `chore:`, `docs:`, `test:`, `refactor:`).
- Keep commits atomic — one logical change per commit.

## File Naming

- TypeScript files: `camelCase.ts` or `kebab-case.ts` (follow existing pattern in directory).
- React components: `PascalCase.tsx`.
- Config files: lowercase with dots (`drizzle.config.ts`, `vitest.config.ts`).

## Imports

- Use path aliases when available.
- Barrel exports (`index.ts`) for public API of each package.
- Internal implementation files should not be imported directly from outside the package.
