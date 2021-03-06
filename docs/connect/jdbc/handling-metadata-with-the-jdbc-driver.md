---
title: JDBC ドライバーによるメタデータの処理 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5cfb35d4-ddcd-40a2-8091-f29cddc32552
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 57e5ac25c8196b15bd204e993090efd69f2cb55c
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2018
ms.locfileid: "42786698"
---
# <a name="handling-metadata-with-the-jdbc-driver"></a>JDBC ドライバーによるメタデータの処理
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース内のメタデータは、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] を使用して、さまざまな方法で操作することができます。 JDBC ドライバーでは、データベースのメタデータを、結果セットまたはパラメーターとして取得することができます。  
  
 JDBC ドライバーには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースからメタデータを取得するための 3 つのクラスがあります。  
  
-   [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) クラス。現在接続しているデータベースの情報が返されます。  
  
-   [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) クラス。結果セットの情報が返されます。  
  
-   [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md) クラス。準備されたステートメントおよび呼び出し可能なステートメントのパラメーターの情報が返されます。  
  
 このセクションのトピックでは、3 つのメタデータ クラスを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのメタデータを処理する方法を説明します。  
  
> [!NOTE]  
>  このセクションで説明されているメタデータ メソッドは、通常はアプリケーションのパフォーマンスに対する負荷が大きいため、使用する際は注意が必要です。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|[説明]|  
|-----------|-----------------|  
|[データベースのメタデータの使用](../../connect/jdbc/using-database-metadata.md)|現在接続しているデータベースのメタデータ情報を取得する方法を説明します。|  
|[結果セットのメタデータの使用](../../connect/jdbc/using-result-set-metadata.md)|現在の結果セットのメタデータ情報を取得する方法を説明します。|  
|[パラメーターのメタデータの使用](../../connect/jdbc/using-parameter-metadata.md)|準備されたステートメントおよび呼び出し可能なステートメントのパラメーターのメタデータ情報を取得する方法を説明します。|  
  
## <a name="see-also"></a>参照  
 [JDBC ドライバーの概要](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
