---
title: Columns コレクション (ADOX) |Microsoft ドキュメント
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Index::Columns
- Table::Columns
- Key::Columns
- Columns
helpviewer_keywords:
- Columns collection [ADOX]
ms.assetid: 23b9fea8-4f76-4a51-95ce-1a6ce4560b34
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 65b5ae6a15ee5da44c2876c75dc21e658b50fed6
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2018
ms.locfileid: "35285201"
---
# <a name="columns-collection-adox"></a>Columns コレクション (ADOX)
すべてを含む[列](../../../ado/reference/adox-api/column-object-adox.md)テーブル、インデックス、またはキーのオブジェクト。  
  
## <a name="remarks"></a>コメント  
 [Append](../../../ado/reference/adox-api/append-method-adox-columns.md)のメソッド、**列**コレクションは ADOX に一意です。 可能な代替手段としては以下の方法があります。  
  
-   使用して、コレクションに新しい列を追加、 **Append**メソッドです。  
  
 残りのプロパティとメソッドは、standard ADO コレクションには、 可能な代替手段としては以下の方法があります。  
  
-   使用して、コレクション内の列へのアクセス、[項目](../../../ado/reference/ado-api/item-property-ado.md)プロパティです。  
  
-   使用して、コレクションに含まれる列の数を返す、[カウント](../../../ado/reference/ado-api/count-property-ado.md)プロパティです。  
  
-   使用して、コレクションから列を削除、[削除](../../../ado/reference/adox-api/delete-method-adox-collections.md)メソッドです。  
  
-   現在のデータベースのスキーマを反映するようにコレクション内のオブジェクトを更新、[更新](../../../ado/reference/ado-api/refresh-method-ado.md)メソッドです。  
  
> [!NOTE]
>  追加するときにエラーが発生、**列**を**列**のコレクション、[インデックス](../../../ado/reference/adox-api/index-object-adox.md)場合、**列**に存在しません[テーブル](../../../ado/reference/adox-api/table-object-adox.md)に既に追加されて、[テーブル](../../../ado/reference/adox-api/tables-collection-adox.md)コレクション。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [Columns コレクションのプロパティ、メソッド、およびイベント](../../../ado/reference/adox-api/columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [列とテーブル名プロパティの例 (VB) のメソッドを追加します。](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [テーブル型のプロパティの例 (VB) である接続 Close メソッド](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [キーは、メソッド、キーの種類、RelatedColumn、RelatedTable および UpdateRule プロパティの例 (VB を) 追加します。](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog プロパティの例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [SortOrder プロパティの例 (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Column オブジェクト (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)
