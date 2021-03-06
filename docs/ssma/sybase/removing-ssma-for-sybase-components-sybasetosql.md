---
title: SSMA for Sybase コンポーネント (SybaseToSQL) の削除 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: aec09593-17d9-4ec2-ac56-3cd8851406fd
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6e676ff9adb8d098cf795d7599788bcfa3d0f515
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2018
ms.locfileid: "40394935"
---
# <a name="removing-ssma-for-sybase-components-sybasetosql"></a>SSMA for Sybase コンポーネントの削除 (SybaseToSQL)
終了したらデータベースを移行してから Sybase Adaptive Server Enterprise (ASE) に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、SSMA コンポーネントをアンインストールしたい場合があります。 いつでも、クライアント コンポーネントをアンインストールすることができますから拡張機能パックをアンインストールしないでください[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は、移行されたデータベース内の関数を使用できなくする場合を除き、 **ssma_syb** のスキーマ**sysdb**データベース。  
  
## <a name="uninstalling-the-ssma-for-sybase-client"></a>Sybase クライアント用の SSMA のアンインストール  
SSMA をアンインストールするにを使用して**プログラム追加と削除**します。  
  
**SSMA をアンインストールするには**  
  
1.  コントロール パネルで、開く**プログラム追加と削除**します。  
  
2.  選択**Microsoft SQL Server Migration Assistant for Sybase**、 をクリックし、**削除**します。  
  
3.  SSMA をアンインストールすることを確認するには、次のようにクリックします。**はい**します。  
  
## <a name="uninstalling-the-extension-pack"></a>拡張機能パックをアンインストールします。  
データベースを移行は、内のオブジェクトを使用しない場合は、確認、 **sysdb.ssma_syb**スキーマ、拡張機能パックを削除するを使用**プログラム追加と削除**します。  
  
拡張機能パックをアンインストールするには  
  
1.  コントロール パネルで、開く**プログラム追加と削除**します。  
  
2.  選択**Microsoft SQL Server Migration Assistant for Sybase 拡張パック**、 をクリックし、**削除**します。  
  
3.  拡張機能パックをアンインストールすることを確認するには、次のようにクリックします。**はい**します。  
  
4.  ユーティリティのデータベースのスクリプト ページで、インスタンスで次のようにクリックします。**次**します。  
  
5.  接続パラメーター ページで、認証方式を選択し、クリックして**次**します。  
  
    Windows 認証は SQL Server のインスタンスにログオンしようとするのに Windows 資格情報を使用します。 SQL Server 認証を選択した場合、SQL Server ログイン名とパスワードを入力する必要があります。  
  
6.  操作の完了 ページで、 **OK**します。  
  
7.  [完了] ページで、次のようにクリックします。**終了**します。  
  
をアンインストールした後、ことを確認できる、 **sysdb.ssma_syb**スキーマ、および場合によっては、全体**sysdb**データベース、を使用して削除されました[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]します。 ただし、他の SSMA 製品を使用する場合も使用、 **sysdb**データベース。 場合は、データベースが存在し、他のデータベースにこのデータベース内のオブジェクトが参照されていないことを確認したら、データベースをデタッチすることができます。  
  
## <a name="see-also"></a>参照  
[SSMA for Sybase クライアントのインストール&#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[SQL Server での SSMA コンポーネントのインストール&#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
  
