---
title: SharePoint 2013 への Power Pivot の移行 |Microsoft ドキュメント
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 877697915df0bd082ea4972464572f4236556e36
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2018
ms.locfileid: "34018459"
---
# <a name="migrate-power-pivot-to-sharepoint-2013"></a>SharePoint 2013 への Power Pivot の移行
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  
  
 SharePoint 2013 では、インプレース アップグレードはサポートされていません。 ただし、 **データベース接続アップグレードの手順はサポートされています**。 インプレース アップグレードとデータベース アタッチ アップグレードの 2 つの基本的なアップグレード方法をユーザーが選択できた SharePoint 2010 へのアップグレードとは動作が異なります。  
  
 SharePoint 2010 と統合された [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] のインストールを使用している場合は、SharePoint サーバーのインプレース アップグレードを行うことはできません。 ただし、SharePoint 2010 ファームから SharePoint 2013 ファームにコンテンツ データベースとサービス アプリケーション データベースを移行することは可能です。 このトピックでは、データベース接続アップグレードを完了し、 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]に関連する移行を完了するために必要な手順の概要について説明します。  
  
### <a name="migration-overview"></a>移行の概要  
  
|1|2|3|4|  
|-------|-------|-------|-------|  
|SharePoint 2013 ファームを準備する|データベースをバックアップ、コピー、および復元する|コンテンツ データベースをマウントする|[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] のスケジュールを移行する|  
||[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|- SharePoint サーバーの全体管理<br /><br /> - Windows PowerShell|- SharePoint アプリケーション ページ<br /><br /> - Windows PowerShell|  
  
##  <a name="bkmk_prepare_sharepoint2013"></a>SharePoint 2013 ファームを準備します。  
  
  > [!TIP]  
    >  既存の Web アプリケーション用に構成されている認証方法を確認します。 SharePoint 2013 Web アプリケーションの既定値は、要求ベースの認証です。 クラシック モード認証用に構成された SharePoint 2010 Web アプリケーションでは、SharePoint 2010 から SharePoint 2013 にデータベースを移行する追加の手順が必要です。 Web アプリケーションがクラシック モード認証用に構成されている場合は、SharePoint 2013 のドキュメントを確認してください。  
  
1.  新しい SharePoint Server 2013 ファームをインストールします。  
  
2.  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] サーバーのインスタンスを SharePoint モードでインストールします。 詳細については、「 [Install Analysis Services in Power Pivot Mode](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)」を参照してください。  
  
3.  SharePoint ファーム内の各サーバーで [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013 のインストール パッケージ **spPowerPivot.msi** を実行します。 詳細については、「 [Power Pivot for SharePoint アドインのインストールまたはアンインストール &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)をアンインストールするには、Analysis Services のシステム管理者であり、ローカル Administrators グループのメンバーであることが必要です。  
  
4.  SharePoint 2013 サーバーの全体管理で、前の手順で作成した SharePoint モードの [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] サーバーを使用するように Excel Services サービス アプリケーションを構成します。 詳細については、「 [Install Analysis Services in Power Pivot Mode](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)」の「基本的な Analysis Services SharePoint 統合の構成」セクションを参照してください。  
  
##  <a name="bkmk_backup_restore"></a>バックアップ、コピー、およびデータベースを復元します。  
 "SharePoint のデータベース接続アップグレード" プロセスとは、 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 関連のコンテンツとサービス アプリケーション データベースを SharePoint 2013 ファームにバックアップ、コピー、および復元する一連の手順です。  
  
1.  **データベースを読み取り専用に設定する** : [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]で、データベース名を右クリックし、 **[プロパティ]** をクリックします。 **[オプション]** ページで、 **[読み取り専用データベース]** プロパティを **[True]** に設定します。  
  
2.  **バックアップする** : SharePoint 2013 ファームに移行する各コンテンツ データベースとサービス アプリケーション データベースをバックアップします。 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]で、データベース名を右クリックし、 **[タスク]**、 **[バックアップ]** を順にクリックします。  
  
3.  データベース バックアップ ファイル (.bak) をバックアップ先サーバーにファイル コピーします。  
  
4.  **復元する** : データベースを復元先の [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]に復元します。 この手順は、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]を使用して行うことができます。  
  
5.  **データベースを読み取り/書き込み用に設定する** : **[読み取り専用データベース]** を **[False]** に設定します。  
  
