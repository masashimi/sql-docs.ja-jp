---
title: "ステートメント ハンドル |Microsoft ドキュメント"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 65d6d78b-a8c8-489a-9dad-f8d127a44882
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 64c949c8b3b3c794d6089ff159e597aeec02cfed
ms.contentlocale: ja-jp
ms.lasthandoff: 09/09/2017

---
# <a name="statement-handles"></a>ステートメント ハンドル
A*ステートメント*を最も簡単に考えるの SQL ステートメントとしてなど**選択\*から従業員**です。 ただし、ステートメントは、SQL ステートメントでは単 — のすべての結果セットが、ステートメントによって作成された、ステートメントの実行で使用されるパラメーターなど、その SQL ステートメントに関連付けられた情報で構成されます。 ステートメントは、アプリケーション定義の SQL ステートメントでもは必要ありません。 カタログなどの関数とではたとえば、 **SQLTables**が実行されるテーブル名の一覧を返す定義済みの SQL ステートメントを実行して、ステートメントでします。  
  
 各ステートメントは、ステートメント ハンドルによって識別されます。 ステートメントが 1 つの接続に関連付けられて、その接続で複数のステートメントがあります。 一部のドライバー サポート; のアクティブなステートメントの数を制限します。オプション、SQL_MAX_CONCURRENT_ACTIVITIES **SQLGetInfo**単一の接続でドライバーをサポートしている数のアクティブなステートメントを指定します。 ステートメントは、定義*active*結果保留中の場合は、ここで結果は結果セットまたは影響を受ける行の数、**挿入**、**更新**、または**削除**ステートメント、またはデータが複数の呼び出しで送信される**SQLPutData**です。  
  
 ODBC ドライバー マネージャー (ドライバー) を実装するコード内では、ステートメント ハンドルは、ステートメントの情報を含む構造体を識別します。  
  
-   ステートメントの状態  
  
-   現在のステートメント レベルの診断  
  
-   アプリケーション変数のアドレスが、ステートメントのパラメーターにバインドされ、結果セット列  
  
-   各ステートメント属性の現在の設定  
  
 ステートメント ハンドルは、ほとんどの ODBC 関数で使用されます。 特に、パラメーターをバインドし、結果セット列に関数で使用されます (**SQLBindParameter**と**SQLBindCol**)、準備のステートメントを実行 (**SQLPrepare**、 **SQLExecute**、および**SQLExecDirect**)、メタデータの取得 (**SQLColAttribute**と**SQLDescribeCol**)、フェッチ結果 (**SQLFetch**)、および診断の取得 (**SQLGetDiagField**と**SQLGetDiagRec**)。 カタログ関数で使用されることも (**SQLColumns**、 **SQLTables**など) とその他の関数の数。  
  
 ステートメント ハンドルが割り当てられます**SQLAllocHandle**およびに解放された**SQLFreeHandle**です。