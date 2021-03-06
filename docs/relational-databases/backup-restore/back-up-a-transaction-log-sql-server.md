---
title: トランザクション ログのバックアップ (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transaction log backups [SQL Server], SQL Server Management Studio
- backups [SQL Server], creating
- backing up transaction logs [SQL Server], SQL Server Management Studio
ms.assetid: 3426b5eb-6327-4c7f-88aa-37030be69fbf
caps.latest.revision: 49
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 51e618a3b81243883276193260b68848d8b2f9fe
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2018
ms.locfileid: "40175210"
---
# <a name="back-up-a-transaction-log-sql-server"></a>トランザクション ログのバックアップ (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、または PowerShell を使用して、トランザクション ログをバックアップする方法について説明します。  
  
   
##  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   BACKUP ステートメントは、明示的または [暗黙的](../../t-sql/statements/set-implicit-transactions-transact-sql.md) なトランザクションでは使用できません。  明示的なトランザクションとは、トランザクションの開始と終了を明示的に定義したものです。
  
##  <a name="Recommendations"></a> 推奨事項  
  
-   データベースで完全または一括ログ[復旧モデル](recovery-models-sql-server.md)を使用している場合は、データを保護し、[トランザクション ログがいっぱいになる](../logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)のを防ぐために、十分な頻度で定期的にトランザクション ログをバックアップする必要があります。 これによってログが切り捨てられ、特定の時点へのデータベースの復元がサポートされます。 
  
-   既定では、バックアップ操作が成功するたびに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログおよびシステム イベント ログにエントリが 1 つ追加されます。 ログを頻繁にバックアップすると、これらの成功メッセージがすぐに蓄積され、エラー ログが大きくなり、他のメッセージを探すのが困難になります。 そのような場合、これらのエントリに依存するスクリプトがなければ、トレース フラグ 3226 を使用することによってこれらのログ エントリを除外できます。 詳細については、「[トレース フラグ &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)」を参照してください。  
  
  
##  <a name="Permissions"></a> Permissions  
**始める前に、適切な権限があることを確認してください。** 

必要な BACKUP DATABASE 権限と BACKUP LOG 権限は、既定では、 **sysadmin** 固定サーバー ロール、 **db_owner** 固定データベース ロール、および **db_backupoperator** 固定データベース ロールのメンバーに与えられています。  
  
 バックアップ デバイスの物理ファイルに対する所有と許可の問題によって、バックアップ操作が妨げられることがあります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、デバイスに対して読み書きを実行できる必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが実行されているアカウントには書き込み権限が必要です。 ただし、システム テーブルにバックアップ デバイスのエントリを追加する [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)では、ファイル アクセスの権限は確認されません。 バックアップ デバイスの物理ファイルに対する権限の問題は、バックアップや復元を試行したときに [物理リソース](backup-devices-sql-server.md) がアクセスされるまで、表面化しない可能性があります。 そのため、始める前に権限を確認してください。
  
  
## <a name="back-up-using-ssms"></a>SSMS を使用したバックアップ  
  
1.  適切な [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスへの接続後、オブジェクト エクスプローラーでサーバー名をクリックしてサーバー ツリーを展開します。  
  
2.  **[データベース]** を展開します。さらに、そのデータベースに応じて、ユーザー データベースを選択するか、または **[システム データベース]** を展開してシステム データベースを選択します。  
  
3.  データベースを右クリックして **[タスク]** をポイントし、 **[バックアップ]** をクリックします。 **[データベースのバックアップ]** ダイアログ ボックスが表示されます。  
  
4.  **[データベース]** ボックスに、適切なデータベース名が表示されていることを確認します。 必要に応じて、このボックスの一覧から別のデータベースを選択することもできます。  
  
5.  復旧モデルが **[FULL]** または **[BULK_LOGGED]** であることを確認します。  
  
6.  **[バックアップの種類]** ボックスの一覧で、 **[トランザクション ログ]** を選択します。  
  
7.  必要に応じて、 **[コピーのみのバックアップ]** を選択して、コピーのみのバックアップを作成します。 *コピーのみのバックアップ*は、従来の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップのシーケンスから独立した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップです。 詳細については、「[コピーのみのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)」を参照してください。  
  
    >**注** **[差分]** オプションが選択されている場合、コピーのみのバックアップは作成できません。  
  
8.  **[名前]** ボックスに表示された既定のバックアップ セット名をそのまま使用するか、または別のバックアップ セット名を入力します。  
  
9. 必要に応じて、 **[説明]** ボックスに、バックアップ セットの説明を入力します。  
  
10. バックアップ セットの有効期限を指定します。  
  
    -   バックアップ セットが指定の日数後に期限切れになるようにするには、 **[期間指定]** \(既定のオプション) をクリックし、セットを作成してからセットが期限切れになるまでの日数を入力します。 0 ～ 99,999 日の値を指定できます。0 日を指定すると、バックアップ セットの有効期限は無期限になります。  
  
         既定値は、 **[サーバーのプロパティ]** ダイアログ ボックス ( **[データベースの設定]** ページ) の **[バックアップ メディアの既定の保有期間 (日)]** オプションで設定されています。 このダイアログ ボックスを開くには、オブジェクト エクスプローラーでサーバー名を右クリックし、[プロパティ] をクリックして、 **[データベースの設定]** ページを選択します。  
  
    -   バックアップ セットが特定の日付に期限切れになるようにするには、 **[日時指定]** をクリックし、セットの有効期限が切れる日付を入力します。  
  
11. **[ディスク]**、 **[URL]** 、または **[テープ]** をクリックして、バックアップ先を選択します。 1 つのメディア セットを含んでいる最大 64 個のディスク ドライブまたはテープ ドライブのパスを選択するには、 **[追加]** をクリックします。 選択したパスは、 **[バックアップ先]** ボックスの一覧に表示されます。  
  
     バックアップ先を削除するには、バックアップ先を選択して **[削除]** をクリックします。 バックアップ先の内容を表示するには、バックアップ先を選択して **[内容]** をクリックします。  
  
12. 詳細設定オプションを表示または選択するには、 **[ページの選択]** ペインの **[オプション]** をクリックします。  
  
13. 次のいずれかをクリックして、 **[メディアに上書きします]** オプションを選択します。  
  
    -   **[既存のメディア セットにバックアップする]**  
  
         このオプションでは、 **[既存のバックアップ セットに追加する]** または **[既存のすべてのバックアップ セットを上書きする]** をクリックします。 詳細については、「 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)」を参照してください。  
  
         必要に応じて、 **[メディア セット名とバックアップ セットの有効期限を確認する]** チェック ボックスをオンにします。これにより、バックアップ操作で、メディア セットとバックアップ セットの有効期限が切れる日付と時刻の確認が行われます。  
  
         必要に応じて、 **[メディア セット名]** ボックスに名前を入力します。 名前を指定しなかった場合、空の名前でメディア セットが作成されます。 メディア セット名を指定した場合は、メディア (テープまたはディスク) の実際の名前がここで入力した名前と一致しているかどうかが確認されます。  
  
         メディア名を指定せずに、このチェック ボックスをオンにしてこのメディアを確認するよう指定した場合は、実際のメディア名も空でないとエラーになります。  
  
    -   **[新しいメディア セットにバックアップし、すべての既存のバックアップ セットを消去する]**  
  
         このオプションでは、 **[新しいメディア セット名]** ボックスに名前を入力し、必要に応じて **[新しいメディア セットの説明]** ボックスにメディア セットの説明を入力します。 詳細については、「[メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)」を参照してください。  
  
14. **[信頼性]** セクションで、必要に応じて次の項目をオンにします。  
  
    -   **[完了時にバックアップを検証する]**。  
  
    -   **[メディアに書き込む前にチェックサムを行う]**、および、必要に応じて、 **[チェックサム エラーのまま続行する]**。 チェックサムの詳細については、「[バックアップ中および復元中に発生する可能性があるメディア エラー &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)」を参照してください。  
  
15. **[トランザクション ログ]** セクションで、次の手順を実行します。  
  
    -   定期的なログ バックアップの場合は、既定の選択肢の **[アクティブでないエントリを削除してトランザクション ログを切り捨てる]** のままにします。  
  
    -   ログ末尾 (アクティブなログ) をバックアップするには、 **[ログの末尾をバックアップし、データベースを復元中の状態にしておく]** をオンにします。  
  
         ログ末尾のバックアップは、作業内容が消失しないようにログの末尾をバックアップするために、エラー後に実行されます。 アクティブなログのバックアップ (ログ末尾のバックアップ) は、エラーの後とデータベースの復元開始前の両方か、またはセカンダリ データベースへのフェールオーバー時に行われます。 このオプションを選択すると、Transact-SQL の BACKUP LOG ステートメントで NORECOVERY オプションを指定した場合と同じ結果になります。 ログ末尾のバックアップの詳細については、「[ログ末尾のバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)」をご覧ください。  
  
16. **[全般]** ページの **[バックアップ先]** セクションで、テープ ドライブにバックアップするように指定した場合は、 **[バックアップ後にテープをアンロードする]** チェック ボックスがアクティブになります。 このオプションをオンにすると、 **[アンロードの前にテープを巻き戻す]** オプションがアクティブになります。  
  
17. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 以降では、 [バックアップの圧縮](../../relational-databases/backup-restore/backup-compression-sql-server.md)がサポートされています。 既定では、バックアップが圧縮されるかどうかは、 **[バックアップ圧縮の既定]** サーバー構成オプションの値によって決まります。 ただし、現在のサーバー レベルの既定の設定にかかわらず、 **[バックアップを圧縮する]** をオンにしてバックアップを圧縮することも、 **[バックアップを圧縮しない]** をオンにして圧縮しないようにすることもできます。  
  
     **現在の backup compression default 値を表示するには**  
  
    -   [backup compression default サーバー構成オプションの表示または構成](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
 **暗号化**  
  
 バックアップ ファイルを暗号化するには、 **[バックアップ ファイルを暗号化する]** チェック ボックスをオンにします。 バックアップ ファイルの暗号化に使用する暗号化アルゴリズムを選択し、証明書または非対称キーを指定します。 暗号化に使用できるアルゴリズムは次のとおりです。  
  
-   AES 128  
  
-   AES 192  
  
-   AES 256  
  
-   Triple DES  
  
 
## <a name="back-up-using-t-sql"></a>T-SQL を使用したバックアップ  
  
1.  BACKUP LOG ステートメントを実行して、トランザクション ログをバックアップします。ここでは、以下を指定します。  
  
    -   バックアップするトランザクション ログが属しているデータベースの名前。  
  
    -   トランザクション ログのバックアップが書き込まれるバックアップ デバイス。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
  
> **重要!!!** この例では、単純復旧モデルを使用する [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースを使用しています。 ただし、ログ バックアップを可能にするために、データベースの完全バックアップを行う前に、データベースが完全復旧モデルを使用するように設定されています。 詳細については、「[データベースの復旧モデルの表示または変更 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)」を参照してください。  
  
 この例では、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースのトランザクション ログ バックアップを、以前作成した名前付きバックアップ デバイスである `MyAdvWorks_FullRM_log1`に作成します。  
  
```sql  
BACKUP LOG AdventureWorks2012  
   TO MyAdvWorks_FullRM_log1;  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
  
1.  **Backup-SqlDatabase** コマンドレットを使用して **-BackupAction** パラメーターの値の **ログ** を指定します。  
  
     次の例では、 `MyDB` データベースのログのバックアップを、サーバー インスタンス `Computer\Instance`の既定のバックアップ場所に作成します。  
  
    ```sql  
    --Enter this command at the PowerShell command prompt, C:\PS>  
    Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Log  
    ```  
  
 **SQL Server PowerShell プロバイダーを設定して使用するには**  
  
-   [SQL Server PowerShell プロバイダー](../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [トランザクション ログ バックアップの復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [SQL Server データベースを特定の時点に復元する方法 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
-   [満杯になったトランザクション ログのトラブルシューティング &#40;SQL Server エラー 9002&#41;](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
## <a name="more-information"></a>詳細情報 
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [メンテナンス プラン](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [ファイルの完全バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)  
  
  
