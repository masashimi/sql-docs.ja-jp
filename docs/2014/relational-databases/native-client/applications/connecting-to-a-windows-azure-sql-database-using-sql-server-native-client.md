---
title: SQL Server Native Client を使用して Azure SQL Database に接続する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 0dc20bb6-b142-4259-b87b-427d2ba798af
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c0734537d44382e6a638b3033d4a3d822821dbf
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393755"
---
# <a name="connecting-to-a-azure-sql-database-using-sql-server-native-client"></a>SQL Server Native Client を使用した Azure SQL データベースへの接続
  接続する方法を示すサンプルについては、[!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]を使用して[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ネイティブ クライアントを参照してください[の開発: 操作方法に関するトピック (Windows Azure SQL データベース)](http://msdn.microsoft.com/library/ee621787.aspx)。  
  
## <a name="known-issues-when-connecting-to-a-sql-database"></a>SQL データベースに接続するときの既知の問題  
 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] Native Client を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に接続する場合、次のような既知の問題があります。  
  
-   各段階で `SQLBrowseConnect` が使用されている場合、`SQLBrowseConnect` との接続が拒否される可能性がある。  たとえば、最初の通話でドライバー名が送信され、サーバーと資格情報 (ユーザー名とパスワード) が 2 番目の通話で送信されて接続が確立し、データベース名と言語が 3 番目の通話で送信されたとします。  3 番目の通話によって、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は USE ステートメントを発行してデータベースを変更します。 しかし、USE ステートメントは [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] ではサポートされないため、次のエラーが生成されます。  
  
    ```  
    [Microsoft][SQL Server Native Client 11.0][SQL Server]USE statement is not supported to switch between databases. Use a new connection to connect to a different Database.  
    ```  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client を使用したアプリケーションのビルド](building-applications-with-sql-server-native-client.md)  
  
  
