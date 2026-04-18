# Project Structure

## Top-Level Layout

```
src/                  — Library source code
__tests__/            — All test files (*.test.ts, *.spec.ts, *.test.tsx, *.spec.tsx)
config/               — Application bootstrap configuration (container.config.ts)
dist/                 — Build output (generated, not committed)
.examples/            — Usage examples (basic-di, dynamic-modules, react-integration)
```

## Source Organization (`src/`)

The source is organized by concern, with each folder containing an `index.ts` barrel export.

```
src/
├── index.ts                — Main entry point, re-exports everything
├── application/            — Application bootstrap and global singleton
│   ├── application.ts      — Application.create() factory, get/has/select/close API
│   └── global.application.ts — Global app singleton (set/get/has/clear)
├── constants/              — Metadata keys used by decorators and the injector
│   └── tokens.constant.ts  — MODULE_METADATA, INJECTABLE_WATERMARK, PARAMTYPES_METADATA, etc.
├── contexts/               — React contexts
│   └── container.context.ts — ContainerContext for React provider
├── decorators/             — All decorators
│   ├── injectable.decorator.ts — @Injectable()
│   ├── inject.decorator.ts     — @Inject() (constructor + property)
│   ├── optional.decorator.ts   — @Optional()
│   ├── module.decorator.ts     — @Module()
│   └── global.decorator.ts     — @Global()
├── enums/                  — Enumerations
│   └── scope.enum.ts       — Scope.DEFAULT, Scope.TRANSIENT
├── hooks/                  — React hooks (each in its own subfolder)
│   ├── use-inject/         — useInject()
│   ├── use-optional-inject/ — useOptionalInject()
│   └── use-container/      — useContainer()
├── injector/               — Core DI engine
│   ├── container.ts        — ModuleContainer (top-level module registry)
│   ├── scanner.ts          — DependenciesScanner (module tree traversal)
│   ├── injector.ts         — Injector (dependency resolution)
│   ├── instance-loader.ts  — InstanceLoader (instantiation + lifecycle hooks)
│   ├── instance-wrapper.ts — InstanceWrapper (provider binding metadata)
│   ├── module.ts           — Module (runtime module representation)
│   └── registry-scanner.ts — RegistryScanner (compile-time alternative)
├── interfaces/             — All TypeScript interfaces and type aliases
│   └── index.ts            — Barrel export of all interfaces
├── providers/              — React provider components
│   └── container.provider.tsx — <ContainerProvider>
└── utils/                  — Utility functions
    ├── forward-ref.util.ts — forwardRef()
    └── define-config.util.ts — defineConfig() helper for typed app options
```

## Conventions

- Each domain folder has an `index.ts` barrel file that re-exports its public API.
- React hooks each live in their own subfolder (`use-inject/use-inject.hook.ts`).
- Interfaces are type-only exports (`export type { ... }`).
- The main `src/index.ts` is the single public API surface — it groups exports by category (decorators, interfaces, enums, utilities, application, DI engine, React bindings, constants).
- React-specific code (hooks, providers, contexts) is separated from the core DI engine so the `/react` export entry point can be tree-shaken independently.
- Tests go in `__tests__/`, not alongside source files.
- Examples go in `.examples/` and are excluded from the build and lint.

## DI Engine Data Flow

```
Application.create(RootModule)
  → DependenciesScanner.scan()     — builds module graph in ModuleContainer
  → InstanceLoader.createInstances() — resolves providers via Injector, runs lifecycle hooks
  → Application instance             — exposes get/has/select/close
```
