---
title: '[パラメーター] ([データセットのプロパティ] ダイアログ ボックス) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "10150"
- sql12.rtp.rptdesigner.datasetproperties.parameters.f1
ms.assetid: 43b00aab-e2c3-4e85-abe1-a2b5a21efeed
caps.latest.revision: 39
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 551372ad850f94ea12f8970a6a24bbf5693fcad0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37247912"
---
# <a name="dataset-properties-dialog-box-parameters"></a>[パラメーター] ([データセットのプロパティ] ダイアログ ボックス)
  **[データセットのプロパティ]** ダイアログ ボックスの **[パラメーター]** を選択すると、クエリ パラメーター (レポート パラメーターにリンクするクエリ パラメーターを含む) の追加、変更、および削除を実行できます。  
  
 [クエリ] タブでクエリが変更されるたびに、クエリ コマンドが解析されます。 識別されたクエリ パラメーターごとに、大文字と小文字の区別も含めて同じ名前のレポート パラメーターが作成されます。 既定では、クエリ パラメーターは自動的にクエリ パラメーターの一覧に追加され、対応するレポート パラメーターにリンクされます。  
  
 レポート パラメーターの既定値が、クエリ パラメーターにリンクする別のレポート パラメーターに依存している場合は、( **[レポート パラメーターのプロパティ]** ダイアログ ボックスに表示されている) レポート パラメーターの順序が重要になります。 一覧で後方にあるレポート パラメーターは、一覧で前方にあるレポート パラメーターを参照できます。 レポート パラメーターの詳細については、次を参照してください。[レポート パラメーター&#40;レポート ビルダーおよびレポート デザイナー&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)します。  
  
## <a name="options"></a>および  
 **[追加]**  
 一覧に新しいパラメーターを追加します。  
  
 **削除**  
 選択したパラメーターを一覧から削除します。  
  
 **[パラメーター名]**  
 **[データセットのプロパティ]** ダイアログ ボックスの **[クエリ]** タブでデータセットに追加したクエリ パラメーターの名前を入力します。  
  
 **[パラメーター値]**  
 クエリ パラメーターの値を入力します。 この値には、静的な値、またはレポート内のオブジェクトを参照するがレポート アイテムやフィールドは参照できない式を指定できます。 既定では、 **[値]** に、レポート パラメーターを参照する式が設定されています。  
  
 **上矢印**  
 選択したパラメーターを一覧内で上に移動します。  
  
 **下矢印**  
 選択したパラメーターを一覧内で下に移動します。  
  
## <a name="see-also"></a>参照  
 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [レポートにデータを追加&#40;レポート ビルダーおよび SSRS&#41;](report-datasets-ssrs.md)   
 [レポート パラメーターの順序を変更&#40;レポート ビルダーおよび SSRS&#41;](../report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)  
  
  
