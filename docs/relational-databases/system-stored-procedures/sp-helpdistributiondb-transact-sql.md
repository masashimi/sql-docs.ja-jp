---
title: sp_helpdistributiondb (TRANSACT-SQL) |Microsoft Docs
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
- sp_helpdistributiondb_TSQL
- sp_helpdistributiondb
helpviewer_keywords:
- sp_helpdistributiondb
ms.assetid: a2917020-26d1-4011-99f8-9212d120fd2d
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: df4a44be4ef3271e6af8e7148bfee50f40c71617
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43018298"
---
# <a name="sphelpdistributiondb-transact-sql"></a>sp_helpdistributiondb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定したディストリビューション データベースのプロパティを返します。 このストアド プロシージャは、ディストリビューター側でディストリビューション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpdistributiondb [ [ @database= ] 'database_name' ]  
```  
  
## <a name="arguments"></a>引数  
 [  **@database=**] **'***database_name***'**  
 プロパティを返すデータベース名を指定します。 *database_name*は**sysname**、既定値は**%** とをディストリビューターに関連付けられているすべてのデータベース、ユーザーがアクセス許可。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|ディストリビューション データベースの名前です。|  
|**min_distretention**|**int**|トランザクションが削除されるまでの時間の最小保有期間。|  
|**max_distretention**|**int**|トランザクションが削除されるまでの時間の最大保有期間。|  
|**履歴の保有期間**|**int**|履歴を保持する時間数。|  
|**history_cleanup_agent**|**sysname**|履歴後処理エージェントの名前。|  
|**distribution_cleanup_agent**|**sysname**|ディストリビューション後処理エージェントの名前。|  
|**status**|**int**|内部使用のみです。|  
|**data_folder**|**nvarchar (255)**|データベース ファイルを格納するときに使用するディレクトリの名前。|  
|**data_file**|**nvarchar (255)**|データベース ファイルの名前。|  
|**data_file_size**|**int**|データ ファイルの初期サイズ (MB 単位)。|  
|**log_folder**|**nvarchar (255)**|データベース ログ ファイルを格納するディレクトリの名前。|  
|**log_file**|**nvarchar (255)**|ログ ファイルの名前。|  
|**log_file_size**|**int**|ログ ファイルの初期サイズ (MB 単位)。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helpdistributiondb**はあらゆる種類のレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバー、 **db_owner**固定データベース ロール、または**replmonitor**ディストリビューション データベースでロールと、ディストリビューション データベースを使用するパブリケーションのパブリケーション アクセス リスト内のユーザーが実行できます。**sp_helpdistributiondb**ファイル関連の情報を返します。 メンバー、**パブリック**実行できるロール**sp_helpdistributiondb**アクセスあるディストリビューション データベースのファイルには関連の情報を返します。  
  
## <a name="see-also"></a>参照  
 [View and Modify Distributor and Publisher Properties (ディストリビューターとパブリッシャーのプロパティの表示および変更)](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistributiondb &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [sp_changedistributiondb &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
