---
title: レポート デザインに関するヒント (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: c1490ff0-5b8a-43c1-8d22-e459395db4f6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d9582c17aef675835049e50ff363dfb860ee113b
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2018
ms.locfileid: "43271017"
---
# <a name="report-design-tips-report-builder-and-ssrs"></a>レポート デザインに関するヒント (レポート ビルダーおよび SSRS)
  ここでは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のページ分割されたレポートをデザインする際のヒントを紹介します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="DesigningReports"></a> レポートのデザイン  
  
-   適切にデザインされたレポートでは、具体的な行動につながる情報が伝達されます。 レポートで回答できる質問を特定します。 レポートをデザインする際は、その質問に注意してください。  
  
-   効果的なデータ ビジュアライゼーションをデザインするために、情報をどのように表示すればレポート ユーザーにわかりやすいかを検討します。 視覚化対象のデータに適したデータ領域を選択してください。 たとえば、要約および集計情報を伝達するには、詳細な情報を含む多数のページにまたがるテーブルよりもグラフの方が効果的です。 グラフ、マップ、インジケーター、スパークライン、データ バー、Tablix に基づくさまざまなグリッド レイアウトの表形式データなど、あらゆるデータ領域でデータセットのデータを視覚化できます。  
  
-   レポートを特定のエクスポート形式で配信する場合は、デザイン時の早い段階でエクスポート形式をテストします。 使用するレンダラーによって、サポートされる機能が異なります。  
  
-   レポートをサブスクリプションとして配信する場合は、デザイン時の早い段階でサブスクリプションをテストします。 作成するサブスクリプションによって、サポートされるパラメーターが異なります。  
  
-   複雑なレイアウトを作成する場合は、複数の段階に分けて、レイアウトを作成します。 四角形をコンテナーとして使用して、レポート アイテムを整理できます。 作業領域を最大化するために直接デザイン画面上でデータ領域を作成し、各領域が完成したら四角形のコンテナーにドラッグできます。 四角形をコンテナーとして使用することにより、すべてのコンテンツの位置を 1 回の操作で調整できます。 四角形を使用すると、各ページにレポート アイテムを表示する方法を制御することもできます。  
  
-   レポートを見やすくするために、特定のレポート アイテムに条件付き表示を使用して、そのアイテムを表示するかどうかをユーザーが選択できるようにすることを検討します。 表示/非表示は、パラメーターまたはテキスト ボックスの切り替えに基づいて設定できます。 条件によって非表示になるテキスト ボックスを追加して、式の中間結果を表示することができます。 レポートに予想外のデータが表示された場合に、それらの中間結果を表示して式をデバッグすることができます。  
  
-   Tablix セルまたは四角形内の入れ子になったアイテムを操作する場合、コンテナーやそこに含まれているアイテムに対して異なる背景色を設定することができます。 既定の背景色は **[色なし]** です。 特定の背景色のアイテムは、背景色が **[色なし]** に設定されたアイテムを透過して見えます。 Tablix セル上の境界線を表示するかどうかなどの表示プロパティを設定する際は、この方法を利用すると、対象となるアイテムを的確に選択することができます。  
  
 レポートを設計する際の考慮事項の詳細については、「[レポートの計画 &#40レポート ビルダー&#41;](../../reporting-services/report-design/planning-a-report-report-builder.md)」を参照してください。  
  
##  <a name="NamingConventions"></a> レポート、データ ソース、およびデータセットの名前付け規則  
  
-   データ ソースおよびデータセットには、データのソースがわかるような名前付け規則を使用します。  
  
    1.  **データ ソース:** セキュリティ上の理由から実際のサーバーまたはデータベースを使用できない場合、ユーザーには、データのソースを別名で示します。  
  
    2.  **データセット:** 基になっているデータ ソースを示す名前を使用します。  
  
    3.  **データ領域:** データ領域の種類とそこに表示されるデータを示します。 データ領域の名前は、次のシナリオで役立ちます。  
  
        1.  **レポート パーツとしてのデータ領域:** レポート作成者がレポート パーツ ギャラリーの保存先を参照する際、わかりやすい名前になっていると、レポート パーツが見つけやすくなります。  
  
        2.  **データ フィードとしてのデータ領域:** 適切な権限を持ったレポート閲覧者は、データ領域から ATOM データ フィードを作成することができます。  
  
-   レポート名には、スペースではなくアンダースコアを使用します。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] からレポートをダウンロードすると、スペースがアンダースコアに置換されます。 ダウンロード機能を使用してレポートをローカルに保存してから、そのレポートを [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]に含めると、アンダースコアの使用により、サブレポートとドリルスルー リンクのレポート依存関係が正確に維持されます。  
  
##  <a name="Data"></a> データの処理  
  
-   まず、使用するすべてのデータをレポート データ ペインに表示します。 レポートで回答するようにデザインされている質問を絞り込む際に、レポート データセット内のデータを、必要なデータのみに制限する方法を検討してください。  
  
-   一般には、レポートに表示するデータのみを含めます。 データセット クエリでクエリ変数を使用して、レポートに表示するデータをユーザーが選択できるようにします。 共有データセットを作成する場合は、レポート パラメーターに基づくフィルターを用意することで、同じ機能を提供できます。  
  
-   クエリの作成経験が豊富な場合、データの量が大きくなりすぎないようにするには、クエリではなくレポートでデータをグループ化すればよいことがわかります。 グループ化をすべてクエリで実行すると、レポートというよりは、クエリの結果セットをそのまま表示したような体裁になりがちです。 しかし、大量のデータの集計値をグラフまたはマトリックスに表示するには、詳細データを含める必要はありません。  
  
-   必要に応じて、レポート データ ソースの名前や場所、データセット クエリ コマンド テキスト、およびパラメーター値をレポートに表示できます。 データの取得元に関する情報は、新しいユーザーの多くが最初に抱く疑問です。 この種の情報を含んだテキスト ボックスは条件によって非表示にし、表示するかどうかをユーザーが選択できるようにすることで、雑然としたレポートとなるのを防ぐことが可能です。 この情報は、レポートの最後のページに追加するようにしてください。 テキスト ボックスの表示/非表示は、ユーザーによる変更が可能なパラメーターに基づいて設定します。  
  
##  <a name="DesignSurface"></a> レポート デザイン画面の操作  
 レポート デザイン画面は WYSIWYG ではありません。 デザイン画面にレポート アイテムを配置すると、その相対的な位置により、実際のレポート ページにアイテムがどのように表示されるかが決まります。 空白は保持されます。  
  
-   レポート デザイン画面上でアイテムを揃えたり整列したりするには、スナップ線とレイアウト ボタンを使用します。 たとえば、選択したアイテムの上端などを揃えたり、別のアイテムのサイズに合わせてアイテムを拡大したり、アイテムの間隔を調整したりできます。  
  
-   デザイン画面で選択したアイテムの位置とサイズを調整するには、方向キーを使用します。 たとえば、次のキーの組み合わせはとても便利です。  
  
    -   **方向キー** 選択したレポート アイテムを移動します。  
  
    -   **Ctrl + 方向キー** 選択したレポート アイテムの位置を微調整します。  
  
    -   **Ctrl + Shift + 方向キー** 選択したレポート アイテムのサイズを増減します。  
  
-   アイテムを四角形に追加するには、マウスの左上のヒントを使用して、四角形のコンテナー内でのアイテムの初期位置を指定します。 選択したオブジェクトの位置を調整するには、キーボード ショートカットを使用します。 四角形は、含まれているアイテムのサイズに合わせて自動的に拡大されます。  
  
-   複数のアイテムを Tablix セルに追加するには、先に四角形を追加してからアイテムを追加します。  
  
     各 Tablix セルには、既定でテキスト ボックスが含まれます。 セルに四角形を追加すると、そのテキスト ボックスが四角形に置き換えられます。 たとえば、Tablix セル内の四角形に入れ子になったインジケーターを配置すると、そのセルを含む行の高さを変更したときにグラフやインジケーターのサイズがどのように拡大されるかを制御できます。  
  
-   デザイン画面の表示を調整するには、 **[ズーム]** コントロールを使用します。 これにより、ページ全体で作業したり、対象をページの特定のセクションに絞って作業したりできます。  
  
-   レポート データ ペインからグループ化ペインにフィールドをドラッグするときに、デザイン画面上の他のレポート アイテムを横切ってドラッグしないようにしてください。そのようにした場合、他のアイテムが選択され、Tablix データ領域が選択解除されるためです。 フィールドは、レポート データ ペインの下からグループ化ペインにドラッグしてください。  
  
###  <a name="Selecting"></a> アイテムの選択  
 レポート デザイン画面で目的のオブジェクトを選択できるようにするには、Esc キー、右クリックのショートカット メニュー、プロパティ ペイン、およびグループ化ペインを使用します。  
  
-   -   デザイン画面で 1 か所に積み重なっているレポート アイテムの選択を順番に切り替えるには、Esc キーを押します。  
  
    -   一部のレポート アイテムでは、右クリックのショートカット メニューを使用して、必要なレポート アイテムまたはレポート アイテムの一部を選択できます。  
  
    -   プロパティ ペインには、現在選択されているアイテムのプロパティが表示されます。  
  
    -   Tablix データ領域の行グループと列グループを操作するには、グループ化ペインからグループを選択します。  
  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]のレポート デザイナーでは、プロパティ ペインのツール バーにあるオブジェクトのドロップダウン リストから選択できるほか、[ドキュメント アウトライン] ウィンドウのレポート アイテムの階層ビューから選択することもできます。 このペインでアイテムを選択すると、デザイン画面に選択したアイテムを表示できます。 [ドキュメント アウトライン] ウィンドウ開くには、 **[表示]** メニューの **[その他のウィンドウ]** をポイントし、 **[ドキュメント アウトライン]** をクリックします。  
  
