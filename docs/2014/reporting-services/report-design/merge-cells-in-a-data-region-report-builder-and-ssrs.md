---
title: データ領域内のセルの結合 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 43551300-89b2-4f4e-af09-69084324afaf
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: a05f5b165c72fa57795d22b2dc86d8dac616268b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37198532"
---
# <a name="merge-cells-in-a-data-region-report-builder-and-ssrs"></a>データ領域内のセルの結合 (レポート ビルダーおよび SSRS)
  データ領域内のセルを結合すると、セルとセルの合成や、データ領域の外観の向上のほか、複数の列グループおよび行グループにまたがるラベルの指定が可能になります。  
  
> [!NOTE]  
>  セルは、コーナー、列ヘッダー、グループ定義 (または行ヘッダー)、および本文など、データ領域の各領域内でのみ結合できます。 領域の境界を越えるセルを結合することはできません。 たとえば、データ領域のコーナー領域のセルと行グループ領域のセルを結合することはできません。 Tablix 領域の詳細については、次を参照してください。[一覧&#40;レポート ビルダーおよび SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-merge-cells-in-a-data-region"></a>データ領域内のセルを結合するには  
  
1.  レポート デザイン画面上のデータ領域で、結合する最初のセルをクリックします。 マウスの左ボタンを押したまま垂直方向または水平方向にドラッグして、隣接するセルを選択します。 選択したセルは強調表示されます。  
  
2.  選択したセルを右クリックし、 **[セルの結合]** を選択します。 選択したセルが 1 つのセルに結合されます。  
  
3.  手順 1. と手順 2. を繰り返し、データ領域内で隣接する他のセルを結合します。  
  
## <a name="see-also"></a>参照  
 [Tablix データ領域 &#40;レポート ビルダーおよび SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [テーブル &#40;レポート ビルダーおよび SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [マトリックス &#40;レポート ビルダーおよび SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [一覧 &#40;レポート ビルダーおよび SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [一覧 &#40;レポート ビルダーおよび SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
