---
title: デシジョン ツリー モデルのクエリ例 |Microsoft ドキュメント
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 123de8ac0fd3b29be624528b063056caca12a650
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="decision-trees-model-query-examples"></a>デシジョン ツリー モデルのクエリ例
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  データ マイニング モデルに対するクエリを作成する際には、コンテンツ クエリを作成することも、予測クエリを作成することもできます。コンテンツ クエリでは、分析で検出されたパターンの詳細情報を取得できます。予測クエリでは、モデル内のパターンを使用して新しいデータについての予測を行うことができます。 たとえば、デシジョン ツリー モデルでコンテンツ クエリを使用すると、ツリーの各レベルのケースの数に関する統計や、ケースを区別するルールを取得できます。 一方、予測クエリを使用すると、モデルを新しいデータにマップして、提案や分類などを生成することができます。 クエリを使用してモデルに関するメタデータを取得することもできます。  
  
 ここでは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムに基づくモデルに対するクエリの作成方法について説明します。  
  
 **Content Queries**  
  
 [データ マイニング スキーマ行セットからモデル パラメーターを取得する](#bkmk_Query1)  
  
 [DMX を使用してモデルのツリーについての詳細を取得する](#bkmk_Query2)  
  
 [モデルからサブツリーを取得する](#bkmk_Query3)  
  
 **予測クエリ**  
  
 [確率付きの予測を取得する](#bkmk_Query4)  
  
 [デシジョン ツリー モデルからアソシエーションを予測する](#bkmk_Query5)  
  
 [デシジョン ツリー モデルから回帰式を取得する](#bkmk_Query6)  
  
##  <a name="bkmk_top2"></a> デシジョン ツリー モデルに関する情報の入手  
 デシジョン ツリー モデルのコンテンツに対して意味のあるクエリを作成するには、モデル コンテンツの構造や、各種類のノードに格納されている情報の種類を把握しておく必要があります。 詳細については、「[デシジョン ツリー モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)」を参照してください。  
  
###  <a name="bkmk_Query1"></a> サンプル クエリ 1: データ マイニング スキーマ行セットからモデル パラメーターを取得する  
 データ マイニング スキーマ行セットに対してクエリを実行すると、モデルに関するメタデータを取得できます (作成された日時、最後に処理された日時、基になるマイニング構造の名前、予測可能な属性として使用されている列の名前など)。 モデルが最初に作成されたときに使用されたパラメーターを取得することもできます。  
  
```  
select MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_Decision Tree'  
```  
  
 サンプルの結果 :  
  
 MINING_PARAMETERS  
  
 COMPLEXITY_PENALTY=0.5, MAXIMUM_INPUT_ATTRIBUTES=255,MAXIMUM_OUTPUT_ATTRIBUTES=255,MINIMUM_SUPPORT=10,SCORE_METHOD=4,SPLIT_METHOD=3,FORCE_REGRESSOR=  
  
###  <a name="bkmk_Query2"></a> サンプル クエリ 2: DMX を使用してモデル コンテンツに関する詳細を取得する  
 次のクエリは、「 [基本的なデータ マイニング チュートリアル](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)」でモデルを構築したときに作成したデシジョン ツリーに関する基本的な情報を返します。 各ツリー構造は、それ自体のノードに格納されます。 このモデルに含まれている予測可能な属性は 1 つなので、ツリー ノードは 1 つしかありません。 しかし、デシジョン ツリー アルゴリズムを使用してアソシエーション モデルを作成した場合は、各製品に 1 つずつ、何百ものツリーがあることもあります。  
  
 このクエリでは、種類が 2 のノード (特定の予測可能な属性を表すツリーの最上位のノード) がすべて返されます。  
  
> [!NOTE]  
>  CHILDREN_CARDINALITY という列は、MDX の同名の予約済みキーワードと区別するために角かっこで囲む必要があります。  
  
```  
SELECT MODEL_NAME, NODE_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY]  
FROM TM_DecisionTrees.CONTENT  
WHERE NODE_TYPE = 2  
```  
  
 例の結果を次に示します。  
  
|MODEL_NAME|NODE_NAME|NODE_CAPTION|NODE_SUPPORT|CHILDREN_CARDINALITY|  
|-----------------|----------------|-------------------|-------------------|---------------------------|  
|TM_DecisionTree|000000001|すべて|12939|5|  
  
 この結果からわかることは何でしょうか。 デシジョン ツリー モデルの特定のノードの基数は、そのノードの直接の子の数を表します。 このノードの基数は 5 なので、このモデルでは、対象になる母集団 (自転車を購入する可能性がある顧客) が 5 つのサブグループに分割されていることがわかります。  
  
 次の関連するクエリは、この 5 つのサブグループの子を、子ノードの属性と値の分布と共に返します。 サポート、確率、分散などの統計は、NODE_DISTRIBUTION という入れ子になったテーブルに格納されているため、この例では、入れ子になったテーブル列を出力するために `FLATTENED` キーワードを使用しています。  
  
> [!NOTE]  
>  入れ子になったテーブル列である SUPPORT は、同名の予約済みキーワードと区別するために角かっこで囲む必要があります。  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,  
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT]  
FROM NODE_DISTRIBUTION) AS t  
FROM TM_DecisionTree.CONTENT  
WHERE [PARENT_UNIQUE_NAME] = '000000001'  
```  
  
 例の結果を次に示します。  
  
|NODE_NAME|NODE_CAPTION|T.ATTRIBUTE_NAME|T.ATTRIBUTE_VALUE|SUPPORT|  
|----------------|-------------------|-----------------------|------------------------|-------------|  
|00000000100|Number Cars Owned = 0|Bike Buyer|Missing|0|  
|00000000100|Number Cars Owned = 0|Bike Buyer|0|1067|  
|00000000100|Number Cars Owned = 0|Bike Buyer|1|1875|  
|00000000101|Number Cars Owned = 3|Bike Buyer|Missing|0|  
|00000000101|Number Cars Owned = 3|Bike Buyer|0|678|  
|00000000101|Number Cars Owned = 3|Bike Buyer|1|473|  
  
 これらの結果から、自転車を購入した顧客 ([Bike Buyer] = 1) のうち、1067 人の顧客は車を 1 台も所有しておらず、473 人の顧客は車を 3 台所有していることがわかります。  
  
###  <a name="bkmk_Query3"></a> サンプル クエリ 3: モデルからサブツリーを取得する  
 実際に自転車を購入した顧客についてさらに調査する場合は、 次の例のようにクエリで [IsDescendant &#40;DMX&#41;](../../dmx/isdescendant-dmx.md) 関数を使用すると、任意のサブツリーについて追加の詳細を表示することができます。 次のクエリは、42 歳以上の顧客を含むツリーのリーフ ノード (NODE_TYPE = 4) を取得して、自転車を購入した顧客の数を返します。 このクエリでは、入れ子になったテーブルの行が Bike Buyer = 1 の行のみに制限されています。  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,NODE_TYPE,  
(  
SELECT [SUPPORT] FROM NODE_DISTRIBUTION WHERE ATTRIBUTE_NAME = 'Bike Buyer' AND ATTRIBUTE_VALUE = '1'  
) AS t  
FROM TM_DecisionTree.CONTENT  
WHERE ISDESCENDANT('0000000010001')  
AND NODE_TYPE = 4  
```  
  
 例の結果を次に示します。  
  
|NODE_NAME|NODE_CAPTION|t.SUPPORT|  
|----------------|-------------------|---------------|  
|000000001000100|Yearly Income >= 26000 and < 42000|266|  
|00000000100010100|Total Children = 3|75|  
|0000000010001010100|Number Children At Home = 1|75|  
  
## <a name="making-predictions-using-a-decision-trees-model"></a>デシジョン ツリー モデルを使用して予測を作成する  
 デシジョン ツリーは、分類、回帰、アソシエーションなど、さまざまなタスクに使用できるため、デシジョン ツリー モデルに対する予測クエリを作成する際にはさまざまな選択肢があります。 予測の結果を理解するには、モデルが作成された目的を把握しておく必要があります。 以下のクエリ サンプルでは、次の 3 つのシナリオについて説明します。  
  
-   分類モデルの予測を、その予測が正しい確率と共に取得して、その確率で結果をフィルター処理する  
  
-   単一クエリを作成してアソシエーションを予測する  
  
-   入力と出力が直線関係にあるデシジョン ツリーの部分の回帰式を取得する  
  
###  <a name="bkmk_Query4"></a> サンプル クエリ 4: 確率付きの予測を取得する  
 次のサンプル クエリでは、「 [基本的なデータ マイニング チュートリアル](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)」で作成したデシジョン ツリー モデルを使用します。 クエリは [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] DW のテーブル dbo.ProspectiveBuyers にあるサンプル データの新しいセットを渡して、新しいデータ セット内のどの顧客が自転車を購入するかを予測します。  
  
 このクエリでは、予測関数 [PredictHistogram &#40;DMX&#41;](../../dmx/predicthistogram-dmx.md)を使用しています。この関数は、モデルで検出された確率に関する有用な情報を含む入れ子になったテーブルを返します。 クエリの最後の WHERE 句は結果をフィルター処理して、自転車を購入する確率が 0% より大きいと予測された顧客のみを返します。  
  
```  
SELECT  
  [TM_DecisionTree].[Bike Buyer],  
  PredictHistogram([Bike Buyer]) as Results  
From  
  [TM_DecisionTree]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT  
      [FirstName],  
      [LastName],  
      [MaritalStatus],  
      [Gender],  
      [YearlyIncome],  
      [TotalChildren],  
      [NumberChildrenAtHome],  
      [HouseOwnerFlag],  
      [NumberCarsOwned]  
    FROM  
      [dbo].[ProspectiveBuyer]  
    ') AS t  
ON  
  [TM_DecisionTree].[First Name] = t.[FirstName] AND  
  [TM_DecisionTree].[Last Name] = t.[LastName] AND  
  [TM_DecisionTree].[Marital Status] = t.[MaritalStatus] AND  
  [TM_DecisionTree].[Gender] = t.[Gender] AND  
  [TM_DecisionTree].[Yearly Income] = t.[YearlyIncome] AND  
  [TM_DecisionTree].[Total Children] = t.[TotalChildren] AND  
  [TM_DecisionTree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
  [TM_DecisionTree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
  [TM_DecisionTree].[Number Cars Owned] = t.[NumberCarsOwned]  
WHERE [Bike Buyer] = 1  
AND PredictProbability([Bike Buyer]) >'.05'  
```  
  
 既定では、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、入れ子になったテーブルを列ラベル **[Expression]** を使用して返します。 このラベルを変更するには、返される列に別名を付けます。 その別名 (この例の場合は **Results**) は、列見出しと、入れ子になったテーブルの値の両方に使用されます。 結果を表示するには、入れ子になったテーブルを展開する必要があります。  
  
 **Bike Buyer** = 1 を使用した結果の例:  
  
|Bike Buyer|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|----------------|--------------|------------------|--------------------------|---------------|------------|  
|1|2540|0.634849242045644|0.013562168281562|0|0|  
|0|1460|0.364984174579377|0.00661336932550915|0|0|  
||0|0.000166583374979177|0.000166583374979177|0|0|  
  
 使用しているプロバイダーが、ここに示されているような階層的な行セットをサポートしていない場合は、クエリで FLATTENED キーワードを使用すると、繰り返される列値の代わりに NULL を含むテーブルとして結果を返すことができます。 詳細については、「[入れ子になったテーブル &#40;Analysis Services - データ マイニング&#41;](../../analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)」または「[DMX 選択ステートメントについて](../../dmx/understanding-the-dmx-select-statement.md)」を参照してください。  
  
###  <a name="bkmk_Query5"></a> サンプル クエリ 5: デシジョン ツリー モデルからアソシエーションを予測する  
 次のサンプル クエリは、Association マイニング構造に基づいています。 このサンプルに従って作業するために、このマイニング構造に新しいモデルを追加し、アルゴリズムとして Microsoft デシジョン ツリーを選択できます。 アソシエーション マイニング モデルの作成方法の詳細については、「[レッスン 3 : マーケット バスケット シナリオの作成 &#40;中級者向けデータ マイニング チュートリアル&#41;](http://msdn.microsoft.com/library/651eef38-772e-4d97-af51-075b1b27fc5a)」を参照してください。  
  
 次のサンプル クエリは単一クエリです。このクエリは、[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] でフィールドを選択し、それらのフィールドの値をドロップダウン リストから選択するだけで簡単に作成できます。  
  
```  
SELECT PredictAssociation([DT_Association].[v Assoc Seq Line Items],3)  
FROM  
  [DT_Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Patch kit' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 期待される結果:  
  
|[モデル]|  
|-----------|  
|Mountain-200|  
|Mountain Tire Tube|  
|Touring Tire Tube|  
  
 この結果から、Patch Kit という製品を購入した顧客に提案するのに最適な 3 つの製品がわかります。 提案を行う際に複数の製品を入力として指定することもできます。そのためには、値を入力するか、 **[単一クエリ入力]** ダイアログ ボックスを使用して値を追加または削除します。 次のサンプル クエリは、複数の値を指定して予測を行う方法を示しています。 値は、入力値を定義する SELECT ステートメント内の UNION 句で接続されています。  
  
```  
SELECT PredictAssociation([DT_Association].[v Assoc Seq Line Items],3)  
From  
  [DT_Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Racing Socks' AS [Model]  
  UNION SELECT 'Women''s Mountain Shorts' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 期待される結果:  
  
|[モデル]|  
|-----------|  
|Long-Sleeve Logo Jersey|  
|Mountain-400-W|  
|Classic Vest|  
  
###  <a name="bkmk_Query6"></a> サンプル クエリ 6: デシジョン ツリー モデルから回帰式を取得する  
 連続属性の回帰を含むデシジョン ツリー モデルを作成すると、回帰式を使用して予測を行ったり、回帰式に関する情報を抽出したりすることができます。 回帰モデルに対するクエリの詳細については、「 [線形回帰モデルのクエリ例](../../analysis-services/data-mining/linear-regression-model-query-examples.md)」を参照してください。  
  
 デシジョン ツリー モデルに回帰ノードと、不連続属性や範囲で分割されるノードが混在している場合は、回帰ノードのみを返すクエリを作成できます。 NODE_DISTRIBUTION テーブルには、回帰式の詳細が含まれています。 この例では、見やすくするために列をフラット化して、NODE_DISTRIBUTION テーブルに別名を付けています。 しかし、このモデルでは、Income を他の連続属性に関連付けるためのリグレッサーは検出されませんでした。 このような場合、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、その属性の平均値とモデル内の全分散を返します。  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION AS t  
FROM DT_Predict. CONTENT  
WHERE NODE_TYPE = 25  
```  
  
 例の結果を次に示します。  
  
|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|Yearly Income|Missing|0|0.000457142857142857|0|1|  
|Yearly Income|57220.8876687257|17484|0.999542857142857|1041275619.52776|3|  
||57220.8876687257|0|0|1041216662.54387|11|  
  
 回帰モデルで使用される値型と統計の詳細については、「[線形回帰モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)」を参照してください。  
  
## <a name="list-of-prediction-functions"></a>予測関数の一覧  
 すべての [!INCLUDE[msCoName](../../includes/msconame-md.md)] アルゴリズムでは、共通の関数セットがサポートされています。 ただし、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] デシジョン ツリー アルゴリズムでは、次の表のような追加の関数がサポートされています。  
  
|||  
|-|-|  
|予測関数|使用方法|  
|[IsDescendant (&) #40";"DMX"&"#41;](../../dmx/isdescendant-dmx.md)|あるノードがモデル内の別のノードの子であるかどうかを示します。|  
|[IsInNode (&) #40";"DMX"&"#41;](../../dmx/isinnode-dmx.md)|指定されたノードが現在のケースを含んでいるかどうかを示します。|  
|[PredictAdjustedProbability & #40";"DMX"&"#41;](../../dmx/predictadjustedprobability-dmx.md)|重み付け確率を返します。|  
|[PredictAssociation & #40";"DMX"&"#41;](../../dmx/predictassociation-dmx.md)|結合データセットのメンバーシップを予測します。|  
|[PredictHistogram (&) #40";"DMX"&"#41;](../../dmx/predicthistogram-dmx.md)|現在の予測値に関連する値のテーブルを返します。|  
|[PredictNodeId & #40";"DMX"&"#41;](../../dmx/predictnodeid-dmx.md)|各ケースの Node_ID を返します。|  
|[PredictProbability & #40";"DMX"&"#41;](../../dmx/predictprobability-dmx.md)|予測値の確率を返します。|  
|[PredictStdev & #40";"DMX"&"#41;](../../dmx/predictstdev-dmx.md)|指定された列に対して、予測された標準偏差を返します。|  
|[PredictSupport & #40";"DMX"&"#41;](../../dmx/predictsupport-dmx.md)|指定された状態に対するサポート値を返します。|  
|[PredictVariance & #40";"DMX"&"#41;](../../dmx/predictvariance-dmx.md)|指定された列の分散を返します。|  
  
 すべての [!INCLUDE[msCoName](../../includes/msconame-md.md)] アルゴリズムに共通の関数の一覧については、「[一般的な予測関数 (DMX)](../../dmx/general-prediction-functions-dmx.md)」を参照してください。 特定の関数の構文については、「[データ マイニング拡張機能 (DMX) 関数リファレンス](../../dmx/data-mining-extensions-dmx-function-reference.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データ マイニング クエリ](../../analysis-services/data-mining/data-mining-queries.md)   
 [Microsoft デシジョン ツリー アルゴリズム](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)   
 [Microsoft デシジョン ツリー アルゴリズム テクニカル リファレンス](../../analysis-services/data-mining/microsoft-decision-trees-algorithm-technical-reference.md)   
 [デシジョン ツリー モデル & #40; のマイニング モデル コンテンツAnalysis Services - データ マイニング & #41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)  
  
  