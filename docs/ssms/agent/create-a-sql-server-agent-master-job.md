---
title: SQL Server エージェントのマスター ジョブの作成 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], master jobs
- jobs [SQL Server Agent], creating
- master SQL Server Agent job [SQL Server]
ms.assetid: c12ab23f-d7ee-43a5-8cd2-0a9121292bcd
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b572a5fe585d36f106c15ccc48e8a18215141f23
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2018
ms.locfileid: "42775495"
---
# <a name="create-a-sql-server-agent-master-job"></a>SQL Server エージェントのマスター ジョブの作成
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのマスター ジョブを作成する方法について説明します。  
  
**このトピックの内容**  
  
-   **作業を開始する準備:**  
  
    [制限事項と制約事項](#Restrictions)  
  
    [Security](#Security)  
  
-   **SQL Server エージェントのマスター ジョブを作成する方法:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Restrictions"></a>制限事項と制約事項  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのマスター ジョブの変更は、関係するすべての対象サーバーに伝達する必要があります。 これらのターゲットが指定されるまで対象サーバーはジョブをダウンロードしないので、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] では、対象サーバーを指定する前に、特定のジョブのすべてのジョブ ステップとジョブ スケジュールを完了しておくことをお勧めしています。 この順序に従わなかった場合は、 **sp_post_msx_operation** ストアド プロシージャを実行するか、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用してジョブを変更することによって、変更されたジョブを対象サーバーが再びダウンロードするように手動で要求する必要があります。 詳細については、「 [sp_post_msx_operation (Transact-SQL)](http://msdn.microsoft.com/085deef8-2709-4da9-bb97-9ab32effdacf) 」または「 [ジョブの変更](../../ssms/agent/modify-a-job.md)」を参照してください。  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
プロキシに関連付けられているステップを持つ分散ジョブは、対象サーバーのプロキシ アカウントのコンテキストで実行されます。 次の条件を満たしていることを確認してください。満たしていないと、プロキシに関連付けられているジョブ ステップがマスター サーバーから対象サーバーにダウンロードされません。  
  
-   レジストリのサブキー **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<&#42;instance_name&#42;>\SQL Server Agent\AllowDownloadedJobsToMatchProxyName** (REG_DWORD) が 1 (true) に設定されていること。 既定では、この値は 0 (false) に設定されます。  
  
-   ジョブ ステップを実行するマスター サーバー プロキシ アカウントと同じ名前を持つ対象サーバーにプロキシ アカウントが存在すること。  
  
マスター サーバーから対象サーバーにプロキシ アカウントをダウンロード中に、これらのアカウントを使用するジョブ ステップが失敗した場合は、 **msdb** データベースの **sysdownloadlist** テーブルの **error_message** 列を参照して、以下のエラー メッセージの有無を確認します。  
  
-   "ジョブ ステップではプロキシ アカウントが必要ですが、対象サーバーで一致するプロキシが無効です。" このエラーを解決するには、 **AllowDownloadedJobsToMatchProxyName** レジストリ サブキーを 1 に設定します。  
  
-   "プロキシ アカウントが見つかりませんでした。" このエラーを解決するには、対象サーバー上にプロキシ アカウントが存在し、ジョブ ステップを実行するマスター サーバー プロキシ アカウントと同じ名前が付けられているかどうかを確認します。  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
  
#### <a name="to-create-a-master-sql-server-agent-job"></a>SQL Server エージェントのマスター ジョブを作成するには  
  
1.  **オブジェクト エクスプローラー**で、SQL Server エージェント ジョブを作成するサーバーをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[SQL Server エージェント]** を展開します。  
  
3.  **[ジョブ]** フォルダーを右クリックし、 **[新しいジョブ]** を選択します。  
  
4.  **[新しいジョブ]** ダイアログ ボックスの **[全般]** ページで、ジョブの全般的なプロパティを変更します。 このページで利用可能なオプションの詳細については、「[ジョブのプロパティ - [新しいジョブ] ([全般] ページ)](../../ssms/agent/job-properties-new-job-general-page.md)」を参照してください。  
  
5.  **[ステップ]** ページで、ジョブ ステップを編成します。 このページで利用可能なオプションの詳細については、「[ジョブのプロパティ - [新しいジョブ] ([全般] ページ)](../../ssms/agent/job-properties-new-job-steps-page.md)」を参照してください。  
  
6.  **[スケジュール** ] ページで、ジョブのスケジュールを編成します。 このページで利用可能なオプションの詳細については、「[ジョブのプロパティ - [新しいジョブ] ([スケジュール] ページ)](../../ssms/agent/job-properties-new-job-schedules-page.md)」を参照してください。  
  
7.  **[警告]** ページで、ジョブの警告を編成します。 このページで利用可能なオプションの詳細については、「[ジョブのプロパティ - [新しいジョブ] ([警告] ページ)](../../ssms/agent/job-properties-new-job-alerts-page.md)」を参照してください。  
  
8.  **[通知]** ページで、ジョブの完了時に [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行するアクションを設定します。 このページで利用可能なオプションの詳細については、「[ジョブのプロパティ - [新しいジョブ] ([通知] ページ)](../../ssms/agent/job-properties-new-job-notifications-page.md)」を参照してください。  
  
9. **[ターゲット]** ページで、ジョブの対象サーバーを管理します。 このページで利用可能なオプションの詳細については、「[ジョブのプロパティ - [新しいジョブ] ([対象サーバー] ページ)](../../ssms/agent/job-properties-new-job-targets-page.md)」を参照してください。  
  
10. 完了したら、 **[OK]** をクリックします。  
  
## <a name="TsqlProcedure"></a>Transact-SQL の使用  
  
#### <a name="to-create-a-master-sql-server-agent-job"></a>SQL Server エージェントのマスター ジョブを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE msdb ;  
    GO  
    -- Adds a new job executed by the SQLServerAgent service called 'Weekly Sales Data Backup'  
    EXEC dbo.sp_add_job  
        @job_name = N'Weekly Sales Data Backup' ;  
    GO  
    -- Adds a step (operation) to the 'Weekly Sales Data Backup' job.  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    -- Creates a schedule called RunOnce  
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',  
        @freq_type = 1,  
        @active_start_time = 233000 ;  
    USE msdb ;  
    GO  
    -- Sets the 'RunOnce' schedule to the "Weekly Sales Data Backup' Job  
    EXEC sp_attach_schedule  
       @job_name = N'Weekly Sales Data Backup',  
       @schedule_name = N'RunOnce';  
    GO  
    -- assigns the multiserver job Weekly Sales Backups to the server SEATTLE2  
    -- assumes that SEATTLE2 is registered as a target server for the current instance.  
    EXEC dbo.sp_add_jobserver  
        @job_name = N'Weekly Sales Data Backups',  
        @server_name = N'SEATTLE2' ;  
    GO  
    ```  
  
詳細については、以下をご覧ください。  
  
-   [sp_add_job (Transact-SQL)](http://msdn.microsoft.com/6ca8fe2c-7b1c-4b59-b4c7-e3b7485df274)  
  
-   [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/97900032-523d-49d6-9865-2734fba1c755)  
  
-   [sp_add_schedule (Transact-SQL)](http://msdn.microsoft.com/9060aae3-3ddd-40a5-83bb-3ea7ab1ffbd7)  
  
-   [sp_attach_schedule (Transact-SQL)](http://msdn.microsoft.com/80c80eaf-cf23-4ed8-b8dd-65fe59830dd1)  
  
-   [sp_add_jobserver (Transact-SQL)](http://msdn.microsoft.com/485252cc-0081-490a-9bd1-cbbd68eea286)  
  
