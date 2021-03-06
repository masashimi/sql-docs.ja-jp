---
title: 追加、削除、パッケージ内のユーザー定義変数のスコープの変更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- variables [Integration Services], adding
ms.assetid: cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e
caps.latest.revision: 46
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2fdccdecea434aa3fe56c362f932b3ba0da396b3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37213602"
---
# <a name="add-delete-change-scope-of-user-defined-variable-in-a-package"></a>パッケージ内のユーザー定義変数のスコープの追加、削除、変更
  この手順では、**[変数]** ウィンドウを使用して、パッケージ内のユーザー定義変数のスコープを追加、削除、および変更する方法について説明します。  
  
 変数のスコープの詳細については、次を参照してください。 [Integration Services &#40;SSIS&#41;変数](integration-services-ssis-variables.md)します。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 実行時にシステムの情報を使用できるようにパッケージやイベント ハンドラーなどのコンテナーで使用できるシステム変数も用意されています。 システム変数は削除できません。  
  
### <a name="to-add-a-variable"></a>変数を追加するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、操作する [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで、変数のスコープを定義するには、次のいずれかの操作を行います。  
  
    -   スコープをパッケージに設定するには、 **[制御フロー]** タブのデザイン画面上の任意の場所をクリックします。  
  
    -   スコープをイベント ハンドラーに設定するには、 **[イベント ハンドラー]** タブのデザイン画面で、実行可能ファイルおよびイベント ハンドラーを選択します。  
  
    -   スコープをタスクまたはコンテナーに設定するには、 **[制御フロー]** タブまたは **[イベント ハンドラー]** タブのデザイン画面で、タスクまたはコンテナーをクリックします。  
  
4.  **SSIS** メニューの **[変数]** をクリックします。 必要に応じて、View.Variables コマンドを **[オプション]** ダイアログ ボックスの **[キーボード]** ページで選択したキーの組み合わせにマップすることによって、 **[変数]** ウィンドウを表示することもできます。  
  
5.  **[変数]** ウィンドウで、 **[変数の追加]** アイコンをクリックします。 新しい変数が一覧に追加されます。  
  
6.  必要に応じて、 **[グリッドのオプション]** アイコンをクリックし、 **[可変グリッドのオプション]** ダイアログ ボックスに表示する追加の列を選択して、 **[OK]** をクリックします。  
  
7.  必要に応じて、変数のプロパティを設定します。 詳細については、「 [ユーザー定義変数のプロパティを設定する](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)」を参照してください。  
  
8.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
### <a name="to-delete-a-variable"></a>変数を削除するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージを右クリックして開きます。  
  
3.  **SSIS** メニューの **[変数]** をクリックします。 必要に応じて、View.Variables コマンドを **[オプション]** ダイアログ ボックスの **[キーボード]** ページで選択したキーの組み合わせにマップすることによって、 **[変数]** ウィンドウを表示することもできます。  
  
4.  削除する変数を選択し、 **[変数の削除]** をクリックします。  
  
     [変数] ウィンドウに変数が表示されない場合は、 **[グリッドのオプション]** をクリックし、 **[すべてのスコープの変数を表示する]** を選択します。  
  
5.  **[変数の削除の確認]** ダイアログ ボックスが開いた場合は、 **[はい]** をクリックして確定します。  
  
6.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
### <a name="to-change-the-scope-of-a-variable"></a>変数のスコープを変更するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージを右クリックして開きます。  
  
3.  **SSIS** メニューの **[変数]** をクリックします。 必要に応じて、View.Variables コマンドを **[オプション]** ダイアログ ボックスの **[キーボード]** ページで選択したキーの組み合わせにマップすることによって、 **[変数]** ウィンドウを表示することもできます。  
  
4.  変数を選択して、 **[変数の移動]** をクリックします。  
  
     [変数] ウィンドウに変数が表示されない場合は、 **[グリッドのオプション]** をクリックし、 **[すべてのスコープの変数を表示する]** を選択します。  
  
5.  **[新しいスコープの選択]** ダイアログ ボックスで、パッケージまたはパッケージ内のコンテナー、タスク、またはイベント ハンドラーを選択して、変数のスコープを変更します。  
  
6.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41;変数](integration-services-ssis-variables.md)   
 [パッケージで変数を使用します。](../../2014/integration-services/use-variables-in-packages.md)   
 [ユーザー定義変数のプロパティを設定します。](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)   
 [子パッケージでの変数およびパラメーターの値の使用](../../2014/integration-services/use-the-values-of-variables-and-parameters-in-a-child-package.md)  
  
  
