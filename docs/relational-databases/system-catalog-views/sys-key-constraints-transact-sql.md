---
title: "sys.key_constraints (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.key_constraints
- key_constraints
- sys.key_constraints_TSQL
- key_constraints_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.key_constraints catalog view
ms.assetid: 0f782d2f-7126-46ab-85b7-bcba44862231
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9ade8a9ce0fc36b9f7dfe2f1b7d098d23f00e791
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="syskeyconstraints-transact-sql"></a>sys.key_constraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  主キー制約または一意制約であるオブジェクトごとに 1 行のデータを格納します。 含む**sys.objects.type** PK と UQ です。  
  
|列名|データ型|Description|  
|-----------------|---------------|-----------------|  
|**\<Sys.objects から継承された列 >**||このビューが継承する列の一覧は、次を参照してください。 [sys.objects &#40;です。TRANSACT-SQL と #41 です。](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**unique_index_id**|**int**|この制約を設定するために作成された、親オブジェクトの対応する一意インデックスの ID。|  
|**is_system_named**|**bit**|1 = 名前はシステムによって生成されました。<br /><br /> 0 = ユーザー指定の名前。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;です。TRANSACT-SQL と #41 です。](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server システム カタログに対するクエリに関してよくあるご質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  