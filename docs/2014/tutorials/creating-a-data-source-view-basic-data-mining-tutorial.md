---
title: 作成、データ ソース ビュー (基本的なデータ マイニング チュートリアル) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c1e68a88-0f82-415d-becc-78d180d4f845
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2b64202ccd2b5f420eceeb0287407656dde1cefe
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37241842"
---
# <a name="creating-a-data-source-view-basic-data-mining-tutorial"></a>データ ソース ビューの作成 (基本的なデータ マイニング チュートリアル)
  データ ソース ビューは、データ ソース上に構築され、データのサブセットを定義します。このデータ ソース ビューを、マイニング構造で使用できます。 また、データ ソース ビューを使用して、列の追加、計算列や集計の作成、および名前付きビューの追加を行うこともできます。 データ ソース ビューを使用すると、プロジェクトに関連するデータの選択、テーブルどうしの関連付け、データの構造の変更などの操作を、元のデータ ソースを変更せずに実行できます。 詳細については、 [「多次元モデルのデータ ソース ビュー」](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)を参照してください。  
  
### <a name="to-create-a-data-source-view"></a>データ ソース ビューを作成するには  
  
1.  **ソリューション エクスプローラー**で **[データ ソース ビュー]** を右クリックし、 **[新しいデータ ソース ビュー]** をクリックします。  
  
2.  **[データ ソース ビュー ウィザードへようこそ]** ページで **[次へ]** をクリックします。  
  
3.  **[データ ソースの選択]** ページの **[リレーショナル データ ソース]** で、前回の作業で作成した [Adventure Works DW 2012] データ ソースを選択します。 **[次へ]** をクリックします。  
  
    > [!NOTE]  
    >  新しいデータ ソースを作成する場合は、 **[データ ソース]** を右クリックし、 **[新しいデータ ソース]** をクリックして、データ ソース ウィザードを開始します。  
  
4.  **[テーブルとビューの選択]** ページで次のオブジェクトを選択し、右矢印をクリックして、これらのオブジェクトを新しいデータ ソース ビューに追加します。  
  
    -   **[ProspectiveBuyer (dbo)]** : 自転車の購入見込み者のテーブル  
  
    -   **[vTargetMail (dbo)]** : 過去の自転車購入者に関する履歴データのビュー  
  
5.  **[次へ]** をクリックします。  
  
6.  既定では、Adventure Works DW 2012 という名前のデータ ソース ビューが **[ウィザードの完了]** ページに表示されます。 名を変更して`Targeted Mailing`、 をクリックし、**完了**します。  
  
     新しいデータ ソース ビューが **[Targeted Mailing.dsv [Design]]** タブで開きます。  
  
## <a name="previous-task-in-lesson"></a>このレッスンの前の作業  
 [データ ソースを作成する&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 2: 絞り込みメール構造を作成する&#40;基本的なデータ マイニング チュートリアル&#41;](../../2014/tutorials/lesson-2-building-a-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>参照  
 [ソース ビューのデータを定義する&#40;Analysis Services&#41;](../analysis-services/multidimensional-models/defining-a-data-source-view-analysis-services.md)  
  
  
