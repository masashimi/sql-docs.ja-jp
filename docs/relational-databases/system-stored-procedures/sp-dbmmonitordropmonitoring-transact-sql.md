---
title: sp_dbmmonitordropmonitoring (TRANSACT-SQL) |Microsoft ドキュメント
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitordropmonitoring_TSQL
- sp_dbmmonitordropmonitoring
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitordropmonitoring
- database mirroring [SQL Server], monitoring
ms.assetid: 6f2d552d-bfd7-47a5-8dcb-05560aa1a32d
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a0e22f9aa73b8287d96a145e940eaab39dfeb9c9
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33237293"
---
# <a name="spdbmmonitordropmonitoring-transact-sql"></a>sp_dbmmonitordropmonitoring (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  サーバー インスタンスのすべてのデータベースに対し、ミラーリング監視ジョブを停止して削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dbmmonitordropmonitoring   
```  
  
## <a name="arguments"></a>引数  
 なし  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="permissions"></a>権限  
 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、サーバー インスタンスのすべてのミラー化されたデータベースで、データベース ミラーリング監視を削除します。  
  
```  
EXEC sp_dbmmonitordropmonitoring ;  
```  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリングと &#40; の監視SQL Server と &#41; です。](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangemonitoring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitoraddmonitoring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
