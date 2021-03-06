---
title: 予測モデル (中級者向けデータ マイニング チュートリアル) の検証 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0a00f409-050f-4b92-9763-ba31a6aa3052
caps.latest.revision: 52
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f3e41c8060a007e52af23c0637c744e72f0d1fb4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37167769"
---
# <a name="exploring-the-forecasting-model-intermediate-data-mining-tutorial"></a>予測モデルの検証 (中級者向けデータ マイニング チュートリアル)
  使用して、結果を表示するには予測マイニング モデルを構築したら、これで、**マイニング モデル ビューアー**データ マイニング デザイナーのタブ。 [!INCLUDE[msCoName](../includes/msconame-md.md)]タイム シリーズ ビューアーには、2 つのタブが含まれています:**グラフ**と**モデル**します。  
  
 また、すべてのモデルで Microsoft 汎用ツリー ビューアーを使用できます。 それぞれのビューに、時系列モデルの情報が少しずつ異なる方法で表示されます。  
  
-   [[グラフ] タブ](#bkmk_Charts)  
  
-   [[モデル] タブ](#bkmk_Model)  
  
-   [Microsoft 汎用コンテンツ ビューアー](#bkmk_Content)  
  
##  <a name="bkmk_Charts"></a> [グラフ] タブ  
 **グラフ**のタブ、[!INCLUDE[msCoName](../includes/msconame-md.md)]タイム シリーズ ビューアー グラフィカルに表示する履歴データと予測を含むシリーズの各します。 時系列グラフのそれぞれの線は、製品、地域、および予測可能な属性の一意の組み合わせを表します。  
  
 ビューアーの右側の凡例には、ドロップダウン リストでの選択に基づいて、選択可能なすべての時系列が表示されます。 凡例で、これらのチェック ボックスをオンまたはオフにして、グラフに表示する時系列を指定できます。  
  
 各時系列に対して使用する色などの表示オプション、またはグラフの点に値を表示するかどうかを変更することもできます。  
  
#### <a name="to-select-a-time-series"></a>時系列を選択するには  
  
1.  をクリックして、**グラフ**のタブ、**マイニング モデル ビューアー**タブが表示されていない場合。  
  
2.  グラフ ビューの右側にあるドロップダウン リストをクリックし、すべてのチェック ボックスをオンにします。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     グラフに 24 本の異なる系列線が表示されます。  
  
3.  グラフの右側にあるチェック ボックス、量に基づくすべての系列の線を一時的に非表示にあるボックスをオフにします。  
  
     次に、R750 と R250 という自転車に関連するチェック ボックスをオフにします。  
  
     これで、グラフに含まれる系列線は次の 6 つだけになるため、M200 と T1000 という自転車の傾向を比較しやすくなります。  
  
    -   **M200 Europe: Quantity**  
  
    -   **M200 North America: 数量**  
  
    -   **M200 Pacific: 数量**  
  
    -   **T1000 Europe: Quantity**  
  
    -   **T1000 North America: 数量**  
  
    -   **T1000 Pacific: 数量**  
  
 ![M200 および T1000 の数量を予測するシリーズ](../../2014/tutorials/media/6series-defaultforecasting.gif "M200 および T1000 の数量を予測するシリーズ")  
  
 このビューアーに表示されるグラフには、履歴データと予測データの両方が含まれます。 履歴データと区別できるよう、予測データの部分は網掛けされています。 個々の系列を比較しやすくするために、グラフのそれぞれの線に関連付けられている色を変更することもできます。 詳細については、「 [データ マイニング ビューアーで使用する色の変更](../../2014/analysis-services/data-mining/change-the-colors-used-in-the-data-mining-viewer.md)」を参照してください。  
  
 これらの傾向線からは、どの地域でも総売上がしだいに増加しており、12 か月目 (つまり 12 月) でピークに達していることがわかります。 またグラフから、T1000 という自転車のデータが他の製品系列のデータより大幅に遅れて始まっていることもわかります。 これは、この製品が新しい製品であるためです。この系列については、基になるデータが十分でないため、正確な予測が得られない可能性があります。  
  
 既定では、各時系列について、5 つの予測期間分の予測が点線で表示されます。 この値を変更して、表示する予測を増減することもできます。 グラフに誤差範囲を追加することで、その予測の標準偏差もグラフィカルに表示できます。  
  
#### <a name="to-change-prediction-and-display-options-in-the-chart-view"></a>グラフ ビューの予測オプションと表示オプションを変更するには  
  
1.  値を変更してみてください**予測期間**、徐々 に増やしてから**5**に**10**に再び**6**します。  
  
     履歴データの変動幅が大きい場合は、予測の数を増やすと変動が繰り返される傾向にあり、増幅されることもあります。 多くの場合、この時点である程度の調査が必要になります。この調査で、履歴データの大幅な増加の原因を特定し、それらの結果をそのまま使用するか、ソース データに修正する箇所がないかどうかを探すか、モデルの線をいずれかの方法で滑らかにするかを判断することになります。  
  
2.  選択、**偏差の表示**チェック ボックスをオンします。  
  
     このオプションをオンにすると、それぞれの予測値について、推定される誤差が表示されます。  
  
3.  X 軸のスケールを確認します。 履歴データと予測データの変化はどちらも常に比率で表されますが、実際の値はグラフにすべての値が表示されるように自動的に調整されます。 そのため、モデルを比較するときは、視覚的な見た目だけに頼らないように注意が必要です。 正確なを取得する値、または増加率や予測の値は、点線または実線の上にマウス ポインターを置くまたは内の値を表示する行をクリックして、**マイニング凡例**します。  
  
     **ヒント:**: 場合、**マイニング凡例**が表示されないに切り替える**モデル**ビュー、任意のノードを右クリックし、選択**凡例を表示する**します。  
  
 これらの傾向を見て、一部の系列のデータが十分でないことが気になるときは、モデル別の売上の平均 (地域別の売上の平均など) を求めて予測の信頼性を高めることもできます。 この方法については、このチュートリアルのレッスンで後ほど説明します。  
  
 [ページのトップへ](#bkmk_Charts)  
  
##  <a name="bkmk_Model"></a> [モデル] タブ  
 **モデル**のタブ、[!INCLUDE[msCoName](../includes/msconame-md.md)]データ マイニング デザイナーでタイム シリーズ ビューアーを使用して、ツリー グラフの形式で予測モデルを表示できます。  
  
 最初に注目する点は、ここで使用しているデータでは、複数の製品ライン (T1000 など) について、売上を示すメジャーがそれぞれ 2 つ (Amount と Quantity) あり、地域がそれぞれ 3 つ (ヨーロッパ、北米、および太平洋) に分かれているため、作成したモデルは実質的に 24 個のツリーで構成されているということです。それらの各ツリーが、地域、製品、および予測可能な属性の組み合わせがそれぞれ異なる売上パターンのモデルを表しています。  
  
 製品ライン、地域、および系列を選択して表示する販売のメトリックの組み合わせを選択することができます、**ツリー**ドロップダウン リストでは、**モデル**タブ。  
  
 ここで、モデルをツリーとして表示すると何がわかるか考えてみましょう。 ツリーに複数のレベルがあるモデルとノードが 1 つだけのモデルを例に、それらのモデルの違いについて考えてみます。  
  
-   ツリー グラフのノードが 1 つだけの場合は、モデルで検出された傾向が時間の経過によってほとんど変化しないことを意味します。 この 1 つのノード、ラベル付けを使用する**すべて**、入力変数と結果の間の関係を表す式を表示します。  
  
-   時系列のツリー グラフに複数の分岐がある場合は、検出された時系列が複雑すぎて、1 つの式では表せないことを意味します。 複数の分岐、各分岐にツリーを原因となった条件ラベルが付いた代わりに、ツリー グラフを含む可能性があります*分割*します。 ツリーが分割されている場合、各分岐はそれぞれの時間の単位を表し、その時間単位ごとに 1 つの式で傾向を表すことができます。  
  
     たとえば、グラフのグラフを見て、開始年 9 月のある時点から年末休暇伸び売り上げ高が急激に増加を表示する場合に切り替える、**モデル**を傾向が変更された正確な日付を表示するビュー。 この場合、ツリー内の "9 月前" を表す分岐には分割前までの売上傾向を数学的に示す式、"9 月以降" を表す分岐には 9 月から年末休暇までの売上傾向を示す式のように、それぞれの分岐に異なる式が含まれます。  
  
#### <a name="to-explore-the-decision-tree-for-a-time-series-model"></a>時系列モデルに対応するデシジョン ツリーを調査するには  
  
1.  **ツリー**ボックスの一覧、**モデル**、ビューアーのタブ、 **T1000 Europe: Amount**シリーズ。  
  
     というラベルの付いたノードをクリックします。**すべて**します。  
  
     **すべて**ノードに表示されるツールヒントには、系列全体でのケースの数などの情報が含まれています、られた時系列式から派生したデータを分析します。  
  
2.  場合、**マイニング凡例**が表示されない、ノードを右クリックして**凡例を表示する**します。  
  
     **マイニング凡例**はるかツールヒントには、同じ情報を提供します。 不連続な独立変数がある場合は、ノード内の変数の分布を示すヒストグラムも表示されます。  
  
3.  次に、別の時系列を選択して表示します。 使用して、**ツリー**ボックスの一覧、**モデル**、ビューアーのタブ、 **M200 North America: Amount**シリーズ。  
  
     ツリー グラフが含まれています、**すべて**ノードと 2 つの子ノード。 子ノードのラベルから、どの時点で傾向線が変化したか確認できます。  
  
     各子ノードの説明で、**マイニング凡例**ツリーの各分岐のケースの数も含まれます。  
  
 ツリー ビューアーには、ほかにも次のような機能があります。  
  
-   使用して、グラフで表される変数を変更することができます、**バック グラウンド**コントロール。 ため、既定では、ノードが濃くなりますがより多くの状況を含む値の**バック グラウンド**に設定されている**母集団**します。 ケースの数がノードに含まれるだけを表示するノードの上にマウス ポインターを置くし、が表示されたら、またはノードをクリックし、内の数値を表示するツールヒントを表示、**ノード凡例**ウィンドウ。  
  
-   ツールヒントにはノードの回帰式も表示されます。これについても、ノードをクリックして確認することもできます。 混合モデルを作成した場合は、ARIMA の式 (リーフ ノード内) と ARTXP の式 (ツリーのルート ノード内) の 2 つが表示されます。  
  
-   ノードでは、連続する数値が小さなひし形で表されます。 属性の範囲は、そのひし形が示されたバーに表示されます。 このひし形はノードの中間にあり、ひし形の幅がそのノードの属性の分散を表します。  
  
 [ページのトップへ](#bkmk_Charts)  
  
##  <a name="bkmk_Content"></a> (省略可能)汎用コンテンツ ツリー ビューアー  
 だけでなく、時系列用のカスタム ビューアー[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]提供、 **MicrosoftGeneric コンテンツ ツリー ビューアー**すべてのデータ マイニング モデルで使用するためです。 このビューアーには、次のような利点があります。  
  
-   **Microsoft タイム シリーズ ビューアー**: このビューは、2 つのアルゴリズムの結果をマージします。 各系列を別々に表示することもできますが、その場合、各アルゴリズムの結果がどのように結合されたかを判別できません。 また、このビューでは、ツールチップと [マイニング凡例] に重要な統計情報だけが表示されます。  
  
-   **汎用コンテンツ ツリー ビューアー**: 参照し、一度に 1 つ、モデル内のすべての使用されたデータ系列を表示することができ、混合を作成した場合、ARIMA の両方のモデルし ARTXP のツリーが同じグラフに表示されます。  
  
     このビューアーを使用すると、両方のアルゴリズムからすべての統計情報を取得できるだけでなく、値の分布も確認できます。  
  
     ARIMA と ARTXP の分析について詳しく調べたい場合など、データ マイニングの上級ユーザー向けのビューアーです。  
  
#### <a name="to-view-details-for-a-particular-data-series-in-the-generic-content-viewer"></a>汎用コンテンツ ビューアーで特定のデータ系列の詳細を表示するには  
  
1.  **マイニング モデル ビューアー** ] タブで [ **Microsoft 汎用コンテンツ ツリー ビューアー**から、**ビューアー**ドロップダウン リスト。  
  
2.  **ノードのキャプション**ウィンドウで、最上位にある (すべて) ノードをクリックします。  
  
3.  **ノードの詳細**ペインで ATTRIBUTE_NAME の値を確認します。  
  
     この値から、このノードにどの系列 (製品と地域の組み合わせ) が含まれているかがわかります。 AdventureWorks の例では、最上位ノードは M200 Europe 系列のノードです。  
  
4.  **ノードのキャプション**ウィンドウで、子ノードを持つ最初のノードを見つけます。  
  
     表示されるツリー ビュー シリーズ ノードに子がある場合、**モデル**Microsoft タイム シリーズ ビューアーのタブには、分岐構造があります。  
  
5.  ノードを展開し、いずれかの子ノードをクリックします。  
  
     スキーマの NODE_DESCRIPTION 列に、ツリーが分割される原因になった条件が含まれています。  
  
6.  **ノードのキャプション**ウィンドウで、最上位の ARIMA ノードをクリックし、すべての子ノードが表示されるまで、ノードを展開します。  
  
7.  **ノードの詳細**ペインで ATTRIBUTE_NAME の値を確認します。  
  
     この値から、このノードに含まれている時系列がわかります。 ARIMA セクションの最上位ノードは [(すべて)] セクションの最上位ノードと一致するはずです。 AdventureWorks の例では、このノードには M200 Europe 系列に対する ARIMA 分析が含まれています。  
  
 詳細については、「[タイム シリーズ モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)」を参照してください。  
  
 [ページのトップへ](#bkmk_Charts)  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [時系列予測の作成&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/creating-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>参照  
 [タイム シリーズ モデルのクエリ例](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [Microsoft タイム シリーズ アルゴリズム テクニカル リファレンス](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)  
  
  
