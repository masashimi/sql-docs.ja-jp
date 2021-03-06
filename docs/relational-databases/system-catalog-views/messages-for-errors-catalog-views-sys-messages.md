---
title: sys.messages (TRANSACT-SQL) |Microsoft Docs
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
- messages_TSQL
- sys.messages_TSQL
- sys.messages
- messages
dev_langs:
- TSQL
helpviewer_keywords:
- error messages [SQL Server]
- sys.messages catalog view
- error numbers [SQL Server]
ms.assetid: 8c16ecdf-68f4-4a2a-b594-086e3344e58a
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ac13b8d68accd744803b7524f9d6d179cca0446b
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43032435"
---
# <a name="messages-for-errors-catalog-views---sysmessages"></a>メッセージ (エラー) 用のカタログ ビュー - sys.messages
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  それぞれの行を含む**message_id**または**language_id**のシステム定義し、ユーザー定義の両方のメッセージについて、システム内のエラー メッセージ。 詳細については、「[sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)」を参照してください。  
   
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**message_id**|**int**|メッセージの ID です。 これはサーバー内で一意です。 50000 未満のメッセージ ID はシステム メッセージです。|  
|**language_id**|**smallint**|対象の言語 ID 内のテキスト**テキスト**で定義されているは、使用**syslanguages**します。 これは、指定した一意**message_id**します。|  
|**severity**|**tinyint**|メッセージの重大度レベルです。有効値は 1 ～ 25 です。 これは、同じすべてのメッセージ内での言語、 **message_id**します。|  
|**is_event_logged**|**bit**|1 = メッセージは、エラーが発生するとイベントがログに記録されます。 これは、同じすべてのメッセージ内での言語、 **message_id**します。|  
|**text**|**nvarchar(2048)**|メッセージのテキストに使用されるときに、対応する**language_id**がアクティブになっています。|  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [メッセージ&#40;エラー&#41;カタログ ビュー &#40;TRANSACT-SQL&#41;](http://msdn.microsoft.com/library/8ac78c53-7b97-41b3-9cbd-5f97c179f1f2)   
 [例外メッセージ ボックスのプログラミング](http://msdn.microsoft.com/library/0b1ba514-6959-4e69-bfd2-3cf3c1ac4b9c)   
 [エラー メッセージ](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [データベース エンジンのイベントとエラー](../../relational-databases/errors-events/database-engine-events-and-errors.md)  
  
  
