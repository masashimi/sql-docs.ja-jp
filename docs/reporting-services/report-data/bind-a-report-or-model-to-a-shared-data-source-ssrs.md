---
title: レポートを共有データ ソースにバインドする (SSRS) | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-data
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
ms.assetid: 23cc15f2-2883-48e2-bc6c-fa0ab61a2e21
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e417d14e4c46172fc93eb4f0e386d4e211dee989
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2018
ms.locfileid: "43279994"
---
# <a name="bind-a-report-to-a-shared-data-source-ssrs"></a>レポートを共有データ ソースにバインドする (SSRS)
  レポートをテスト サーバーから実稼働サーバーに移動するときなど、ファイルをローカル コンピューターに保存した後で別のレポート サーバーにアップロードする操作が必要になる場合があります。 レポートを新しいサーバーにアップロードしたときは、新しいレポート サーバー上に格納されている共有データ ソースにレポートを再バインドする必要があります。 レポートの再バインドを行わないと、レポートが新しいレポート サーバーからアクセスされたときに正常に動作しません。  
  
> [!IMPORTANT]  
>  レポートを共有データ ソースに再バインドする前に、データ ソースがレポート サーバーまたは SharePoint ライブラリに既に存在している必要があります。 データ ソースの詳細については、「[共有データ ソースを作成、変更、および削除する (SSRS)](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)」を参照してください。  
  
## <a name="to-bind-a-report-to-a-shared-data-source-on-a-report-server-running-in-native-mode"></a>ネイティブ モードで実行されているレポート サーバー上の共有データ ソースにレポートをバインドするには  
  
1.  Web ポータルで、レポート タイルの右上隅にある省略記号 (...)、**[管理]** の順にクリックします。  

2.  **[データ ソース]** をクリックします。  
  
3.  **[共有データ ソース]** をクリックし、レポートをバインドするデータ ソースに移動します。  
  
4.  データ ソースを選択し、**[保存]** をクリックします。  
  
5.  **[適用]** をクリックします。  
  
     これで選択したデータ ソースにレポートがバインドされます。  
  
## <a name="to-bind-a-report-to-a-shared-data-source-on-a-report-server-running-in-sharepoint-integrated-mode"></a>SharePoint 統合モードで実行されているレポート サーバー上の共有データ ソースにレポートをバインドするには  
  
1.  まだライブラリが開いていない場合は、クイック起動バーでライブラリの名前をクリックします。 ライブラリの名前が表示されていない場合は、 **[すべてのサイト コンテンツの表示]** をクリックし、ライブラリの名前をクリックします。  
  
2.  レポートをポイントして、下向きの矢印をクリックします。  
  
3.  **[データ ソースの管理]** をクリックします。  
  
4.  **[dataSource1]** をクリックします。  
  
5.  **[接続の種類]** 領域で、 **[共有データ ソース]** が選択されていることを確認します。  
  
6.  **[データ ソース リンク]** 領域で、省略記号ボタン ([...]) をクリックします。  
  
7.  使用するデータ ソースを探します。  
  
8.  データ ソースを選択し、 **[OK]** をクリックします。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. **[閉じる]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [SharePoint ライブラリへのドキュメントのアップロード (Reporting Services の SharePoint モード)](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)   
 [共有データ ソースを作成および管理する (Reporting Services の SharePoint 統合モード)](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76)   
 [データ接続、データ ソース、および接続文字列 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Reporting Services でサポートされるデータ ソース &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  
  
  
