---
title: ATOMIC ブロック | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 40e0e749-260c-4cfc-a848-444d30c09d85
caps.latest.revision: 12
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: be0f2ca66b0d2efaf07e394c5912cbaa13518c88
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394524"
---
# <a name="atomic-blocks"></a>ATOMIC ブロック
  `BEGIN ATOMIC` は、ANSI SQL 標準の一部です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ネイティブ コンパイル ストアド プロシージャの最上位でのみ ATOMIC ブロックがサポートされます。  
  
-   各ネイティブ コンパイル ストアド プロシージャには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが正確に 1 ブロックずつ含まれています。 これが ATOMIC ブロックです。  
  
-   ネイティブでない、解釈された [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャおよびアドホック バッチでは、ATOMIC ブロックはサポートされません。  
  
 ATOMIC ブロックはトランザクション内部で (自動的に) 実行されます。 ブロック内のすべてのステートメントが成功するか、またはブロック全体がブロックの先頭で作成したセーブポイントまでロールバックされます。 また、ATOMIC ブロックのセッション設定は固定されています。 同じ ATOMIC ブロックを異なる設定のセッションで実行しても、現在のセッション設定とは関係なく動作は同じになります。  
  
## <a name="transactions-and-error-handling"></a>トランザクションとエラー処理  
 バッチによって `BEGIN TRANSACTION` ステートメントが実行されてトランザクションがアクティブな状態になっているため、トランザクションがセッションに存在する場合、ATOMIC ブロックの処理を開始するとトランザクションにセーブポイントが作成されます。 ブロックが例外なしで終了すると、ブロックに対して作成されたセーブポイントがコミットされますが、セッション レベルでコミットされるまでトランザクションはコミットされません。 ブロックで例外がスローされるとブロックの結果はロールバックされますが、例外によってトランザクションの失敗が決定的にならない限り、セッション レベルのトランザクションは続行されます。 たとえば、書き込みの競合によってトランザクションの失敗は決定的になりますが、型キャスト エラーの場合はそうではありません。  
  
 セッションにアクティブなトランザクションがない場合、`BEGIN ATOMIC` は新しいトランザクションを開始します。 ブロックのスコープ外でスローされる例外が存在しない場合、トランザクションはブロックの末尾でコミットされます。 ブロックで例外がスローされた場合 (つまり、ブロック内で例外をキャッチして処理できなかった場合)、トランザクションはロールバックされます。 1 つの atomic ブロック (1 つは、ストアド プロシージャをネイティブ コンパイル) にまたがるトランザクションの必要はありません書き込む明示的な`BEGIN TRANSACTION`と`COMMIT`または`ROLLBACK`ステートメント。  
  
 ストアド プロシージャのサポートをネイティブ コンパイル、 `TRY`、 `CATCH`、および`THROW`エラー処理を構築します。 `RAISERROR` サポートされていません。  
  
 次の例は、ATOMIC ブロックおよびネイティブ コンパイル ストアド プロシージャでのエラー処理動作を示しています。  
  
```tsql  
-- sample table  
CREATE TABLE dbo.t1 (  
  c1 int not null primary key nonclustered  
)  
WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
-- sample proc that inserts 2 rows  
CREATE PROCEDURE dbo.usp_t1 @v1 bigint not null, @v2 bigint not null  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS  
BEGIN ATOMIC  
WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english', DELAYED_DURABILITY = ON)  
  
  INSERT dbo.t1 VALUES (@v1)  
  INSERT dbo.t1 VALUES (@v2)  
  
END  
GO  
  
-- insert two rows  
EXEC dbo.usp_t1 1, 2  
GO  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify the rows 1 and 2 were committed  
SELECT c1 FROM dbo.t1  
GO  
  
-- execute proc with arithmetic overflow  
EXEC dbo.usp_t1 3, 4444444444444  
GO  
-- expected error message:  
-- Msg 8115, Level 16, State 0, Procedure usp_t1  
-- Arithmetic overflow error converting bigint to data type int.  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify rows 3 was not committed; usp_t1 has been rolled back  
SELECT c1 FROM dbo.t1  
GO  
  
-- start a new transaction  
BEGIN TRANSACTION  
  -- insert rows 3 and 4  
  EXEC dbo.usp_t1 3, 4  
  
  -- verify there is still an active transaction  
  SELECT @@TRANCOUNT  
  
  -- verify the rows 3 and 4 were inserted  
  SELECT c1 FROM dbo.t1 WITH (SNAPSHOT)   
  ORDER BY c1  
  
  -- catch the arithmetic overflow error  
  BEGIN TRY  
    EXEC dbo.usp_t1 5, 4444444444444  
  END TRY  
  BEGIN CATCH  
    PRINT N'Error occurred: ' + error_message()  
  END CATCH  
  
  -- verify there is still an active transaction  
  SELECT @@TRANCOUNT  
  
  -- verify rows 3 and 4 are still in the table, and row 5 has not been inserted  
  SELECT c1 FROM dbo.t1 WITH (SNAPSHOT)   
  ORDER BY c1  
  
COMMIT  
GO  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify rows 3 and 4 has been committed  
SELECT c1 FROM dbo.t1  
ORDER BY c1  
GO  
```  
  
 メモリ最適化テーブルに固有の次のエラー メッセージは、トランザクションの失敗が決定的であることを示しています。 ATOMIC ブロックのスコープ内で、10772、41301、41302、41305、41325、41332、または 41333 のエラーが発生した場合、トランザクションは中止されます。  
  
## <a name="session-settings"></a>セッションの設定  
 ATOMIC ブロックのセッション設定は、ストアド プロシージャのコンパイル時に固定されます。 一部の設定で指定できます`BEGIN ATOMIC`他の設定は、常に同じ値に固定します。  
  
 `BEGIN ATOMIC` では以下のオプションは必須です。  
  
|必須の設定|説明|  
|----------------------|-----------------|  
|`TRANSACTION ISOLATION LEVEL`|サポートされる値は`SNAPSHOT`、 `REPEATABLEREAD`、および`SERIALIZABLE`します。|  
|`LANGUAGE`|日付と時刻の形式とシステム メッセージが決まります。 [sys.syslanguages &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-syslanguages-transact-sql) のすべての言語とエイリアスがサポートされます。|  
  
 次の設定は省略可能です。  
  
|省略可能な設定|説明|  
|----------------------|-----------------|  
|`DATEFORMAT`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべての日付形式がサポートされています。 指定した場合、`DATEFORMAT`に関連付けられている既定の日付形式を上書き`LANGUAGE`します。|  
|`DATEFIRST`|指定した場合、`DATEFIRST` は `LANGUAGE` に関連付けられた既定値をオーバーライドします。|  
|`DELAYED_DURABILITY`|サポートされる値は`OFF`と`ON`します。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によるトランザクションのコミットには、完全持続性、既定値、または遅延持続性が適用されます。詳細については、「[Control Transaction Durability](../logs/control-transaction-durability.md)」 (トランザクションの持続性の制御) を参照してください。|  
  
 次の SET オプションには、すべてのネイティブ コンパイル ストアド プロシージャのすべての ATOMIC ブロックについて同じシステム既定値が設定されます。  
  
|SET オプション|ATOMIC ブロックのシステム既定値|  
|----------------|--------------------------------------|  
|ANSI_NULLS|ON|  
|ANSI_PADDING|ON|  
|ANSI_WARNING|ON|  
|ARITHABORT|ON|  
|ARITHIGNORE|OFF|  
|CONCAT_NULL_YIELDS_NULL|ON|  
|IDENTITY_INSERT|OFF|  
|NOCOUNT|ON|  
|NUMERIC_ROUNDABORT|OFF|  
|QUOTED_IDENTIFIER|ON|  
|ROWCOUNT|0|  
|TEXTSIZE|0|  
|XACT_ABORT|OFF<br /><br /> 処理できない例外により ATOMIC ブロックはロールバックされますが、そのエラーが致命的でない限りトランザクションは中止されません。|  
  
## <a name="see-also"></a>参照  
 [ネイティブ コンパイル ストアド プロシージャ](natively-compiled-stored-procedures.md)  
  
  
