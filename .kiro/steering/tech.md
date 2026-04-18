# Tech Stack

## Language & Runtime

- TypeScript 6.x (strict mode, `experimentalDecorators` + `emitDecoratorMetadata` enabled)
- Node.js >= 18
- ESM-first (`"type": "module"` in package.json)
- Target: ES2020

## Dependencies

- `reflect-metadata` — runtime reflection for decorator metadata (`design:paramtypes`)
- `@vivtel/metadata` — typed wrapper around `Reflect.defineMetadata` / `Reflect.getMetadata`
- `react` (optional peer dependency, ^18 || ^19) — only needed for React bindings

## Build

- **Bundler**: tsup (via `@nesvel/tsup-config` base preset)
- **Output**: dual format — ESM (`.js`) + CJS (`.cjs`) with `.d.ts` declarations
- **Package manager**: pnpm 10.x

## Testing

- **Runner**: Vitest 4.x with `globals: true`
- **Environment**: jsdom (for React hook/component tests)
- **Setup file**: `__tests__/vitest.setup.ts` — mocks DI decorators so tests run without the full IoC container
- **Test location**: `__tests__/**/*.{test,spec}.{ts,tsx}`
- **Coverage**: v8 provider, reports in text/json/html

## Linting & Formatting

- **ESLint**: typescript-eslint flat config. `@typescript-eslint/no-explicit-any` and `no-non-null-assertion` are intentionally off (reflection-based DI requires `any`). Consistent type imports enforced (`prefer: type-imports`, `fixStyle: inline-type-imports`).
- **Prettier**: extends `@nesvel/prettier-config` (single quotes, trailing commas ES5, 100 char width, 2-space indent, semicolons, LF)

## Path Aliases

- `@/*` → `./src/*` (configured in tsconfig and vitest)

## Common Commands

| Command | Purpose |
|---|---|
| `pnpm build` | Production build via tsup |
| `pnpm test` | Run tests once (`vitest run --passWithNoTests`) |
| `pnpm test:watch` | Run tests in watch mode |
| `pnpm test:coverage` | Run tests with v8 coverage |
| `pnpm typecheck` | Type-check without emitting (`tsc --noEmit`) |
| `pnpm lint` | Lint with zero warnings allowed |
| `pnpm lint:fix` | Lint and auto-fix |
| `pnpm format` | Format all files with Prettier |
| `pnpm format:check` | Check formatting without writing |
| `pnpm clean` | Remove `dist/` |
