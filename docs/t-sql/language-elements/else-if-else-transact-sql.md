---
title: ELSE (IF...ELSE) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ELSE
- ELSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ELSE (IF...ELSE) keyword
- ELSE keyword
- IF keyword
ms.assetid: 6f2b4278-0dea-4603-bbd3-7cbad602a645
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bf41c43143dee3d4fa21594ab320b35182fd931e
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43068073"
---
# <a name="else-ifelse-transact-sql"></a>ELSE (IF...ELSE) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行する条件を設定します。 *Boolean_expression* が TRUE に評価された場合、*Boolean_expression* に続く [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント (*sql_statement*) が実行されます。 オプションの ELSE キーワードは、*Boolean_expression* が FALSE または NULL と評価される場合に、代わりに実行される [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを指定します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
IF Boolean_expression   
     { sql_statement | statement_block }   
[ ELSE   
     { sql_statement | statement_block } ]   
```  
  
## <a name="arguments"></a>引数  
 *Boolean_expression*  
 TRUE または FALSE を返す式です。 *Boolean_expression* が SELECT ステートメントを含む場合は、SELECT ステートメントをかっこで囲む必要があります。  
  
 { *sql_statement* | *statement_block* }  
 有効な 1 つの [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、またはステートメント ブロックとして定義した一連のステートメントです。 ステートメント ブロック (バッチ) を定義するのには、BEGIN と END は、フロー制御言語キーワードを使用します。 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントはすべて BEGIN...END ブロック内で有効ですが、同じバッチ (ステートメント ブロック) 内で一緒にグループ化できない [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントもあります。  
  
## <a name="result-types"></a>戻り値の型  
 **ブール値**  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-a-simple-boolean-expression"></a>A. 簡単なブール式を使用する  
 次の例では、簡単なブール式 (`1=1`) があり、これは true であるため、最初のステートメントが出力されます。  
  
```  
IF 1 = 1 PRINT 'Boolean_expression is true.'  
ELSE PRINT 'Boolean_expression is false.' ;  
```  
  
 次の例の簡単なブール式 (`1=2`) は false を返します。したがって、この例では 2 番目のステートメントが出力されます。  
  
```  
IF 1 = 2 PRINT 'Boolean_expression is true.'  
ELSE PRINT 'Boolean_expression is false.' ;  
GO  
```  
  
### <a name="b-using-a-query-as-part-of-a-boolean-expression"></a>B. クエリをブール式の一部として使用する  
 次の例では、クエリをブール式の一部として実行します。 `Product` テーブルには `WHERE` 句を満たす自転車が 10 台あるため、最初の print ステートメントが実行されます。 どのような場合に 2 番目のステートメントが実行されるかを確認するには、`> 5` を `> 15` に変更します。  
  
```  
USE AdventureWorks2012;  
GO  
IF   
(SELECT COUNT(*) FROM Production.Product WHERE Name LIKE 'Touring-3000%' ) > 5  
PRINT 'There are more than 5 Touring-3000 bicycles.'  
ELSE PRINT 'There are 5 or less Touring-3000 bicycles.' ;  
GO  
```  
  
### <a name="c-using-a-statement-block"></a>C. ステートメント ブロックを使用する  
 次の例では、クエリをブール式の一部として実行してから、ブール式の結果に基づいて若干異なるステートメント ブロックを実行します。 各ステートメント ブロックは `BEGIN` で始まり、`END` で終わります。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @AvgWeight decimal(8,2), @BikeCount int  
IF   
(SELECT COUNT(*) FROM Production.Product WHERE Name LIKE 'Touring-3000%' ) > 5  
BEGIN  
   SET @BikeCount =   
        (SELECT COUNT(*)   
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%');  
   SET @AvgWeight =   
        (SELECT AVG(Weight)   
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%');  
   PRINT 'There are ' + CAST(@BikeCount AS varchar(3)) + ' Touring-3000 bikes.'  
   PRINT 'The average weight of the top 5 Touring-3000 bikes is ' + CAST(@AvgWeight AS varchar(8)) + '.';  
END  
ELSE   
BEGIN  
SET @AvgWeight =   
        (SELECT AVG(Weight)  
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%' );  
   PRINT 'Average weight of the Touring-3000 bikes is ' + CAST(@AvgWeight AS varchar(8)) + '.' ;  
END ;  
GO  
```  
  
### <a name="d-using-nested-ifelse-statements"></a>D. 入れ子になった IF...ELSE ステートメントを使用する  
 次の例では、IF のかを示します。 別の内部は、ELSE ステートメントを入れ子にすることができます。 各ステートメントをテストするには、`@Number` 変数を `5`、`50`、および `500` に設定します。  
  
```  
DECLARE @Number int;  
SET @Number = 50;  
IF @Number > 100  
   PRINT 'The number is large.';  
ELSE   
   BEGIN  
      IF @Number < 10  
      PRINT 'The number is small.';  
   ELSE  
      PRINT 'The number is medium.';  
   END ;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-a-query-as-part-of-a-boolean-expression"></a>E. クエリをブール式の一部として使用する  
 次の例では、`IF…ELSE` を使用し、`DimProduct` テーブルの項目の重み付けを基にして、2 つの応答のどちらをユーザーに表示するかを決定します。  
  
```  
-- Uses AdventureWorks  
  
DECLARE @maxWeight float, @productKey integer  
SET @maxWeight = 100.00  
SET @productKey = 424  
IF @maxWeight <= (SELECT Weight from DimProduct WHERE ProductKey=@productKey)   
    (SELECT @productKey, EnglishDescription, Weight, 'This product is too heavy to ship and is only available for pickup.' FROM DimProduct WHERE ProductKey=@productKey)  
ELSE  
    (SELECT @productKey, EnglishDescription, Weight, 'This product is available for shipping or pickup.' FROM DimProduct WHERE ProductKey=@productKey)  
```  
  
## <a name="see-also"></a>参照  
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [フロー制御言語 &#40;TRANSACT-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [IF...ELSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/if-else-transact-sql.md)  
  
  


