# @starter/tsconfig

Shared TypeScript configurations for the monorepo.

## Configs

| File                  | Use case                |
| --------------------- | ----------------------- |
| `base.json`           | Base strict config      |
| `library.json`        | TypeScript libraries    |
| `react-library.json`  | React component libs    |
| `nextjs.json`         | Next.js applications    |

## Usage

In your package's `tsconfig.json`:

```json
{
  "extends": "@starter/tsconfig/library.json"
}
```
