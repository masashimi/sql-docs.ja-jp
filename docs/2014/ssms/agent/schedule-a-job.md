---
title: ジョブのスケジュール設定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- scheduling jobs [SQL Server]
- SQL Server Agent jobs, scheduling
- jobs [SQL Server Agent], scheduling
ms.assetid: f626390a-a3df-4970-b7a7-a0529e4a109c
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: feb21e74909aa89d3a43e392a434d22b7c07d9d3
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2018
ms.locfileid: "43814808"
---
# <a name="schedule-a-job"></a>Schedule a Job
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブのスケジュールを設定する方法について説明します。  
  
-   **作業を開始する準備:**   
  
     [Security](#Security)  
  
-   **ジョブのスケジュールを設定する方法:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理オブジェクト](#SMO)  
  
##  <a name="BeforeYouBegin"></a> 作業を開始する準備  
  
###  <a name="Security"></a> セキュリティ  
 詳細については、「 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)」をご覧ください。  
  
##  <a name="SSMS"></a> SQL Server Management Studio の使用  
  
#### <a name="to-create-and-attach-a-schedule-to-a-job"></a>スケジュールを作成してジョブにアタッチするには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]**、 **[ジョブ]** の順に展開し、スケジュールを設定するジョブを右クリックします。次に、 **[プロパティ]** をクリックします。  
  
3.  **[スケジュール]** ページをクリックし、 **[新規作成]** をクリックします。  
  
4.  **[名前]** ボックスに新しいスケジュールの名前を入力します。  
  
5.  スケジュールを作成してもすぐに有効にしない場合は、 **[有効]** チェック ボックスをオフにします。  
  
6.  **[スケジュールの種類]** ボックスの一覧で、次のいずれかを選択します。  
  
    -   **[SQL Server エージェントの開始時に自動的に開始]** 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスが開始されたときにジョブを開始します。  
  
    -   **[CPU がアイドル状態になったときに開始]** 。CPU がアイドル状態になったときにジョブを開始します。  
  
    -   **[定期的]** 。スケジュールを繰り返し実行します。 定期的なスケジュールを設定するには、ダイアログ ボックス上の **[頻度]**、 **[一日のうちの頻度]**、および **[実行時間]** のグループに値を指定します。  
  
    -   **[指定日時]** 。スケジュールを 1 回のみ実行します。 **指定日時** のスケジュールを設定するには、ダイアログ ボックス上の **[指定日時に発生]** グループに値を指定します。  
  
#### <a name="to-attach-a-schedule-to-a-job"></a>ジョブにスケジュールをアタッチするには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]**、 **[ジョブ]** の順に展開し、スケジュールを設定するジョブを右クリックして、 **[プロパティ]** をクリックします。  
  
3.  **[スケジュール]** ページをクリックし、 **[選択]** をクリックします。  
  
4.  アタッチするスケジュールを選択して、 **[OK]** をクリックします。  
  
5.  **[ジョブのプロパティ]** ダイアログ ボックスで、アタッチされたスケジュールをダブルクリックします。  
  
6.  **[開始日]** が正しく設定されていることを確認します。 正しく設定されていない場合は、スケジュールの開始日を設定し、 **[OK]** をクリックします。  
  
7.  **[ジョブのプロパティ]** ダイアログ ボックスで、 **[OK]** をクリックします。  
  
##  <a name="TSQL"></a> Transact-SQL の使用  
  
#### <a name="to-schedule-a-job"></a>ジョブのスケジュールを設定するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE msdb ;  
    GO  
    -- creates a schedule named NightlyJobs.   
    -- Jobs that use this schedule execute every day when the time on the server is 01:00.   
    EXEC sp_add_schedule  
        @schedule_name = N'NightlyJobs' ,  
        @freq_type = 4,  
        @freq_interval = 1,  
        @active_start_time = 010000 ;  
    GO  
    -- attaches the schedule to the job BackupDatabase  
    EXEC sp_attach_schedule  
       @job_name = N'BackupDatabase',  
       @schedule_name = N'NightlyJobs' ;  
    GO  
    ```  
  
 詳細については、次を参照してください。 [sp_add_schedule &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-add-schedule-transact-sql)と[sp_attach_schedule &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql)します。  
  
##  <a name="SMO"></a> SQL Server 管理オブジェクトの使用  
 使用して、 `JobSchedule` Visual Basic、Visual c#、PowerShell など、選択したプログラミング言語を使用してクラス。 詳細については、「[SQL Server 管理オブジェクト (SMO) プログラミング ガイド](http://msdn.microsoft.com/library/ms162169.aspx)」を参照してください。  
  
  
