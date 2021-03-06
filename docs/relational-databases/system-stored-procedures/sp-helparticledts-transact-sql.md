---
title: sp_helparticledts (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_helparticledts
- sp_helparticledts_TSQL
helpviewer_keywords:
- sp_helparticledts
ms.assetid: cd1aed60-e056-4ff3-86ee-62b19433d890
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c095e7567a61758c23c434ddd04f26730a57b058
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43029383"
---
# <a name="sphelparticledts-transact-sql"></a>sp_helparticledts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用して変換サブスクリプションを作成するときに使用する正しいカスタム タスク名に関する情報を取得するために使用[!INCLUDE[msCoName](../../includes/msconame-md.md)]Visual Basic です。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helparticledts [ @publication = ] 'publication', [ @article = ] 'article'  
```  
  
## <a name="arguments"></a>引数  
 [  **@publication =**] **'***パブリケーション***'**  
 パブリケーションの名前です。 *パブリケーション*は**sysname**、既定値はありません。  
  
 [  **@article=**] **'***記事***'**  
 パブリケーション内のアーティクルの名前を指定します。 *記事*は**sysname**、既定値はありません。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**pre_script_ignore_error_task_name**|**sysname**|スナップショット データをコピーする前に発生するプログラミング タスクのタスク名。 スクリプト エラーが発生しても、プログラムはそのまま実行されます。|  
|**pre_script_task_name**|**sysname**|スナップショット データをコピーする前に発生するプログラミング タスクのタスク名。 エラーが発生すると、プログラムの実行は中止します。|  
|**transformation_task_name**|**sysname**|データ ドリブン クエリ タスクを使用する場合の、プログラミング タスクのタスク名。|  
|**post_script_ignore_error_task_name**|**sysname**|スナップショット データをコピーした後に発生するプログラミング タスクのタスク名。 スクリプト エラーが発生しても、プログラムはそのまま実行されます。|  
|**post_script_task_name**|**sysname**|スナップショット データをコピーした後に発生するプログラミング タスクのタスク名。 エラーが発生すると、プログラムの実行は中止します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helparticledts**スナップショット レプリケーションおよびトランザクション レプリケーションで使用されます。  
  
 レプリケーション データ変換サービス (DTS) プログラム内のタスクに名前を付ける場合は、レプリケーション エージェントで要求される名前付け規則に従う必要があります。 SQL 実行タスクなどのカスタム タスクの場合、その名前は、アーティクル名、プレフィックス、およびオプションの部分で構成される連結文字列です。 コードを記述するときには、この結果セットで正しいタスク名を確認できます。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールおよび**db_owner**固定データベース ロールが実行できる**sp_helparticledts**します。  
  
  