##  <a name="ReportItems"></a> 特定の種類のレポート アイテムの操作  
  
###  <a name="Parameters"></a> パラメーターの操作  
  
-   レポート パラメーターの主な目的は、データ ソースでデータをフィルター処理して、レポートに必要なデータのみを取得することです。  
  
-   レポート パラメーターの場合、対話機能を有効にすることと、ユーザーが目的の結果を得られるようにすることの間でバランスをとるようにします。 たとえば、パラメーターの既定値を一般的な値に設定できます。  
  
###  <a name="Text"></a> テキストの操作  
  
-   1 つのテキスト ボックスに複数行を貼り付けると、テキストは 1 つのテキスト ランとして追加されます。 各テキスト ランでは、書式設定は 1 つのまとまりとして行うことしかできません。 各行を個別に書式設定するには、テキスト ランで必要に応じて Return キーを押して新しい行を挿入します。 これにより、テキスト ボックス内の各行に個別に書式設定やスタイルを適用できます。  
  
-   テキスト ボックスまたはテキスト ボックス内のプレースホルダー テキストで、書式設定のプロパティとアクションを設定できます。 テキストが 1 行のみの場合は、テキストよりテキスト ボックスでプロパティを設定する方が効率的です。  
  
###  <a name="Expressions"></a> 式の操作  
  
