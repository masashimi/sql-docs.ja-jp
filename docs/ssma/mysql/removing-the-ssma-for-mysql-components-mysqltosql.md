---
title: MySQL コンポーネント (MySQLToSql) 用の SSMA の削除 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Uninstalling, Extension pack
- Uninstalling, SSMA for MySQL client
ms.assetid: 87cdbd49-a0c9-4b00-8a93-34188b18d11a
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: adab686126cb608ae32870a9a138720b77d212bf
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393069"
---
# <a name="removing-the-ssma-for-mysql-components-mysqltosql"></a>SSMA for MySQL コンポーネントの削除 (MySQLToSql)
終了したらから MySQL へのデータベースを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、SSMA コンポーネントをアンインストールしたい場合があります。 クライアント コンポーネントは、いつでもアンインストールできます。 ただしから拡張機能パックをアンインストールする場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、SSMA では MySQL からデータをサーバー側のデータ移行のエンジンを使用してターゲット データベース (SQL Server または SQL Azure) への移行をサポートできなくします。  
  
## <a name="uninstalling-the-ssma-for-mysql-client"></a>MySQL クライアント用の SSMA のアンインストール  
SSMA をアンインストールするにを使用して**プログラム追加と削除**します。  
  
**SSMA をアンインストールするには**  
  
1.  コントロール パネルで、開く**プログラム追加と削除**します。  
  
2.  選択**Microsoft SQL Server Migration Assistant for MySQL**、 をクリックし、**削除**します。  
  
3.  SSMA をアンインストールすることを確認するには、次のようにクリックします。**はい**します。  
  
## <a name="uninstalling-the-extension-pack"></a>拡張機能パックをアンインストールします。  
使用して、拡張機能パックを削除する**プログラム追加と削除**します。  
  
**拡張機能パックをアンインストールするには**  
  
1.  コントロール パネルで、開く**プログラム追加と削除**します。  
  
2.  選択**Microsoft SQL Server Migration Assistant for MySQL の拡張機能パック**、 をクリックし、**削除**します。  
  
3.  拡張機能パックをアンインストールすることを確認するには、次のようにクリックします。**はい**します。  
  
4.  ユーティリティのデータベースのスクリプト ページを使用して、インスタンス、インスタンスを選択し、順にクリックします**次**します。  
  
5.  接続パラメーター ページで、認証方式を選択し、クリックして**次**します。  
  
    Windows 認証は、Windows 資格情報を使用してのインスタンスにログオンしようとする[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 選択した場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を入力する必要があります、認証、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログイン名とパスワード。  
  
6.  操作の完了 ページで、 **OK**します。  
  
7.  [完了] ページで、次のようにクリックします。**終了**します。  
  
内のオブジェクトを確認するには、アンインストール プロセスが完了した後、 **sysdb.ssma_MySQL**スキーマ、および場合によっては、全体**sysdb**データベースを使用して削除されました[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]します。 ただし、他の SSMA 製品を使用する場合も使用、 **sysdb**データベース。 場合は、データベースが存在し、このデータベース内のオブジェクトに他のデータベースが参照されていないことを確認したら、データベースをデタッチすることができます。  
  
## <a name="see-also"></a>参照  
[SSMA for MySQL クライアントのインストール&#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[SQL Server での SSMA コンポーネントのインストール](installing-ssma-components-on-sql-server-mysqltosql.md)  
  
