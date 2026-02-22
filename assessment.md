# .NET Upgrade Assessment: .NET 9.0 → .NET 10.0

## Solution Overview

| Property | Value |
|---|---|
| **Solution** | `BaGetter.sln` |
| **Current Target** | .NET 9.0 (16 projects) / .NET Standard 2.0 (1 project) |
| **Upgrade Target** | .NET 10.0 |
| **Total Projects** | 19 |
| **Package Management** | Central Package Management (`Directory.Packages.props`) |
| **SDK Pinning** | `global.json` → `9.0.306` |
| **Containerization** | `Dockerfile` (Alpine-based, SDK + ASP.NET runtime) |

---

## Projects Inventory

| # | Project | Current TFM | Target TFM | SDK | Notes |
|---|---------|-------------|------------|-----|-------|
| 1 | `src\BaGetter\BaGetter.csproj` | net9.0 | net10.0 | Microsoft.NET.Sdk.Web | Main host app |
| 2 | `src\BaGetter.Web\BaGetter.Web.csproj` | net9.0 | net10.0 | Microsoft.NET.Sdk.Razor | Razor class library |
| 3 | `src\BaGetter.Core\BaGetter.Core.csproj` | net9.0 | net10.0 | Microsoft.NET.Sdk | Core library |
| 4 | `src\BaGetter.Protocol\BaGetter.Protocol.csproj` | netstandard2.0 | net10.0 | Microsoft.NET.Sdk | Protocol library |
| 5 | `src\BaGetter.Aws\BaGetter.Aws.csproj` | net9.0 | net10.0 | Microsoft.NET.Sdk | AWS storage |
| 6 | `src\BaGetter.Azure\BaGetter.Azure.csproj` | net9.0 | net10.0 | Microsoft.NET.Sdk | Azure storage |
| 7 | `src\BaGetter.Gcp\BaGetter.Gcp.csproj` | net9.0 | net10.0 | Microsoft.NET.Sdk | GCP storage |
| 8 | `src\BaGetter.Aliyun\BaGetter.Aliyun.csproj` | net9.0 | net10.0 | Microsoft.NET.Sdk | Alibaba Cloud |
| 9 | `src\BaGetter.Tencent\BaGetter.Tencent.csproj` | net9.0 | net10.0 | Microsoft.NET.Sdk | Tencent Cloud |
| 10 | `src\BaGetter.Database.MySql\BaGetter.Database.MySql.csproj` | net9.0 | net10.0 | Microsoft.NET.Sdk | MySQL DB |
| 11 | `src\BaGetter.Database.PostgreSql\BaGetter.Database.PostgreSql.csproj` | net9.0 | net10.0 | Microsoft.NET.Sdk | PostgreSQL DB |
| 12 | `src\BaGetter.Database.Sqlite\BaGetter.Database.Sqlite.csproj` | net9.0 | net10.0 | Microsoft.NET.Sdk | SQLite DB |
| 13 | `src\BaGetter.Database.SqlServer\BaGetter.Database.SqlServer.csproj` | net9.0 | net10.0 | Microsoft.NET.Sdk | SQL Server DB |
| 14 | `tests\BaGetter.Tests\BaGetter.Tests.csproj` | net9.0 | net10.0 | Microsoft.NET.Sdk | Integration tests |
| 15 | `tests\BaGetter.Core.Tests\BaGetter.Core.Tests.csproj` | net9.0 | net10.0 | Microsoft.NET.Sdk | Core unit tests |
| 16 | `tests\BaGetter.Web.Tests\BaGetter.Web.Tests.csproj` | net9.0 | net10.0 | Microsoft.NET.Sdk | Web unit tests |
| 17 | `tests\BaGetter.Protocol.Tests\BaGetter.Protocol.Tests.csproj` | net9.0 | net10.0 | Microsoft.NET.Sdk | Protocol tests |
| 18 | `samples\BaGetterWebApplication\BaGetterWebApplication.csproj` | net9.0 | net10.0 | Microsoft.NET.Sdk.Web | Sample app |
| 19 | `samples\BaGetter.Protocol.Samples.Tests\BaGetter.Protocol.Samples.Tests.csproj` | net9.0 | net10.0 | Microsoft.NET.Sdk | Sample tests |

---

## Key Findings

### 1. Target Framework Changes (19 projects)
- **16 projects** currently target `net9.0` → will change to `net10.0`
- **1 project** (`BaGetter.Protocol`) targets `netstandard2.0` → will change to `net10.0`
- **Risk**: Low – straightforward TFM update

### 2. `global.json` SDK Version
- Currently pinned to `9.0.306` with `rollForward: latestFeature`
- Must update to `10.0.100` (or appropriate .NET 10 SDK version)
- **Risk**: Low

### 3. `Dockerfile` Base Images
- SDK image: `mcr.microsoft.com/dotnet/sdk:9.0-alpine` → `10.0-alpine`
- Runtime image: `mcr.microsoft.com/dotnet/aspnet:9.0-alpine` → `10.0-alpine`
- **Risk**: Low

### 4. NuGet Packages – Microsoft Packages (Central Package Management)
The following Microsoft packages in `Directory.Packages.props` need .NET 10 compatible versions:

