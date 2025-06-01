# AppTemplate AGENT Configuration (.NET 6)

## Environment
- Use .NET 6 SDK.
- Load environment variables from `.env.ci` (if present) before any commands.
- Restore NuGet packages via `dotnet restore`.

## Formatting & Style
- Run `dotnet format --verify-no-changes`; if formatting issues are found, run `dotnet format` to fix.
- Enforce StyleCop rules: ensure no warnings or errors after `dotnet build`.
- Fail if any StyleCop or formatter violations remain.

## Testing & Coverage
- Run `dotnet test --no-restore --verbosity minimal --logger "console;verbosity=normal"`.
- Include code coverage: e.g. `dotnet test --no-restore --collect:"XPlat Code Coverage"`.
- Fail if any test fails.
- Enforce a minimum coverage threshold of 80% on new or modified code.

## Commit Message Conventions
- Use Conventional Commits:
- `feat(scope): short description`
- `fix(scope): short description`
- `chore(scope): short description`
- If a change is non-trivial, include a body explaining **why** and **what**.
- Reference issue or ticket numbers in parentheses at the end, e.g.: feat(authentication): add JWT refresh endpoint (#123).

## Build & Deployment
- After tests pass, build in Release mode: `dotnet build --configuration Release`.
- Publish artifacts for deployment: `dotnet publish --configuration Release --output ./artifacts`.
- If running in CI, package artifacts and push to the staging server.
- Abort automation if build or publish fails.

## Documentation
- Update `README.md` for any new features or breaking changes.
- Add XML documentation comments for all publicly exported classes and methods.
- Regenerate API docs via: `dotnet tool run docfx build docfx.json`


## Sample Workflow
1. **Create/Update Code**  
 - Ensure `.csproj` files are updated when adding/removing dependencies.
2. **Format & Lint**  
 - `dotnet format --verify-no-changes` → if it fails, run `dotnet format`.
 - `dotnet build` → must pass without StyleCop warnings.
3. **Run Tests**  
 - `dotnet test --no-build --collect:"XPlat Code Coverage"`.
 - Verify coverage ≥ 80%; fail otherwise.
4. **Commit**  
 - Craft a Conventional Commit message (e.g., `fix(api): correct null-reference in UserController`).
5. **Build & Publish**  
 - `dotnet build --configuration Release`
 - `dotnet publish --configuration Release --output ./artifacts`

*Note:* Codex will merge any `AGENTS.md` in `~/.codex/AGENTS.md`, the repo root, and the current folder (in that order). Use `--no-project-doc` to skip loading this file if needed.  
