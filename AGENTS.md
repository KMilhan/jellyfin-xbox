# Repository Guidelines

## Project Structure & Module Organization
- Solution entrypoint: `JellyfinUwp.sln` with the UWP client project `Jellyfin/Jellyfin.csproj`.
- App code and resources live under `Jellyfin/`:
  - Core services and utilities: `Core/`, `Helpers/`, `Utils/`.
  - UI layers: `Views/`, `ViewModels/`, `Controls/`, `Behaviors/`, and XAML assets in `Resources/`, `Assets/`, `Fonts/`.
  - Packaging and platform metadata: `Package.appxmanifest`, `Package.StoreAssociation.xml`, and `Jellyfin_TemporaryKey.pfx`.
- Shared configuration: `Directory.Packages.props`, `stylecop.json`, `BannedSymbols.txt`, and `JellyfinUwp.sln`.

## Build, Test, and Development Commands
- Restore dependencies: `dotnet restore JellyfinUwp.sln`.
- Build on Windows with the UWP workload installed (Visual Studio 2022 recommended):
  - Debug: `dotnet build JellyfinUwp.sln -c Debug -p:Platform=x64`.
  - Release bundle: `dotnet msbuild JellyfinUwp.sln /p:Configuration=Release /p:Platform=x64 /p:AppxBundle=Always`.
- Static analysis runs via the included analyzers (StyleCop, Banned API, Serilog, multithreading analyzers). Treat warnings as actionable and avoid suppressions unless justified in code comments.
- Tests are currently absent. If you add test projects, run `dotnet test` before committing and document new commands in this file.

## Coding Style & Naming Conventions
- C#: 4-space indentation; `PascalCase` for public/protected members and classes; `camelCase` for locals/parameters; prefix private fields with `_`.
- Favor expression-bodied members for short properties/methods; keep methods focused and small.
- XAML: indent with 2 spaces; prefer attribute ordering that groups layout, visuals, behavior; avoid inline code-behind unless necessary.
- Logging: use `ILogger` with structured messages; avoid string interpolation in log templates.
- Imports: sort and remove unused `using` directives; never wrap imports in try/catch.

## Commit & Pull Request Guidelines
- Commit messages must start with a colon-coded gitmoji (no Unicode emoji), followed by an imperative subject without redundant tags (e.g., `:memo: add contributing agent file`). Keep the tone meaningful and professional.
- Keep commits atomic per logical change, and include a brief body describing the why/what when the change is non-trivial.
- Branch names should be in en-us.
- Pull requests need witty yet informative English titles plus a body summarizing changes, linked issues, and any commands run (build/analysis/tests). Mention notable tooling requirements when relevant.

## Security & Configuration
- Do not commit secrets or real certificates. The included temporary signing key is for development only.
- Platform builds assume Windows 10/11 SDK availability; document deviations if you rely on alternative SDK versions or build tools.
