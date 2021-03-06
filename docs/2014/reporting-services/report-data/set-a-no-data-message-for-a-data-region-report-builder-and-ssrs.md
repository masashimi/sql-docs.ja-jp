---
title: データ領域にデータがないことを示すメッセージの設定 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4b194714-46f7-4f0e-9632-7f89d9600762
caps.latest.revision: 7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e3c75fe02c7db5857f9f3977c3808df0b61f0ede
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37179209"
---
# <a name="set-a-no-data-message-for-a-data-region-report-builder-and-ssrs"></a>データ領域にデータがないことを示すメッセージの設定 (レポート ビルダーおよび SSRS)
  データのないデータ領域の代わりに表示レポートに表示するテキストを指定するときは、テーブル、マトリックス、または一覧データ領域に対して NoRowsMessage プロパティを、グラフ データ領域に対して NoDataMessage を、マップのカラー スケールに対して NoDataText を、それぞれ設定します。 実行時にレポート プロセッサによってレポートの各データセットに対しクエリが実行されますが、データセット クエリによって結果セットが生成されない場合があります。 空のデータセットにバインドされるデータ領域に対し、空のデータ領域を表示する代わりに表示するテキストを指定できます。 また、サブレポートのデータセットに実行時のデータがない場合、サブレポートに対し NoRowsMessage プロパティを設定することもできます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-the-norowsmessage-property-for-a-table-matrix-or-list"></a>テーブル、マトリックス、リストに NoRowsMessage プロパティを設定するには  
  
1.  [デザイン] ビューで、デザイン画面のテーブル、マトリックス、一覧データ領域、またはサブレポートをクリックして選択します。 選択したアイテムのプロパティがプロパティ ペインに表示されます。  
  
2.  プロパティ ペインで、メッセージとして表示するテキストを入力`NoRowsMessage`プロパティ フィールド。  
  
     または、ドロップダウン リストから **[式]** をクリックして **[式]** ダイアログ ボックスを開き、式を作成します。  
  
### <a name="to-set-the-nodatamessage-property-for-a-chart"></a>グラフに NoDataMessage プロパティを設定するには  
  
1.  [デザイン] ビューで、デザイン画面のグラフをクリックして選択します。 選択したアイテムのプロパティがプロパティ ペインに表示されます。  
  
2.  プロパティ ペインでのノードを展開`NoDataMessage`します。  
  
3.  **キャプション**、内のメッセージとして表示するテキストを入力`NoDataMessage`プロパティ フィールド。  
  
     または、ドロップダウン リストから **[式]** をクリックして **[式]** ダイアログ ボックスを開き、式を作成します。  
  
### <a name="to-set-the-norowsmessage-for-a-subreport"></a>サブレポートに NoRowsMessage を設定するには  
  
1.  [デザイン] ビューで、デザイン画面のサブレポートをクリックして選択します。 選択したアイテムのプロパティがプロパティ ペインに表示されます。  
  
2.  プロパティ ペインで、メッセージとして表示するテキストを入力`NoRowsMessage`プロパティ フィールド。  
  
     または、ドロップダウン リストから **[式]** をクリックして **[式]** ダイアログ ボックスを開き、式を作成します。  
  
### <a name="to-set-the-nodatatext-property-for-a-color-scale-for-a-map"></a>マップのカラー スケールに NoDataText プロパティを設定するには  
  
1.  [デザイン] ビューで、マップのカラー スケールをクリックして選択します。 選択したアイテムのプロパティがプロパティ ペインに表示されます。  
  
2.  プロパティ ウィンドウで `NoDataText`データ値を持たない色のラベルとして表示するテキストを入力します。  
  
     または、ドロップダウン リストから **[式]** をクリックして **[式]** ダイアログ ボックスを開き、式を作成します。  
  
## <a name="see-also"></a>参照  
 [サブレポート&#40;レポート ビルダーおよび SSRS&#41;](../report-design/subreports-report-builder-and-ssrs.md)   
 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [グラフ &#40;レポート ビルダーおよび SSRS&#41;](../report-design/charts-report-builder-and-ssrs.md)   
 [マップ &#40;レポート ビルダーおよび SSRS&#41;](../report-design/maps-report-builder-and-ssrs.md)   
 [サブレポート&#40;レポート ビルダーおよび SSRS&#41;](../report-design/subreports-report-builder-and-ssrs.md)  
  
  
