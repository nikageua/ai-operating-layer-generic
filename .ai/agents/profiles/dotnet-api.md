# Profile: dotnet-api

## Status
draft

## Target Environment
- Repository: [fill in repo name]
- Language: C# (12+)
- Framework: .NET 8+ (ASP.NET Core Web API)
- Package manager: dotnet CLI / NuGet

## Required Tools / Skills
- .NET SDK 8+: build, test, publish
- dotnet CLI: primary tool for all operations
- xUnit or NUnit: test runner (check .csproj to confirm)
- dotnet-format or Roslyn analyzers: code style
- Bash: bootstrap and validation scripts

## Bootstrap Command
```bash
dotnet restore
```

## Validate Command
```bash
dotnet build --no-restore --configuration Release
```

## Test Command
```bash
dotnet test --no-build --configuration Release --logger "console;verbosity=normal"
```

## Build Command
```bash
dotnet publish --configuration Release --no-restore
```

## Key Instructions For Sub-Agent
- Read the solution `.sln` file first to understand project structure before touching any `.csproj`.
- Follow existing namespace conventions exactly — do not invent new namespaces.
- Use dependency injection everywhere. Do not use static service locators.
- Controller actions must be thin. Business logic belongs in services.
- Always add XML doc comments to new public API surface.
- Do not add NuGet packages without declaring them in the task scope.

## Known Pitfalls
- `dotnet restore` may fail in air-gapped environments. Check for a local NuGet feed config.
- Entity Framework migrations must not be auto-applied in code. Use explicit migration commands.
- Nullable reference types are likely enabled. Handle nullability explicitly.
- `appsettings.json` vs `appsettings.Development.json` — never commit secrets to either.
- Minimal API vs. controller-based routing — match what the project already uses.

## Metaharness Optimization History
- initial — draft created from bootstrap template
