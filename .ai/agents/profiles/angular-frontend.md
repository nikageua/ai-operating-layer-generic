# Profile: angular-frontend

## Status
draft

## Target Environment
- Repository: [fill in repo name]
- Language: TypeScript (5.x)
- Framework: Angular (17+)
- Package manager: npm or pnpm

## Required Tools / Skills
- Node.js 20+: runtime
- Angular CLI: `ng` commands for generate, build, test
- Jest or Karma: test runner (check angular.json to confirm)
- ESLint + Prettier: linting and formatting
- Bash: bootstrap and validation scripts

## Bootstrap Command
```bash
npm ci
```

## Validate Command
```bash
npx ng build --configuration production --dry-run 2>/dev/null || npx ng build --configuration production
```

## Test Command
```bash
npx ng test --watch=false --browsers=ChromeHeadless
```

## Build Command
```bash
npx ng build --configuration production
```

## Key Instructions For Sub-Agent
- Always check `angular.json` before creating or modifying components to confirm
  project structure, prefixes, and style format (scss/css).
- Use `ng generate` for new components, services, pipes, and guards — do not create
  files manually unless absolutely necessary.
- Keep components small and single-responsibility. Prefer smart/dumb component split.
- Do not modify `angular.json` or `tsconfig*.json` unless the task explicitly requires it.
- After changes, confirm `ng build` still exits 0 before marking task done.

## Known Pitfalls
- Standalone components (Angular 17+) behave differently from module-based ones.
  Inspect existing components to determine which pattern the project uses.
- Change detection strategy matters for performance. Match existing components.
- Angular Material imports must be explicit — do not import the whole module.
- Zone.js vs. zoneless differs by project version. Do not assume.

## Metaharness Optimization History
- initial — draft created from bootstrap template