-   単純式と複合式の違いを把握します。 単純式は、テキスト ボックス、プロパティ ペインのプロパティ、またはダイアログ ボックス内で式を入力できる場所に、直接入力できます。 詳細については、「[式 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)」を参照してください。  
  
-   式を作成するときは、それぞれの部分を別々に作成し、その値を確認することをお勧めします。 その後で、すべての部分を結合して最終的な式を作成できます。 マトリックスのセルにテキスト ボックスを追加し、式の各部分を表示して、テキスト ボックスに条件付き表示を設定する方法が役立ちます。 テキスト ボックスが非表示の場合の罫線のスタイルと色を制御するには、まず四角形の中にテキスト ボックスを配置してから、マトリックスに適した四角形の罫線のスタイルと色を設定します。  
  
###  <a name="Indicators"></a> インジケーターの操作  
  
-   既定では、インジケーターは少なくとも 3 つの状態を示します。 インジケーターは、レポートに追加した後、状態を追加または削除することによって構成できます。 ユーザーが見やすいように、色と形の両方が変化するインジケーターを使用することをお勧めします。  
  
##  <a name="Rendering"></a> レポート ページでのレポート アイテムの表示の制御  
  
-   レポート デザイン画面上のレポート アイテムは、関連付けられたデータセット、式、サブレポート、またはテキストのコンテンツに合わせて拡大されます。  
  
    -   レポート ページにアイテムを配置すると、そのアイテムとその右側にあるすべてのアイテムとの距離が、レポート アイテムが左右に拡大されても維持される最小距離になります。 同様に、アイテムとその上にあるアイテムとの距離が、上のアイテムが上下に拡大されても維持される最小距離になります。  
  
    -   レポート内のアイテムがそのデータに合わせて拡大されると、ピア アイテム (同じ親コンテナーに含まれるアイテム) が影響を受けます。その際の規則を以下に示します。  
  
    -   各アイテムは、上にあるアイテムとの最小間隔が維持されるように下に移動します。  
  
    -   各アイテムは、左側にあるアイテムとの最小間隔が維持されるように右に移動します。 右から左のレイアウトのシステムでは、右側にあるアイテムとの最小間隔が維持されるように左に移動します。  
  
    -   子アイテムが拡大されると、それに合わせてコンテナーも拡大されます。 アイテムのコンテナーを特定するには、アイテムを選択し、プロパティ ペインで Parent プロパティを確認します。 ドキュメント アウトライン ペインを使用してレポート アイテムの包含階層を表示することもできます。  
  
    -   **[レイアウト]** ツール バーには、レポート アイテムの端、中心、および間隔を揃えるためのさまざまなボタンが用意されています。 **[レイアウト]** ツール バーを有効にするには、 **[表示]** メニューの **[ツール バー]** をポイントし、 **[レイアウト]** をクリックします。  
  
