---
title: 式の追加 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: a60ee091-b4ed-41e1-9b6a-032c316cd03f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 22df6842a6ac787080dbc834ce3ba699c91f0ecc
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2018
ms.locfileid: "43278878"
---
# <a name="add-an-expression-report-builder-and-ssrs"></a>式の追加 (レポート ビルダーおよび SSRS)
  レポート アイテムのプロパティ、フィルター、グループ、並べ替え順、接続文字列、パラメーター値などを定義するために、レポートには随所に式が使用されます。 式は等号 (=) で始まり、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]に書き込まれます。 式は、評価結果とレポート レイアウト要素を組み合わせるレポート プロセッサによって実行時に評価されます。  
  
 式には単純式と複合式があります。 単純式は、組み込みコレクションの 1 つのアイテムを指します。 複合式には、定数、演算子、グローバル コレクションのアイテム、および関数呼び出しを含めることができます。 詳細については、「[式 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-an-expression-to-a-text-box"></a>テキスト ボックスに式を追加するには  
  
-   **[デザイン]** ビューで、式を追加するデザイン画面のテキスト ボックスをクリックします。  
  
    -   単純式の場合、テキスト ボックスに式の表示テキストを入力します。 たとえば、Sales データセット フィールドには、 `[Sales]`を入力します。  
  
    -   複合式の場合、テキスト ボックスを右クリックし、 **[式]** をクリックします。 **[式]** ダイアログ ボックスが表示されます。 式ペインの '=' の後に式を入力するか、対話形式で式を作成し、[OK] をクリックします。  
  
         式がデザイン画面に `<<Expr>>`として表示されます。  
  
## <a name="see-also"></a>参照  
 [テキストとプレースホルダーの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [テキスト ボックス &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)   
 [レポートでの式の使用 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [フィルター式の例 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)   
 [グループ式の例 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)   
 [[式] ダイアログ ボックス &#40;レポート ビルダー&#41;](http://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)   
 [式の例 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [レポートにコードを追加する &#40;SSRS&#41;](../../reporting-services/report-design/add-code-to-a-report-ssrs.md)  
  
  
