---
title: sys.dm_os_memory_pools (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_pools_TSQL
- dm_os_memory_pools
- dm_os_memory_pools_TSQL
- sys.dm_os_memory_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_pools dynamic management view
ms.assetid: 1ef053f3-c6f3-456e-82b6-26e4bd630d46
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8c814f58f327598d6e5adcdd3fb30357aa9b6009
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43062155"
---
# <a name="sysdmosmemorypools-transact-sql"></a>sys.dm_os_memory_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  インスタンスに各オブジェクトのストアの行を返します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 このビューを使用すると、キャッシュ メモリの使用状況を監視したり、無効なキャッシュ動作を識別できます。  
  
> [!NOTE]  
>  これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_os_memory_pools**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**memory_pool_address**|**varbinary(8)**|メモリ プールを表すエントリのメモリ アドレス。 NULL 値は許可されません。|  
|**pool_id**|**int**|プールのセット内にある特定プールの ID。 NULL 値は許可されません。|  
|**type**|**nvarchar(60)**|オブジェクト プールの種類。 NULL 値は許可されません。 詳細については、次を参照してください。 [sys.dm_os_memory_clerks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)します。|  
|**name**|**nvarchar (256)**|システムによって割り当てられた、メモリ オブジェクトの名前。 NULL 値は許可されません。|  
|**max_free_entries_count**|**bigint**|プールに含めることができる空きエントリの最大数。 NULL 値は許可されません。|  
|**free_entries_count**|**bigint**|現在プール内にある空きエントリ数。 NULL 値は許可されません。|  
|**removed_in_all_rounds_count**|**bigint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの起動後、プールから削除されたエントリ数。 NULL 値は許可されません。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]が必要です、`VIEW DATABASE STATE`データベースの権限。   

## <a name="remarks"></a>コメント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントは、場合によってキャッシュの同種でステートレスな種類のデータに共通のプール フレームワークを使用します。 プール フレームワークは、キャッシュ フレームワークよりも単純です。 プール内のすべてのエントリは、等しいと見なされます。 内部的には、プールはメモリ クラークであり、メモリ クラークが使用される場所で使用できます。  
  
## <a name="see-also"></a>参照  
 
  [SQL Server オペレーティング システム関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


