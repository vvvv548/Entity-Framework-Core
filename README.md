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

# 2070417 課程
### 管理容器映像生命週期與基本指令(IMAGE)    
    • 列出所有容器映像 ( container image ) – docker images 
    
    • 搜尋容器映像 ( Docker Hub ) – docker search TERM 
    
    • 建立容器映像 ( 從現有容器建立 ) – docker commit CONTAINER IMAGE 
    
    • 建立容器映像 ( 從 Dockerfile 建立 ) – docker build -t REPO:TAG PATH 
    
    • 標記指定容器映像 – docker tag IMAGE[:TAG] NEWIMAGE[:TAG] 
    
    • 刪除指定容器映像 – docker rmi IMAG
    
    
### 管理容器生命週期與基本指令(CONTAINER)

    • 建立映像實體( image instance ) ( container ) – docker run -it IMAGE COMMAND 
    
    • 列出所有容器 – docker ps -a 
    
    • 啟動指定容器 – docker start CONTAINER 
    
    • 在指定容器中執行命令 – docker exec -it CONTAINER cmd 
    
    • 停止指定容器 – docker stop CONTAINER 
    
    • 刪除指定容器 – docker rm CONTAINE
    
#### Asp.net 複製並測試
    docker run -name myASP -d microsoft/aspnet 
    
    docker exec -it myASP powershell
    
    Add-WindowsFeature Web-ASP 
    
    docker stop myASP
    
    docker commit myASP myasp:1.0
    
    docker rm myASP
    
    docker run -name myASP -p 8088:80 -d myASP 
    
    docker cp C:\a.asp myASP:C:\inetpub\wwwroot
    
# 2070425 單元測試

### 必要的特性
    單元測試只應該測試一個程式的最小單元

    測試目標不應該直接相依外部任何資源    

    測試程式要可以重複執行

    測試程式不應有邏輯判斷

    測試程式應該是完全獨立

    測試結果應該是穩定的

    測試失敗時必須可以清楚掌握原本預期的結果與發生失敗的原因
 
 ### 3A原則
 
 #### 一個單元測試主要包含三個動作
 
 Arrange 安排測試目標
 
 Act 執行測試目標
 
 Assert 斷言測試結果
