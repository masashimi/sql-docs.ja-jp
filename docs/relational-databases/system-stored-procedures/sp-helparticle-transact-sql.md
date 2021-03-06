---
title: sp_helparticle (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
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
- sp_helparticle_TSQL
- sp_helparticle
helpviewer_keywords:
- sp_helparticle
ms.assetid: 9c4a1a88-56f1-45a0-890c-941b8e0f0799
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 48e07b380b8128c2fccd200b1fd2d8f9d5962e44
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43030612"
---
# <a name="sphelparticle-transact-sql"></a>sp_helparticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  アーティクルに関する情報を表示します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。 Oracle パブリッシャーの場合、このストアド プロシージャは、ディストリビューター側で任意のデータベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helparticle [ @publication = ] 'publication'   
    [ , [ @article = ] 'article' ]  
    [ , [ @returnfilter = ] returnfilter ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @found = ] found OUTPUT ]  
```  
  
## <a name="arguments"></a>引数  
 [  **@publication =**] **'***パブリケーション***'**  
 パブリケーションの名前です。 *パブリケーション*は**sysname**、既定値はありません。  
  
 [  **@article=**] **'***記事***'**  
 パブリケーション内のアーティクルの名前を指定します。 *記事*は**sysname**、既定値は **%** します。 場合*記事*は省略すると、指定されたパブリケーションのすべてのアーティクルに関する情報が返されます。  
  
 [  **@returnfilter=**] *､ レプリケーション*  
 フィルター句を返すかどうかを指定します。 *､ レプリケーション*は**ビット**、既定値は**1**フィルター句が返されます。  
  
 [ **@publisher**=] **'***パブリッシャー***'**  
 以外を指定[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーです。 *パブリッシャー*は**sysname**、既定値は NULL です。  
  
> [!NOTE]  
>  *パブリッシャー*によって発行されたアーティクルの情報を要求するときに指定しないで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーです。  
  
 [  **@found=** ]*見つかった*出力  
 内部使用のみです。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**アーティクル id**|**int**|アーティクルの ID です。|  
|**アーティクルの名前**|**sysname**|アーティクルの名前。|  
|**基本オブジェクト**|**nvarchar (257)**|アーティクルまたはストアド プロシージャが表す基になるテーブルの名前です。|  
|**対象オブジェクト**|**sysname**|パブリッシュ先の (サブスクリプション) テーブル名です。|  
|**同期オブジェクト**|**nvarchar (257)**|パブリッシュされるアーティクルを定義するビューの名前です。|  
|**type**|**smallint**|アーティクルのタイプです。<br /><br /> **1** = ログ ベースします。<br /><br /> **3** = 手動フィルター付きログベースの。<br /><br /> **5** = 手動ビュー付きログベースします。<br /><br /> **7** = 手動フィルターおよび手動ビュー付きログベースします。<br /><br /> **8**ストアド プロシージャの実行を = です。<br /><br /> **24**シリアル化可能なストアド プロシージャの実行を = です。<br /><br /> **32** = ストアド プロシージャ (スキーマのみ)。<br /><br /> **64** = ビュー (スキーマのみ)。<br /><br /> **96** = 集計関数 (スキーマのみ)。<br /><br /> **128** = 関数 (スキーマのみ)。<br /><br /> **257** = ログ ベースのインデックス付きビュー。<br /><br /> **259** = 手動フィルター付きログベースのインデックス付きビュー。<br /><br /> **261** = 手動ビュー付きログベースのインデックス付きビュー。<br /><br /> **263** = 手動フィルター付きログベースのインデックス付きビューと手動ビュー。<br /><br /> **320** = インデックス付きビュー (スキーマのみ)。<br /><br />|  
|**status**|**tinyint**|[& (ビット演算子 AND)](../../t-sql/language-elements/bitwise-and-transact-sql.md)アーティクルのプロパティを 1 つまたは複数またはこれらの結果。<br /><br /> **0x00** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> **0x01** = アーティクルはアクティブです。<br /><br /> **0x08** = insert ステートメントに列名を含みます。<br /><br /> **0x16** = ステートメントをパラメーター化を使用します。<br /><br /> **0x32** = パラメーター化ステートメントおよび insert ステートメントに列名が含まれます。|  
|**フィルター (filter)**|**nvarchar (257)**|テーブルを行方向にフィルター選択するために使用するストアド プロシージャです。 このストアド プロシージャは FOR REPLICATION 句を使用して作成されている必要があります。|  
|**description**|**nvarchar (255)**|アーティクルを説明するエントリです。|  
|**insert_command**|**nvarchar (255)**|テーブル アーティクルの挿入をレプリケートするときに使用されるレプリケーション コマンドの種類です。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。|  
|**update_command**|**nvarchar (255)**|テーブル アーティクルの更新をレプリケートするときに使用されるレプリケーション コマンドの種類です。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。|  
|**delete_command**|**nvarchar (255)**|テーブル アーティクルの削除をレプリケートするときに使用されるレプリケーション コマンドの種類です。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。|  
|**作成スクリプトのパス**|**nvarchar (255)**|ターゲット テーブルを作成するのに使用されるアーティクル スキーマ スクリプトのパスと名前です。|  
|**垂直方向のパーティション**|**bit**|アーティクルに対して垂直的パーティション分割が有効になっているかどうか値が**1**垂直的パーティション分割が有効になっていることを意味します。|  
|**pre_creation_cmd**|**tinyint**|DROP TABLE、DELETE TABLE、または TRUNCATE TABLE の事前作成コマンドです。|  
|**filter_clause**|**ntext**|行方向のフィルター選択を指定する WHERE 句です。|  
|**schema_option**|**binary(8)**|指定されたアーティクルに対するスキーマ生成オプションのビットマップです。 完全な一覧については**schema_option**値を参照してください[sp_addarticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)します。|  
|**dest_owner**|**sysname**|対象オブジェクトの所有者名です。|  
|**source_owner**|**sysname**|ソース オブジェクトの所有者です。|  
|**unqua_source_object**|**sysname**|所有者名の部分を除いたソース オブジェクトの名前です。|  
|**sync_object_owner**|**sysname**|パブリッシュされるアーティクルを定義するビューの所有者です。 .|  
|**unqualified_sync_object**|**sysname**|所有者名の部分を除いた、パブリッシュされるアーティクルを定義するビューの名前です。|  
|**filter_owner**|**sysname**|フィルターの所有者です。|  
|**unqua_filter**|**sysname**|所有者名の部分を除いたフィルター名です。|  
|**auto_identity_range**|**int**|パブリケーションの作成時に、ID 範囲の自動処理がパブリケーションで有効に設定されたかどうかを示すフラグです。 **1**自動 id 範囲が有効であることを意味します**0**無効になっていることを意味します。|  
|**publisher_identity_range**|**int**|場合、アーティクルはパブリッシャー側で id 範囲のサイズの範囲*identityrangemanagementoption*に設定**自動**または**auto_identity_range**設定**true**します。|  
|**identity_range**|**bigint**|場合、アーティクルはサブスクライバーで id 範囲のサイズの範囲*identityrangemanagementoption*に設定**自動**または**auto_identity_range**設定**true**します。|  
|**threshold**|**bigint**|ディストリビューション エージェントが新しい id 範囲を割り当てるときを示すパーセント値。|  
|**identityrangemanagementoption**|**int**|アーティクルに対して処理される ID 範囲管理を示します。|  
|**fire_triggers_on_snapshot**|**bit**|初期スナップショットが適用されたときに、レプリケートされたユーザー トリガーが実行されるかどうかを示します。<br /><br /> **1** = ユーザー トリガーを実行します。<br /><br /> **0** = ユーザー トリガーは実行されません。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helparticle**スナップショット レプリケーションおよびトランザクション レプリケーションで使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロール、 **db_owner**固定データベース ロール、または現在のパブリケーションのパブリケーション アクセス リストが実行できる**sp_helparticle**.  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_helptranarticle](../../relational-databases/replication/codesnippet/tsql/sp-helparticle-transact-_1.sql)]  
  
## <a name="see-also"></a>参照  
 [表示およびアーティクルのプロパティの変更](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [sp_addarticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlecolumn (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_changearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
