---
title: セキュリティ構成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- reducing attackable surface area
- upgrading SQL Server, security
- surface area configuration [SQL Server]
- surface area configuration [SQL Server], about surface area configuration
- attackable surface area [SQL Server]
- installing SQL Server, security
ms.assetid: f741169c-1453-4ad2-830b-bf2be27d712f
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: ff538aed10cf6fa9c3ad0ae3f6fa04b223edd1dd
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43019808"
---
# <a name="surface-area-configuration"></a>セキュリティ構成
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の新規インストール時の既定の構成では、多くの機能が有効化されていません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 悪意あるユーザーの攻撃を受ける可能性がある機能を最小限にするために、主要なサービスおよび機能のみが選択的にインストールされ、起動されます。 システム管理者はインストール時のこれらの既定を変更することができ、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンス実行機能の有効化と無効化を選択的に行うこともできます。 また、別のコンピューターから接続する場合、一部のコンポーネントはプロトコルが構成されるまで使用できないことがあります。  
  
> [!NOTE]  
>  アップグレードを行う際には、新規インストールとは異なり、既存のサービスや機能を停止しないようにします。ただし、追加のセキュリティ構成オプションは、アップグレードが完了してから適用することができます。  
  
## <a name="protocols-connection-and-startup-options"></a>プロトコル、接続、およびスタートアップのオプション  
 サービスを開始または停止したり、スタートアップ オプションを構成したり、プロトコルや他の接続オプションを有効にしたりするには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用します。  
  
#### <a name="to-start-sql-server-configuration-manager"></a>SQL Server 構成マネージャーを起動するには  
  
1.  **[スタート]** メニューで、 **[すべてのプログラム]**、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。  
  
    -   コンポーネントを起動して自動開始オプションを構成するには、 **[SQL Server のサービス]** 領域を使用します。  
  
    -   接続プロトコル、固定 TCP/IP ポートなどの接続オプションを有効にしたり、暗号化を適用するには、 **[SQL Server ネットワークの構成]** 領域を使用します。  
  
 詳細については、「 [SQL Server Configuration Manager](../sql-server-configuration-manager.md)」を参照してください。 リモート接続は、ファイアウォールの構成が正しいかどうかによっても異なります。 詳細については、「 [Analysis Services のアクセスを許可するための Windows ファイアウォールの構成](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)」をご参照ください。  
  
## <a name="enabling-and-disabling-features"></a>機能の有効化と無効化  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能の有効化と無効化は [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]内のファセットを使用して構成できます。  
  
#### <a name="to-configure-surface-area-using-facets"></a>ファセットを使用してセキュリティを構成するには  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のコンポーネントに接続します。  
  
2.  オブジェクト エクスプローラーで、サーバーを右クリックし、 **[ファセット]** をクリックします。  
  
3.  **[ファセットの表示]** ダイアログ ボックスで、 **[ファセット]** の一覧を展開し、適切な **[セキュリティ構成]** ファセット (**[セキュリティ構成]**、 **[Analysis Services のセキュリティ構成]**、または **[Reporting Services のセキュリティ構成]**) を選択します。  
  
4.  **[ファセットのプロパティ]** 領域で、それぞれのプロパティに使用する値を選択します。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 ファセットの構成を定期的に確認するには、ポリシー ベースの管理を使用します。 条件と各ファセットおよびポリシーとの関係の詳細については、「 [ポリシー ベースの管理を使用したサーバーの管理](../policy-based-management/administer-servers-by-using-policy-based-management.md)」を参照してください。  
  
 `sp_configure` ストアド プロシージャを使って[!INCLUDE[ssDE](../../includes/ssde-md.md)] オプションを設定することもできます。 詳細については、「 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)構成オプションを構成する方法について説明します。  
  
 [!INCLUDE[ssRS](../../includes/ssrs.md)] の **EnableIntegrated Security** プロパティを変更するには、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のプロパティ設定を使用します。 **[定期的なイベントおよびレポート配信]** プロパティと **[Web サービスおよび HTTP アクセス]** プロパティを変更するには、 **RSReportServer.config** 構成ファイルを編集します。  
  
## <a name="command-prompt-options"></a>コマンド プロンプト オプション  
 **Invoke-PolicyEvaluation**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell コマンドレットを使用して、セキュリティ構成ポリシーを呼び出します。 詳細については、「 [データベース エンジン コマンドレットの使用](../../database-engine/use-the-database-engine-cmdlets.md)」を参照してください。  
  
## <a name="soap-and-service-broker-endpoints"></a>SOAP および Service Broker のエンドポイント  
 エンドポイントを無効にするには、ポリシー ベースの管理を使用します。 エンドポイントのプロパティを作成および変更するには、[CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql) および [ALTER ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql) を使用します。  
  
## <a name="related-content"></a>関連コンテンツ  
 [SQL Server データベース エンジンと Azure SQL Database のセキュリティ センター](security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
