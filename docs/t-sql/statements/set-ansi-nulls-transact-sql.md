---
title: SET ANSI_WARNINGS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SET_ANSI_NULLS_TSQL
- ANSI_NULLS
- SET ANSI_NULLS
- ANSI_NULLS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET ANSI_NULLS statement
- not equal to operator (<>)
- ANSI_NULLS option
- equals operator (=)
- null values [SQL Server], comparison operators
- comparison operators [SQL Server], null values
ms.assetid: aae263ef-a3c7-4dae-80c2-cc901e48c755
caps.latest.revision: 43
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2c26c23cfca578a7d729aac4dd3817f6dc24f954
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43083231"
---
# <a name="set-ansinulls-transact-sql"></a>SET ANSI_NULLS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で = (等号) 比較演算子と <> (不等号) 比較演算子を NULL 値に対して使用した場合の ISO 準拠動作を指定します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の今後のバージョンでは、ANSI_NULLS が ON になり、このオプションを明示的に OFF に設定するすべてのアプリケーションでエラーが発生します。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="syntax"></a>構文

```
-- Syntax for SQL Server

SET ANSI_NULLS { ON | OFF }
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET ANSI_NULLS ON
```

## <a name="remarks"></a>Remarks  
 SET ANSI_NULLS が ON の場合、WHERE *column_name* = **NULL** を使用する SELECT ステートメントを実行すると、*column_name* に NULL 値が指定されていても、0 行が返されます。 WHERE *column_name* <> **NULL** を使用する SELECT ステートメントでは、*column_name* に NULL 以外の値が指定されていても、0 行が返されます。  
  
 SET ANSI_NULLS が OFF の場合は、= (等号) 比較演算および <> (不等号) 比較演算の実行結果に、ISO 標準が適用されません。 WHERE *column_name* = **NULL** を使用する SELECT ステートメントでは、*column_name* に NULL 値を持つ行が返されます。 WHERE *column_name* <> **NULL** を使用する SELECT ステートメントでは、列に NULL 以外の値を持つ行が返されます。 また、WHERE *column_name* <> *XYZ_value* を使用する SELECT ステートメントでは、*XYZ_value* 以外の非 NULL 値を持つすべての行が返されます。  
  
 SET ANSI_NULLS が ON に設定されていると、NULL 値に対するすべての比較は UNKNOWN に評価されます。 SET ANSI_NULLS が OFF に設定されていて、データ値が NULL の場合は、NULL 値に対するすべてのデータ比較は TRUE に評価されます。 SET ANSI_NULLS が指定されていない場合は、現在のデータベースの ANSI_NULLS オプションの設定が適用されます。 ANSI_NULLS データベース オプションについて詳しくは、「[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)」を参照してください。  

 次の表は、ANSI_NULLS の設定が null 値と非 null 値を利用したさまざまなブール式の結果に影響を与えるしくみを示しています。  
  
|ブール式|SET ANSI_NULLS ON|SET ANSI_NULLS OFF|  
|---------------|---------------|------------|  
|NULL = NULL|UNKNOWN|TRUE|  
|1 = NULL|UNKNOWN|FALSE|  
|NULL <> NULL|UNKNOWN|FALSE|  
|1 <> NULL|UNKNOWN|TRUE|  
|NULL > NULL|UNKNOWN|UNKNOWN|  
|1 > NULL|UNKNOWN|UNKNOWN|  
|NULL IS NULL|TRUE|TRUE|  
|1 IS NULL|FALSE|FALSE|  
|NULL IS NOT NULL|FALSE|FALSE|  
|1 IS NOT NULL|TRUE|TRUE|  

 比較のオペランドの 1 つが NULL またはリテラル NULL のいずれかの変数であるとき、SET ANSI_NULLS が ON の場合のみ比較に影響します。 比較の両側が列または複合式の場合は、この設定は比較に影響しません。  
  
 スクリプトが意図どおりに動作するようにするには、ANSI_NULLS データベース オプションや SET ANSI_NULLS の設定とは無関係に、NULL 値を含む可能性のある比較で、IS NULL と IS NOT NULL を使用するようにしてください。  
  
 分散クエリを実行する際には、SET ANSI_NULLS を ON に設定してください。  
  
 計算列やインデックス付きビューのインデックスを作成または変更するときには、SET ANSI_NULLS を ON に設定する必要があります。 SET ANSI_NULLS が OFF の場合、計算列にインデックスが設定されているテーブルやインデックス付きビューにおける CREATE、UPDATE、INSERT、および DELETE のステートメントはいずれも失敗します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、要求された値に違反するすべての SET オプションを一覧表示するエラーが返されます。 また、SELECT ステートメントの実行時に SET ANSI_NULLS が OFF の場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は計算列やビュー上のインデックス値を無視し、テーブルやビューにそのようなインデックスがないものとして SELECT 操作を処理します。  
  
