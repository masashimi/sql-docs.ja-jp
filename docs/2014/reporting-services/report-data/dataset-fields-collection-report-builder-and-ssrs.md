---
title: データセット フィールド コレクション (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b3884576-1f7e-4d40-bb7d-168312333bb3
caps.latest.revision: 13
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f8890c0ccab740444845180a328f9753c7a50976
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37194913"
---
# <a name="dataset-fields-collection-report-builder-and-ssrs"></a>データセット フィールド コレクション (レポート ビルダーおよび SSRS)
  データセット フィールドは、データ接続のデータを表します。 フィールドは数値データまたは非数値データを表すことができます。 売上高、売上合計、顧客名、データベース識別子、URL、画像、空間データ、電子メール アドレスなどがその例です。 デザイン画面では、フィールドがテキスト ボックス、テーブル、グラフなどのレポート アイテムの式として表示されます。  
  
 レポートには、データセット フィールド、データセット計算フィールド、および組み込みフィールドという 3 種類のフィールドがあり、レポート データ ペインに表示されます。  
  
-   **データセット フィールド :** データ ソースにデータセット クエリを実行したときに返されるフィールドのコレクションを表すメタデータ。  
  
-   **データセット計算フィールド :** データセットに作成する追加フィールド。 各計算フィールドは、ユーザー定義の式を評価して作成されます。  
  
-   **組み込みフィールド :** レポート ビルダーによって提供されるフィールドのコレクションを表すメタデータで、レポートの処理時にレポート名や時間などのレポート情報を提供します。 詳細については、「[組み込み Globals および Users 参照 &#40;レポート ビルダーおよび SSRS&#41;](../report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)」をご覧ください。  
  
 データセットのフィールド名は、レポートのデータセット定義の一部として保存されます。 詳細については、「 [レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)と呼ばれます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Fields"></a> データセット フィールドとクエリ  
 データセット フィールドは、データセット クエリ コマンドおよびユーザー定義の計算フィールドによって指定されます。 レポートに表示されるフィールド コレクションは、データセットの型に依存します。  
  
-   **共有データセット :** フィールド コレクションは、共有データセットをレポートに直接追加したときや、共有データセットを含むレポート パーツを追加したときの、共有データセット定義内のクエリのフィールドの一覧です。 レポート サーバー上で共有データセット定義が変更されても、ローカル フィールド コレクションは変化しません。 ローカル フィールド コレクションを更新するには、ローカル共有データセットの一覧を更新する必要があります。  
  
-   **埋め込みデータセット :** フィールド コレクションは、データ ソースに対して現在のクエリを実行したときに返されるフィールドの一覧です。  
  
 詳細については、「[レポート データ ペインでのフィールドの追加、編集、更新 &#40;レポート ビルダーおよび SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)」を参照してください。  
  

  
### <a name="calculated-fields"></a>計算フィールド  
 計算フィールドは、式を作成して手動で指定します。 計算フィールドは、データ ソースに存在しない新しい値を作成するために使用できます。 たとえば、計算フィールドでは、新しい値を表すほかに、一連のフィールド値のカスタム並べ替え順や、別のデータ型に変換される既存のフィールドを表すことができます。  
  
 計算フィールドは、レポートに対してローカルであり、共有データセットの一部として保存することはできません。  
  
 詳細については、「[レポート データ ペインでのフィールドの追加、編集、更新 &#40;レポート ビルダーおよび SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)」を参照してください。  
  

  
### <a name="entities-and-entity-fields"></a>エンティティとエンティティ フィールド  
 レポート モデル データ ソースを使用する場合、レポート データとしてエンティティとエンティティ フィールドを指定します。 レポート モデルのクエリ デザイナーでは、関連エンティティを対話的に探索して選択し、レポート データセットに含めるフィールドを選択することができます。 クエリのデザインを終了すると、レポート データ ペインにエンティティの識別子とエンティティ フィールドのコレクションが表示されます。 エンティティの識別子はレポート モデルにより自動的に生成され、通常エンド ユーザーには表示されません。  
  
### <a name="using-extended-field-properties"></a>拡張フィールド プロパティの使用  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]などの多次元クエリをサポートするデータ ソースは、フィールドのフィールド プロパティをサポートします。 フィールド プロパティは、クエリの結果セットに表示されますが、 **レポート データ** ペインには表示されません。 これらは、レポートで使用することが可能です。 フィールドのプロパティを参照するには、フィールドをレポートにドラッグし、既定のプロパティの `Value` を、目的のプロパティのフィールド名に変更します。 たとえば、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] キューブでは、キューブ セルの値の書式を定義できます。 フィールド プロパティを使用して書式設定された値が使用可能な`FormattedValue`します。 値を使用してテキスト ボックスの書式プロパティを設定するのではなく、値を直接使用するには、フィールドをテキスト ボックスにドラッグして、既定式 `=Fields!FieldName.Value` を `=Fields!FieldName.FormattedValue`に変更します。  
  
> [!NOTE]  
>  すべての `Field` プロパティをすべてのデータ ソースに使用できるわけではありません。 `Value` と `IsMissing` プロパティは、すべてのデータ ソースで定義されます。 その他の定義済みプロパティ (多次元データ ソースの `Key`、`UniqueName`、`ParentUniqueName` など) は、データ ソースが、それらのプロパティを提供している場合にのみサポートされます。 一部のデータ プロバイダーでは、カスタム プロパティがサポートされます。 詳細については、「[レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)」で、目的のデータ ソースの種類の拡張フィールド プロパティについてのトピックを参照してください。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ ソースの場合は、「[Analysis Services Database データベースに対する拡張フィールド プロパティ&#40;SSRS&#41;](extended-field-properties-for-an-analysis-services-database-ssrs.md)」を参照してください。  
  

  
##  <a name="Defaults"></a> フィールドの既定式について  
 テキスト ボックスは、レポート本文のテキスト ボックス レポート アイテム、または Tablix データ領域のセル内のテキスト ボックスです。 フィールドをテキスト ボックスにリンクするとき、テキスト ボックスの位置によって、フィールド参照の既定式が決定されます。 レポート本文のテキスト ボックス値の式は、集計およびデータセットを指定する必要があります。 レポートに 1 つのデータセットしか存在しない場合、この既定式が作成されます。 数値を表すフィールドの場合、既定の集計関数は Sum です。 数値以外の値を表すフィールドの場合、既定の集計は First です。  
  
 Tablix データ領域では、既定のフィールド式は、フィールドを追加するテキスト ボックスの行およびグループ メンバーシップに依存します。 テーブルの詳細行のテキスト ボックスに追加した場合、フィールド Sales のフィールド式は、 `[Sales]`です。 同じフィールドをグループ ヘッダー内のテキスト ボックスに追加した場合、グループ ヘッダーには詳細値ではなくグループの集計値が表示されるので、既定の式は `(Sum[Sales])`です。 レポートの実行時に、レポート プロセッサによって各式が評価され、レポート内の結果が置き換えられます。  
  
 式の詳細については、「[式 &#40;レポート ビルダーおよび SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)」を参照してください。  
  

  
##  <a name="DataTypes"></a> フィールド データ型  
 データセットを作成したとき、データ ソースのフィールドのデータ型がレポートで使用される正確なデータ型ではない場合があります。 データ型は、1 つまたは 2 つのマッピング レイヤーを通過することがあります。 データ処理拡張機能またはデータ プロバイダーが、データ ソースのデータ型を共通言語ランタイム (CLR) データ型にマップすることがあります。 データ処理拡張機能によって返されるデータ型は、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]の共通言語ランタイム (CLR) データ型のサブセットにマップされます。  
  
 データ ソースでは、データは、データ ソースでサポートされるデータ型に格納されます。 たとえば、データを[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースは、サポートされているいずれかを指定する必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]などのデータ型`nvarchar`または`datetime`します。 データ ソースからデータを取得するとき、データは、データ ソースの種類に関連付けられているデータ処理拡張機能またはデータ プロバイダーを通過します。 データ処理拡張機能によっては、データは、データ ソースで使用されるデータ型からデータ処理拡張機能でサポートされるデータ型に変換されることがあります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]と共にインストールされる共通言語ランタイム (CLR) バージョンでサポートされるデータ型を使用します。 データ プロバイダーは、ネイティブ データ型の結果セットの各列を [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 共通言語ランタイム (CLR) データ型にマップします。  
  
 各ステージにおいて、データは、次の一覧で説明するデータ型によって表現されます。  
  
-   **データ ソース** 接続先のデータ ソースの種類のバージョンでサポートされるデータ型。  
  
     たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ ソースの一般的なデータ型には、`int`、`datetime`、および `varchar` が含まれます。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] で追加されたデータ型により、`date`、`time`、`datetimetz`、および `datetime2` のサポートが追加されました。 詳細については、「 [データ型 (Transact-SQL)](http://go.microsoft.com/fwlink/?linkid=98362)」を参照してください。  
  
-   **データ プロバイダーまたはデータ処理拡張機能** データ ソースに接続するときに選択したデータ処理拡張機能のデータ プロバイダーのバージョンによってサポートされるデータ型。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] に基づくデータ プロバイダーは、CLR でサポートされるデータ型を使用します。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] データ プロバイダーのデータ型の詳細については、MSDN の「 [データ型のマッピング (ADO.NET)](http://go.microsoft.com/fwlink/?LinkId=112178) 」および「 [基本型の操作](http://go.microsoft.com/fwlink/?LinkId=112177) 」を参照してください。  
  
     一般的なデータ型のサポートなど、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]含める`Int32`と`String`します。 カレンダー日付および時刻は `DateTime` 構造体でサポートされています。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0 Service Pack 1 が導入されたサポート、`DateTimeOffset`タイム ゾーン オフセットを含む日付の構造体。  
  
    > [!NOTE]  
    >  レポート サーバーは、レポート サーバー上にインストールされ構成されたデータ プロバイダーを使用します。 プレビュー モードのレポート作成クライアントは、クライアント マシン上にインストールされ構成されたデータ処理拡張機能を使用します。 レポート クライアントとレポート サーバー環境の両方でレポートをテストする必要があります。  
  
-   **レポート プロセッサ** データ型は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]のインストール時にインストールされた CLR のバージョンに基づきます。  
  
     たとえば、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] で追加された新しい日付および時刻型に対してレポート プロセッサが使用するデータ型を次の表に示します。  
  
    |SQL データ型|CLR データ型|説明|  
    |-------------------|-------------------|-----------------|  
    |`Date`|`DateTime`|日付のみ|  
    |`Time`|`TimeSpan`|時刻のみ|  
    |`DateTimeTZ`|`DateTimeOffset`|タイム ゾーン オフセットを含む日付と時刻|  
    |`DateTime2`|`DateTime`|小数ミリ秒を含む日付と時刻|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの型の詳細については、「 [データ型 (データベース エンジン)](http://go.microsoft.com/fwlink/?linkid=98362) 」および「 [日付と時刻のデータ型および関数 (Transact-SQL)](http://go.microsoft.com/fwlink/?linkid=98360)」を参照してください。  
  
 式のデータセット フィールドへの参照を含める方法については、「[式で使用されるデータ型 &#40;レポート ビルダーおよび SSRS&#41;](../report-design/data-types-in-expressions-report-builder-and-ssrs.md)」を参照してください。  
  

  
##  <a name="MissingFields"></a> 実行時に存在しないフィールドの検出  
 レポートを処理したときに、データ ソースに列が存在しないために、データセットの結果セットに指定されたすべての列の値が含まれていないことがあります。 フィールド プロパティの IsMissing を使用して、フィールドの値が実行時に返されたかどうかを検出できます。 詳細については、「[データセット フィールド コレクションの参照 &#40;レポート ビルダーおよび SSRS&#41;](../report-design/built-in-collections-dataset-fields-collection-references-report-builder.md)」を参照してください。  
  

  
## <a name="see-also"></a>参照  
 [データセットのプロパティ] ダイアログ ボックスの [フィールド&#40;レポート ビルダー&#41;](../dataset-properties-dialog-box-fields-report-builder.md)   
 [レポート ビルダーのレポート パーツおよびデータセット](report-parts-and-datasets-in-report-builder.md)   
 [レポート埋め込みデータセットと共有データセット (レポート ビルダーおよび SSRS)](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
