---
title: ネイティブ コンパイル ストアド プロシージャの呼び出しに関するベスト プラクティス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f39fc1c7-cfec-4a95-97f6-6b95954694bb
caps.latest.revision: 8
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 3c867721b0e7868a57f4a76108e2b9029dc22172
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393938"
---
# <a name="best-practices-for-calling-natively-compiled-stored-procedures"></a>ネイティブ コンパイル ストアド プロシージャの呼び出しに関するベスト プラクティス
  ネイティブ コンパイル ストアド プロシージャの特徴:  
  
-   通常、アプリケーションのパフォーマンスが重要な部分に使用されます。  
  
-   頻繁に実行されます。  
  
-   非常に高速であることが求められます。  
  
 ネイティブ コンパイル ストアド プロシージャを使用することに伴うパフォーマンス上の利点は、プロシージャによって処理される行の数と論理の量に従って大きくなります。 たとえば、次の 1 つ以上を使用している場合は、ネイティブ コンパイル ストアド プロシージャのパフォーマンスが向上します。  
  
-   集計。  
  
-   入れ子になっているループ結合。  
  
-   複数ステートメントの SELECT、INSERT、UPDATE、および DELETE 操作。  
  
-   複合式。  
  
-   条件ステートメントとループなど、手続き型のロジック。  
  
 単一行のみを処理する必要がある場合は、ネイティブ コンパイル ストアド プロシージャを使用しても、パフォーマンス上の利点が得られるとは限りません。  
  
 サーバーによるパラメーター名のマップと型の変換を回避するには:  
  
-   プロシージャに渡されるパラメーターの型をプロシージャ定義の型に一致させます。  
  
-   ネイティブ コンパイル ストアド プロシージャを呼び出すときに序数 (名前のない) パラメーターを使用します。 最も効率的に実行するには、名前付きパラメーターを使用しないでください。  
  
 ネイティブ コンパイル ストアド プロシージャでの (非効率的な) 名前付きパラメーターの使用は、XEvent の `hekaton_slow_parameter_passing` を `reason=named_parameters` と共に使用して検出できます。  
  
 同様に、同じ xevent の一致しない型の使用を検出できます`hekaton_slow_parameter_passing`で`reason=parameter_conversion`します。  
  
 メモリ最適化テーブルを使用するときは (多くのシナリオで) 再試行ロジックを実装する必要があり、特定の機能制限に対処する必要があるため、インタープリターによって処理されるラッパー形式の [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャを作成する必要が生じることがあります。 例については、次を参照してください。 [Retry Logic for Transactions on Memory-Optimized Tables に関するガイドライン](memory-optimized-tables.md)します。  
  
## <a name="see-also"></a>参照  
 [ネイティブ コンパイル ストアド プロシージャ](natively-compiled-stored-procedures.md)  
  
  
