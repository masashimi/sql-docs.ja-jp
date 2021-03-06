---
title: SESSION_CONTEXT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SESSION_CONTEXT
- sys.SESSION_CONTEXT
- SESSION_CONTEXT_TSQL
- sys.SESSION_CONTEXT_TSQL
helpviewer_keywords:
- SESSION_CONTEXT function
ms.assetid: b6bdbc54-331a-43cc-ab3d-3872d6a12100
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f959c49d8ecde2549da413df049800a5e83adf5c
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/04/2018
ms.locfileid: "37786683"
---
# <a name="sessioncontext-transact-sql"></a>SESSION_CONTEXT (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  現在のセッションのコンテキストでは、指定したキーの値を返します。 値が、を使用して設定 [sp_set_session_context (& a) #40 です。TRANSACT-SQL と #41; ](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)プロシージャです。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
SESSION_CONTEXT(N'key')  
```  
  
## <a name="arguments"></a>引数  
 ' key'  
 取得される値のキー (sysname 型)。  
  
## <a name="return-type"></a>戻り値の型  
 **sql_variant**  
  
## <a name="return-value"></a>戻り値  
 そのキーの値が設定されていない場合は、セッションのコンテキスト、または NULL で指定されたキーに関連付けられている値です。  
  
## <a name="permissions"></a>アクセス許可  
 すべてのユーザーは、そのセッションのセッションのコンテキストを読み取ることができます。  
  
## <a name="remarks"></a>Remarks  
 SESSION_CONTEXT の MARS の動作は CONTEXT_INFO の動作と同様です。 MARS バッチにキーと値のペアが設定された場合、新しい値を設定しているバッチが完了した後に他のバッチが開始された場合を除き、同じ接続上の他の MARS バッチで新しい値が返されることはありません。 接続上で複数の MARS バッチがアクティブな場合、値には "read_only" を設定できません。 これにより、どちらの値が "勝つ" かという観点での競合状態と非決定論を回避します。  
  
## <a name="examples"></a>使用例  
 次のような単純な例は、キーのセッション コンテキスト値を設定 `user_id` 4、および、使用する、 **SESSION_CONTEXT** 値を取得する関数。  
  
```  
EXEC sp_set_session_context 'user_id', 4;  
SELECT SESSION_CONTEXT(N'user_id');  
```  
  
## <a name="see-also"></a>参照  
 [sp_set_session_context &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)   
 [CURRENT_TRANSACTION_ID &#40;Transact-SQL&#41;](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [行レベルのセキュリティ](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO  &#40;Transact-SQL&#41;](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  
