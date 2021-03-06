---
title: Locks イベント カテゴリ | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Locks event category [SQL Server]
- SQL Server event classes, Locks event category
- event classes [SQL Server], Locks event category
- lock escalation [SQL Server], locks event category
ms.assetid: 27d6afa2-7dab-4fe7-a1ad-064b879dc654
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f864c20f8697428733f86b32d3741a1de45a3446
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43068615"
---
# <a name="locks-event-category"></a>Locks イベント カテゴリ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **Locks** イベント カテゴリのイベント クラスを使用して、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスでのロックの利用状況を監視します。 これらのイベント クラスを使用すると、複数のユーザーが同時にデータの読み取りや変更を行うことによって生じるロックの問題を調査できます。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] では多数のロックが処理されることが多いため、トレース時に **Locks** イベント クラスがキャプチャされると、大きなオーバーヘッドが発生し、結果としてトレース ファイルまたはトレース テーブルが大きくなります。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|[説明]|  
|-----------|-----------------|  
|[Deadlock Graph イベント クラス](../../relational-databases/event-classes/deadlock-graph-event-class.md)|デッドロックについての XML の説明が提供されます。|  
|[Lock:Acquired イベント クラス](../../relational-databases/event-classes/lock-acquired-event-class.md)|テーブルの行などのリソースに対してロックが取得されたことを示します。|  
|[Lock:Cancel イベント クラス](../../relational-databases/event-classes/lock-cancel-event-class.md)|デッドロックを防ぐなどの理由で、ロックが取得される前に取り消されたロックの要求を追跡します。|  
|[Lock:Deadlock Chain イベント クラス](../../relational-databases/event-classes/lock-deadlock-chain-event-class.md)|デッドロック状態が発生した時点と、関与しているオブジェクトを監視します。|  
|[Lock:Deadlock イベント クラス](../../relational-databases/event-classes/lock-deadlock-event-class.md)|別のトランザクションによって既にロックされているリソースに対してトランザクションがロックを要求し、結果としてデッドロックが発生した時点を追跡します。|  
|[Lock:Escalation イベント クラス](../../relational-databases/event-classes/lock-escalation-event-class.md)|細かい単位のロックが大きい単位のロックに変換されたことを示します。|  
|[Lock:Released イベント クラス](../../relational-databases/event-classes/lock-released-event-class.md)|ロックが解除された時点を追跡します。|  
|[Lock:Timeout &#40;timeout &#62; 0&#41; イベント クラス](../../relational-databases/event-classes/lock-timeout-timeout-0-event-class.md)|要求されたリソースに対して別のトランザクションによるブロッキング ロックが存在するために、ロック要求が完了しなかった時点を追跡します。 このイベントは、ロック タイムアウト値が 0 より大きい場合にのみ発生します。|  
|[Lock:Timeout イベント クラス](../../relational-databases/event-classes/lock-timeout-event-class.md)|要求されたリソースに対して別のトランザクションによるブロッキング ロックが存在するために、ロック要求が完了しなかった時点を追跡します。|  
  
  
