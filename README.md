# Entity-Framework-Core

### StartUp.cs

- Startup=>設定檔
- ConfigureServices =>設定服務
- Configure =>設定Pipe Line 管理整個程式生命週期

### 建立資料庫

- 開啟套件管理器主控台 – [檢視] -> [其他視窗] -> [套件管理器主控台]
- 新增資料庫移轉 (必須執行資料庫移轉才能建立資料庫) – Add-Migration Initial
- 建立資料庫 (首次執行會自動建立資料庫) – Update-Database
- 使用 SSMS 檢查資料庫結構 – __EFMigrationsHistory *用來記錄所有資料庫結構變更歷史*
#### Add-Migration Initial
#### Remove-Migration
#### 產生還原指定版本 T-SQL 指令
- Script-Migration -from **較新的Migration檔** -to **較舊的Migration檔**
#### 產生更新指定版本 T-SQL 指令
- Script-Migration -from **較舊的Migration檔** -to **較新的Migration檔**

#### MyBlogContextModelSnapshot

紀錄上一版本

#### -DataAnnotations

包含資料庫的Model DataAnnotations(欄位長度、必填等控制)

#### DB First指令

Scaffold-DbContext "Server=(localdb)\MSSQLLocalDB;Database=MyBlog;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models -DataAnnotations

### [ 11 安裝 Entity Framework Core 的 .NET Core CLI 工具 ]


Entity Framework | .NET Core CLI | Microsoft Docs
( Entity Framework Core .NET Command Line Tools )
https://docs.microsoft.com/en-us/ef/core/miscellaneous/cli/dotnet

##### 安裝

    <DotNetCliToolReference Include="Microsoft.EntityFrameworkCore.Tools.DotNet" Version="1.0.0" />

    Install-Package Microsoft.EntityFrameworkCore.Design

    dotnet add package Microsoft.EntityFrameworkCore.Design
    dotnet restore

##### 使用

dotnet ef [subcommand]
dotnet ef --help
dotnet ef database

    dotnet ef database drop
    dotnet ef database drop -f

    dotnet ef database update               (預設為最新的 Migration 版本)
    dotnet ef database update 0             (還原到最初版本，等於清空所有資料庫表格)
    dotnet ef database update [<MIGRATION>] (自動移轉到特定版本) (可降版)
    dotnet ef database update 20170412140305_Initial

dotnet ef dbcontext

    dotnet ef dbcontext list

    dotnet ef dbcontext info
    dotnet ef dbcontext info -c EFCoreWithExistingDatabase.Models.FabricsContext
    dotnet ef dbcontext info -c EFCoreWithExistingDatabase.Models.MyBlogContext

    dotnet ef dbcontext scaffold [<CONNECTION>] [<PROVIDER>]
    dotnet ef dbcontext scaffold "Server=(localdb)\MSSQLLocalDB;Database=MyBlog;Trusted_Connection=True;" "Microsoft.EntityFrameworkCore.SqlServer"
    dotnet ef dbcontext scaffold "Server=(localdb)\MSSQLLocalDB;Database=Fabrics;Trusted_Connection=True;" "Microsoft.EntityFrameworkCore.SqlServer"

dotnet ef migrations

    dotnet ef migrations list

    dotnet ef migrations add <Name>
    dotnet ef migrations add Initial

    dotnet ef migrations remove             ( 移除最後一個移轉設定 )

    dotnet ef migrations script             ( 預設從 0 移轉到最新版的所有資料庫變更指令碼 )
    dotnet ef migrations script [<FROM>] [<TO>]

    降版: dotnet ef migrations script 20170412143011_Blogs_SchemaChanges 20170412140305_Initial -o down.txt
    升版: dotnet ef migrations script 20170412140305_Initial 20170412143011_Blogs_SchemaChanges -o up.txt
