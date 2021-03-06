---
title: AddNew を使用してレコードを追加する |Microsoft ドキュメント
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: cab4adff-f22f-4fb1-9217-f8138c795268
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 36827d102d7e6ef0850c557eb6555135343fbec0
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2018
ms.locfileid: "35270091"
---
# <a name="adding-records-using-addnew-method"></a>AddNew メソッドを使用してレコードを追加します。
これは、基本的な構文、 **AddNew**メソッド。

 *レコード セット*です。AddNew *FieldList*、*値*

 *FieldList*と*値*引数が必要です。 *フィールド リスト*は、単一の名前か名前の配列。 または、新しいレコードにフィールドの序数位置。

 *値*引数 1 つの値か、新しいレコードのフィールドの値の配列です。

 通常、1 つのレコードを追加する場合にを呼び出す、 **AddNew**メソッドを引数なし。 具体的を呼び出す**AddNew**以外の設定、**値**それぞれの新しいレコードのフィールドを呼び出す**更新**または**UpdateBatch**、または両方とも。 できるようにする、**レコード セット**を使用して新しいレコードの追加をサポートしている、**サポート**を持つプロパティ、 **adAddNew**列挙型定数。

 次のコードでは、この手法を使用して、サンプルを新しい配送会社を追加する**Recordset**です。 SQL Server では、運送フィールドの値を自動的に提供します。 したがって、コードは、新しいレコードのフィールド値を指定するは試みません。

```
'BeginAddNew1.1
If objRs.Supports(adAddNew) Then
    With objRs
        .AddNew
        .Fields("CompanyName") = "Sample Shipper"
        .Fields("Phone") = "(931) 555-6334"
        .Update
    End With
End If
'EndAddNew1.1
```

## <a name="remarks"></a>コメント
 このコードを使用して、切断されているため**Recordset**バッチ モードでクライアント側カーソルでは、再接続する必要があります、 **Recordset**を新しいデータ ソースに**接続**オブジェクトを呼び出す前に、 **UpdateBatch**データベースへの変更を行うメソッドです。 新しい関数を使用してこれを簡単に行う**GetNewConnection**です。
