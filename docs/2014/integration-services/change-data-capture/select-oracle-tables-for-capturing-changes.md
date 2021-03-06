---
title: 変更をキャプチャするための Oracle テーブルの選択 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- selOraTabDia
ms.assetid: 2e295dc8-999d-4c4d-96cc-1519674b47a4
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8bff65efbe755045a46721436d3b058725b9ed31
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37150963"
---
# <a name="select-oracle-tables-for-capturing-changes"></a>変更をキャプチャするための Oracle テーブルの選択
  このダイアログ ボックスを使用すると、CDC インスタンスに含めるテーブルを選択できます。 選択したテーブルは、新しいインスタンス ウィザードの **[テーブルと列の選択]** ページの一覧に追加されます。 このダイアログ ボックスでは次の操作を実行できます。  
  
 既定では、このダイアログ ボックスのテーブルの一覧にはテーブルが含まれていません。 チェック ボックス列の最上部にあるチェック ボックスをオンにしてすべてのテーブルを選択するか、特定のテーブルを検索することができます。  
  
 **特定のテーブルを検索するには**  
 次のように検索条件を入力し、 **[検索]** をクリックします。  
  
-   **[スキーマ]**: データベース スキーマを一覧から選択します。 そのスキーマを持つテーブルだけが一覧に表示されます。  
  
-   **[テーブル名パターン]**: 任意の文字列を入力します。 入力した文字列を含むテーブルのみが表示されます。  
  
> [!NOTE]  
>  これらのフィールドの一方または両方に条件を入力できます。  
  
-   **[一致するテーブルのうち最初の 1000 個を表示する]**: 既定ではこのチェック ボックスはオンになっています。 一致するテーブルのうち最初の 1000 個のみが表示されます。 このチェック ボックスをオフにすると、条件に一致するすべてのテーブルが表示されます。 テーブルが多数存在する場合、一覧の表示に時間がかかる場合があります。  
  
 **CDC インスタンスに含めるテーブルを選択するには**  
 含めるテーブルの横のチェック ボックスをオンにして、 **[追加]** をクリックします。 新しいインスタンス ウィザードの **[テーブルと列の選択]** ページの一覧にテーブルが追加されます。  
  
 その他のテーブルを追加せずにダイアログ ボックスを閉じる場合は、 **[閉じる]** をクリックします。  
  
> [!NOTE]  
>  サポートされていないデータ型が含まれているテーブルを選択すると、エラー メッセージが表示され、そのテーブルは追加されません。  
  
## <a name="see-also"></a>参照  
 [SQL Server 変更データベース インスタンスを作成する方法](how-to-create-the-sql-server-change-database-instance.md)   
 [Oracle のテーブルおよび列の選択](select-oracle-tables-and-columns.md)  
  
  
