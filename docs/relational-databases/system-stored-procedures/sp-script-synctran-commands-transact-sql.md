---
title: sp_script_synctran_commands (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_script_synctran_commands
- sp_script_synctran_commands_TSQL
helpviewer_keywords:
- sp_script_synctran_commands
ms.assetid: f132694a-dd05-405b-9d84-21acce9e564a
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b86c1064eb96174243ea15cba6f5f84a77e40a1f
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43031809"
---
# <a name="spscriptsynctrancommands-transact-sql"></a>sp_script_synctran_commands (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  含むスクリプトを生成、 **sp_addsynctrigger**更新可能なサブスクリプションのサブスクライバーで適用される呼び出しです。 1 つである**sp_addsynctrigger**パブリケーション内の各アーティクルに対して呼び出します。 生成されるスクリプトにも含まれています、 **sp_addqueued_artinfo**作成の呼び出し、 **MSsubsciption_articles**キュー パブリケーションの処理に必要なテーブルです。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_script_synctran_commands [@publication = ] 'publication'  
    [ , [@article = ] 'article']  
```  
  
## <a name="arguments"></a>引数  
 [ **@publication** =] **'***パブリケーション***'**  
 スクリプト作成の対象となるパブリケーションの名前を指定します。 *パブリケーション*は**sysname**、既定値はありません。  
  
 [ **@article** =] **'***記事***'**  
 スクリプト作成の対象となるアーティクルの名前を指定します。 *記事*は**sysname**、既定値は**すべて**、すべてのアーティクルがスクリプト化します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="results-set"></a>結果セット  
 **sp_script_synctran_commands**結果セットを返しますが、1 つから成る**nvarchar (4000)** 列。 結果セットのフォーム、完全なスクリプト作成の両方に必要な**sp_addsynctrigger**と**sp_addqueued_artinfo**の呼び出しをサブスクライバーで適用します。  
  
## <a name="remarks"></a>コメント  
 **sp_script_synctran_commands**スナップショットおよびトランザクション レプリケーションで使用されます。  
  
 **sp_addqueued_artinfo**キュー更新サブスクリプションに対して使用します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_script_synctran_commands**します。  
  
## <a name="see-also"></a>参照  
 [sp_addsynctriggers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsynctriggers-transact-sql.md)   
 [sp_addqueued_artinfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqueued-artinfo-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
