---
title: sp_get_query_template (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_get_query_template
- sp_get_query_template_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_get_query_template
ms.assetid: 85e9bef7-2417-41a8-befa-fe75507d9bf2
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e2d96ffa9a2375905246a515601c77afdc50d231
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43027748"
---
# <a name="spgetquerytemplate-transact-sql"></a>sp_get_query_template (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  パラメーター化形式のクエリを返します。 返される結果は、強制パラメーター化の使用によるパラメーター化形式のクエリに似ています。 sp_get_query_template は、主に TEMPLATE プラン ガイドの作成時に使用されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_get_query_template  
   [ @querytext = ] N'query_text'  
   , @templatetext OUTPUT   
   , @parameters OUTPUT   
```  
  
## <a name="arguments"></a>引数  
 '*ステートメント*'  
 パラメーター化バージョンを生成する基となるクエリです。 '*ステートメント*' 単一引用符で囲む必要があり、前に、n 個の Unicode を指定します。 N'*ステートメント*' に割り当てられた値は、@querytextパラメーター。 これは、型の**nvarchar (max)** します。  
  
 @templatetext  
 型の出力パラメーター **nvarchar (max)** に示されるように、パラメーター化形式の受信に用意されている*ステートメント*文字列リテラルとして。  
  
 @parameters  
 型の出力パラメーター **nvarchar (max)** でパラメーター化されたパラメーター名とデータ型のリテラル文字列を受信する、指定したとおりに提供@templatetextします。  
  
## <a name="remarks"></a>コメント  
 sp_get_query_template は、以下のことが発生した場合にエラーを返します。  
  
-   内の定数リテラル値をパラメーター化は*ステートメント*します。  
  
-   *ステートメント*が null の場合、Unicode 文字列ではなく、構文が正しくない、またはコンパイルすることはできません。  
  
 Sp_get_query_template は、エラーを返した場合の値は変更されません、@templatetextと@parameters出力パラメーター。  
  
## <a name="permissions"></a>アクセス許可  
 public データベース ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、2 つの定数リテラル値が含まれたパラメーター化形式のクエリが返されます。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @my_templatetext nvarchar(max)  
DECLARE @my_parameters nvarchar(max)  
EXEC sp_get_query_template   
    N'SELECT pi.ProductID, SUM(pi.Quantity) AS Total  
        FROM Production.ProductModel pm   
        INNER JOIN Production.ProductInventory pi  
        ON pm.ProductModelID = pi.ProductID  
        WHERE pi.ProductID = 2  
        GROUP BY pi.ProductID, pi.Quantity  
        HAVING SUM(pi.Quantity) > 400',  
@my_templatetext OUTPUT,  
@my_parameters OUTPUT;  
SELECT @my_templatetext;  
SELECT @my_parameters;  
```  
  
 パラメーター化の結果の次のとおり、`@my_templatetext``OUTPUT`パラメーター。  
  
 `select pi . ProductID , SUM ( pi . Quantity ) as Total`  
  
 `from Production . ProductModel pm`  
  
 `inner join Production . ProductInventory pi`  
  
 `on pm . ProductModelID = pi . ProductID`  
  
 `where pi . ProductID = @0`  
  
 `group by pi . ProductID , pi . Quantity`  
  
 `having SUM ( pi . Quantity ) > 400`  
  
 なお、最初の定数リテラル`2`パラメーターに変換されます。 2 番目のリテラル `400` は `HAVING` 句の内部にあるため、変換されません。 sp_get_query_template によって返される結果は、ALTER DATABASE の PARAMETERIZATION オプションが FORCED に設定されている場合のパラメーター化形式クエリに似ています。  
  
 パラメーター化の結果の次のとおり、`@my_parameters OUTPUT`パラメーター。  
  
```  
@0 int  
```  
  
> [!NOTE]  
>  sp_get_query_template の出力内のパラメーターの順序と名前は、Quick Fix Engineering、Service Pack、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンのアップグレードによって変化する可能性があります。 アップグレードによって、同じクエリに対して異なる定数リテラル群がパラメーター化されるようになったり、両方の出力パラメーターの結果に使用される文字間隔が変化したりする可能性もあります。  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [プラン ガイドを使用したクエリのパラメーター化動作の指定](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)  
  
  
