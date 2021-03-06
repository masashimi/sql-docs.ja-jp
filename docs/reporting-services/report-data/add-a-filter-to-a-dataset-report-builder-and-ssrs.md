---
title: データセットへのフィルターの追加 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-data
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: eed37e74-6a43-4d7c-9959-2d5fa6a6aba9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 199c9b89fbf55850a2a887b42ceabb013cf210f4
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2018
ms.locfileid: "43277904"
---
# <a name="add-a-filter-to-a-dataset-report-builder-and-ssrs"></a>データセットへのフィルターの追加 (レポート ビルダーおよび SSRS)
  データが外部データ ソースから取得された後に、データセットにフィルターを追加してレポート内のデータを制限できます。 データセットにフィルターを追加すると、すべてのレポート パーツまたはデータ領域では、フィルター条件に一致するデータのみが使用されます。  
  
 共有データセットの場合、すべての依存アイテムに適用されるフィルターは、レポート サーバー上の共有データセット定義の一部である必要があります。 共有データセットのインスタンスを含むレポートまたはレポート パーツは、インスタンスにのみ適用される追加のフィルターを作成できます。  
  
 フィルターを追加するには、フィルター式となる 1 つ以上の条件を指定する必要があります。 フィルター式は、フィルターの対象となるデータを識別する式、演算子、および、比較対象の値で構成されます。 フィルターの対象となるデータとその比較対象となる値とでは、データ型を一致させる必要があります。 データセットの集計値に対するフィルター処理はサポートされません。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-filter-to-a-shared-dataset"></a>共有データセットにフィルターを追加するには  
  
1.  共有データセット モードで共有データセットを開きます。  
  
2.  **[ホーム]** タブの **[共有データセット]** グループで、[データセット] をクリックします。 **[データセットのプロパティ]** ダイアログ ボックスが表示されます。  
  
3.  **[フィルター]** をクリックします。 現在のフィルター式の一覧が表示されます。 既定では、何も表示されません。  
  
4.  **[追加]** をクリックします。 新しい空のフィルター式が表示されます。  
  
5.  **[式]** で、フィルター処理の対象となるフィールドの式を入力するか、選択します。 式を編集するには、式 (*[fx]*) ボタンをクリックします。  
  
6.  リスト ボックスから、手順 5. で作成した式のデータ型と同じデータ型を選択します。  
  
7.  **[演算子]** ボックスで、 **[式]** ボックスの値と **[値]** ボックスの値とを比較するための演算子を選択します。 選択した演算子によって、次の手順で使用する値の数が異なります。  
  
8.  **[値]** ボックスで、 **[式]** の値を評価するフィルター用の式または値を入力します。  
  
     フィルター式の例については、「[フィルター式の例 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)」を参照してください。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-a-filter-to-an-embedded-dataset-or-a-shared-dataset-instance"></a>埋め込みデータセットまたは共有データセットのインスタンスにフィルターを追加するには  
  
1.  レポート デザイン モードでレポートを開きます。  
  
2.  **レポート データ** ペインでデータセットを右クリックし、 **[データセットのプロパティ]** をクリックします。 **[データセットのプロパティ]** ダイアログ ボックスが表示されます。  
  
3.  **[フィルター]** をクリックします。 現在のフィルター式の一覧が表示されます。 既定では、何も表示されません。  
  
4.  **[追加]** をクリックします。 新しい空のフィルター式が表示されます。  
  
5.  **[式]** で、フィルター処理の対象となるフィールドの式を入力するか、選択します。 式を編集するには、式 (*[fx]*) ボタンをクリックします。  
  
6.  ドロップダウン ボックスから、手順 5. で作成した式のデータ型と同じデータ型を選択します。  
  
7.  **[演算子]** ボックスで、 **[式]** ボックスの値と **[値]** ボックスの値とを比較するための演算子を選択します。 選択した演算子によって、次の手順で使用する値の数が異なります。  
  
8.  **[値]** ボックスで、 **[式]** の値を評価するフィルター用の式または値を入力します。  
  
     フィルター式の例については、「[フィルター式の例 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)」を参照してください。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [データセット フィルター、データ領域フィルター、およびグループ フィルターの追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [式の例 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [フィルターの追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-a-filter-report-builder-and-ssrs.md)  
  
  
