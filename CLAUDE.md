# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Structure

Excalidraw is a **monorepo** with a clear separation between the core library and the application:

- **`packages/excalidraw/`** - Main React component library published to npm as `@excalidraw/excalidraw`
- **`excalidraw-app/`** - Full-featured web application (excalidraw.com) that uses the library
- **`packages/common/`** - Shared utilities and constants
- **`packages/element/`** - Element-related types and utilities
- **`packages/math/`** - Mathematical utilities and types (Point, Radians, Degrees, etc.)
- **`packages/utils/`** - General-purpose utilities
- **`examples/`** - Integration examples (NextJS, browser script)

## Development Commands

### Testing
```bash
yarn test:app           # Run tests with Vitest (watch mode)
yarn test:app --watch=false  # Run tests once
yarn test:update        # Run tests and update snapshots
yarn test:typecheck     # TypeScript type checking
yarn test:code          # Run ESLint
yarn test:other         # Check Prettier formatting
yarn test:all           # Run all tests (typecheck + code + other + app)
yarn test:coverage      # Run tests with coverage report
yarn test:ui            # Run tests with UI dashboard
```

### Development
```bash
yarn start              # Start dev server (runs excalidraw-app)
yarn start:production   # Build and serve production build
yarn start:example      # Build packages and run example app
```

### Building
```bash
yarn build              # Build the app
yarn build:packages     # Build all packages (common, math, element, excalidraw)
yarn build:app          # Build just the app
yarn build:preview      # Build and preview the app
```

### Code Quality
```bash
yarn fix                # Auto-fix Prettier and ESLint issues
yarn fix:code           # Auto-fix ESLint issues only
yarn fix:other          # Auto-fix Prettier formatting only
```

## Development Workflow

1. **Package Development**: Work in `packages/*` for core editor features
2. **App Development**: Work in `excalidraw-app/` for app-specific features (collaboration, PWA, etc.)
3. **Testing**: Always run `yarn test:update` before committing
4. **After Modifications**: Run `yarn test:app` and fix any failing tests

## Architecture Notes

### Package System
- Uses Yarn workspaces for monorepo management
- Internal packages use path aliases defined in `vitest.config.mts`
- Packages reference each other via `@excalidraw/package-name` imports
- Build system uses esbuild for packages, Vite for the app
- TypeScript with strict configuration throughout

### State Management
- Uses Jotai for state management (see `editor-jotai.ts`)
- State stored in `editorJotaiStore`

### Component Architecture
- Functional components with React hooks
- Main entry point: `packages/excalidraw/index.tsx`
- Core app component: `packages/excalidraw/components/App.tsx`
- CSS modules for component styling

## Coding Standards

### TypeScript
- Use TypeScript for all code
- Prefer implementations without allocation where possible
- Prefer performant solutions, trade RAM for CPU cycles
- Use immutable data (const, readonly)
- Use optional chaining (?.) and nullish coalescing (??)

### React
- Use functional components with hooks
- Follow React hooks rules (no conditional hooks)
- Keep components small and focused
- Use CSS modules for styling

### Naming
- PascalCase for component names, interfaces, and type aliases
- camelCase for variables, functions, and methods
- ALL_CAPS for constants

### Math Types
- Always use the Point type from `packages/math/src/types.ts` instead of `{ x, y }`
- Use Radians and Degrees types for angle measurements

### Communication
- Be succinct in responses
- Prefer code over explanations unless asked
- No need to summarize changes unless requested
