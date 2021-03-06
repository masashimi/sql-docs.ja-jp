---
title: sp_clean_db_file_free_space (TRANSACT-SQL) |Microsoft Docs
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
- sp_clean_db_file_free_space
- sp_clean_db_file_free_space_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ghost records
- sp_clean_db_file_free_space
ms.assetid: 3eb53a67-969d-4cb8-9681-b1c8e6fd55b6
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bcd6c21404593244104bc58cc9beab4164c4283a
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43036664"
---
# <a name="spcleandbfilefreespace-transact-sql"></a>sp_clean_db_file_free_space (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ変更ルーチンのためにデータベース ページに残った残存情報を削除します。 sp_clean_db_file_free_space は、データベースの 1 つのファイルのすべてのページをクリーニングします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_clean_db_file_free_space   
[ @dbname ] = 'database_name'   
, @fileid = 'file_number'   
 [ , [ @cleaning_delay = ] 'delay_in_seconds' ] [;]  
```  
  
## <a name="arguments"></a>引数  
 [ @dbname=] '*database_name*'  
 クリーニングするデータベースの名前です。 *dbname*は**sysname** NULL にすることはできません。  
  
 [ @fileid=] '*file_number が*'  
 クリーニングするデータ ファイルの ID です。 *file_number が*は**int** NULL にすることはできません。  
  
 [ @cleaning_delay=] '*delay_in_seconds*'  
 ページをクリーニングする間隔を指定します。 この値を指定することにより、I/O システムへの影響を低減することができます。 *delay_in_seconds*は**int**既定値は 0。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 テーブルからの削除操作や、行の移動を伴うような更新操作では、行への参照を削除することにより、直ちにページ上の領域が解放されます。 ただし、特定の状況下では、行がゴースト レコードとして、物理的にデータ ページ上に残ってしまう場合があります。 ゴースト レコードは、バックグラウンド プロセスによって定期的に削除されます。 この残存データがによって返されない、[!INCLUDE[ssDE](../../includes/ssde-md.md)]クエリに応答します。 ただし、データまたはバックアップ ファイルの物理的なセキュリティに不安があるような環境では、sp_clean_db_file_free_space を使用することで、これらのゴースト レコードをクリーニングすることができます。  
  
 sp_clean_db_file_free_space の実行にかかる時間は、ファイルのサイズ、使用可能な空き領域、および、ディスク容量によって異なります。 sp_clean_db_file_free_space プロシージャは、I/O アクティビティに著しく影響する場合があるため、通常の業務時間を避けて実行することをお勧めします。  
  
 sp_clean_db_file_free_space を実行する前に、データベースの完全バックアップを作成することをお勧めします。  
  
 関連する[sp_clean_db_free_space](../../relational-databases/system-stored-procedures/sp-clean-db-free-space-transact-sql.md)ストアド プロシージャは、データベース内のすべてのファイルをクリーンアップします。  
  
## <a name="permissions"></a>アクセス許可  
 db_owner データベース ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例は、のプライマリ データ ファイルからすべての残存情報をクリーンアップ、`AdventureWorks2012`データベース。  
  
```  
USE master;  
GO  
EXEC sp_clean_db_file_free_space   
@dbname = N'AdventureWorks2012', @fileid = 1 ;  
```  
  
## <a name="see-also"></a>参照  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)
 <br>[ゴースト クリーンアップ プロセス ガイド](../ghost-record-cleanup-process-guide.md) 
  
  
