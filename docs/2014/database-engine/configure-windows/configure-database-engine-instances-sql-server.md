---
title: データベース エンジンのインスタンスの構成 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 84e36fcb-2c78-48e8-8e4b-bf784a3ee557
caps.latest.revision: 5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1ab5c7785fed8f22a12e265426d485fd65ed9a66
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37325092"
---
# <a name="configure-database-engine-instances-sql-server"></a>データベース エンジンのインスタンスの構成 (SQL Server)
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] の各インスタンスは、インスタンスによってホストされているデータベース用に定義されているパフォーマンスと可用性の要件を満たすように構成する必要があります。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] には、リソースの使用などの動作や、監査またはトリガー再帰などの機能の可用性を制御する構成オプションがあります。  
  
## <a name="instance-configuration"></a>インスタンスの構成  
 データベースを実稼働環境に配置するときには、多くの場合、データベースが必要とするパフォーマンス レベルや、データベースの必要な可用性レベルなどの分野が、サービス レベル契約 (SLA) で定義されます。 SLA の条件によって、通常はインスタンスの構成要件が決まります。  
  
 インスタンスは、通常、インストールの直後に構成されます。 初期構成は、インスタンスに配置されることになる種類のデータベースの SLA 要件によって決められるのが一般的です。 データベースの配置後、データベース管理者はインスタンスのパフォーマンスを監視し、インスタンスが SLA 要件を満たしていないことをパフォーマンス指標が示している場合は、必要に応じて構成設定を調整します。  
  
## <a name="configuration-tasks"></a>構成のタスク  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|インスタンスの各種構成オプションとその表示方法、変更方法について説明します。|[サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)|  
|インスタンス内の新しいデータ ファイルとログ ファイルの既定の場所を表示および構成する方法について説明します。|[データ ファイルとログ ファイルの既定の場所の表示または変更 &#40;SQL Server Management Studio&#41;](view-or-change-the-default-locations-for-data-and-log-files.md)|  
|ソフト NUMA を使用するための SQL Server の構成方法について説明します。|[ソフト NUMA を使用する SQL Server を構成する&#40;SQL Server&#41;](soft-numa-sql-server.md)|  
|TCP/IP ポートを NUMA (non-uniform memory access) ノード関係にマップする方法について説明します。|[NUMA ノードへの TCP/IP ポートのマッピング &#40;SQL Server&#41;](map-tcp-ip-ports-to-numa-nodes-sql-server.md)|  
|Windows の "メモリ内のページのロック" ポリシーを有効にする方法について説明します。 このポリシーにより、プロセスを使用して物理メモリにデータを保持できるアカウントを指定し、ディスク上の仮想メモリへのデータのページングを防止します。|[Lock Pages in Memory オプションの有効化 &#40;Windows&#41;](enable-the-lock-pages-in-memory-option-windows.md)|  
  
## <a name="see-also"></a>参照  
 [データベース エンジンのインスタンス &#40;SQL Server&#41;](database-engine-instances-sql-server.md)  
  
  