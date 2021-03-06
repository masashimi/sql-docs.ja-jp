---
title: sys.dm_io_cluster_shared_drives (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_io_cluster_shared_drives_TSQL
- sys.dm_io_cluster_shared_drives
- dm_io_cluster_shared_drives_TSQL
- dm_io_cluster_shared_drives
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_cluster_shared_drives dynamic management view
ms.assetid: c8fcced8-c780-49dc-99bd-6beb3ca532c4
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d2c6dbc9b88bde892cae76fdbc7405896f88a28a
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43109810"
---
# <a name="sysdmioclustershareddrives-transact-sql"></a>sys.dm_io_cluster_shared_drives (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  このビューは、現在のサーバー インスタンスがクラスター化されたサーバーの場合、各共有ドライブのドライブ名を返します。 現在のサーバー インスタンスがクラスター化されたサーバーでない場合は、空の行セットを返します。  
  
> [!NOTE]  
>  これから[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_io_cluster_shared_drives**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**DriveName**|**nchar(2)**|クラスターの共有ディスク アレイを構成する個別のディスクを表すドライブの名前 (ドライブ文字)。 列値が許容されません。|  
|**pdw_node_id**|**int**|**適用対象**: ssPDW<br /><br /> この配布であるノードの識別子。|  
  
## <a name="remarks"></a>コメント  
 クラスター化が有効な場合、フェールオーバー クラスター インスタンスには、共有ディスク上にデータ ファイルとログ ファイルが置かれ、別のノードにフェールオーバーした後アクセスできるようになっている必要があります。 このビューの各行は、クラスター化された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで使用される 1 つの共有ディスクを表します。 データを格納したり、ログ ファイルのこのインスタンスをこのビューで表示されているディスクのみを使用できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 このビューで表示されるディスクは、SQL Server インスタンスに関連付けられているクラスター リソース グループに属するディスクです。  
  
> [!NOTE]  
>  このビューは、今後のリリースでは非推奨とされます。 使用することをお勧めします。 [sys.dm_io_cluster_valid_path_names &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md)代わりにします。  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、sys.dm_io_cluster_shared_drives を使用して、クラスター サーバー インスタンスの共有デバイスを特定します。  
  
```  
SELECT * FROM sys.dm_io_cluster_shared_drives;  
```  
  
 これは、結果セットです。  
  
 DriveName  
  
 --------\-  
  
 m  
  
 n  
  
## <a name="see-also"></a>参照  
 [sys.dm_io_cluster_valid_path_names &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md)   
 [sys.dm_os_cluster_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [sys.fn_servershareddrives &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-servershareddrives-transact-sql.md)   
 [動的管理ビューおよび関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  