##  <a name="bkmk_prepare_mount_databases"></a>Web アプリケーションとマウント コンテンツ データベースを準備します。  
 次の手順の詳細については、次を参照してください。 [SharePoint 2010 から SharePoint 2013 にデータベースをアップグレード](http://go.microsoft.com/fwlink/p/?LinkId=256690)(http://go.microsoft.com/fwlink/p/?LinkId=256690)です。  
  
1.  **データベースをオフラインにする**  
  
     SharePoint サーバーの全体管理を使用して、SharePoint 2013 の各コンテンツ データベースをオフラインにします。 コンテンツ データベースを、コピーしたデータベースに置き換えます。 使用環境にとってどのシーケンスが最適かを検討してください。 次のコンテンツ データベースをオフラインにする前に、各データベースをオフラインにして、関連する置換データベースをマウントすることを検討します。 もう 1 つの方法として、すべてのコンテンツ データベースをグループとしてオフラインにします。  
  
    1.  SharePoint サーバーの全体管理で、 **[アプリケーション構成の管理]** をクリックします。  
  
    2.  **[コンテンツ データベースの管理]** をクリックします。  
  
    3.  データベース名をクリックします。  
  
    4.  **[コンテンツ データベース設定の管理]** で、 **[データベースの状態]** を **[オフライン]** に設定します。  
  
    5.  **[コンテンツ データベースの削除]** を選択します。 コンテンツ データベースに格納されているサイトにアクセスできなくなるという警告に注意してください。  
  
-   **コンテンツ データベースをマウントする:**  
  
     移行したコンテンツ データベースをマウントするには、SharePoint 2013 管理シェルで PowerShell コマンドレットを使用します。 サービス アプリケーション データベースがマウントする必要はありません、コンテンツ データベースのみ: ![PowerShell 関連コンテンツ](../../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 関連コンテンツ")  
  
    ```  
    Mount-SPContentDatabase "SharePoint_Content_O14-KJSP1" -DatabaseServer "[server name]\powerpivot" -WebApplication [web application URL]  
    ```  
  
     詳細については、次を参照してください。[アタッチ/デタッチするコンテンツ データベース (SharePoint Server 2010)](http://technet.microsoft.com/library/ff628582.aspx) (http://technet.microsoft.com/library/ff628582.aspx)です。  
  
     **手順の完了後の状態**  : マウント操作が完了すると、前のコンテンツ データベースに格納されていたファイルが表示されます。 そのため、ユーザーはドキュメント ライブラリのブックを表示して開くことができます。  
  
    -   > [!TIP]  
        >  移行したブックの新しいスケジュールは、移行プロセスのこの時点で作成することができます。 ただし、スケジュールは、前の SharePoint ファームからコピーしたデータベースではなく、新しい [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] サービス アプリケーション データベースで作成されるため、 古いスケジュールは含められません。 前のデータベースを使用して古いスケジュールを移行する次の手順を完了すると、新しいスケジュールは使用できなくなります。  
  
### <a name="troubleshoot-issues-when-you-attempt-to-mount-databases"></a>データベースをマウントしようとすると発生する問題のトラブルシューティング  
 ここでは、データベースをマウントするときに発生する可能性のある問題についてまとめます。  
  
1.  **認証エラー** : 認証関連のエラーが発生する場合は、元の Web アプリケーションで使用している認証モードを確認します。 エラーは、SharePoint 2013 と SharePoint 2010 の Web アプリケーション間の認証の不一致によって発生する可能性があります。 詳細については、「 [1) SharePoint 2013 ファームを準備する](#bkmk_prepare_sharepoint2013) 」を参照してください。  
  
2.  **PowerPivot ファイルの不足:** [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] の .dll ファイルの不足に関連するエラーが発生する場合は、 **spPowerPivot.msi** がインストールされていないか、 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 構成ツールを使用して [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]が構成されていません。  
  
##  <a name="bkmk_upgrade_powerpivot_schedules"></a>Power Pivot のスケジュールをアップグレードします。  
 ここでは、 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] のスケジュールの移行に関する詳細とオプションについて説明します。 スケジュールを移行するには、2 つの手順を実行します。 まず、移行したサービス アプリケーション データベースを使用するように [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] サービス アプリケーションを構成します。 次に、スケジュールを移行する 2 つの方法のうちいずれかを選択します。  
  
 **移行したサービス アプリケーション データベースを使用するようにサービス アプリケーションを構成する**  
  
 SharePoint サーバーの全体管理で、コピーした前のサービス アプリケーション データベースを使用するように [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] サービス アプリケーションを構成します。 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] サービスによって、サービス アプリケーション データベースが新しいスキーマにアップグレードされます。  
  
1.  SharePoint サーバーの全体管理で **[サービス アプリケーションの管理]** をクリックします。  
  
2.  [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] サービス アプリケーション ("既定の [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] サービス アプリケーション" など) を探して、サービス アプリケーション名をクリックし、SharePoint リボンの **[プロパティ]** をクリックします。  
  
3.  データベース サーバーの名前付きインスタンスとデータベース名を、 バックアップ、コピー、および復元したデータベースの正しい名前に更新します。 **[OK]** をクリックすると、サービス アプリケーション データベースがアップグレードされます。 エラーは ULS ログに格納されます。  
  
 **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] スケジュールのアップグレード**  
  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] サービス アプリケーションを構成して、更新スケジュールを移行します。  
  
