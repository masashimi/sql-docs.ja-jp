---
title: MSSQLSERVER_2530 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5d4be07a-38a5-4b25-819c-4dcb4636cc15
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2bd6d32cc73171415294b169e26912bf641eb88c
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2018
ms.locfileid: "37428361"
---
# <a name="mssqlserver2530"></a>MSSQLSERVER_2530
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|2530|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC_INDEX_IS_OFFLINE|  
|メッセージ テキスト|テーブル "%.\*ls" のインデックス "%.*ls" は無効です。|  
  
## <a name="explanation"></a>説明  
 指定されたインデックスが無効になっているため、DBCC ステートメントを実行できません。 インデックスを無効にすると、そのインデックスは再構築、または削除されて再作成されるまで無効になります。  
  
## <a name="user-action"></a>ユーザーの操作  
  
1.  次のいずれかの方法を使用して、無効になっているインデックスを有効にします。  
  
    -   REBUILD 句を指定した ALTER INDEX ステートメント  
  
    -   DROP_EXISTING 句を指定した CREATE INDEX  
  
    -   DBCC DBREINDEX  
  
2.  DBCC ステートメントを再実行します。  
  
## <a name="see-also"></a>参照  
 [インデックスと制約を有効にします。](../indexes/enable-indexes-and-constraints.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [DBCC DBREINDEX &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dbreindex-transact-sql)  
  
  
