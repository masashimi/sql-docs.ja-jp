---
title: クエリの実行 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC applications, executing queries
- SQL Server Native Client ODBC driver, statements
- ODBC applications, statements
- SQL Server Native Client ODBC driver, queries
- queries [ODBC]
ms.assetid: d935bcba-8ce6-4159-8395-6c86431602ad
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e6fa2c9d27ef93fe171270f89229a84323061b81
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43084571"
---
# <a name="executing-queries-odbc"></a>クエリの実行 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC アプリケーションでは、接続ハンドルを初期化してデータ ソースに接続した後、その接続ハンドルに 1 つ以上のステートメント ハンドルを割り当てます。 アプリケーションを実行できます[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ステートメント ハンドルでのステートメント。 次に、SQL ステートメントを実行するときの一般的な手順を示します。  
  
1.  必要なステートメント属性を設定します。  
  
2.  ステートメントを構築します。  
  
3.  ステートメントを実行します。  
  
4.  任意の結果セットを取得します。  
  
 アプリケーションは、SQL ステートメントから返されたすべての結果セット内にあるすべての行を取得した後、同一ステートメント ハンドルで別のクエリを実行できます。 いずれかを呼び出すと、結果セットの残りの部分を取り消すことができる場合、アプリケーションでは、特定の結果セット内のすべての行を取得する必要がないことを確認します[SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)または[SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)します。  
  
 ODBC アプリケーションで、異なるデータを使用して同じ SQL ステートメントを複数回実行する必要がある場合は、SQL ステートメントの構築時に、次のように疑問符 (?) で表されるパラメーター マーカーを使用します。  
  
```  
INSERT INTO MyTable VALUES (?, ?, ?)  
```  
  
 各パラメーター マーカーは、呼び出すプログラム変数にバインドされた[SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)します。  
  
 アプリケーションは、すべての SQL ステートメントの実行と結果セットの処理を完了後、ステートメント ハンドルを解放します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、接続ハンドルごとに複数のステートメント ハンドルをサポートしています。 また、トランザクションは接続レベルで管理されます。これにより、1 つの接続ハンドルのすべてのステートメント ハンドルで実行されるすべての作業が、同一のトランザクションの一部として管理されます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [ステートメント ハンドルの割り当て](../../relational-databases/native-client-odbc-queries/allocating-a-statement-handle.md)  
  
-   [SQL ステートメントの構築&#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/constructing-an-sql-statement-odbc.md)  
  
-   [カーソル用の SQL ステートメントの作成](../../relational-databases/native-client-odbc-queries/constructing-sql-statements-for-cursors.md)  
  
-   [ステートメント パラメーターの使用](../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)  
  
-   [ステートメントを実行する&#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
-   [ステートメント ハンドルの解放](../../relational-databases/native-client-odbc-queries/freeing-a-statement-handle.md)  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
