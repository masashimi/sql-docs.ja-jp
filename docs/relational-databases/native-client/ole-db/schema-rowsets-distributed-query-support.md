---
title: 分散スキーマ行セット内のクエリのサポート |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], SQL Server Native Client OLE DB provider
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
ms.assetid: 11354bb6-be42-4d8d-854c-42dd3dc38656
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f9cc4aaa6792e1876a833cbe1fdff5575d4446d7
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43075985"
---
# <a name="schema-rowsets---distributed-query-support"></a>スキーマ行セット - 分散クエリのサポート
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  サポートするために[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]分散クエリ、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー **IDBSchemaRowset**インターフェイスは、リンク サーバー上のメタデータを返します。  
  
 DBPROPSET_SQLSERVERSESSION の SSPROP_QUOTEDCATALOGNAMES プロパティが VARIANT_TRUE の場合、カタログ名には引用符で囲んだ識別子 ("my.catalog" など) を指定できます。 カタログ、スキーマ行セットの出力を制限する場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、リンク サーバーとカタログの名前を含む 2 つの部分名を認識します。 次の表のスキーマ行セットでは、2 部構成のカタログ名を *linked_server ***.*** catalog* の形式で指定することで、名前の付いたリンク サーバーの適切なカタログに出力が制限されます。  
  
|スキーマ行セット|カタログの制限|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMNS|TABLE_CATALOG|  
|DBSCHEMA_PRIMARY_KEYS|TABLE_CATALOG|  
|DBSCHEMA_TABLES|TABLE_CATALOG|  
|DBSCHEMA_FOREIGN_KEYS|PK_TABLE_CATALOG FK_TABLE_CATALOG|  
|DBSCHEMA_INDEXES|TABLE_CATALOG|  
|DBSCHEMA_COLUMN_PRIVILEGES|TABLE_CATALOG|  
|DBSCHEMA_TABLE_PRIVILEGES|TABLE_CATALOG|  
  
> [!NOTE]  
>  スキーマ行セットをリンク サーバーのすべてのカタログに制限するには、*linked_server* 構文を使用します (ピリオドを区切り文字として名前を指定します)。 この構文は、カタログ名の制限で NULL を指定する場合と同じで、カタログをサポートしないデータ ソースをリンク サーバーが示している場合にも使用されます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、リンク サーバーとして登録されている OLE DB データ ソースの一覧を返す、LINKEDSERVERS スキーマ行セットを定義します。  
  
## <a name="see-also"></a>参照  
 [スキーマ行セットのサポート &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)   
 [LINKEDSERVERS 行セット&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
