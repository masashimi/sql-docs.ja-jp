---
title: sys.user_token (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.user_token
- user_token
- sys.user_token_TSQL
- user_token_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], security tokens
- sys.user_token catalog view
- user tokens [SQL Server]
- tokens [SQL Server]
- user_token catalog view
ms.assetid: be018103-5e57-43a4-9160-9bf420892aa7
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 217528671012e90ab126ad39b079791c6ced022b
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43036821"
---
# <a name="sysusertoken-transact-sql"></a>sys.user_token (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ユーザー トークンの一部であるデータベース プリンシパルごとに 1 つの行を返します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**principal_id**|**int**|プリンシパルの ID です。 値はデータベース内で一意です。|  
|**sid**|**varbinary(85)**|プリンシパルがデータベースの外部として定義されている場合のプリンシパルのセキュリティ識別子。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン、Windows ログイン、Windows グループ ログイン、証明書にマップされるログインなどです。それ以外の場合、この値は NULL になります。|  
|**name**|**nvarchar (128)**|プリンシパルの名前。 値はデータベース内で一意です。|  
|**type**|**nvarchar (128)**|プリンシパルの種類の説明。 すべての型にマップされます**sid**します。 値は、次のいずれかです。<br /><br /> SQL USER<br /><br /> WINDOWS LOGIN<br /><br /> WINDOWS GROUP<br /><br /> ROLE<br /><br /> APPLICATION ROLE<br /><br /> DATABASE ROLE<br /><br /> USER MAPPED TO CERTIFICATE<br /><br /> USER MAPPED TO ASYMMETRIC KEY<br /><br /> CERTIFICATE<br /><br /> ASYMMETRIC KEY|  
|**使用状況**|**nvarchar (128)**|GRANT または DENY 権限の評価にプリンシパルが参加するかどうか、または認証子としての役割を果たすかどうかを示します。<br /><br /> この値は次のいずれかになります。<br /><br /> GRANT OR DENY<br /><br /> DENY ONLY<br /><br /> AUTHENTICATOR|  
  
## <a name="see-also"></a>参照  
 [sys.login_token &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-login-token-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
