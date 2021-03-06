---
title: データ型 (JDBC) の使用 |Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b39f44d0-3710-4bc6-880c-35bd8c10a734
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 81a71bc89bf4dcf62bb5119bc8af60664f33a75a
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784951"
---
# <a name="working-with-data-types-jdbc"></a>データ型の処理 (JDBC)

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] の主な機能は、Java 開発者が、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースに含まれたデータにアクセスできるようにすることです。 これを可能にするために、JDBC ドライバーは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型と Java 言語の型やオブジェクトとの間の変換を仲介します。  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] および JDBC ドライバーのデータ型の相違や、これらのデータ型を Java 言語のデータ型に変換する方法などの詳細については、「[JDBC ドライバーのデータ型について](../../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)」を参照してください。  
  
SQL Server のデータ型を処理するために、JDBC ドライバーには、[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) クラスおよび [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) クラスに get\<Type> メソッドおよび set\<Type> メソッドがあり、[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) クラスに get\<Type> メソッドおよび update\<Type> メソッドがあります。 使用するメソッドは、処理するデータの型と、結果セットまたはクエリを使用するかどうかによって決まります。  
  
このセクションのトピックでは、JDBC ドライバーのデータ型を使用して Java アプリケーションの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データにアクセスする方法について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
| トピック                                                                         | [説明]                                                                                                                                                                                                                                                  |
| ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [基本データ型のサンプル](../../../connect/jdbc/code-samples/basic-data-types-sample.md)   | 結果セットの getter メソッドを使用して基本的な [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型の値を取得する方法と、結果セットの update メソッドを使用してそれらの値を更新する方法を示しています。                                             |
| [SQLXML データ型のサンプル](../../../connect/jdbc/code-samples/sqlxml-data-type-sample.md)   | XML データのリレーショナル データベースへの格納、データベースからの XML データの取得、および、XML データの解析を、**SQLXML** Java データ型を使用して行う方法を示しています。                                                                                   |
| [空間データ型のサンプル](../../../connect/jdbc/code-samples/spatial-data-types-sample.md) | SQL Server の空間データ型を格納する方法と SQL Server からこれらの型を取得する方法について説明します。 新しく定義したクラスを使用する方法についても説明します。 **Geometry**と**Geography** Java リファレンスのこれらのデータ型を管理するため、ドライバーから。 |
  
## <a name="see-also"></a>参照

[サンプル JDBC Driver アプリケーション](../../../connect/jdbc/code-samples/sample-jdbc-driver-applications.md)  
