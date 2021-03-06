---
title: sp_setsubscriptionxactseqno (TRANSACT-SQL) |Microsoft Docs
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
- sp_setsubscriptionxactseqno
- sp_setsubscriptionxactseqno_TSQL
helpviewer_keywords:
- sp_setsubscriptionxactseqno
ms.assetid: cdb4e0ba-5370-4905-b03f-0b0c6f080ca6
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 96592ae1f8f2b1de9e2d294c27d68598d2718ed7
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43037979"
---
# <a name="spsetsubscriptionxactseqno-transact-sql"></a>sp_setsubscriptionxactseqno (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  トラブルシューティングを行うときに、サブスクライバー側のディストリビューション エージェントによって適用される次のトランザクションのログ シーケンス番号 (LSN) を指定する場合に使用します。これにより、エージェントでは失敗したトランザクションをスキップできます。 このストアド プロシージャは、サブスクライバー側でサブスクリプション データベースについて実行されます。 SQL Server 以外のサブスクライバーに対してはサポートされていません。  
  
> [!CAUTION]  
>  このストアド プロシージャの使用方法を誤ったり、不正な LSN 値を指定すると、ディストリビューション エージェントでは、サブスクライバー側で既に適用された変更が元に戻されたり、残っているすべての変更がスキップされることがあります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_setsubscriptionxactseqno [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @xact_seqno = ] xact_seqno   
```  
  
## <a name="arguments"></a>引数  
 [  **@publisher=** ] **'***パブリッシャー***'**  
 パブリッシャーの名前です。 *パブリッシャー*は**sysname**、既定値はありません。  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 パブリケーション データベースの名前です。 *publisher_db*は**sysname**、既定値はありません。 SQL Server 以外のパブリッシャー、 *publisher_db*ディストリビューション データベースの名前を指定します。  
  
 [  **@publication=** ] **'***パブリケーション***'**  
 パブリケーションの名前です。 *パブリケーション*は**sysname**、既定値はありません。 ディストリビューション エージェントは、1 つ以上のパブリケーションが共有しているときにのすべての値を指定する必要があります*パブリケーション*します。  
  
 [  **@xact_seqno=** ] *xact_seqno*  
 サブスクライバーで適用される、ディストリビューターの次のトランザクションの LSN を指定します。 *xact_seqno*は**varbinary (16)**、既定値はありません。  
  
## <a name="result-set"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**元の XACT_SEQNO**|**varbinary(16)**|サブスクライバー側で適用される次のトランザクションの、元の LSN。|  
|**更新された XACT_SEQNO**|**varbinary(16)**|サブスクライバー側で適用される次のトランザクションの、更新された LSN。|  
|**サブスクリプション ストリームの数**|**int**|最後の同期中に使用されたサブスクリプション ストリームの数。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_setsubscriptionxactseqno**はトランザクション レプリケーションで使用します。  
  
 **sp_setsubscriptionxactseqno**ピア ツー ピア トランザクション レプリケーション トポロジでは使用できません。  
  
 **sp_setsubscriptionxactseqno**エラーの原因となっている特定のトランザクションをスキップするために使用するときに、サブスクライバーで適用されます。 障害が発生したときにディストリビューション エージェントが停止し、呼び出す[sp_helpsubscriptionerrors &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helpsubscriptionerrors-transact-sql.md)して失敗したトランザクションの xact_seqno 値を取得し、を呼び出してディストリビューター**sp_setsubscriptionxactseqno**のこの値を渡す*xact_seqno*します。 こうすると、この LSN より後のコマンドだけが処理されます。  
  
 値を指定**0**の*xact_seqno*ディストリビューション データベースで保留中のすべてのコマンドをサブスクライバーに配信します。  
  
 **sp_setsubscriptionxactseqno**ディストリビューション エージェントでマルチ サブスクリプション ストリームを使用する場合に失敗する可能性があります。  
  
 このエラーが発生した場合は、単一のサブスクリプション ストリームでディストリビューション エージェントを実行する必要があります。 詳細については、「 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_setsubscriptionxactseqno**します。  
  
  
