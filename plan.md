# .NET Upgrade Plan: .NET 9.0 → .NET 10.0

## Upgrade Strategy

**Approach**: Bottom-up — upgrade leaf dependencies first, then work up the project dependency graph.  
**Branch**: `upgrade-to-NET10` (from `main`)  
**Risk**: 🟢 Low  

---

## Execution Order

### Phase 1: Infrastructure Files
Update SDK pinning, central package versions, and container images before touching any project files.

| Step | File | Change | Risk |
|------|------|--------|------|
| 1.1 | `global.json` | Update SDK version from `9.0.306` to `10.0.100` | 🟢 Low |
| 1.2 | `Directory.Packages.props` | Update all Microsoft 9.0.x package versions to 10.0.x | 🟢 Low |
| 1.3 | `Directory.Packages.props` | Update EF Core ecosystem packages (`Npgsql`, `Pomelo`) to 10.0.x | 🟢 Low |
| 1.4 | `Dockerfile` | Update base images from `9.0-alpine` to `10.0-alpine` | 🟢 Low |

### Phase 2: Leaf Library Projects (no project dependencies on other src projects)
These projects have no downstream src project dependencies so they are safe to upgrade first.

| Step | Project | Change | Risk |
|------|---------|--------|------|
| 2.1 | `src\BaGetter.Protocol\BaGetter.Protocol.csproj` | `netstandard2.0` → `net10.0` | 🟢 Low |

### Phase 3: Core Library
Depends on `BaGetter.Protocol`.

| Step | Project | Change | Risk |
|------|---------|--------|------|
| 3.1 | `src\BaGetter.Core\BaGetter.Core.csproj` | `net9.0` → `net10.0` | 🟢 Low |

### Phase 4: Mid-Tier Libraries
All depend on `BaGetter.Core`. No ordering constraint among themselves.

| Step | Project | Change | Risk |
|------|---------|--------|------|
| 4.1 | `src\BaGetter.Web\BaGetter.Web.csproj` | `net9.0` → `net10.0` | 🟢 Low |
| 4.2 | `src\BaGetter.Aws\BaGetter.Aws.csproj` | `net9.0` → `net10.0` | 🟢 Low |
| 4.3 | `src\BaGetter.Azure\BaGetter.Azure.csproj` | `net9.0` → `net10.0` | 🟢 Low |
| 4.4 | `src\BaGetter.Gcp\BaGetter.Gcp.csproj` | `net9.0` → `net10.0` | 🟢 Low |
| 4.5 | `src\BaGetter.Aliyun\BaGetter.Aliyun.csproj` | `net9.0` → `net10.0` | 🟢 Low |
| 4.6 | `src\BaGetter.Tencent\BaGetter.Tencent.csproj` | `net9.0` → `net10.0` | 🟢 Low |
| 4.7 | `src\BaGetter.Database.MySql\BaGetter.Database.MySql.csproj` | `net9.0` → `net10.0` | 🟢 Low |
| 4.8 | `src\BaGetter.Database.PostgreSql\BaGetter.Database.PostgreSql.csproj` | `net9.0` → `net10.0` | 🟢 Low |
| 4.9 | `src\BaGetter.Database.Sqlite\BaGetter.Database.Sqlite.csproj` | `net9.0` → `net10.0` | 🟢 Low |
| 4.10 | `src\BaGetter.Database.SqlServer\BaGetter.Database.SqlServer.csproj` | `net9.0` → `net10.0` | 🟢 Low |

### Phase 5: Host Application
Depends on all mid-tier libraries.

| Step | Project | Change | Risk |
|------|---------|--------|------|
| 5.1 | `src\BaGetter\BaGetter.csproj` | `net9.0` → `net10.0` | 🟢 Low |

### Phase 6: Samples

| Step | Project | Change | Risk |
|------|---------|--------|------|
| 6.1 | `samples\BaGetterWebApplication\BaGetterWebApplication.csproj` | `net9.0` → `net10.0` | 🟢 Low |
| 6.2 | `samples\BaGetter.Protocol.Samples.Tests\BaGetter.Protocol.Samples.Tests.csproj` | `net9.0` → `net10.0` | 🟢 Low |

