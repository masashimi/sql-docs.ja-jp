---
title: Broker:Forwarded Message Dropped イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Broker:Forwarded Message Dropped event class
ms.assetid: ec242d0b-77b0-45f5-8b12-186a14b173a8
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c17fe8a30934741751a1c0f02cd93430a9f30a0f
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43070674"
---
# <a name="brokerforwarded-message-dropped-event-class"></a>Broker:Forwarded Message Dropped イベント クラス
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、Service Broker が転送予定のメッセージを削除すると Broker:Forwarded Message Dropped イベントが生成されます。  
  
## <a name="brokerforwarded-message-dropped-event-class-data-columns"></a>Broker:Forwarded Message Dropped イベント クラスのデータ列  
  
|データ列|型|[説明]|列番号|フィルターの適用|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|[ユーザー アカウント制御]|  
|BigintData1|**bigint**|メッセージのシーケンス番号。|52|いいえ|  
|ClientProcessID|**int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターによって割り当てられた ID。 クライアントでクライアント プロセス ID が指定されると、このデータ列が作成されます。|9|[ユーザー アカウント制御]|  
|DatabaseID|**int**|USE *database* ステートメントで指定されたデータベースの ID、または特定のインスタンスについて USE *database*ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、ServerName データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|[ユーザー アカウント制御]|  
|DatabaseName|**nvarchar**|ユーザーのステートメントが実行されているデータベースの名前。|35|[ユーザー アカウント制御]|  
|DBUserName|**nvarchar**|このメッセージの送信元であるブローカー インスタンスの ID。|40|いいえ|  
|[エラー]|**int**|イベント内のテキストの、sys.messages 内でのメッセージ ID 番号。|31|いいえ|  
|EventClass|**int**|キャプチャされたイベント クラスの種類。 Broker:Forwarded Message Dropped の場合は、常に 191 です。|27|いいえ|  
|EventSequence|**int**|このイベントのシーケンス番号。|51|いいえ|  
|FileName|**nvarchar**|メッセージの送信先のサービス名。|36|いいえ|  
|GUID|**uniqueidentifier**|ダイアログのメッセージ交換 ID。 この ID はメッセージの一部として転送され、メッセージ交換の両側で共有されます。|54|いいえ|  
|HostName|**nvarchar**|クライアントが実行しているコンピューターの名前。 このデータ列には、クライアントがホスト名を指定している場合にデータが格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|[ユーザー アカウント制御]|  
|IndexID|**int**|転送されるメッセージに残っているホップの数。|24|いいえ|  
|IntegerData|**int**|転送されるメッセージのフラグメント番号。|25|いいえ|  
|LoginSid|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 各 SID はサーバーのログインごとに一意です。|41|[ユーザー アカウント制御]|  
|NTDomainName|**nvarchar**|ユーザーが属している Windows ドメイン。|7|[ユーザー アカウント制御]|  
|NTUserName|**nvarchar**|このイベントが生成された接続を所有するユーザーの名前。|6|[ユーザー アカウント制御]|  
|ObjectId|**int**|転送されるメッセージの有効期限の値。|22|いいえ|  
|ObjectName|**nvarchar**|転送されたメッセージのメッセージ ID。|34|いいえ|  
|OwnerName|**nvarchar**|このメッセージの送信先のブローカー インスタンス ID。|37|いいえ|  
|RoleName|**nvarchar**|メッセージ交換ハンドルのロール。 次のいずれかです。<br /><br /> -Initiator: このブローカーがメッセージ交換の発信側です。<br /><br /> -Target: このブローカーがメッセージ交換の発信先です。|38|いいえ|  
|ServerName|**nvarchar**|トレースされる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前。|26|いいえ|  
|Severity|**int**|イベントのテキストの重大度を表す数値。|29|いいえ|  
|SPID|**int**|クライアントに関連付けられているプロセスに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって割り当てられているサーバー プロセス ID。|12|[ユーザー アカウント制御]|  
|StartTime|**datetime**|イベントの開始時刻 (取得できた場合)。|14|[ユーザー アカウント制御]|  
|状態|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のソース コード内のイベントが生成された場所を示します。 イベントが生成された場所によって、状態コードが異なることがあります。 マイクロソフトのサポート エンジニアはこの状態コードを使用して、イベントが生成されたソース コード内の場所を特定することができます。|30|いいえ|  
|成功|**int**|メッセージが存続している時間。 この値が有効期限の値以上の場合は、メッセージが削除されます。|23|いいえ|  
|TargetLoginName|**nvarchar**|メッセージの転送先になるネットワーク アドレス。|42|いいえ|  
|TargetUserName|**nvarchar**|メッセージを発信したサービスの名前。|39|いいえ|  
|TextData|**ntext**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がメッセージを削除した理由の説明。|1|[ユーザー アカウント制御]|  
|Transaction ID|**bigint**|トランザクションに対してシステムが割り当てた ID。|4|いいえ|  
  
 このイベントの TextData 列に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がメッセージを削除した理由の説明が格納されます。  
  
## <a name="see-also"></a>参照  
 [SQL Server Service Broker (SQL Server Service Broker)](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
