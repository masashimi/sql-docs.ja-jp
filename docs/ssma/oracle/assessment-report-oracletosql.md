---
title: 評価レポート (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 168b7465-a6d6-4329-b46e-fc6c5a3f2d9d
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 2dd0a63d9637a44f387c3e3f862387a8c4866d18
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2018
ms.locfileid: "40394699"
---
# <a name="assessment-report-oracletosql"></a>評価レポート (OracleToSQL)
評価レポート ウィンドウには、データベース オブジェクトの変換の結果が表示されます。[!INCLUDE[tsql](../../includes/tsql-md.md)]構文、およびヘルプの複雑さと、移行プロジェクトのコストを見積もることができます。  
  
ソース メタデータ エクスプ ローラーで変換するオブジェクトの選択、評価レポートにアクセスするを右クリックして**スキーマ**または**シノニム**、し、**レポートの作成**です。  
  
## <a name="options"></a>および  
  
|||  
|-|-|  
|項目|定義|  
|**変換の統計情報**|ステートメントの種類別の変換の統計を示します。 このウィンドウが表示されるは、スキーマなどのグループ オブジェクトまたは左側のウィンドウでコードがないオブジェクトを選択します。|  
|**カテゴリ別のオブジェクト**|カテゴリ別のオブジェクトの数を示します。 このウィンドウが表示されるは、スキーマなどのグループ オブジェクト場合にのみまたは左側のウィンドウでコードがないオブジェクトを選択します。|  
|**統計**|選択したオブジェクトの変換の統計情報を示します。 このペインは、コードの個々 のオブジェクトが左側のウィンドウで選択したときにだけ表示されます。 展開する必要があります**統計**をすぐに、**ソース**ウィンドウで、このウィンドウを表示します。|  
|**Source**|選択したオブジェクトの Oracle のコードを示しに変換されていないコードに注目[!INCLUDE[tsql](../../includes/tsql-md.md)]します。 このペインは、コードの個々 のオブジェクトが左側のウィンドウで選択したときにだけ表示されます。<br /><br />ブックマークを設定または行番号をクリックします。 ウィンドウの上部にあるボタンを使用して、コードを移動します。|  
|**移行先**|変換の結果を示しています。[!INCLUDE[tsql](../../includes/tsql-md.md)]変換されていないコードのエラー メッセージと、選択したオブジェクトのコード。 このペインは、コードの個々 のオブジェクトが左側のウィンドウで選択したときにだけ表示されます。<br /><br />ブックマークを設定または行番号をクリックします。 ウィンドウの上部にあるボタンを使用して、コードを移動します。|  
|**[メッセージ] ウィンドウ**|エラー、警告、および評価レポートを作成するときに生成された情報のメッセージを示しています。 メッセージは、番号でグループ化されます。 エラーの原因となったコードを表示するには、次のようにクリックします。**エラー**、**警告**、または**情報**、メッセージのカテゴリを展開し、メッセージをクリックします。|  
  
