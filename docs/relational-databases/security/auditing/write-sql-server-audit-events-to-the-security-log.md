---
title: セキュリティ ログへの SQL サーバー監査イベントの書き込み | Microsoft Docs
ms.custom: ''
ms.date: 09/21/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], Security Log
- server audit [SQL Server]
- audits [SQL Server], writing to Security Log
- security logs [SQL Server]
ms.assetid: 6fabeea3-7a42-4769-a0f3-7e04daada314
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 5b21bddd4c82c6265d77ad3b031c3d8636e0904f
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43030422"
---
# <a name="write-sql-server-audit-events-to-the-security-log"></a>セキュリティ ログへの SQL サーバー監査イベントの書き込み  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

高度なセキュリティ環境では、オブジェクト アクセスを記録するイベントを書き込むのに適切な場所は Windows セキュリティ ログです。 他の監査場所は、サポートされていますが、改ざんされる可能性が高くなります。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サーバー監査を Windows セキュリティ ログに書き込むための主要な要件は 2 つあります。  
  
-   オブジェクト アクセスの監査の設定は、イベントをキャプチャするように構成する必要があります。 監査ポリシー ツール (`auditpol.exe`) は、" **オブジェクト アクセスの監査** " カテゴリでさまざまなサブポリシー設定を公開しています。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] がオブジェクト アクセスを監査できるようにするには、 **application generated** 設定を構成します。  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスを実行しているアカウントは、Windows セキュリティ ログに書き込むための " **セキュリティ監査の生成** " 権限を持っている必要があります。 既定では、LOCAL SERVICE アカウントおよび NETWORK SERVICE アカウントにこの権限があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] がこれらのアカウントのいずれかで実行されている場合、この手順は必要ありません。  
-   レジストリ ハイブ `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\EventLog\Security` への [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントに完全なアクセス許可を提供します。  

  > [!IMPORTANT]  
  > [!INCLUDE[ssnoteregistry-md](../../../includes/ssnoteregistry-md.md)]   
  
Windows の監査ポリシーは、Windows セキュリティ ログに書き込むように構成されている場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の監査に影響を与えることがあります。監査ポリシーが不適切に構成された場合は、イベントが失われる可能性があります。 通常、Windows セキュリティ ログは、古いイベントを上書きするよう設定されます。 これにより、最新のイベントが保持されます。 ただし、Windows セキュリティ ログが古いイベントを上書きするよう設定されていない場合、セキュリティ ログがいっぱいになると、システムは Windows イベント 1104 (ログがいっぱいです) を発行します。 このとき、次の点に注意してください。  
-   それ以降のセキュリティ イベントは記録されません。  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] はシステムがイベントをセキュリティ ログに記録できないことを検出できないため、監査イベントが失われる場合があります。  
-   ボックス管理者によってセキュリティ ログが修復されると、ログ動作は正常に戻ります。  
  
##  <a name="BeforeYouBegin"></a> 作業を開始する準備  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コンピューターの管理者は、セキュリティ ログのローカル設定がドメイン ポリシーによって上書きされることを理解している必要があります。 この場合、ドメイン ポリシーによってサブカテゴリ設定 (**auditpol /get /subcategory:"application generated"**) が上書きされる可能性があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の監査対象であるイベントが記録されないことを検出する方法がない場合、これがイベントをログに記録する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の機能に影響します。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 これらの設定を行うには、Windows 管理者である必要があります。  
  
##  <a name="auditpolAccess"></a> auditpol を使用して Windows のオブジェクト アクセスの監査の設定を行うには  
  
1.  管理権限を使用してコマンド プロンプトを開きます。  
  
    1.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]**、 **[アクセサリ]** の順にポイントします。次に、 **[コマンド プロンプト]** を右クリックし、 **[管理者として実行]** をクリックします。  
  
    2.  **[ユーザー アカウント制御]** ダイアログ ボックスが表示されたら、 **[続行]** をクリックします。  
  
2.  次のステートメントを実行して、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]からの監査を有効にします。  
  
    ```  
    auditpol /set /subcategory:"application generated" /success:enable /failure:enable  
    ```  
  
3.  コマンド プロンプト ウィンドウを閉じます。  
  
##  <a name="secpolAccess"></a> secpol を使用して "セキュリティ監査の生成" 権限をアカウントに許可するには  
  
1.  任意の Windows オペレーティング システムで、 **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。  
  
2.  「 **secpol.msc** 」と入力し、 **[OK]** をクリックします。 **[ユーザー アクセス制御]** ダイアログ ボックスが表示されたら、 **[続行]** をクリックします。  
  
3.  ローカル セキュリティ ポリシー ツールで、 **[セキュリティの設定]**、 **[ローカル ポリシー]** の順に展開し、 **[ユーザー権利の割り当て]** をクリックします。  
  
4.  結果ペインで **[セキュリティ監査の生成]** をダブルクリックします。  
  
5.  **[ローカル セキュリティの設定]** タブの **[ユーザーまたはグループの追加]** をクリックします。  
  
6.  **[ユーザー、コンピューター、またはグループの選択]** ダイアログ ボックスで、ユーザー アカウントの名前 ( **domain1\user1** など) を入力して **[OK]** をクリックするか、 **[詳細設定]** をクリックしてアカウントを検索します。  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
8.  セキュリティ ポリシー ツールを閉じます。  
  
9. この設定を有効にするために [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を再起動します。  
  
##  <a name="secpolPermission"></a> secpol を使用して Windows のオブジェクト アクセスの監査の設定を行うには  
  
1.  [!INCLUDE[wiprlhext](../../../includes/wiprlhext-md.md)] または Windows Server 2008 より前のオペレーティング システムでは、 **[スタート]** ボタンをクリックして、 **[ファイル名を指定して実行]** をクリックします。  
  
2.  「 **secpol.msc** 」と入力し、 **[OK]** をクリックします。 **[ユーザー アクセス制御]** ダイアログ ボックスが表示されたら、 **[続行]** をクリックします。  
  
3.  ローカル セキュリティ ポリシー ツールで、 **[セキュリティの設定]**、 **[ローカル ポリシー]** の順に展開し、 **[監査ポリシー]** をクリックします。  
  
4.  結果ペインで、 **[オブジェクト アクセスの監査]** をダブルクリックします。  
  
5.  **[ローカル セキュリティの設定]** タブの **[次の場合に監査する]** で、 **[成功]** チェック ボックスと **[失敗]** チェック ボックスの両方をオンにします。  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  セキュリティ ポリシー ツールを閉じます。  
  
## <a name="see-also"></a>参照  
 [SQL Server Audit &#40;データベース エンジン&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)  
  
  
