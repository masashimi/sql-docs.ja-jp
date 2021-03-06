---
title: カスケード型パラメーターのレポートへの追加 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: 3a22eec3-57a7-478e-b6fc-102a9dbe0591
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a434a4d72c63c4915208256647a6ebcd86b3d45f
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2018
ms.locfileid: "43270465"
---
# <a name="add-cascading-parameters-to-a-report-report-builder-and-ssrs"></a>カスケード型パラメーターのレポートへの追加 (レポート ビルダーおよび SSRS)
  カスケード型パラメーターを使用すると、大量のレポート データの管理が可能になります。 パラメーターの値の一覧が、別のパラメーターで選択された値によって決まるように、関連するパラメーターのセットを定義できます。 たとえば、最初のパラメーターが独立しており、製品カテゴリの一覧を表すとします。 ユーザーが任意のカテゴリを選択すると、2 番目のパラメーターは最初のパラメーターの値によって決まります。 その値は、選択したカテゴリ内のサブカテゴリの一覧で更新されます。 ユーザーがレポートを表示するとき、カテゴリ パラメーターとサブカテゴリ パラメーターの両方の値を使用して、レポート データにフィルターが適用されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 カスケード型パラメーターを作成するには、まずデータセット クエリを定義し、必要な各カスケード型パラメーターにクエリ パラメーターを指定します。 各カスケード型パラメーターについて、使用可能な値を提供する独立したデータセットを作成する必要もあります。 詳細については、「[レポート パラメーターの値の追加、変更、または削除 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-available-values-for-a-report-parameter.md)」を参照してください。  
  
 一覧の後半にあるパラメーターのデータセット クエリには一覧の前半にある各パラメーターへの参照が含まれているため、カスケード型パラメーターでは順序が重要な意味を持ちます。 実行時には、レポート データ ペインのパラメーターの順序によって、パラメーター クエリがレポート内で作成される順序が決まります。したがって、ユーザーが後続の各パラメーター値を選択する順序が決まります。  
  
 複数の値を使用したカスケード型パラメーターを作成する方法、および [すべて選択] 機能を含める方法の詳細については、「 [How to have a Select All Multivalue Cascading Parameter](http://go.microsoft.com/fwlink/?LinkId=184757)」を参照してください。  
  
## <a name="to-create-the-main-dataset-with-a-query-that-includes-multiple-related-parameters"></a>関連する複数のパラメーターを含むクエリを使用してメイン データセットを作成するには  
  
1.  レポート データ ペインでデータ ソースを右クリックし、 **[データセットの追加]** をクリックします。  
  
2.  **[名前]** ボックスに、データセットの名前を入力します。  
  
3.  **[データ ソース]** ボックスのデータ ソースの名前を選択するか、 **[新規]** をクリックして名前を作成します。  
  
4.  **[クエリの種類]** ボックスで、選択したデータ ソースにクエリの種類を選択します。 このトピックでは、クエリの種類として **[テキスト]** を使用します。  
  
5.  **[クエリ]** ボックスに、このレポートにデータを取得するためのクエリを入力します。 クエリには次の要素が必要です。  
  
    1.  データ ソース フィールドの一覧。 たとえば [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントでは、SELECT ステートメントは指定されたテーブルまたはビューのデータベース列名の一覧を指定します。  
  
    2.  カスケード型パラメーターごとに 1 つのクエリ パラメーター。 クエリ パラメーターは、クエリに含める特定の値またはクエリから除外する特定の値を指定することによって、データ ソースから取得するデータを制限します。 通常、クエリ パラメーターはクエリの制約句で使用されます。 たとえば [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT ステートメントでは、クエリ パラメーターは WHERE 句で使用されます。  
  
6.  **[実行]** (**!**) をクリックします。 クエリ パラメーターを指定し、クエリを実行したら、クエリ パラメーターに対応するレポート パラメーターが自動的に作成されます。  
  
    > [!NOTE]  
    >  最初にクエリを実行したときのクエリ パラメーターの順序によって、クエリ パラメーターがレポート内で作成される順序が決まります。 順序を変更するには、「[レポート パラメーターの順序の変更 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)」を参照してください。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 次に、独立したパラメーターの値を提供するデータセットを作成します。  
  
## <a name="to-create-a-dataset-to-provide-values-for-an-independent-parameter"></a>独立したパラメーターの値を提供するデータセットを作成するには  
  
1.  レポート データ ペインでデータ ソースを右クリックし、 **[データセットの追加]** をクリックします。  
  
2.  **[名前]** ボックスに、データセットの名前を入力します。  
  
3.  **[データ ソース]** ボックスに表示された名前が、手順 1. で選択したデータ ソースの名前であることを確認します。  
  
4.  **[クエリの種類]** ボックスで、選択したデータ ソースにクエリの種類を選択します。 このトピックでは、クエリの種類として **[テキスト]** を使用します。  
  
5.  **[クエリ]** ボックスに、このパラメーターに値を取得するためのクエリを入力します。 通常、独立したパラメーターのクエリにはクエリ パラメーターが含まれません。 たとえば、すべてのカテゴリの値を提供するパラメーターのクエリを作成するには、次のような [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用できます。  
  
    ```  
    SELECT DISTINCT <column name> FROM <table>  
    ```  
  
     SELECT DISTINCT コマンドは、指定したテーブルの指定した列から一意の各値を取得できるように、結果セットから重複する値を削除します。  
  
     **[実行]** (**!**) をクリックします。 結果セットには、この最初のパラメーターに使用可能な値が表示されます。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 次に、このデータセットを使用する最初のパラメーターのプロパティを設定して、実行時に使用可能な値を入力します。  
  
## <a name="to-set-available-values-for-a-report-parameter"></a>レポート パラメーターに使用可能な値を設定するには  
  
1.  レポート データ ペインでパラメーター フォルダーの最初のパラメーターを右クリックし、 **[パラメーターのプロパティ]** をクリックします。  
  
2.  **[名前]** ボックスのパラメーターの名前が正しいことを確認します。  
  
3.  **[使用できる値]** をクリックします。  
  
4.  **[クエリから値を取得]** をクリックします。 3 つのフィールドが表示されます。  
  
5.  **[データセット]** ボックスのドロップダウン リストから、前の手順で作成したデータセットの名前をクリックします。  
  
6.  **[値]** フィールドで、パラメーター値を指定するフィールドの名前をクリックします。  
  
7.  **[ラベル]** フィールドで、パラメーターのラベルを指定するフィールドの名前をクリックします。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 次に、従属パラメーターの値を提供するデータセットを作成します。  
  
## <a name="to-create-a-dataset-to-provide-values-for-a-dependent-parameter"></a>従属パラメーターの値を提供するデータセットを作成するには  
  
1.  レポート データ ペインでデータ ソースを右クリックし、 **[データセットの追加]** をクリックします。  
  
2.  **[名前]** ボックスに、データセットの名前を入力します。  
  
3.  **[データ ソース]** ボックスに表示された名前が、手順 1. で選択したデータ ソースの名前であることを確認します。  
  
4.  **[クエリの種類]** ボックスで、選択したデータ ソースにクエリの種類を選択します。 このトピックでは、クエリの種類として **[テキスト]** を使用します。  
  
5.  **[クエリ]** ボックスに、このパラメーターに値を取得するためのクエリを入力します。 通常、従属パラメーターのクエリには、このパラメーターが依存している各クエリ パラメーターが含められます。 たとえば、カテゴリ (独立したパラメーター) のすべてのサブカテゴリ (従属パラメーター) の値を提供するパラメーターのクエリを作成するには、次のような [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用できます。  
  
    ```  
    SELECT DISTINCT Subcategory FROM <table>   
    WHERE (Category = @Category)  
    ```  
  
     WHERE 句の Category は \<table> のフィールドの名前であり、@Category はクエリ パラメーターです。 このステートメントを使用すると、@Category に指定したカテゴリのサブカテゴリの一覧が生成されます。 この値は実行時に、ユーザーが同名のレポート パラメーターに選択した値を使用して入力されます。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 次に、このデータセットを使用する 2 番目のパラメーターのプロパティを設定して、実行時に使用可能な値を入力します。  
  
## <a name="to-set-available-values-for-a-report-parameter"></a>レポート パラメーターに使用可能な値を設定するには  
  
1.  レポート データ ペインでパラメーター フォルダーの最初のパラメーターを右クリックし、 **[パラメーターのプロパティ]** をクリックします。  
  
2.  **[名前]** ボックスのパラメーターの名前が正しいことを確認します。  
  
3.  **[使用できる値]** をクリックします。  
  
4.  **[クエリから値を取得]** をクリックします。  
  
5.  **[データセット]** ボックスのドロップダウン リストから、前の手順で作成したデータセットの名前をクリックします。  
  
6.  **[値]** フィールドで、パラメーター値を指定するフィールドの名前をクリックします。  
  
7.  **[ラベル]** フィールドで、パラメーターのラベルを指定するフィールドの名前をクリックします。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-test-the-cascading-parameters"></a>カスケード型パラメーターをテストするには  
  
1.  **[実行]** をクリックします。  
  
2.  最初の独立したパラメーターのドロップダウン リストから値を選択します。  
  
     レポート プロセッサによって、次のパラメーターのデータセット クエリが実行され、最初のパラメーターに選択した値が渡されます。 最初のパラメーターの値に基づいて、使用可能な値を使用して 2 番目のパラメーターのドロップダウン リストが入力されます。  
  
3.  2 番目の従属パラメーターのドロップダウン リストから値を選択します。  
  
     選択肢を変更できるように、最後のパラメーターを選択した後、レポートは自動的に実行されません。  
  
4.  **[レポートの表示]** をクリックします。 選択したパラメーターに基づいて、レポートの表示が更新されます。  
  
## <a name="see-also"></a>参照  
 [レポート パラメーターの追加、変更、または削除 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [チュートリアル: レポートへのパラメーターの追加 &#40;レポート ビルダー&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [レポート ビルダー チュートリアル](../../reporting-services/report-builder-tutorials.md)   
 [データセット フィルター、データ領域フィルター、およびグループ フィルターの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [レポート埋め込みデータセットと共有データセット (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
