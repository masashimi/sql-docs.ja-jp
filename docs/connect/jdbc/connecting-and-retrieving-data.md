---
title: 接続およびデータの取得 |Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ce43cc20-46a3-42ff-a3fb-75ad1ed10e08
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 674903bc9e2b8818609def5006dfc7351266a89f
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784081"
---
# <a name="connecting-and-retrieving-data"></a>接続およびデータの取得

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] を使用する場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースへの接続を確立する 2 つの主な方法があります。 1 つは、接続 URL の接続プロパティを設定してから、DriverManager クラスの getConnection メソッドが呼び出され、[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトが返される方法です。  
  
> [!NOTE]  
> JDBC ドライバーでサポートされる接続のプロパティの一覧は、次を参照してください。[接続プロパティの設定](../../connect/jdbc/setting-the-connection-properties.md)します。  
  
2 つ目の方法では、[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) クラスの setter メソッドを使用して接続プロパティを設定してから、[getConnection](../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) メソッドが呼び出され、SQLServerConnection オブジェクトが返されます。  
  
このセクションのトピックでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに接続するさまざまな方法について説明し、データを取得するさまざまな手法も示します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
| トピック                                                                | [説明]                                                                                                                                                   |
| -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [接続 URL のサンプル](../../connect/jdbc/connection-url-sample.md) | 接続 URL を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続してから、SQL ステートメントを使用してデータを取得する方法について説明します。 |
| [データ ソースのサンプル](../../connect/jdbc/data-source-sample.md)       | データ ソースを使用して SQL Server に接続し、ストアド プロシージャを使用してデータを取得する方法について説明します。                                                 |
  
## <a name="see-also"></a>参照

[サンプル JDBC Driver アプリケーション](../../connect/jdbc/sample-jdbc-driver-applications.md)  
  