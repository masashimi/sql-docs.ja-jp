---
title: バインドされたテキスト列と Image 列にバインドされていない |Microsoft Docs
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
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: ffd3442e-d880-46e9-b848-2365a09a2406
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8439982e197354dc786a82ea627500975d870f3c
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43091105"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>バインドされたtext、image 型の列とバインドされない text、image 型の列
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  サーバー カーソルを使用する場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーにバインドされていないため、データを転送しないように最適化された**テキスト**、 **ntext**、または**イメージ**列で、時間**SQLFetch**が実行されます。 **テキスト**、 **ntext**、または**イメージ**データは実際には取得されません、サーバーからアプリケーションの問題まで[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)用、列です。  
  
 多くのアプリケーションを作成できるようにありません**テキスト**、 **ntext**、または**イメージ**中に、ユーザーがカーソル内を上下スクロール単にデータが表示されます。 アプリケーションが呼び出すことができますし、ユーザーは、詳細を表示する行を選択するときに**SQLGetData**を取得する、**テキスト**、 **ntext**、または**イメージ**データ。 これにより、送信、**テキスト**、 **ntext**、または**イメージ**ユーザーの選択、およびことができますがない行のいずれかのデータが非常に大きな転送を防ぐ大量のデータ。  
  
## <a name="see-also"></a>参照  
 [テキストとイメージの列の管理](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [カーソル動作](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
