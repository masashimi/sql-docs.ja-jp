---
title: レポート、レポート パーツ、およびレポート定義 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- report definitions
- reports
ms.assetid: 2d746550-f8cc-4e97-8a06-d0f03cffc18d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a931367813e3fb474bba65648d5d93fbc02af10a
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2018
ms.locfileid: "43265686"
---
# <a name="reports-report-parts-and-report-definitions-report-builder-and-ssrs"></a>レポート、レポート パーツ、およびレポート定義 (レポート ビルダーおよび SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 初期定義、パブリッシュされたレポート、ユーザーに表示される表示レポートなど、改ページ調整されたレポートの異なる状態を示すさまざまな用語が使用されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-definition-rdl-files"></a>レポート定義 (.rdl) ファイル  
 レポート定義は、レポート ビルダーまたはレポート デザイナーで作成するファイルです。 このファイルには、データ ソース接続、データ取得に使用するクエリ、式、パラメーター、画像、テキスト ボックス、テーブルなど、デザイン時にレポートに含めるあらゆる要素についての完全な説明が記述されます。 レポート定義は複雑になることがありますが、最小のレポート定義では、クエリと他のレポート コンテンツ、レポートのプロパティ、およびレポートのレイアウトが指定されます。  
  
 レポート定義は、実行時に処理済みレポートとして表示されます。 その時点で、レポート定義の説明に従って、データがデータ ソースから取得されて書式設定されます。 レポート定義は、コンピューターから直接実行してローカルに保存することも、他のユーザーが実行できるようにレポート サーバーにパブリッシュすることもできます。  
  
 レポート定義は、レポート定義言語 (RDL) と呼ばれる XML 文法に準拠した XML で記述されます。 RDL は、レポートで使用可能なすべてのバリエーションを表す XML 要素を記述します。  
  
## <a name="client-report-definition-rdlc-files"></a>クライアント レポート定義 (.rdlc) ファイル  
 Visual Studio のレポート デザイナーでは、ReportViewer コントロールで使用するクライアント レポート定義 (.rdlc) ファイルが生成されます。 この .rdlc ファイルは、Reporting Services のレポート デザイナーで使用する .rdl ファイルに変換できます。  
  
## <a name="report-part-rsc-files"></a>レポート パーツ (.rsc) ファイル  
 レポート パーツは、他のレポートに含めることができる、レポート サーバー上に格納された自己完結型のレポート アイテムです。 レポート パーツ ギャラリーでパーツを参照し、選択したパーツをレポートに追加するには、レポート ビルダーを使用します。 レポート パーツをレポート パーツ ギャラリーで使用できるように保存するには、レポート デザイナーまたはレポート ビルダーを使用します。  
  
 レポート パーツ定義は、レポート定義ファイルの XML フラグメントです。 レポート パーツを作成するには、レポート定義を作成し、そのレポート内のレポート アイテムを選択して、レポート パーツとして個別にパブリッシュします。 レポート パーツには、データ領域、四角形とそれに含まれているアイテム、画像などがあります。 レポート パーツと共に依存データセットおよび共有データ ソース参照を保存して、他のレポートで再利用できます。  
  
 詳細については、「[レポート パーツ (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)」および「[レポート デザイナーでのレポート パーツ (SSRS)](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md)」を参照してください。  
  
## <a name="published-reports"></a>パブリッシュされたレポート  
 作成した .rdl ファイルは、ローカルに保存することも、レポート サーバーの個人フォルダー ([個人用レポート] フォルダーなど) に保存することもできます。 レポートを他のユーザーに見せる準備ができたら、レポート ビルダーからレポート サーバーのパブリック フォルダーに保存するか、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web ポータルを使用してアップロードするか、レポート デザイナーからレポート プロジェクト ソリューションを配置することでパブリッシュします。 パブリッシュされたレポートとは、レポート サーバー データベースに保存され、レポート サーバーまたは SharePoint サイトで管理されるアイテムです。  
  
 パブリッシュされたレポートのセキュリティは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のロールベースのセキュリティ モデルを使用したロールの割り当てによって確保されます。 パブリッシュされたレポートにアクセスするには、URL、SharePoint Web パーツ、または [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web ポータルを使用します。また、レポート ビルダーでレポートの場所に移動して開くこともできます。  
  
### <a name="report-snapshots"></a>レポート スナップショット  
 レポートは、レイアウト情報とレポートが最初に実行された時点のデータの両方を含むスナップショットとしてパブリッシュすることもできます。 レポート スナップショットは、特定の表示形式では保存されません。 その代わりに、レポート スナップショットは、ユーザーまたはアプリケーションが要求したときのみ、最終的な表示形式 (HTML など) で表示されます。 詳細については、[Web ポータルを使用したレポートの検索と表示](../report-builder/finding-and-viewing-reports-with-a-browser-report-builder-and-ssrs.md)に関するページを参照してください。  
  
## <a name="rendered-reports"></a>表示レポート  
 表示レポートは、表示に適した形式 (HTML など) で、データおよびレイアウト情報の両方を含む完全に処理されたレポートです。 レポートは出力形式に変換しないと、表示されません。 レポートを表示するには、次のいずれかの操作を実行します。  
  
-   レポート ビルダーまたはレポート デザイナーでレポートを作成するか開いて、レポートを実行します。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web ポータルでレポートを検索して実行します。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーと統合されている SharePoint サイト上でレポートを検索して実行します。  
  
-   レポートをサブスクライブします。このレポートは、指定した出力形式で電子メールの受信トレイまたはファイル共有に配信されます。  
  
 レポートをサブスクライブします。このレポートは、指定した出力形式で電子メールの受信トレイまたはファイル共有に配信されます。 レポートの既定の表示形式は HTML 4.0 です。 HTML に加えて、Excel、Word、XML、PDF、TIFF、CSV などのさまざまな出力形式でレポートを表示できます。 パブリッシュされたレポートと同様に、表示レポートは、レポート サーバーに戻って編集したり保存することはできません。 詳細については、「 [レポートのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [レポート作成の概念 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/report-authoring-concepts-report-builder-and-ssrs.md)   
 [SQL Server 2016 のレポート ビルダー](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
 [レポートの検索、表示、管理 (レポート ビルダーおよび SSRS)](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [レポートのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
