---
title: sp_db_increased_partitions |Microsoft Docs
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
- sp_db_increased_partitions_TSQL
- sp_db_increased_partitions
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_increased_partitions
ms.assetid: a8c043ec-b504-4929-ac0e-8babaa99d989
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a67ef2ad7c4e8c289fb67275e6680dfa440ab029
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43025381"
---
# <a name="spdbincreasedpartitions"></a>sp_db_increased_partitions
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定したデータベースに最大 15, 000 のパーティションのサポートを有効または無効にします。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dp_increased_partitions   
[ @dbname ] = 'database_name'   
[ , [ @increased_partitions = ] 'increased_partitions' ] [;]  
```  
  
## <a name="arguments"></a>引数  
 [ @dbname=] '*database_name*'  
 データベースの名前です。 *dbname*は**sysname**既定値は NULL です。 場合*dbname*が指定されていない、現在のデータベースを使用します。  
  
 [ @increased_partitions=] '*increased_partitions*'  
 指定したデータベースに対して 15, 000 個のパーティションのサポートを有効または無効にします。 *increased_partitions*は**varchar (6)** 既定値は NULL です。 サポートを有効にするための承認済みの値は 'ON' または 'TRUE' です。サポートを無効にするための承認済みの値は 'OFF' または 'FALSE' です。 場合*increased_partitions*が指定されていない、プロシージャが指定されたデータベースのサポートを有効にするサポートを示すために 0 が無効になっているかを示す 1 を返します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 指定したデータベースに対する ALTER DATABASE 権限が必要です。  
  
  