-   .pdf ファイルとしてレポートを保存する予定の場合、レポートの幅には、エクスポート ファイルの形式で目的の結果が得られるように、明示的に値を設定する必要があります (レポート ページの幅を 7.9375 インチ、左右の余白を .5 インチに設定するなど)。  
  
-   レポート ビューアー ツール バーの **[印刷レイアウト]** と **[ページ設定]** を使用すると、レポートを印刷に対応したビューで表示できます。 不要な水平方向の改ページを削除するには、次の手順を実行します。  
  
    1.  データ領域の間やレポートの端にある余分な空白をすべて削除します。  
  
    2.  **[レポートのプロパティ]** ダイアログ ボックスでページ余白を減らします。  
  
    3.  **四角形** をコンテナーとして使用して、レポート アイテムの表示を制御しやすくします。  
  
    4.  列ヘッダーで、テキスト ボックス プロパティの WritingMode を変更して縦書きテキストを使用します。  
  
 このような操作の組み合わせ、レポート アイテムの幅と高さのプロパティ、レポート本文のサイズ、ページの高さと幅の定義、親レポートの余白の設定、およびレンダラー固有の改ページ調整のすべてが総合されて、表示されるページでのレポート アイテムのレイアウトが決まります。 詳細については、「 [Reporting Services の改ページ (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server 2016 のレポート ビルダー](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
 [Reporting Services チュートリアル &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)   
 [レポート ビルダー チュートリアル](../../reporting-services/report-builder-tutorials.md)  
  
  
