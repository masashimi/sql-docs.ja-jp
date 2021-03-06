---
title: Excel の行制限の回避 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a4c8700b-bef5-4440-a99c-bba5dcc46bfd
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 041872122516c411e7b02b7dde85c248600904cc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37260468"
---
# <a name="work-around-the-excel-row-limitation"></a>Excel の行制限を回避する
  このトピックでは、Excel にレポートをエクスポートときに Excel 2003 の行制限を回避する方法について説明します。 回避策は、テーブルのみを含むレポート向けのものです。  
  
 Excel 2003 でサポートされる行数は、ワークシートあたり最大 65,536 行です。 この制限を回避するには、特定の行数の後に明示的な改ページを適用します。 Excel レンダラーでは、それぞれの明示的な改ページごとに、新しいワークシートが作成されます。  
  
### <a name="to-create-an-explicit-page-break"></a>明示的な改ページを作成するには  
  
1.  [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] またはレポート マネージャーでレポートを開きます。  
  
2.  テーブルのデータ行を右クリックし、 **[グループの追加]**  >  **[親グループ]** の順にクリックして、外部テーブルのグループを追加します。  
  
     ![親グループの選択](../media/datarow-selectparentgroup.png "親グループの選択")  
  
3.  次の式を **[グループ化]** の式ボックスに入力し、 **[OK]** をクリックして、親グループを追加します。  
  
     =Int((RowNumber(Nothing)-1)/65000)  
  
     この式によって、データセット内の 65,000 行ごとに数値が割り当てられます。 グループに改ページが定義されている場合は、この式の結果として、65,000 行ごとに改ページが行われます。  
  
     外部テーブルのグループを追加すると、レポートにグループ列が追加されます。  
  
4.  グループ列を削除するには、列ヘッダーを右クリックし、 **[列の削除]** をクリックして、 **[列のみの削除]** を選択します。その後で、 **[OK]** をクリックします。  
  
     ![グループ列の削除](../media/groupcolumn-delete-updated.png "グループ列の削除")  
  
5.  **[行グループ]** の **[グループ 1]** を右クリックし、 **[グループ プロパティ]** をクリックします。  
  
     ![グループのプロパティの表示](../media/groupproperties-updated.png "グループのプロパティの表示")  
  
6.  **[グループ プロパティ]** ダイアログ ボックスの **[並べ替え]** ページで、既定の並べ替えオプションを選択し、 **[削除]** をクリックします。  
  
     ![既定の並べ替えの削除](../media/groupproperties-sorting-updated.png "既定の並べ替えの削除")  
  
7.  **[改ページ]** ページで、 **[グループの各インスタンスの間]** をクリックし、 **[OK]** をクリックします。  
  
     ![改ページの設定](../media/groupproperties-pagebreaks-updated.png "改ページの設定")  
  
8.  レポートを保存します。 Excel にレポートをエクスポートするとき、複数のワークシートへのエクスポートが行われ、各ワークシートには最大で 65,000 行が含まれます。  
  
  
