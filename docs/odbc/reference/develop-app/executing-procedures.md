---
title: プロシージャの実行 |Microsoft ドキュメント
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], executing
ms.assetid: a75e497a-4661-438a-a10e-f598c65f81be
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d61929c1d2afb756be5157f3378ff0fe6b4d7e95
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910777"
---
# <a name="executing-procedures"></a>プロシージャの実行
ODBC では、プロシージャを実行するための標準のエスケープ シーケンスを定義します。 このシーケンスおよびそれを使用するコード例の構文を参照してください。[プロシージャ呼び出し](../../../odbc/reference/develop-app/procedure-calls.md)です。  
  
 プロシージャを実行するには、アプリケーションには、次の操作を実行します。  
  
1.  すべてのパラメーターの値を設定します。 詳細については、次を参照してください。[ステートメント パラメーター](../../../odbc/reference/develop-app/statement-parameters.md)、このセクションで後述します。  
  
2.  呼び出し**SQLExecDirect**し、プロシージャを実行する SQL ステートメントを含む文字列を渡します。 このステートメントは、ODBC または DBMS に固有の構文で定義されているエスケープ シーケンスを使用できます。DBMS に固有の構文を使用するステートメントは、相互運用可能ではありません。  
  
3.  ときに**SQLExecDirect**が呼び出されると、ドライバー。  
  
    -   現在のパラメーター値を取得し、必要に応じてそれらを変換します。 詳細については、次を参照してください。[ステートメント パラメーター](../../../odbc/reference/develop-app/statement-parameters.md)、このセクションで後述します。  
  
    -   データ ソースのプロシージャを呼び出し、変換後のパラメーターの値を送信します。 ドライバーが、プロシージャを呼び出す方法と、ドライバー固有です。 データ ソースの SQL 文法を使用して、実行のためには、このステートメントを送信する SQL ステートメントが変更されることなど、DBMS のデータ ストリーム プロトコルで定義されているリモート プロシージャ コール (RPC) メカニズムを使用して直接、プロシージャを呼び出す可能性があります。  
  
    -   任意の入力/出力や出力パラメーターの値またはプロシージャが成功したと仮定した場合、プロシージャの戻り値を返します。 これらの値は、すべてその他の (行数と結果セット) で生成された結果、プロシージャが処理された後まで使用できない可能性があります。 プロシージャが失敗した場合、ドライバーはエラーを返します。