### Phase 7: Test Projects

| Step | Project | Change | Risk |
|------|---------|--------|------|
| 7.1 | `tests\BaGetter.Protocol.Tests\BaGetter.Protocol.Tests.csproj` | `net9.0` → `net10.0` | 🟢 Low |
| 7.2 | `tests\BaGetter.Core.Tests\BaGetter.Core.Tests.csproj` | `net9.0` → `net10.0` | 🟢 Low |
| 7.3 | `tests\BaGetter.Web.Tests\BaGetter.Web.Tests.csproj` | `net9.0` → `net10.0` | 🟢 Low |
| 7.4 | `tests\BaGetter.Tests\BaGetter.Tests.csproj` | `net9.0` → `net10.0` | 🟢 Low |

### Phase 8: Validation
Build the solution and run tests to confirm the upgrade.

| Step | Action | Details |
|------|--------|---------|
| 8.1 | Build solution | `dotnet build BaGetter.sln` |
| 8.2 | Fix any issues | Address compilation errors if any |

---

## Package Version Mapping

### Microsoft Packages (9.0.x → 10.0.x)

| Package | From | To |
|---------|------|----|
| `Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation` | 9.0.10 | 10.0.x (latest) |
| `Microsoft.EntityFrameworkCore.Design` | 9.0.10 | 10.0.x (latest) |
| `Microsoft.EntityFrameworkCore.Relational` | 9.0.10 | 10.0.x (latest) |
| `Microsoft.Extensions.Configuration` | 9.0.10 | 10.0.x (latest) |
| `Microsoft.Extensions.Configuration.Abstractions` | 9.0.10 | 10.0.x (latest) |
| `Microsoft.Extensions.DependencyInjection.Abstractions` | 9.0.10 | 10.0.x (latest) |
| `Microsoft.Extensions.Diagnostics.HealthChecks` | 9.0.10 | 10.0.x (latest) |
| `Microsoft.Extensions.Diagnostics.HealthChecks.EntityFrameworkCore` | 9.0.10 | 10.0.x (latest) |
| `Microsoft.Extensions.Logging.Abstractions` | 9.0.10 | 10.0.x (latest) |
| `Microsoft.Extensions.Options.ConfigurationExtensions` | 9.0.10 | 10.0.x (latest) |
| `System.Reflection.Metadata` | 9.0.10 | 10.0.x (latest) |
| `System.Text.Json` | 9.0.8 | 10.0.x (latest) |
| `Microsoft.AspNetCore.Mvc.Testing` | 9.0.10 | 10.0.x (latest) |
| `Microsoft.EntityFrameworkCore.SqlServer` | 9.0.10 | 10.0.x (latest) |
| `Microsoft.EntityFrameworkCore.Sqlite` | 9.0.10 | 10.0.x (latest) |

### EF Core Ecosystem Packages

| Package | From | To |
|---------|------|----|
| `Npgsql.EntityFrameworkCore.PostgreSQL` | 9.0.4 | 10.0.x (latest) |
| `Pomelo.EntityFrameworkCore.MySql` | 9.0.0 | 10.0.x (latest) |

### Third-Party Packages (No Changes Required)
All third-party packages are .NET Standard compatible or already support .NET 10. No version changes needed.

---

## Risk Mitigation

| Risk | Mitigation |
|------|-----------|
| Package version not available for .NET 10 | Use NuGet solver to find latest compatible versions; fall back to pre-release if stable not yet available |
| `netstandard2.0` → `net10.0` breaks downstream consumers | BaGetter.Protocol is only consumed internally — no external package consumers affected |
| Docker base image not yet available | Verify `10.0-alpine` tag exists; fall back to `10.0` if Alpine variant is unavailable |

---

## Summary

- **Total files to modify**: 23 (19 .csproj + `global.json` + `Directory.Packages.props` + `Dockerfile`)
- **Estimated effort**: Low — all changes are version bumps, no code changes expected
- **Validation**: Build + review for compilation errors
