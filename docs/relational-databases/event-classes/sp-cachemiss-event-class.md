---
title: SP:CacheMiss イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SP:CacheMiss event class
ms.assetid: 82229233-f772-4558-95a0-d54584d1b1ae
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1016b963814b1887a7f8cc6ebe79df0aea0cdd01
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43094424"
---
# <a name="spcachemiss-event-class"></a>SP:CacheMiss イベント クラス
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  SP:CacheMiss イベント クラスは、プロシージャをキャッシュ内で検出できなかったことを示します。 SP:CacheMiss イベント クラスが頻繁に発生する場合は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で使用できるメモリを増やす必要があることを示している可能性があります。メモリを増やすと、プロシージャ キャッシュのサイズが増えます。  
  
## <a name="spcachemiss-event-class-data-columns"></a>SP:CacheMiss イベント クラスのデータ列  
  
|データ列名|データ型|[説明]|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|[ユーザー アカウント制御]|  
|ClientProcessID|**int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターが割り当てた ID。 クライアントによりクライアント プロセス ID が指定されると、このデータ列に値が格納されます。|9|[ユーザー アカウント制御]|  
|DatabaseID|**int**|ストアド プロシージャが実行されているデータベースの ID。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|[ユーザー アカウント制御]|  
|EventClass|**int**|イベントの種類 = 34。|27|いいえ|  
|EventSequence|**int**|要求内の特定のイベントのシーケンス。|51|いいえ|  
|GroupID|**int**|SQL トレース イベントが発生したワークロード グループの ID。|66|[ユーザー アカウント制御]|  
|HostName|**nvarchar**|クライアントが実行されているコンピューターの名前。 このデータ列にはクライアントからホスト名が提供されている場合に値が格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|[ユーザー アカウント制御]|  
|IsSystem|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。 1 はシステム、0 はユーザーです。|60|[ユーザー アカウント制御]|  
|LoginName|**nvarchar**|ユーザーのログイン名 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セキュリティ ログインまたは DOMAIN\username という形式の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ログイン資格情報)。|11|[ユーザー アカウント制御]|  
|LoginSid|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 この情報は、sys.server_principals カタログ ビューで参照できます。 各 SID はサーバーのログインごとに一意です。|41|[ユーザー アカウント制御]|  
|NTDomainName|**nvarchar**|ユーザーが所属する Windows ドメイン。|7|[ユーザー アカウント制御]|  
|NTUserName|**nvarchar**|Windows のユーザー名。|6|[ユーザー アカウント制御]|  
|ObjectID|**int**|システムによって割り当てられたオブジェクト ID。|22|[ユーザー アカウント制御]|  
|ObjectName|**nvarchar**|ストアド プロシージャの名前。 ObjectName に値が設定された場合、TextData には値が設定されません。|34|[ユーザー アカウント制御]|  
|ObjectType|**int**|イベントに関係するオブジェクトの種類を表す値。 この値は sys.objects カタログ ビューの type 列に対応します。 値については、「 [ObjectType トレース イベント列](../../relational-databases/event-classes/objecttype-trace-event-column.md)」を参照してください。|28|[ユーザー アカウント制御]|  
|RequestID|**int**|ステートメントが含まれている要求の ID。|49|[ユーザー アカウント制御]|  
|ServerName|**nvarchar**|トレースされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|SessionLoginName|**nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、SessionLoginName には Login1 が表示され、LoginName には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと Windows ログインの両方が表示されます。|64|[ユーザー アカウント制御]|  
|SPID|**int**|イベントが発生したセッションの ID。|12|[ユーザー アカウント制御]|  
|StartTime|**datetime**|イベントの開始時刻 (取得できた場合)。|14|[ユーザー アカウント制御]|  
|TextData|**ntext**|キャッシュされている SQL コードのテキスト。 TextData に値が設定された場合、ObjectName には値が設定されません。|1|[ユーザー アカウント制御]|  
|TransactionID|**bigint**|システムによって割り当てられたトランザクション ID。|4|[ユーザー アカウント制御]|  
|XactSequence|**bigint**|現在のトランザクションを説明するトークン。|50|[ユーザー アカウント制御]|  
  
## <a name="see-also"></a>参照  
 [拡張イベント](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [SP:CacheInsert イベント クラス](../../relational-databases/event-classes/sp-cacheinsert-event-class.md)  
  
  
