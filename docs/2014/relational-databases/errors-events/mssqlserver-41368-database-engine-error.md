---
title: MSSQLSERVER_41368 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 41368 (Database Engine error)
ms.assetid: abc71559-4c4d-4cce-a08f-3299dd167842
caps.latest.revision: 8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8619e3cfb8766caab9d9afbe5ed166761eeeb04f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2018
ms.locfileid: "37409721"
---
# <a name="mssqlserver41368"></a>MSSQLSERVER_41368
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|41368|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQL_IMPLICIT_AND_EXPLICIT_TX_NOT_SUPPORTED|  
|メッセージ テキスト|READ COMMITTED 分離レベルを使用してメモリ最適化テーブルにアクセスする機能は、オートコミット トランザクションでのみサポートされます。 明示的なトランザクションおよび暗黙的なトランザクションではサポートされていません。 メモリ最適化テーブルには WITH (SNAPSHOT) などのテーブル ヒントを使用して、サポートされる分離レベルを指定します。|  
  
## <a name="explanation"></a>説明  
 READ COMMITTED 分離レベルを使用してメモリ最適化テーブルにアクセスする機能は、自動コミット トランザクションでのみサポートされます。 詳細については、「 [Transaction Isolation Levels](../../database-engine/transaction-isolation-levels.md)」をご覧ください。  
  
 BEGIN TRANSACTION を使用して開始された明示的なトランザクション、または IMPLICIT_TRANSACTIONS が ON に設定されている状況で暗黙的なトランザクションからメモリ最適化テーブルにアクセスする場合は、READ COMMITTED 分離レベルはサポートされません。  
  
## <a name="user-action"></a>ユーザーの操作  
 明示的または暗黙的な READ COMMITTED トランザクションからメモリ最適化されたテーブルにアクセスする場合は、テーブルにアクセスするために SNAPSHOT を使用します。 これは、テーブル ヒント WITH (SNAPSHOT) を使用して実現できます (詳細については、次を参照してください[メモリ最適化テーブルでのトランザクション分離レベルに関するガイドライン](../in-memory-oltp/memory-optimized-tables.md)) またはデータベースを設定してオプション MEMORY_OPTIMIZED_ELEVATE_TO_。スナップショットのオプションを on (詳細については、次を参照してください。 [ALTER DATABASE SET Options &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options))。  
  
## <a name="see-also"></a>参照  
 [インメモリ OLTP &#40;インメモリ最適化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
