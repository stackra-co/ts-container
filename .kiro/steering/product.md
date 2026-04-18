# Product Overview

`@stackra/ts-container` is a NestJS-style IoC container and dependency injection library for TypeScript and React. It is built from scratch with no dependency on Inversify or other DI frameworks.

## Purpose

Provide a familiar NestJS-like DI experience for client-side applications, including React apps. The library handles module registration, provider resolution, lifecycle hooks, and React integration via context and hooks.

## Key Capabilities

- Decorator-based DI: `@Injectable()`, `@Inject()`, `@Optional()`, `@Module()`, `@Global()`
- Four provider types: class, value, factory, existing (alias)
- Module system with imports, exports, and dynamic modules (`forRoot`/`forFeature`)
- Singleton and transient scopes
- Lifecycle hooks: `OnModuleInit`, `OnModuleDestroy`, `OnApplicationBootstrap`, `OnApplicationShutdown`, `BeforeApplicationShutdown`
- `forwardRef()` for circular dependency resolution
- React bindings: `ContainerProvider`, `useInject`, `useOptionalInject`, `useContainer`
- `RegistryScanner` as a compile-time alternative to runtime reflection
- Application bootstrap via `Application.create()` with config injection (`APP_CONFIG`)

## Target Users

TypeScript and React developers who want structured dependency injection without a backend framework.

## Package Exports

- `@stackra/ts-container` — core DI engine, decorators, application, interfaces, constants
- `@stackra/ts-container/react` — React-specific bindings (ContainerProvider, hooks)
