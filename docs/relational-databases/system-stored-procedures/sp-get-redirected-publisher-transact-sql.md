---
title: sp_get_redirected_publisher (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- sp_get_redirected_publisher_TSQL
- sp_get_redirected_publisher
ms.assetid: d47a9ab5-f2cc-42a8-8be9-a33895ce44f0
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0a2abcc6205929146a37be95fa3943cad1b0ce4d
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43028619"
---
# <a name="spgetredirectedpublisher-transact-sql"></a>sp_get_redirected_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  元のパブリッシャーがリダイレクトされているかどうかを判断するために、レプリケーション エージェントがディストリビューターに対してクエリを実行するときに使用されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_get_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @bypass_publisher_validation = ] [0 | 1 ]  
```  
  
## <a name="arguments"></a>引数  
 [ **@original_publisher** =] **'***original_publisher***'**  
 パブリッシュされるデータベースの名前。 *publisher_db*は**sysname**、既定値はありません。  
  
 [ **@publisher_db** =] **'***publisher_db***'**  
 パブリッシュされるデータベースの名前。 *publisher_db*は**sysname**、既定値はありません。  
  
 [ **@bypass_publisher_validation** = ] [0 | 1 ]  
 リダイレクトされたパブリッシャーの検証を省略するために使用されます。 0 の場合、検証が実行されます。 1 の場合は、検証が実行されません。 *bypass_publisher_validation*は**ビット**、既定値は 0。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**redirected_publisher**|**sysname**|リダイレクト後のパブリッシャーの名前。|  
|**error_number**|**int**|検証エラーのエラー番号。|  
|**error_severity**|**int**|検証エラーの重大度。|  
|**error_message**|**nvarchar (4000)**|検証エラー メッセージのテキスト。|  
  
## <a name="remarks"></a>コメント  
 *redirected_publisher*現在のパブリッシャー名を返します。 パブリッシャーとパブリッシング データベースがリダイレクトされていない場合は null を返します**sp_redirect_publisher**します。  
  
 検証が要求されていない場合、またはパブリッシャーとパブリッシングのデータベースのエントリが存在しない場合*error_number*と*error_severity* 0 を返しますと*error_message*null を返します。  
  
 検証ストアド プロシージャの検証が要求された場合[sp_validate_redirected_publisher &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)が呼び出され、リダイレクトの対象が公開するのに適したホストであることを確認するにはデータベース。 検証が成功すると、 **sp_get_redirected_publisher**リダイレクトされたパブリッシャー名の場合は 0 を返します、 *error_number*と*error_severity*列、および内の null*error_message*列。  
  
 検証が要求されて失敗した場合は、リダイレクトされたパブリッシャーの名前がエラー情報と一緒に返されます。  
  
## <a name="permissions"></a>アクセス許可  
 呼び出し元する必要がありますいずれかのメンバーである、 **sysadmin**固定サーバー ロール、 **db_owner**固定データベース ロールには、ディストリビューション データベースまたは定義済みパブリケーションのパブリケーション アクセス リストのメンバーパブリッシャー データベースと関連付けられています。  
  
## <a name="see-also"></a>参照  
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
