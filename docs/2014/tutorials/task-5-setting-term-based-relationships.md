---
title: 'タスク 5: 用語ベースの設定のリレーションシップ |Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6569d512-637d-4f7b-82e1-1e8582278b37
caps.latest.revision: 8
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8f3718b42bfb1eb7b2736bf936311e3b0b309e92
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37214212"
---
# <a name="task-5-setting-term-based-relationships"></a>タスク 5: 用語ベースのリレーションを設定する
  このタスクでの値のいくつかの用語ベースのリレーションを定義する、 **Supplier Name**ドメイン。 用語ベースのリレーションを使用すると、ドメインの値の一部になっている用語を修正できます。 用語ベースのリレーションでは、共通する部分のスペルを除いても同一である複数の値は同一のシノニムと見なすことができます。 たとえば、 **Inc.** に修正できます**Incorporated**します。 DQS では、ナレッジの検出、クレンジング、または照合プロセスでこれらのリレーションを使用します。 参照してください[作成用語ベースのリレーション](http://msdn.microsoft.com/library/hh510404.aspx)の詳細。  
  
1.  選択**Supplier Name**で、**ドメイン リスト**します。  
  
2.  切り替えて、**用語ベースのリレーション**右ペインでタブ。  
  
3.  をクリックして**新しいリレーションを追加**テーブルにリレーションを追加するツールバーのボタンをクリックします。  
  
4.  型**Co.** の**値**フィールドと**会社**の**に修正**フィールド。  
  
5.  次の値ごとに、上記 2 つの手順を繰り返します。  
  
    |値|次に修正|  
    |-----------|----------------|  
    |Corp.|Corporation|  
    |Inc.|Incorporated|  
  
     ![用語ベースのリレーション](../../2014/tutorials/media/et-settingtermbasedrelations.jpg "用語ベースのリレーション")  
  
## <a name="next-step"></a>次の手順  
 [タスク 6: シノニムを設定する](../../2014/tutorials/task-6-setting-synonyms.md)  
  
  
