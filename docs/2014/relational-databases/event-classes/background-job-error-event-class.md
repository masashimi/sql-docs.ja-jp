---
title: Background Job Error イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Background Job Error event class
ms.assetid: 9e6d2a0e-919d-4fe2-a306-b20b8d41c197
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 88e96d531d901fbb7b58641069cec3cd235ea1db
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37310042"
---
# <a name="background-job-error-event-class"></a>Background Job Error イベント クラス
  **Background Job Error** イベント クラスは、バックグラウンド ジョブが異常終了したときに発生します。 このような状況では、システム管理者の注意を喚起する必要性が生じる場合があります。  
  
## <a name="background-job-error-event-class-data-columns"></a>Background Job Error イベント クラスのデータ列  
  
|データ列名|データ型|説明|列 ID|フィルターの適用|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|ジョブで指定されているデータベースの ID。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|**DatabaseName**|**nvarchar**|ユーザーのステートメントが実行されているデータベースの名前。|35|はい|  
|**Error**|**int**|最後の試行で発生したエラーのエラー番号 (**EventSubClass** が 1 の場合のみ)。|31|はい|  
|**EventClass**|**int**|イベントの種類 = 193。|27|いいえ|  
|**EventSequence**|**int**|要求内の特定のイベントのシーケンス。|51|いいえ|  
|**EventSubClass**|**int**|イベント サブクラスの種類。<br /><br /> 1 = エラーが発生し、バックグラウンド ジョブを中断中です。<br /><br /> 2 = キューがいっぱいなので、バックグラウンド ジョブが削除されました。<br /><br /> 3 = バックグラウンド ジョブからエラーが返されました。|21|はい|  
|**IndexID**|**int**|イベントの影響を受けるオブジェクトに付けられたインデックス用の ID。 オブジェクトのインデックス ID を調べるには、 **sysindexes** システム テーブルの **indid** 列を使用します。|24|はい|  
|**IntegerData**|**int**|ジョブによって行われた試行回数 (**EventSubClass** が 1 の場合のみ)。|25|はい|  
|**IntegerData2**|**int**|ジョブ シーケンス番号。|55|はい|  
|**Exchange Spill**|**int**|システムによって割り当てられたオブジェクト ID。|22|はい|  
|**SessionLoginName**|**nvarchar**|セッションを開始したユーザーのログイン名。 たとえば、Login1 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、Login2 でステートメントを実行すると、 **SessionLoginName** には Login1 が表示され、 **LoginName** には Login2 が表示されます。 この列には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインと [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ログインの両方が表示されます。|64|はい|  
|**Severity**|**int**|最後の試行におけるエラーの重要度レベル (**EventSubClass** が 1 の場合のみ)。|20|はい|  
|**StartTime**|**datetime**|ジョブが作成された時刻。|14|はい|  
|**状態**|**int**|最後の試行におけるエラーの状態 (**EventSubClass** が 1 の場合のみ)。|30|はい|  
|**TextData**|**ntext**|イベント サブクラスの値についての説明テキスト。|1|はい|  
|**型**|**int**|ジョブの種類。|57|はい|  
  
## <a name="see-also"></a>参照  
 [拡張イベント](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Auto Stats イベント クラス](auto-stats-event-class.md)  
  
  
