---
title: SQL Server:HTTP_STORAGE_OBJECT | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ae849f79-c581-42a5-a5cc-0a9ebea171b9
caps.latest.revision: 4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4a2a329f9c74baeac1996abd193a6b7d19c2263c
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2018
ms.locfileid: "43820018"
---
# <a name="sql-server-httpstorageobject"></a>SQL Server:HTTP_STORAGE_OBJECT
  **SQLServer:HTTP_STORAGE_OBJECT** パフォーマンス オブジェクトは、Windows Azure ストレージ アカウントを監視する各種のパフォーマンス カウンターで構成されています。 使用して[Windows Azure での SQL Server データ ファイル](../databases/sql-server-data-files-in-microsoft-azure.md)機能、Windows Azure Storage Blob にデータベース ファイルを格納できます。 このパフォーマンス オブジェクトでは、各 Windows Azure ストレージ アカウントが別々のドライブとして処理されます。  
  
|カウンター名|説明|  
|------------------|-----------------|  
|**Read Bytes/sec**|読み取り操作中に HTTP ストレージから転送されている 1 秒あたりのデータ量。|  
|**Write Bytes/sec**|書き込み操作中に HTTP ストレージから転送されている 1 秒あたりのデータ量。|  
|**Total Bytes/sec**|読み取りまたは書き込み操作中に HTTP ストレージから転送されている 1 秒あたりのデータ量。|  
|**Reads/sec**|HTTP ストレージでの 1 秒あたりの読み取り数。|  
|**Writes/sec**|HTTP ストレージでの 1 秒あたりの書き込み数。|  
|**Transfers/sec**|HTTP ストレージでの 1 秒あたりの読み取りおよび書き込み操作数。|  
|**平均Bytes/Read**|読み取りごとに HTTP ストレージから転送された平均バイト数。|  
|**平均Bytes/Write**|書き込みごとに HTTP ストレージから転送された平均バイト数。|  
|**平均Bytes/Transfer**|読み取りまたは書き込み操作中に HTTP ストレージから転送された平均バイト数。|  
|**Avg. microsec/Read**|HTTP ストレージからの読み取りごとに要する平均マイクロ秒数。|  
|**Avg. microsec/Write**|HTTP ストレージへの書き込みごとに要する平均マイクロ秒数。|  
|**Avg. microsec/Transfer**|HTTP ストレージへの転送ごとに要する平均マイクロ秒数。|  
|**Outstanding HTTP Storage I/O**|HTTP ストレージに対する未処理 I/O の合計数。|  
|**HTTP Storage I/O Retry/sec**|HTTP ストレージに送信された 1 秒あたりの再試行要求数。|  
  
## <a name="see-also"></a>参照  
 [リソースの利用状況の監視 &#40;システム モニター&#41;](monitor-resource-usage-system-monitor.md)  
  
  