-   **スケジュールを移行するオプション 1: SharePoint ファームの管理者**  
  
    1.  SharePoint 2013 の管理の実行で、`Set-PowerPivotServiceApplication`コマンドレットと、`-StartMigratingRefreshSchedules`自動デマンド スケジュールの移行を有効にするスイッチ![PowerShell 関連コンテンツ](../../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 関連コンテンツ"). 次の Windows PowerShell スクリプトは、 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] サービス アプリケーションが 1 つだけであることを前提としています。  
  
        ```  
        $app=Get-PowerPivotServiceApplication  
        Set-PowerPivotServiceApplication $app -StartMigratingRefreshSchedules  
        ```  
  
         この Windows PowerShell スクリプトを実行すると、スケジュールがアクティブになり、次回の適切なタイミングで実行されるようになります。 ただし、定期更新ページ上の状態は有効になりません。 スケジュールは初めて実行するときに移行され、定期更新ページで **[有効]**  が [True] に変わります。  
  
    2.  StartMigratingRefreshSchedules プロパティの現在値を確認する場合は、次の PowerShell スクリプトを実行します。 このスクリプトは、すべての [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] サービス アプリケーション オブジェクトをループし、名前とプロパティ値を表示します。  
  
        ```  
        $apps = Get-PowerPivotServiceApplication  
        foreach ($app in $apps){}  
        Get-PowerPivotServiceApplication $appp | format-table -property displayname,id,StartMigratingRefreshSchedules  
        ```  
  
     **スケジュールを移行するオプション 2: ユーザーが各ブックを更新する**  
  
    1.  スケジュールを移行するもう 1 つの方法は、ブックごとに定期更新を有効にすることです。 ブックがあるドキュメント ライブラリに移動します。  
  
    2.  ショートカット メニューを開き、**[[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] のデータ更新の管理]** をクリックします。  
  
    3.  **[定期更新]** セクションで、 **[有効化]** をクリックします。  
  
    4.  **[さらに、できるだけ早く更新を行います]** を選択できます。 このオプションでは、[OK] をクリックするとすぐに更新のインスタンスが 1 つキューに追加されます。 通常の更新スケジュールも適切な時間にトリガーされます。  
  
    5.  **[OK]** をクリックします。 これで、更新ページに更新履歴が表示されるようになり、スケジュールは通常の時間に実行されます。  
  
 **SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] ブック**  
  
-   SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] ブックを [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)][!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2013 で使用している場合は、自動的にはアップグレードされません。 2008 R2 ブックが格納されたコンテンツ データベースを移行すると、ブックを使用できるようにはなりますが、スケジュールはアップグレードされません。  
  
-   詳細については、「 [ブックのアップグレードと定期データ更新 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)」を参照してください。  
  
##  <a name="bkmk_additional_resources"></a> その他のリソース  
  
> [!NOTE]  
>  [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] および SharePoint データベース アタッチ アップグレードの詳細については、以下を参照してください。  
  
-   [ブックのアップグレードと定期データ更新 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
-   [SharePoint 2013 へのアップグレード プロセスの概要](http://go.microsoft.com/fwlink/p/?LinkId=256688)(http://go.microsoft.com/fwlink/p/?LinkId=256688)です。  
  
-   [SharePoint 2013 にアップグレードする前に環境をクリーンアップする](http://go.microsoft.com/fwlink/p/?LinkId=256689)(http://go.microsoft.com/fwlink/p/?LinkId=256689)です。  
  
-   [SharePoint 2010 から SharePoint 2013 までデータベースをアップグレード](http://go.microsoft.com/fwlink/p/?LinkId=256690)(http://go.microsoft.com/fwlink/p/?LinkId=256690)です。  
  
  
