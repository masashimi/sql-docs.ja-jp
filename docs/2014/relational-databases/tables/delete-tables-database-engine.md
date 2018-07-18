---
title: テーブルの削除 (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- table deletions [SQL Server]
- deleting tables
- removing tables
- dropping tables
ms.assetid: ca6aa3e9-9885-44c3-bafc-aec441fd97ec
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: de80b12cb5fbe72e520c6f6cf53e671cabfa7145
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37201172"
---
# <a name="delete-tables-database-engine"></a>テーブルの削除 (データベース エンジン)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用してデータベースからテーブルを削除できます。  
  
> [!CAUTION]  
>  テーブルの削除については、十分に検討してください。 テーブルを参照するクエリ、ビュー、ユーザー定義関数、ストアド プロシージャ、またはプログラムがある場合は、テーブルを削除すると、各オブジェクトが無効になります。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **テーブルを削除する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 作業を開始する準備  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   FOREIGN KEY 制約によって参照されているテーブルを削除することはできません。 まず、参照している FOREIGN KEY 制約または参照テーブルを削除する必要があります。 参照しているテーブルと、主キーを格納しているテーブルの両方を同じ DROP TABLE ステートメントで削除する場合には、参照しているテーブルを先に指定する必要があります。  
  
-   テーブルを削除すると、そのテーブルのルールや既定値はバインドを失い、そのテーブルに関係付けられている制約やトリガーも自動的に削除されます。 テーブルを再作成する場合は、適切なルールや既定値を再バインドし、トリガーを再作成し、必要なすべての制約を追加する必要があります。  
  
-   含むテーブルを削除する場合、 `varbinary (max)` FILESTREAM 属性、ファイル システムに格納されているデータを持つ列は削除されません。  
  
-   DROP TABLE と CREATE TABLE を同じバッチ内の同じテーブルに対して実行しないでください。 実行した場合、予期しないエラーが発生する可能性があります。  
  
-   削除されたテーブルを参照しているすべてのビューとストアド プロシージャを、明示的に削除するか、変更してテーブルへの参照を削除する必要があります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 テーブルが属するスキーマに対する ALTER 権限、テーブルに対する CONTROL 権限、または **db_ddladmin** 固定データベース ロールのメンバーシップが必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-delete-a-table-from-the-database"></a>データベースからテーブルを削除するには  
  
1.  オブジェクト エクスプローラーで、削除するテーブルを選択します。  
  
2.  テーブルを右クリックし、ショートカット メニューの **[削除]** をクリックします。  
  
3.  削除の確認を要求するメッセージ ボックスが表示されます。 **[はい]** をクリックします。  
  
    > [!NOTE]  
    >  テーブルを削除すると、テーブルへのリレーションシップが自動的に削除されます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-delete-a-table-in-query-editor"></a>クエリ エディターでテーブルを削除するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    DROP TABLE dbo.PurchaseOrderDetail;  
  
    ```  
  
 詳細については、「[DROP TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-table-transact-sql)」を参照してください。  
  
  