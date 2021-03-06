---
title: Blob と OLE オブジェクト |Microsoft Docs
description: BLOB と OLE オブジェクト
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-blobs
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- OLE DB Driver for SQL Server, BLOBs
- large data, OLE objects
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 52c1793b315e89770efaae9cedca7b4da730c71c
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43034950"
---
# <a name="blobs-and-ole-objects"></a>BLOB と OLE オブジェクト
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server で公開されている **ISequentialStream** インターフェイスにより、コンシューマーはバイナリ ラージ オブジェクト (BLOB) として [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の **ntext** 型、**text** 型、**image** 型、**varchar(max)** 型、**nvarchar(max)** 型、**varbinary(max)** 型、および XML 型にアクセスできます。 **ISequentialStream** の **Read** メソッドを使用すると、扱いやすい単位で大量のデータを取得できます。  
  
 この機能を示すサンプルについては、次を参照してください。[大量のデータを設定&#40;OLE DB&#41;](../../oledb/ole-db-how-to/set-large-data-ole-db.md)します。  
  
 コンシューマーからデータ変更用にバインドされたアクセサーにインターフェイス ポインターを渡すとき、OLE DB Driver for SQL Server は、コンシューマーに実装された **IStorage** インターフェイスを使用できます。  
  
 大きな値データ型の場合、OLE DB Driver for SQL Server では、**IRowset** インターフェイスや DDL インターフェイスで型の想定サイズの確認が行われます。 **varchar** 型、**nvarchar** 型、および **varbinary** データ型の列の最大サイズが無制限に設定されている場合、列のデータ型を返すスキーマ行セットおよびインターフェイスによって列は ISLONG と表されます。  
  
 OLE DB Driver for SQL Server では、**varchar(max)** 型、**varbinary(max)** 型、および **nvarchar(max)** 型が、それぞれ DBTYPE_STR、DBTYPE_BYTES、および DBTYPE_WSTR として公開されます。  
  
 このようなデータ型を使用して作業するために、アプリケーションでは次のような操作を行えます。  
  
-   データ型 DBTYPE_STR、DBTYPE_BYTES、または DBTYPE_WSTR としてバインドします。 バッファーのサイズが十分でない場合、これらのデータ型は以前のリリースでの動作と同様に (以前よりも大きな値を格納できるようになりましたが)、切り捨てが行われます。  
  
-   データ型としてバインドし、DBTYPE_BYREF も指定します。  
  
-   DBTYPE_IUNKNOWN としてバインドし、ストリーミングを使用します。  
  
 DBTYPE_IUNKNOWN にバインドすると、ISequentialStream ストリーム機能が使用されます。 OLE DB Driver for SQL Server では、大きな値データ型の DBTYPE_IUNKNOWN としてバインドの出力パラメーターをサポートします。 これは、ストアド プロシージャが、クライアントに DBTYPE_IUNKNOWN として返される、戻り値としてこれらのデータ型を返すシナリオをサポートします。  
  
## <a name="storage-object-limitations"></a>ストレージ オブジェクトの制限事項  
  
-   OLE DB Driver for SQL Server では、1 つ開いているストレージ オブジェクトのみをサポートできます。 複数の **ISequentialStream** インターフェイス ポインターへの参照を取得するために、複数のストレージ オブジェクトを開こうとすると、DBSTATUS_E_CANTCREATE が返されます。  
  
-   OLE DB Driver for SQL Server の読み取り専用プロパティ DBPROP_BLOCKINGSTORAGEOBJECTS の既定値は VARIANT_TRUE です。 そのため、ストレージ オブジェクトがアクティブの場合は、(ストレージ オブジェクト以外の) 一部のメソッドが失敗して E_UNEXPECTED が返されます。  
  
-   コンシューマーに実装されたストレージ オブジェクトを参照する行アクセサーを作成するときは、そのオブジェクトのデータ長を OLE DB Driver for SQL Server 側で認識しておく必要があります。 コンシューマー側では、アクセサーの作成に使用する DBBINDING 構造体に長さのインジケーターをバインドする必要があります。  
  
-   行に 1 つの大きなデータ値とそれ以外のデータが格納されていて、DBPROP_ACCESSORDER が DBPROPVAL_AO_RANDOM ではない場合は、OLE DB Driver for SQL Server のカーソルに対応した行セットを使用して行のデータを取得するか、すべての大きなデータ値を処理してから行の他の値を取得する必要があります。 DBPROP_ACCESSORDER が DBPROPVAL_AO_RANDOM の場合、OLE DB Driver for SQL Server によりすべての XML データ型がバイナリ ラージ オブジェクト (BLOB) としてキャッシュされ、それらに任意の順序でアクセスできます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [大きなデータの取得](../../oledb/ole-db-blobs/getting-large-data.md)  
  
-   [大きなデータの設定](../../oledb/ole-db-blobs/setting-large-data.md)  
  
-   [BLOB 出力パラメーターのストリーミング サポート](../../oledb/ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server のプログラミング](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)        
 [大きな値の型の使用](../../oledb/features/using-large-value-types.md)  
  
  