| Package | Current Version | Action |
|---------|----------------|--------|
| `Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation` | 9.0.10 | Update to 10.0.x |
| `Microsoft.EntityFrameworkCore.Design` | 9.0.10 | Update to 10.0.x |
| `Microsoft.EntityFrameworkCore.Relational` | 9.0.10 | Update to 10.0.x |
| `Microsoft.Extensions.Configuration` | 9.0.10 | Update to 10.0.x |
| `Microsoft.Extensions.Configuration.Abstractions` | 9.0.10 | Update to 10.0.x |
| `Microsoft.Extensions.DependencyInjection.Abstractions` | 9.0.10 | Update to 10.0.x |
| `Microsoft.Extensions.Diagnostics.HealthChecks` | 9.0.10 | Update to 10.0.x |
| `Microsoft.Extensions.Diagnostics.HealthChecks.EntityFrameworkCore` | 9.0.10 | Update to 10.0.x |
| `Microsoft.Extensions.Logging.Abstractions` | 9.0.10 | Update to 10.0.x |
| `Microsoft.Extensions.Options.ConfigurationExtensions` | 9.0.10 | Update to 10.0.x |
| `System.Reflection.Metadata` | 9.0.10 | Update to 10.0.x |
| `System.Text.Json` | 9.0.8 | Update to 10.0.x |
| `Microsoft.AspNetCore.Mvc.Testing` | 9.0.10 | Update to 10.0.x |
| `Microsoft.EntityFrameworkCore.SqlServer` | 9.0.10 | Update to 10.0.x |
| `Microsoft.EntityFrameworkCore.Sqlite` | 9.0.10 | Update to 10.0.x |
| `Npgsql.EntityFrameworkCore.PostgreSQL` | 9.0.4 | Update to 10.0.x |
| `Pomelo.EntityFrameworkCore.MySql` | 9.0.0 | Update to 10.0.x |

### 5. NuGet Packages – Third-Party Packages
These packages are not tied to .NET version and should remain compatible:

| Package | Current Version | Expected Compatibility |
|---------|----------------|----------------------|
| `Azure.Data.Tables` | 12.10.0 | ✅ Compatible |
| `Azure.Search.Documents` | 11.6.0 | ✅ Compatible |
| `Azure.Storage.Blobs` | 12.24.0 | ✅ Compatible |
| `Azure.Storage.Common` | 12.23.0 | ✅ Compatible |
| `McMaster.Extensions.CommandLineUtils` | 4.1.1 | ✅ Compatible |
| `Newtonsoft.Json` | 13.0.3 | ✅ Compatible |
| `NuGet.Frameworks` | 6.13.2 | ✅ Compatible |
| `NuGet.Protocol` | 6.13.2 | ✅ Compatible |
| `NuGet.Versioning` | 6.13.2 | ✅ Compatible |
| `Microsoft.NET.Test.Sdk` | 17.13.0 | ✅ Compatible |
| `Moq` | 4.20.72 | ✅ Compatible |
| `xunit` | 2.9.3 | ✅ Compatible |
| `xunit.runner.visualstudio` | 3.0.2 | ✅ Compatible |
| `coverlet.collector` | 6.0.4 | ✅ Compatible |
| `Humanizer` | 2.14.1 | ✅ Compatible |
| `Markdig` | 0.40.0 | ✅ Compatible |
| `Microsoft.Data.SqlClient` | 6.0.1 | ✅ Compatible |
| `Aliyun.OSS.SDK.NetCore` | 2.14.1 | ✅ Compatible |
| `AWSSDK.S3` | 3.7.415.16 | ✅ Compatible |
| `AWSSDK.SecurityToken` | 3.7.401.60 | ✅ Compatible |
| `Google.Cloud.Storage.V1` | 4.11.0 | ✅ Compatible |
| `Tencent.QCloud.Cos.Sdk` | 5.4.44 | ✅ Compatible |
| `Microsoft.Azure.Cosmos` | 3.38.1 | ✅ Compatible (unused?) |
| `Microsoft.Azure.Cosmos.Table` | 1.0.8 | ✅ Compatible (legacy, unused?) |
| `Microsoft.Azure.Search` | 10.1.0 | ✅ Compatible (legacy, unused?) |
| `Microsoft.Azure.Storage.Blob` | 11.2.3 | ✅ Compatible (legacy, unused?) |

### 6. .NET Standard 2.0 → .NET 10.0 Migration
- `BaGetter.Protocol` currently targets `netstandard2.0`
- Upgrading to `net10.0` gives access to modern APIs and removes netstandard constraints
- **Risk**: Low – the project only uses `System.Text.Json`, `NuGet.Frameworks`, `NuGet.Versioning`, and `Microsoft.Extensions.Logging.Abstractions`

### 7. Breaking Changes & API Deprecations
- No known critical breaking changes from .NET 9 → .NET 10 that affect this codebase
- The `DotNetCliToolReference` in `BaGetter.Protocol.Samples.Tests.csproj` is deprecated (already deprecated since .NET Core 3.0) – not a blocker but worth noting

### 8. Overall Risk Assessment
- **Overall Risk**: 🟢 **Low**
- The upgrade is primarily a TFM bump + package version update
- No architectural changes required
- No deprecated API usage that blocks the upgrade

---

## Summary

| Category | Items | Risk |
|----------|-------|------|
| TFM updates | 19 projects | 🟢 Low |
| SDK pinning | 1 file (`global.json`) | 🟢 Low |
| Dockerfile | 2 base image references | 🟢 Low |
| Microsoft packages | ~17 packages | 🟢 Low |
| Third-party packages | ~20+ packages | 🟢 Low (no changes needed) |
| Code changes | None expected | 🟢 Low |
