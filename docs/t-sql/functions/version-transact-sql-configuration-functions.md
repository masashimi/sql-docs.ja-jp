---
title: '@@VERSION (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/20/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- '@@VERSION'
- '@@VERSION_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@VERSION function'
- current SQL Server installation information
- versions [SQL Server], @@VERSION
- processors [SQL Server], types
ms.assetid: 385ba80e-7c28-41a5-9cdb-5648f3785983
caps.latest.revision: 40
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d7396889e04ad0b86ca9e0f25243baed3010ff0d
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43058094"
---
# <a name="x40x40version---transact-sql-configuration-functions"></a>&#x40;&#x40;バージョン - Transact SQL 構成関数
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  現在インストールされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に関するシステム情報およびビルド情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
@@VERSION  
```  
  
## <a name="return-types"></a>戻り値の型  
 **nvarchar**  
  
## <a name="remarks"></a>Remarks  
 @@VERSION の結果は 1 つの nvarchar 文字列として表示されます。 を使用する [SERVERPROPERTY (& a) #40 です。TRANSACT-SQL と #41;](../../t-sql/functions/serverproperty-transact-sql.md) 個々 のプロパティの値を取得します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、次の情報が返されます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョン  
  
-   プロセッサ アーキテクチャ  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のビルド日  
  
-   著作権情報  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エディション  
  
-   オペレーティング システムのバージョン  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]では、次の情報が返されます。  
  
-   エディション - "Microsoft SQL Azure"  
  
-   製品レベル - "(RTM)"  
  
-   製品バージョン  
  
-   ビルド日  
  
-   著作権情報  

> [!NOTE]  
> @@VERSION によって報告された製品バージョンが Azure SQL Database で正しくない問題を認識しています。 Azure SQL Database で実行される SQL Server データベース エンジンのバージョンは常に、SQL Server のオンプレミスのバージョンより新しいため、最新のセキュリティ修正プログラムが含まれています。 これは、パッチ レベルが SQL Server のオンプレミスのバージョンと同じかそれより新しく、SQL Server で使用できる最新の機能が Azure SQL Database で使用できることを意味します。
>
> エンジンのエディションをプログラムで確認するには、SELECT SERVERPROPERTY('EngineEdition') を使用します。 このクエリでは、スタンドアロンのデータベースの場合に '5'、Azure SQL Database のマネージド インスタンスの場合に '8' を返します。 
>
> この問題が解決されたら、ドキュメントを更新します。

  
## <a name="examples"></a>使用例  
  
### <a name="a-return-the-current-version-of-includessnoversionincludesssnoversion-mdmd"></a>A: 現在のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を返す  
 次の例では、現在のインストールに関するバージョン情報を返します。  
  
```  
SELECT @@VERSION AS 'SQL Server Version';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-return-the-current-version-of-includessdwincludesssdw-mdmd"></a>B. 現在のバージョンの [!INCLUDE[ssDW](../../includes/ssdw-md.md)] を返す  
  
```  
SELECT @@VERSION AS 'SQL Server PDW Version';  
```  
  
## <a name="see-also"></a>参照  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)  
  
  

