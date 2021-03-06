---
title: インメモリ OLTP データベースにおける高可用性のサポート | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2113a916-3b1e-496c-8650-7f495e492510
caps.latest.revision: 5
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: a15bbc6daf6c6a9b214eae1b9bf01583051a4958
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2018
ms.locfileid: "40395350"
---
# <a name="high-availability-support-for-in-memory-oltp-databases"></a>インメモリ OLTP データベースにおける高可用性のサポート
  メモリ最適化テーブルを含んだデータベースは、ネイティブ コンパイル ストアド プロシージャの有無に関係なく、AlwaysOn 可用性グループで完全にサポートされます。  [!INCLUDE[hek_2](../../includes/hek-2-md.md)] オブジェクトを含んでいる場合とそうでない場合とでデータベースの構成とサポートに違いはありません。  
  
## <a name="alwayson-availability-groups-and-in-memory-oltp-databases"></a>AlwaysOn 可用性グループとインメモリ OLTP データベース  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] のコンポーネントを使ってデータベースを構成する利点を次に示します。  
  
-   **完全に統合された環境**   
    メモリ最適化テーブルを含んだデータベースは、同期と非同期のどちらのセカンダリ レプリカに対しても同じウィザードを使用して構成でき、同じサポート レベルが適用されます。 加えて、使い慣れた SQL Server Management Studio の AlwaysOn ダッシュボードを使用して、正常性の監視を行うことができます。  
  
-   **同等のフェールオーバー時間**   
    持続性のあるメモリ最適化テーブルのインメモリ状態がセカンダリ レプリカで維持されます。 自動フェールオーバーまたは強制フェールオーバーが発生した場合に復旧の必要がないため、新しいプライマリへのフェールオーバーにかかる時間はディスク ベースのテーブルと変わりありません。 この構成では、SCHEMA_ONLY として作成されたメモリ最適化テーブルがサポートされます。 ただしそれらのテーブルに対する変更はログに記録されないため、セカンダリ レプリカ上の該当テーブルにはデータが不在となります。  
  
-   **[読み取り可能セカンダリ]**   
    セカンダリ レプリカが読み取りアクセス用に構成されている場合、セカンダリ レプリカ上のメモリ最適化テーブルにアクセスしてクエリを実行することができます。 詳細については、「[アクティブなセカンダリ: 読み取り可能なセカンダリ レプリカ (AlwaysOn 可用性グループ)](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)」を参照してください。  
  
## <a name="failover-clustering-instance-fci-and-in-memory-oltp-databases"></a>フェールオーバー クラスタリング インスタンス (FCI) とインメモリ OLTP データベース  
 共有記憶域構成で高可用性を実現するには、メモリ最適化テーブルを含んだデータベースと複数のインスタンスに対してフェールオーバー クラスタリングを設定します。 FCI を設定する際、次の要素を考慮する必要があります。  
  
-   **目標復旧時間**   
    フェールオーバーの所要時間は長くなる可能性があります。データベースを使用可能な状態にするためには、メモリ最適化テーブルをメモリに読み込む必要があるためです。  
  
-   **SCHEMA_ONLY テーブル**   
    フェールオーバー後、SCHEMA_ONLY テーブルは、データ行の存在しない空の状態になるので注意してください。 これは仕様であり、アプリケーションで定義された動作です。 1 つ以上の SCHEMA_ONLY テーブルを含む [!INCLUDE[hek_2](../../includes/hek-2-md.md)] データベースを再起動したときもまったく同じ動作となります。  
  
## <a name="support-for-transaction-replication-in-in-memory-oltp"></a>インメモリ OLTP におけるトランザクション レプリケーションのサポート  
 トランザクション レプリケーションのサブスクライバーとして機能するテーブルは、ピア ツー ピア トランザクション レプリケーションを除き、メモリ最適化テーブルとして構成できます。 その他のレプリケーション構成はメモリ最適化テーブルとは互換性がありません。  詳細については、「 [メモリ最適化テーブル サブスクライバーへのレプリケーション](../replication/replication-to-memory-optimized-table-subscribers.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループ (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [アクティブなセカンダリ: 読み取り可能なセカンダリ レプリカ&#40;AlwaysOn 可用性グループ&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [メモリ最適化テーブル サブスクライバーへのレプリケーション](../replication/replication-to-memory-optimized-table-subscribers.md)  
  
  
