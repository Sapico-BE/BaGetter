# .NET Upgrade Tasks: .NET 9.0 → .NET 10.0

## Execution Progress

### Phase 1: Infrastructure Files
- [x] 1.1 Update `global.json` SDK version → `10.0.100`
- [x] 1.2 Update `Directory.Packages.props` Microsoft package versions → `10.0.3`
- [x] 1.3 Update `Directory.Packages.props` EF Core ecosystem packages → Npgsql `10.0.0`, switched Pomelo → `MySql.EntityFrameworkCore 10.0.1`
- [x] 1.4 Update `Dockerfile` base images → `10.0-alpine`

### Phase 2: Leaf Library
- [x] 2.1 `src\BaGetter.Protocol\BaGetter.Protocol.csproj` → `net10.0` (was `netstandard2.0`)

### Phase 3: Core Library
- [x] 3.1 `src\BaGetter.Core\BaGetter.Core.csproj` → `net10.0`

### Phase 4: Mid-Tier Libraries
- [x] 4.1 `src\BaGetter.Web\BaGetter.Web.csproj` → `net10.0`
- [x] 4.2 `src\BaGetter.Aws\BaGetter.Aws.csproj` → `net10.0`
- [x] 4.3 `src\BaGetter.Azure\BaGetter.Azure.csproj` → `net10.0`
- [x] 4.4 `src\BaGetter.Gcp\BaGetter.Gcp.csproj` → `net10.0`
- [x] 4.5 `src\BaGetter.Aliyun\BaGetter.Aliyun.csproj` → `net10.0`
- [x] 4.6 `src\BaGetter.Tencent\BaGetter.Tencent.csproj` → `net10.0`
- [x] 4.7 `src\BaGetter.Database.MySql\BaGetter.Database.MySql.csproj` → `net10.0` + switched to `MySql.EntityFrameworkCore`
- [x] 4.8 `src\BaGetter.Database.PostgreSql\BaGetter.Database.PostgreSql.csproj` → `net10.0`
- [x] 4.9 `src\BaGetter.Database.Sqlite\BaGetter.Database.Sqlite.csproj` → `net10.0`
- [x] 4.10 `src\BaGetter.Database.SqlServer\BaGetter.Database.SqlServer.csproj` → `net10.0`

### Phase 5: Host Application
- [x] 5.1 `src\BaGetter\BaGetter.csproj` → `net10.0`

### Phase 6: Samples
- [x] 6.1 `samples\BaGetterWebApplication\BaGetterWebApplication.csproj` → `net10.0`
- [x] 6.2 `samples\BaGetter.Protocol.Samples.Tests\BaGetter.Protocol.Samples.Tests.csproj` → `net10.0`

### Phase 7: Test Projects
- [x] 7.1 `tests\BaGetter.Protocol.Tests\BaGetter.Protocol.Tests.csproj` → `net10.0`
- [x] 7.2 `tests\BaGetter.Core.Tests\BaGetter.Core.Tests.csproj` → `net10.0`
- [x] 7.3 `tests\BaGetter.Web.Tests\BaGetter.Web.Tests.csproj` → `net10.0`
- [x] 7.4 `tests\BaGetter.Tests\BaGetter.Tests.csproj` → `net10.0`

### Phase 8: Validation
- [x] 8.1 Build solution ✅
- [x] 8.2 Fix issues — switched from Pomelo.EntityFrameworkCore.MySql to MySql.EntityFrameworkCore (no .NET 10 Pomelo release available)

## Additional Changes (not in original plan)
- Replaced `Pomelo.EntityFrameworkCore.MySql 9.0.0` with `MySql.EntityFrameworkCore 10.0.1` (Oracle's official MySQL EF Core provider)
- Updated `MySqlContext.cs`: `UseMySql()` → `UseMySQL()`, `MySqlConnector` → `MySql.Data.MySqlClient`, removed `ServerVersion.AutoDetect()`
- Updated 5 migration files: `MySqlValueGenerationStrategy` → `MySQLValueGenerationStrategy` with `MySql.EntityFrameworkCore.Metadata` namespace
- Updated 2 migration designer files: replaced `MySqlModelBuilderExtensions.HasCharSet()` with annotation-based approach
- Updated `Microsoft.Data.SqlClient` from `6.0.1` → `6.1.4`
