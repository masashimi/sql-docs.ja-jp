---
title: 資格情報 (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- principals [SQL Server], credentials
- schemas [SQL Server], credentials
- permissions [SQL Server], credentials
- groups [SQL Server], credentials
- ALTER ANY CREDENTIAL permission
- security [SQL Server], credentials
- authentication [SQL Server], credentials
- users [SQL Server], credentials
- credentials [SQL Server], about credentials
- credentials [SQL Server]
ms.assetid: c8df6022-e0b4-46b8-9670-3f86938d3177
caps.latest.revision: 31
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0453d00704ff56da07653b924d02a393d36eaeb0
ms.sourcegitcommit: e4e9f02b5c14f3bb66e19dec98f38c012275b92c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2018
ms.locfileid: "43118100"
---
# <a name="credentials-database-engine"></a>資格情報 (データベース エンジン)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  資格情報は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]外部のリソースへの接続に必要な認証情報 (資格情報) を含むレコードです。 この情報は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]によって内部的に使用されます。 通常、資格情報には Windows ユーザー名とパスワードが含まれます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証経由で接続しているユーザーは、資格情報に格納された情報によって、サーバー インスタンスの外部のリソースにアクセスできるようになります。 外部リソースが Windows である場合、ユーザーは、資格情報に指定されている Windows ユーザーとして認証されます。 1 つの資格情報を複数の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインにマッピングすることもできます。 ただし、1 つの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインは 1 つの資格情報にしかマップできません。  
  
 マスター データベースに保存され、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンス全体で使用できる資格情報については、「[CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)」を参照してください。 特定のデータベースで使用され、そのデータベースとともに移植可能な資格情報については、「[CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-scoped-credential-transact-sql.md)」を参照してください。  
  
 システム資格情報は、自動的に作成され、特定のエンドポイントに関連付けられます。 システム資格情報の名前は 2 つのシャープ記号 (##) で始まります。  
  
 資格情報の詳細については、[sys.credentials](../../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md) カタログ ビューおよび [sys.database_scoped_credentials](../../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) カタログ ビューを参照してください。  
  
## <a name="related-content"></a>関連コンテンツ  
 [資格情報の作成](../../../relational-databases/security/authentication-access/create-a-credential.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
 [SQL Server の保護](../../../relational-databases/security/securing-sql-server.md)  
  
  
