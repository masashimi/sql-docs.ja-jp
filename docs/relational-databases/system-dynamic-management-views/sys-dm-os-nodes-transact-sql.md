---
title: sys.dm_os_nodes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 02/13/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_nodes
- dm_os_nodes_TSQL
- dm_os_nodes
- sys.dm_os_nodes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_nodes dynamic management view
ms.assetid: c768b67c-82a4-47f5-850b-0ea282358d50
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e5a330b4da627c74368f032aa89120156c09da31
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43061993"
---
# <a name="sysdmosnodes-transact-sql"></a>sys.dm_os_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

SQLOS という内部コンポーネントは、ハードウェア プロセッサの局所性を疑似的に表現したノード構造を作成します。 使用してこれらの構造を変更できる[ソフト NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md)カスタム ノード レイアウトを作成します。  

> [!NOTE]
> 以降で[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]特定のハードウェア構成のソフト NUMA が自動的に使用します。 詳細については、次を参照してください。[自動ソフト NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md#automatic-soft-numa)します。
  
次の表では、これらのノードに関する情報を示します。  
  
> [!NOTE]
> この DMV からの呼び出しに[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_os_nodes**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|node_id|**smallint**|ノードの ID。|  
|node_state_desc|**nvarchar (256)**|ノード状態の説明。 相互排他的な値から先に表示され、続けて、組み合わせ可能な値が表示されます。 以下に例を示します。<br /> Online、Thread Resources Low、Lazy Preemptive<br /><br />次の 4 つの相互に排他的な node_state_desc 値があります。 以下の説明が表示されます。<br /><ul><li>ノードがオンラインでオンラインにします。<li>ノードがオフライン オフラインです。<li>アイドル状態: ノードは、保留中の作業の要求がなくがアイドル状態の状態になった。<li>IDLE_READY: ノードは、保留中の作業の要求がないとがアイドル状態になります。</li></ul><br />その説明を以下に示す 3 つの組み合わせ可能な node_state_desc 値があります。<br /><ul><li>DAC: このノードが用に予約された[専用管理者接続](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)します。<li>THREAD_RESOURCES_LOW: 新しいスレッドを作成できませんこのノードでメモリ不足状態が原因です。<li>ホット追加されました。 は、ノードが応答に追加されたことを示します、ホット アド CPU イベントです。</li></ul>|  
|memory_object_address|**varbinary(8)**|このノードに関連付けられているメモリ オブジェクトのアドレス。 一対一の関係に[sys.dm_os_memory_objects](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md).memory_object_address します。|  
|memory_clerk_address|**varbinary(8)**|このノードに関連付けられているメモリ クラークのアドレス。 一対一の関係に[sys.dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).memory_clerk_address します。|  
|io_completion_worker_address|**varbinary(8)**|このノードの IO 完了に割り当てられているワーカーのアドレス。 一対一の関係に[sys.dm_os_workers](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).worker_address します。|  
|memory_node_id|**smallint**|このノードが属しているメモリ ノードの ID。 多対一の関係に[sys.dm_os_memory_nodes](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-nodes-transact-sql.md).memory_node_id します。|  
|cpu_affinity_mask|**bigint**|このノードに関連付けられている CPU を識別するビットマップ。|  
|online_scheduler_count|**smallint**|このノードによって管理されるオンライン スケジューラの数。|  
|idle_scheduler_count|**smallint**|アクティブなワーカーの存在しないオンライン スケジューラの数。|  
|active_worker_count|**int**|このノードによって管理されるすべてのスケジューラ上のアクティブ ワーカーの数。|  
|avg_load_balance|**int**|このノード上のスケジューラあたりの平均タスク数。|  
|timer_task_affinity_mask|**bigint**|タイマー タスクの割り当てが可能なスケジューラを識別するビットマップ。|  
|permanent_task_affinity_mask|**bigint**|永続的なタスクの割り当てが可能なスケジューラを識別するビットマップ。|  
|resource_monitor_state|**bit**|各ノードには、1 つのリソース モニターが割り当てられます。 リソース モニターの状態には、実行中とアイドル状態とがあります。 1 は実行中を、0 はアイドル状態を表します。|  
|online_scheduler_mask|**bigint**|このノードのプロセス関係マスクを識別します。|  
|processor_group|**smallint**|このノードのプロセッサ グループを識別します。|  
|cpu_count |**int** |このノードの利用可能な Cpu の数。 |
|pdw_node_id|**int**|この配布であるノードの識別子。<br /><br /> **適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]が必要です、`VIEW DATABASE STATE`データベースの権限。   

## <a name="see-also"></a>参照    
 [SQL Server オペレーティング システム関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [ソフト NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