> [!NOTE]  
>  ANSI_NULLS は、計算列およびインデックス付きビューにおいてインデックスを操作するときに、指定された値に設定する必要がある 7 つの SET オプションの中の 1 つです。 オプションの ANSI_PADDING、ANSI_WARNINGS、ARITHABORT、QUOTED_IDENTIFIER、および CONCAT_NULL_YIELDS_NULL も ON に設定する必要があります。また、NUMERIC_ROUNDABORT は OFF に設定する必要があります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、接続時に自動的に ANSI_NULLS が ON に設定されます。 この設定は、ODBC データ ソースまたは ODBC 接続属性で構成でき、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続する前にアプリケーションの内部で設定される OLE DB 接続プロパティでも構成できます。 SET ANSI_NULLS の既定値は OFF です。  
  
 SET ANSI_DEFAULTS が ON の場合には、SET ANSI_NULLS は有効 (ON) になります。  
  
 SET ANSI_NULLS は、解析時ではなく実行時に設定されます。  
  
 この設定の現在の設定を表示するには、次のクエリを実行します。
  
```  
DECLARE @ANSI_NULLS VARCHAR(3) = 'OFF';  
IF ( (32 & @@OPTIONS) = 32 ) SET @ANSI_NULLS = 'ON';  
SELECT @ANSI_NULLS AS ANSI_NULLS;  
  
```  
  
## <a name="permissions"></a>アクセス許可  
 public ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、`=` (等号) 比較演算子と `<>` (不等号) 比較演算子を使用して、テーブル内の `NULL` 値と NULL 以外の値を比較します。 例は `IS NULL` が `SET ANSI_NULLS` 設定に影響されないことも示しています。  
  
```  
-- Create table t1 and insert values.  
CREATE TABLE dbo.t1 (a INT NULL);  
INSERT INTO dbo.t1 values (NULL),(0),(1);  
GO  
  
-- Print message and perform SELECT statements.  
PRINT 'Testing default setting';  
DECLARE @varname int;   
SET @varname = NULL;  
  
SELECT a  
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- SET ANSI_NULLS to ON and test.  
PRINT 'Testing ANSI_NULLS ON';  
SET ANSI_NULLS ON;  
GO  
DECLARE @varname int;  
SET @varname = NULL  
  
SELECT a   
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- SET ANSI_NULLS to OFF and test.  
PRINT 'Testing SET ANSI_NULLS OFF';  
SET ANSI_NULLS OFF;  
GO  
DECLARE @varname int;  
SET @varname = NULL;  
SELECT a   
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- Drop table t1.  
DROP TABLE dbo.t1;  
  
```  
  
## <a name="see-also"></a>参照  
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/sessionproperty-transact-sql.md)   
 [= &#40;等号&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/equals-transact-sql.md)   
 [IF...ELSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/if-else-transact-sql.md)   
 [&#60;&#62; &#40;不等号&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/not-equal-to-transact-sql-traditional.md)   
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [WHILE &#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)  
  
  
