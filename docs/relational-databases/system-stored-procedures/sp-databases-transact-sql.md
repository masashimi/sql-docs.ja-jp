---
title: sp_databases (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_databases_TSQL
- sp_databases
dev_langs:
- TSQL
helpviewer_keywords:
- sp_databases
ms.assetid: 2a83b92a-9ecc-43c4-8ff4-e91e3a940b5a
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3fefa914e8b4eb591dcd222df1de6753770d85c9
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43029215"
---
# <a name="spdatabases-transact-sql"></a>sp_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  インスタンス内に存在しているデータベースの一覧、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]またはデータベース ゲートウェイを介して外部からアクセスします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_databases  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**DATABASE_NAME**|**sysname**|データベースの名前です。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]に格納されている、この列はデータベース名を表す、 **sys.databases**カタログ ビューです。|  
|**DATABASE_SIZE**|**int**|データベースのサイズをキロバイト数で表します。|  
|**「解説」**|**varchar(254)**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]、このフィールドは常に NULL を返します。|  
  
## <a name="remarks"></a>コメント  
 返されるデータベース名は、現在のデータベース状況を変更するために USE ステートメントでパラメーターとして使えます。  
  
 **sp_databases**を持たないと同等で開いているデータベースの接続 (ODBC)。  
  
## <a name="permissions"></a>アクセス許可  
 CREATE DATABASE 権限、ALTER ANY DATABASE 権限、または VIEW ANY DEFINITION 権限と、データベースへのアクセス許可が必要です。 また、VIEW ANY DEFINITION 権限は拒否されないことが条件となります。  
  
## <a name="examples"></a>使用例  
 次の例を実行する`sp_databases`します。  
  
```sql  
USE master;  
GO  
EXEC sp_databases;  
```  
  
## <a name="see-also"></a>参照  
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [HAS_DBACCESS &#40;TRANSACT-SQL&#41;](../../t-sql/functions/has-dbaccess-transact-sql.md)  
  
  
