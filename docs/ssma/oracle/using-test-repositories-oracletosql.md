---
title: テスト リポジトリ (OracleToSQL) の使用 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Test Cases Repository
- Test Results Repository
ms.assetid: f941cce4-d3e3-4aeb-a88a-4f101a97a9f4
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 863fee753776b0e86408d6ccd0d9d7e0cfc7f33b
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979744"
---
# <a name="using-test-repositories-oracletosql"></a>テスト リポジトリ (OracleToSQL) の使用
SSMA テスト リポジトリ ストア SSMA テスター テスト_ケースとテストの結果を後で使用します。 リポジトリのデータは、SQL Server テーブルに保存されます**TestCaseRepository**と**RunTestCaseResultRepository**スキーマ**ssma_oracle_utilities** の**ssmatesterdb**データベース。  
  
次のボタンは、リポジトリのテスト ケース ダイアログ ボックスを使用できます。  
  
-   をクリックして、**更新**テスト_ケースまたはテスト結果の一覧を更新するボタンをクリックします。  
  
-   をクリックして、**閉じます**リポジトリのテスト ケース ダイアログ ボックスを閉じるボタンをクリックします。  
  
## <a name="test-cases-repository"></a>テスト_ケースのリポジトリ  
クリックして、テスト_ケースのリポジトリを表示する**テスト_ケース.** **テスター**メニュー。 SSMA は、表示、**テスト_ケース リポジトリ**ダイアログ ウィンドウに保存されているテスト_ケースの一覧で、**テスト_ケース**ページ。  
  
グリッドには、各テスト・ケースに関する次の情報が表示されます。  
  
-   名前: テスト_ケース名前。  
  
-   作成されます。 テスト_ケースの作成日。  
  
-   更新日時: テスト_ケース最終更新日。  
  
-   説明: テスト ケース説明です。  
  
次のボタンが [テスト_ケース] ページで。  
  
-   をクリックして、**追加**テスト_ケース ウィザードを実行し、新しいテストを作成するボタンをクリックします。  
  
-   をクリックして、**削除**をリポジトリから、選択したテストを削除します。テスト_ケースが削除されると、関連するすべてのテスト結果も削除されます。  
  
-   をクリックして、**編集**テスト_ケース ウィザードを実行し、選択したテストを変更するボタンをクリックします。  
  
-   をクリックして、**実行**ボタンをクリックする、[を実行しているテスト_ケースは (OracleToSQL)](http://msdn.microsoft.com/fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02)ダイアログし、選択したテストを実行します。  
  
## <a name="test-results-repository"></a>テストの結果リポジトリ  
テストの結果リポジトリを表示することができます、**テスト結果**のページ、**テスト_ケース リポジトリ**ウィンドウ。 クリックして開きます**テスト結果.** **テスター**メニュー。  
  
2 つのフィルターを使用して、**テスト結果**ページ。  
  
-   名前のテスト ケース フィルター: テスト_ケースの名前でテスト結果を選択できます。 このフィルターの**すべてのテスト_ケース**値により、すべてのテスト_ケースのテスト結果を表示します。  
  
-   実行日のテスト ケース フィルター: 保存の日付でのテスト結果をフィルターします。このフィルターの**すべて期間**保存の任意の日付のテスト結果を表示する値を使用できます。  
  
テスト結果の詳細については、次の情報がグリッドに表示されます。  
  
-   名前: テスト_ケースの名前。  
  
-   保存されます。 保存のケースの日付をテストします。  
  
-   結果: テストの実行 (このセルのツールヒントには、テストの実行の完全な概要が表示されます) の概要。  
  
次のボタンは、テスト結果 ページで入手できます。  
  
-   をクリックして、**ビュー**ボタンをクリックする[テスト_ケースのレポートを表示する&#40;OracleToSQL&#41; ](../../ssma/oracle/viewing-test-case-reports-oracletosql.md)の現在のテスト_ケースの結果。  
  
-   をクリックして、**削除** ボタンを選択したテスト結果を削除するには  
  
## <a name="see-also"></a>参照  
[テスト_ケースを実行している&#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[移行されたデータベース オブジェクトのテスト&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
