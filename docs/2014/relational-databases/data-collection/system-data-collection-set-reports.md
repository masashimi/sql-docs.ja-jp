---
title: システム データ コレクション セット レポート | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data collector [SQL Server], server activity
- server activity [SQL Server]
- reports [SQL Server], data collection
- reports [SQL Server], disk usage
- collection sets [SQL Server], reports
- data collector [SQL Server], reports
- reports [SQL Server], query statistics
- query statistics reports [SQL Server]
- disk usage reports [SQL Server]
ms.assetid: 0b126b8d-4fe7-443d-8a9a-c266350181e5
caps.latest.revision: 24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ae558dfd1f87deef2dd42af040bd804457e3b85e
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2018
ms.locfileid: "43813958"
---
# <a name="system-data-collection-set-reports"></a>システム データ コレクション セット レポート
  データ コレクターは、各システム データ コレクション セットの履歴レポートを提供します。 次の各レポートでは、管理データ ウェアハウスに格納されているデータが使用されます。  
  
-   [ディスク使用量の概要](#Disk)  
  
-   [クエリ統計の履歴](#Query)  
  
-   [サーバーの利用状況の履歴](#Server)  
  
 これらのレポートを使用すると、システム容量の監視やシステム パフォーマンスのトラブルシューティングに役立つ情報を取得できます。  
  
##  <a name="Disk"></a> ディスク使用量の概要レポート  
 ディスク使用量の概要レポートには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス内にあるすべてのデータベースのディスク領域の使用状況に関するデータが示されます。 このレポートに表示されるデータは、ジェネリック T-SQL Query コレクター型を使用するディスク使用量コレクション セットを使用して取得されます。  
  
 ディスク使用量の概要レポートには、オブジェクト エクスプローラーからアクセスできます。 レポートを表示するには、 **[管理]** フォルダーを展開し、 **[データ コレクション]** を右クリックします。次に、 **[レポート]**、 **[管理データ ウェアハウス]** の順にポイントし、 **[ディスク使用量の概要]** をクリックします。 詳細については、「 [コレクション セット レポートの表示 &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md)のインスタンス内にあるすべてのデータベースのディスク領域の使用状況に関するデータが示されます。  
  
### <a name="disk-usage-collection-set-report"></a>ディスク使用量コレクション セット レポート  
 ディスク使用量コレクション セット レポートには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス内のすべてのデータベースで使用されるディスク使用量と、それらの各データベースのデータ ファイルとログ ファイルの拡張傾向の概要が示されます。  
  
-   概要テーブルに、データ コレクターが監視しているサーバーにインストールされているすべてのデータベースの開始サイズ (MB) と現在のサイズが表示されます。  
  
-   傾向および平均拡張率の情報が、データ ファイルとログ ファイルの両方についてグラフと数値で示されます。  
  
#### <a name="disk-usage-collection-set---database-databasename-subreport"></a>ディスク使用量コレクション セット - データベース: <database_name> サブレポート  
 ディスク使用量コレクション セット - データベース: *<database_name>* サブレポートは、ディスク使用量コレクション セット レポートの概要テーブルで特定のデータベースまたはログ ファイルの傾向を表す線をクリックすると表示されます。 このレポートでは、レポートの期間にわたるディスク使用領域の拡張傾向がグラフィカルに表示されます。 ディスク使用量は、データ ファイルについては使用済みの領域、データ領域、未割り当ての領域、インデックス領域ごとに、ログ ファイルについては使用済みの領域、未使用領域ごとに分類されてレポートされます。  
  
 グラフの下にあるテーブルには、データ収集時間と、対応する使用量データの一覧が表示されます。  
  
#### <a name="disk-usage-for-database-databasename-subreport"></a>データベースのディスク使用量: <database_name> サブレポート  
 **[データベースのディスク使用量: <*データベース名*>]** サブレポートは、ディスク使用量コレクション セット レポートの概要テーブルでデータベース名をクリックすると表示されます。 このレポートには、データベースのデータ ファイルおよびトランザクション ログ ファイルによる使用領域の内訳が数値とグラフで示されます。 データ ファイルの使用領域は、インデックス ページ、未割り当ての領域、データ ページ、および未使用領域に割り当てられた割合として分類されます。 これらのカテゴリは、次のように定義されています。  
  
|カテゴリ|定義|  
|--------------|----------------|  
|インデックス|インデックス ページを保持するために使用されているディスク領域のサイズ。|  
|未割り当て|データベースで利用可能なディスク領域のうち、どのオブジェクトにもまだ割り当てられていない領域のサイズ。|  
|data|データ ページで使用されているディスク領域のサイズ。|  
|未使用|1 つ以上のオブジェクトに割り当てられているディスク領域のうち、まだ使用されていない領域のサイズ。|  
  
 トランザクション ログ ファイルの使用領域は、使用済み領域と未使用領域に分類されます。  
  
 自動拡張イベントと自動圧縮イベントがデータベースで発生した場合、それらのイベントがデータ ファイルとログ ファイルの両方についてレポートされます。 レポートには、各イベントの開始時刻と実行時間、および変更後のファイル サイズが表示されます。  
  
 データベースの各データ ファイルによって使用されているディスク領域がレポートされます。 予約済みの領域としてレポートされる領域は、使用済みの領域と、ファイルに割り当てられた未使用の領域の合計になります。 使用済みの領域としてレポートされる領域は、割り当て済みの領域を除く、ファイルで現在使用されている実際の領域です。  
  
##  <a name="Query"></a> クエリ統計の履歴レポート  
 クエリ統計の履歴レポートには、クエリ実行の統計が示されます。 このレポートで使用されるデータは、Query Activity コレクター型を使用するクエリ統計情報コレクション セットを使用して取得されます。  
  
 クエリ統計の履歴レポートには、オブジェクト エクスプローラーからアクセスできます。 レポートを表示するには、 **[管理]** フォルダーを展開し、 **[データ コレクション]** を右クリックします。次に、 **[レポート]**、 **[管理データ ウェアハウス]** の順にポイントし、 **[クエリ統計の履歴]** をクリックします。 詳細については、「 [コレクション セット レポートの表示 &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md)のインスタンス内にあるすべてのデータベースのディスク領域の使用状況に関するデータが示されます。  
  
### <a name="selecting-data-to-include-in-the-report"></a>レポートに含めるデータの選択  
 このレポートには、データ コレクション期間全体のクエリ実行の統計が含まれます。 データ コレクション タイムライン内を移動して、表示するデータのセグメントを選択するには、2 つの方法があります。  
  
 **タイムライン コントロールとナビゲーション ボタン**  
  
 タイムライン コントロールとナビゲーション ボタンを使用すると、タイムライン内を移動したり日付範囲を選択したりすることができます。 矢印ボタンを使用すると左右にスクロールでき、タイムライン内を前後に移動できます。 既定では、矢印を使用すると、タイムライン内を 4 時間分移動できます。 拡大鏡ボタンを使用すると、この時間の範囲を拡大または縮小できます。設定できる値は、15 分、1 時間、4 時間、12 時間、または 24 時間です。 現在選択されている時間の範囲は、タイムラインの強調表示された部分で示され、タイムラインの下にテキストで表示されます。 これらの値は、レポート内のデータと同様に、タイムラインをクリックするかナビゲーション ボタンを使用するたびに更新されます。  
  
 **カレンダー ボタン**  
  
 カレンダー ボタンを使用すると、レポート対象にするデータの開始日、開始時刻、および実行時間を指定できます。  
  
#### <a name="query-statistics-history-report"></a>クエリ統計の履歴レポート  
 総 CPU 時間ごとの上位のクエリのグラフには、選択した時間範囲の各クエリの相対的な負荷が総 CPU 使用率に基づいて示されます。 クエリの相対的な負荷の別のビューを表示するには、グラフの下にある **[実行時間]**、 **[I/O の合計数]**、 **[物理読み取り数]**、または **[論理書き込み数]** のいずれかのハイパーリンクをクリックします。  
  
 グラフの下にあるテーブルには、追加のクエリ データが示されます。 このテーブルには、グラフ化された各クエリのテキストの一覧と、詳細な統計情報が表示されます。 テーブルに示された各クエリと同様にグラフ棒もアクティブなリンクになっていることに注意してください。 アクティブなリンクをクリックすると、そのクエリに対応するクエリの詳細サブレポートが開きます。  
  
#### <a name="query-details-subreport"></a>クエリの詳細サブレポート  
 クエリの詳細サブレポートには、クエリ テキスト全体が表示されます。 クエリの隣には、 **[クエリ テキストの編集]** ハイパーリンクがあります。 このリンクをクリックすると、クエリをクエリ エディターで開くことができます。 クエリの下にある表には、クエリの実行ごとの平均実行時間など、クエリ実行の統計が示されます。  
  
 クエリ プランと実行ごとの平均実行時間のグラフが表示されます。 クエリ プランの相対的なコストの別のビューを表示するには、グラフの下にある **[実行時間]**、 **[物理読み取り数]**、または **[論理書き込み数]** のいずれかのハイパーリンクをクリックします。 グラフ線はアクティブで、任意の箇所をクリックするとクエリ プランの詳細サブレポートを開くことができます。  
  
 グラフの下にあるテーブルには、実行ごとの CPU 使用率に基づく上位 10 のクエリ プランが示されます。 **[プラン番号]** 列の各番号はアクティブなリンクで、クリックするとクエリ プランの詳細サブレポートを開くことができます。  
  
#### <a name="query-plan-details-subreport"></a>クエリ プランの詳細サブレポート  
 このレポートには、クエリ プランの情報が表示されます。 クエリの編集や実行統計の表示に加えて、クエリ プランに関する詳細情報も確認できます。 **[グラフィカルなクエリ実行プランの表示]** ハイパーリンクをクリックすると、現在のクエリの実行プランがグラフィカルに表示されます。  
  
## <a name="server-activity-history-report"></a>サーバーの利用状況の履歴レポート  
 サーバーの利用状況の履歴レポートには、サーバーおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスのリソース消費とサーバー利用状況に関するデータが示されます。 このレポートに表示されるデータは、ジェネリック T-SQL Query コレクター型およびパフォーマンス カウンター コレクター型を使用するサーバー利用状況コレクション セットによって収集されます。  
  
 サーバーの利用状況の履歴レポートには、オブジェクト エクスプローラーからアクセスできます。 オブジェクト エクスプローラーで、 **[管理]** フォルダーを展開し、 **[データ コレクション]** を右クリックします。次に、 **[レポート]**、 **[管理データ ウェアハウス]** の順にポイントし、 **[サーバーの利用状況の履歴]** をクリックします。 詳細については、「 [コレクション セット レポートの表示 &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md)のインスタンス内にあるすべてのデータベースのディスク領域の使用状況に関するデータが示されます。  
  
### <a name="selecting-data-to-include-in-the-report"></a>レポートに含めるデータの選択  
 このレポートには、データ コレクション期間全体のサーバーの利用状況が含まれます。 データ コレクション タイムライン内を移動して、表示するデータのセグメントを選択するには、2 つの方法があります。  
  
 **タイムライン コントロールとナビゲーション ボタン**  
  
 タイムライン コントロールとナビゲーション ボタンを使用すると、タイムライン内を移動したり日付範囲を選択したりすることができます。 矢印ボタンを使用すると左右にスクロールでき、タイムライン内を前後に移動できます。 既定では、矢印を使用すると、タイムライン内を 4 時間分移動できます。 拡大鏡ボタンを使用すると、この時間の範囲を拡大または縮小できます。設定できる値は、15 分、1 時間、4 時間、12 時間、または 24 時間です。 現在選択されている時間の範囲は、タイムラインの強調表示された部分で示され、タイムラインの下にテキストで表示されます。 これらの値は、レポート内のデータと同様に、タイムラインをクリックするかナビゲーション ボタンを使用するたびに更新されます。  
  
 **カレンダー ボタン**  
  
 カレンダー ボタンを使用すると、レポート対象にするデータの開始日、開始時刻、および実行時間を指定できます。  
  
###  <a name="Server"></a> サーバーの利用状況の履歴レポート  
 サーバーの利用状況の履歴レポートには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスとホスト オペレーティング システムのサーバー利用状況の初期表示が示されます。  
  
 次の表に、レポートに表示される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] とシステムの利用状況を示すグラフ、およびグラフからアクセスできる詳細なサブレポートを示します。  
  
|グラフ|レポートの説明|  
|-----------|------------------------|  
|CPU 使用率|CPU 使用率のグラフで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] またはシステムのグラフ線の任意の箇所をクリックすると、以下のサブレポートにアクセスできます。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /> クエリ統計の履歴レポートには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス内の最も負荷の高いクエリのグラフが表示されます。 グラフの下にあるテーブルには、クエリの一覧が表示され、各クエリの統計データも表示されます。 クエリをクリックすると、詳細情報を取得できます。<br /><br /> システム<br /> システムの CPU 使用率レポートには、プロセッサごとの CPU 時間 (%) のグラフが表示され、さらに各プロセスの統計データが表形式で示されます。|  
|メモリ使用量|メモリ使用量のグラフで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] またはシステムのグラフ線の任意の箇所をクリックすると、以下のサブレポートにアクセスできます。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メモリの使用量レポートには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセス メモリの使用量、メモリ カウンター、および内部メモリの種類別消費量のグラフと、コンポーネントの種類別のメモリ平均使用量に関するデータを含むテーブルが表示されます。<br /><br /> システム<br /> システムのメモリ使用量レポートには、メモリ使用量およびキャッシュとページのヒット率のグラフと、各プロセスのワーキング セットとプライベート バイトに関する情報を含むテーブルが表示されます。|  
|ディスク I/O の使用量|ディスク I/O の使用量のグラフで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] またはシステムのグラフ線の任意の箇所をクリックすると、以下のサブレポートにアクセスできます。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ディスク I/O の使用量レポートには、ディスクの応答時間およびディスクの転送速度のグラフが表示されます。 また、ディスク、データベース、およびファイル別の仮想ファイルの統計を含むテーブルも表示されます。<br /><br /> システム<br /> システムのディスク使用量レポートには、ディスクの応答時間、ディスク キューの平均の長さ、ディスクの転送速度、および各プロセスの I/O の書き込みと読み取りに関する情報を含むテーブルが表示されます。|  
|ネットワーク使用量|追加のレポートはありません。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の待機|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の待機のグラフには、実行されたスレッドにより検出された待機が待機のカテゴリ別に表示されます。 グラフで任意のセグメントをクリックすると、詳細なレポートにアクセスできます。 このレポートでは、限られたタイムフレームの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の待機統計グラフに加えて、待機のカテゴリに関する情報が表形式で示されます。 このテーブルには、CPU やそのサブカテゴリなどのカテゴリごとに、待機の数、待機時間、および合計待機時間に対する割合が示されます。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の利用状況|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の利用状況のグラフから、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の利用状況のさまざまな側面にアクセスできます。 1 秒あたりの SQL コンパイル数を示すグラフ線をクリックすることで取得できるレポートを次に示します。<br /><br /> 接続とセッション<br /><br /> 要求<br /><br /> プラン キャッシュのヒット率<br /><br /> tempdb の特性|  
  
## <a name="see-also"></a>参照  
 [[データ コレクション]](data-collection.md)   
 [コレクション セット レポートの表示 &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md)  
  
  
