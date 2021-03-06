---
title: SSMA for Oracle (OracleToSQL) における新 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 09/22/2018
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
caps.latest.revision: 24
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 78f1615e375dfeafbcf25a8b0466ed92fbcc16ea
ms.sourcegitcommit: 7076fcb854c033a5dbeac7fcb22c5e15cf8528fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2018
ms.locfileid: "46362046"
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>SSMA for Oracle (OracleToSQL) の新機能新機能
この記事では、各リリースで変更を Oracle の SSMA が一覧表示します。  

## <a name="ssma-v710"></a>SSMA v7.10
SSMA for Oracle の v7.10 リリースには、次の変更が含まれています。
- 対象となる修正プログラムが追加のセキュリティとプライバシーの保護をグローバル要件の変更を満たすために提供するように設計します。
- 階層のクエリに関連する変換の改善。

> [!IMPORTANT]
> SSMA v7.4 と以降のバージョンでは、.Net 4.5.2 は、インストールの前提条件です。

## <a name="ssma-v79"></a>SSMA v7.9
SSMA for Oracle の v7.9 リリースには、次の変更が含まれています。
- 品質と変換のメトリックを向上させる対象となる修正します。
- Oracle から SQL Server への移行の"Continue"ステートメントをサポートします。
- データ型マッピングとプロジェクトの環境設定を変更するコマンドラインの SSMA でサポートします。
- 移行のサポートを SQL Server Integration Services (SSIS) を使用してデータ。 スキーマを変換した後を右クリック コンテキスト メニュー オプションを使用して、SSIS パッケージを作成することができます。
- SSMA で Azure SQL Database の接続ダイアログが、完全修飾サーバー名を指定することも変更されました。 SSMA の以前のバージョンで、Azure SQL Database のプレフィックスは、プロジェクト設定内で明示的に説明する必要があります。

> [!IMPORTANT]
> SSMA v7.4 と以降のバージョンでは、.Net 4.5.2 は、インストールの前提条件です。

## <a name="ssma-v78"></a>SSMA v7.8
SSMA for Oracle の v7.8 リリースには、次の変更が含まれています。
-   サポートが追加されました。
    - IN 句の行の式。
    - 暗黙的な型キャスト。
    - Azure SQL Database の UID 変換します。
- プロジェクトの設定で変更が強調表示されている型のマッピング。
- ユーザーがテレメトリを無効にする機能を提供します。

> [!IMPORTANT]
> SSMA v7.4 と以降のバージョンでは、.Net 4.5.2 は、インストールの前提条件です。

## <a name="ssma-v77"></a>SSMA v7.7
SSMA for Oracle の v7.7 リリースには、次の変更が含まれています。
- SSMA for Oracle は、品質と変換のメトリックを向上させる対象となる修正プログラムで拡張されています。
- SSMA for Oracle の 32 ビット バージョンは戻るには、要望に基づき、です。 (V7.4) より前の以前の実装と比較して、2 つのインストーラー パッケージがあるが、並行してインストールことはできません。 その結果がある場合、接続コンポーネントに基づいて最も適切なバージョンを選択する必要があります。 可能であれば、64 ビット バージョンを使用することをお勧めは常にします。
- SQL Server 2017 のサポートは、Oracle の拡張機能パックでも Linux でサポートされています (新しいリモート インストール オプション) は正式なようになりました。 Linux では、テスト担当者としてインストールされている場合、拡張機能パックの機能が制限されることに注意してくださいし、サーバー側のデータの移行機能はサポートされていません。
- SSMA for Oracle では、通常のテーブルとして具体化されたビューを移行できます (で設定を使用して構成可能な**プロジェクト設定** -> **同期** ->  **具体化されたビューのテーブルのバッキングの検出**)。

> [!IMPORTANT]
> SSMA v7.4 と以降のバージョンでは、.Net 4.5.2 は、インストールの前提条件です。

## <a name="ssma-v76"></a>SSMA v7.6
SSMA for Oracle の v7.6 リリース品質と変換のメトリックを向上させる修正プログラムを対象となると SQL Server 2017 (パブリック プレビュー) のサポートが強化されました。 Windows および Linux 上の SQL Server 2017 のサポートはパブリック プレビューであり、運用環境の移行のために使用しないでください。

> [!IMPORTANT]
> SSMA v7.4 と以降のバージョンでは、.Net 4.5.2 は、インストール前提条件、およびツールの 32 ビット バージョンは廃止されました。

## <a name="ssma-v75"></a>SSMA v7.5
SSMA for Oracle の v7.5 リリースには、次の変更が含まれています。
- 障碍を持つユーザーのアクセシビリティを確認します。 いくつかの機能強化で強化されています。
- お客様からのフィードバックに基づいて、データの移行中に日付と float データ型の処理の向上など、品質と変換の対象となる修正は、メトリックを向上させるために更新されます。

> [!IMPORTANT]
> .Net 4.5.2 は SSMA v7.5 をインストールするための前提条件です。 さらに、v7.4 以降では、SSMA の 32 ビット バージョンは中止されています。

## <a name="ssma-v74"></a>SSMA v7.4
SSMA for Oracle の v7.4 リリースには、次の変更が含まれています。

- SSMA for Oracle では、移行のターゲット プラットフォームとして Azure SQL Data Warehouse をサポートしているようになりました。

    ![新しいプロジェクト ウィンドウ](../media/new-project.png)
  - 次の図のように、データ ウェアハウス ストレージのオプションをサポートしています。

    ![データ ウェアハウスのストレージ オプション](../media/storage-options_red.png)
  - 次の図のように、データの分布オプションをサポートしています。

    ![データ ウェアハウスのデータの分布](../media/data-distribution_red.png)

- **クエリ タイムアウト**オプションは、ソースとターゲットのスキーマ オブジェクトの検出中に使用できるようになりました。

    ![query timeout オプション](../media/query-timeout_red.png)

- 品質と変換のメトリックは、お客様のフィードバックに基づいて、対象となる修正プログラムが強化されています。

> [!IMPORTANT]
> .Net 4.5.2 は SSMA v7.4 をインストールするための前提条件です。 さらに、v7.4 以降では、SSMA の 32 ビット バージョンは中止されています。

## <a name="ssma-v73"></a>SSMA v7.3
SSMA for Oracle の v7.3 リリースには、次の変更が含まれています。
- お客様からのフィードバックに基づいて対象となる修正プログラムで強化された品質と変換メトリック。
- SSMA 拡張性フレームワークは、次のものを使用して公開:
  - SQL Server Data Tools (SSDT) プロジェクトにエクスポートする機能。
    -   SSMA から SSDT プロジェクトにスキーマ スクリプトをエクスポートできます。 スキーマ スクリプトを使用して、追加のスキーマを変更して、データベースをデプロイすることができます。
![SSDT プロジェクト コマンドとして保存します。](../media/export-schema-scripts_red.png)
  - カスタム変換を実行するために、SSMA で使用できるライブラリ。
    - 構文のカスタム変換および変換 SSMA によって処理されなかった以前に対応するコードを作成します。
      - カスタムのコンバーターを作成する方法の手順については、このブログ投稿「[変換機能を拡張する SQL Server Migration Assistant の](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)します。
      - これからの変換のサンプル プロジェクトをダウンロード[ブログの投稿](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)します。


## <a name="ssma-v72"></a>SSMA v7.2
SSMA for Oracle の v7.2 リリースには、次の変更が含まれています。
- お客様からのフィードバックに基づいて対象となる修正プログラムで強化された品質と変換メトリック。
- 顧客の問題をトラブルシューティングし、SSMA のコンバージョン率を向上させるより良いデータ ポイントを提供するテレメトリの機能強化。

## <a name="ssma-v71"></a>SSMA v7.1
SSMA for Oracle の v7.1 リリースには、次の変更が含まれています。
- Windows と Linux CTP1 で SQL Server 2017 は、移行のサポートされているターゲット プラットフォームではようになりました。 この機能は、technical preview ではあり、対象の SQL サーバーにスキーマとデータの移動を許可します。
- SSMA は、使用可能になるとすぐには、SSMA の最新バージョンをダウンロードする自動更新をサポートします。
- SSMA のインストール可能なバイナリは、Windows インストーラー パッケージ ファイル (.msi) が配信されるようになりました。

**リソース**

[SQL Server Migration Assistant の変換機能を拡張します。](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[評価し、Microsoft 以外のデータ プラットフォームから SQL Server にデータを移行 *(Oracle など) を含む*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>2016 年 5 月  
SSMA for Oracle の 2016 年 5 月リリースには、次の変更が含まれています。  

- SQL Server 2016 のサポートが追加されました。
- SQL Server のテンポラル テーブルへの Oracle 後記アーカイブ テーブルの追加の変換。

    **注**-SSMA は、Oracle 後記データ アーカイブ テーブルから履歴データをコピーしません。 その結果、履歴データは、移行プロセス中に手動でコピーする必要があります。 さらに、SSMA は、システム テーブルとして扱われるため、履歴テーブルを SQL Server メタデータ エクスプ ローラーに表示されない、中には、SQL Server Management Studio で履歴テーブルを表示できます。
    SQL Server 2016 では、いくつかの Oracle 後記機能 (など) をサポートされていません。
    - Oracle 後記トランザクション クエリ
    - DBMS_FLASHBACK パッケージ
    - フラッシュ バック ・ トランザクション
    - フラッシュ バック ・ データ アーカイブ
    - フラッシュ バック ・ テーブル
    - フラッシュ バック ・ ドロップ
    - フラッシュ バック データベース
- SQL Server ポリシー オブジェクト (Oracle の行レベルのセキュリティ) に Oracle VPD ポリシーの追加変換します。
- Oracle の初期読み込みの減少の時間。
- 強化されたパーサーと競合回避モジュール。
- .Net 2.0 のインストーラーのチェックを削除します。
- 更新された拡張機能パックの依存関係から .Net 3.5 を .Net 4.0 にします。
- プロジェクト"保存"固定と SSMA コンソールの「プロジェクトを開く」コマンド。
- SSMA コンソールの"securepassword"コマンドを修正しました。
- オブジェクトの初期読み込みのカウントを修正しました。
- Oracle の文字データ型の変換を修正しました。
- グローバル設定でバグを修正しました。
  
## <a name="march-2016"></a>2016 年 3 月  
SSMA for Oracle の 2016 年 3 月のプレビュー リリースには、次の変更が含まれています。  
  
-   SQL Server 2016 への移行のサポートが追加されました。  
-   移行する Oracle 行レベル セキュリティ (をいくつかの制限) のサポートが追加されました。  
-   移行のサポートを追加する SQL Server 列ストア テーブルをメモリ内での Oracle です。  
  
## <a name="january-2016"></a>2016 年 1 月  
2014 年 1 月 SSMA for Oracle のメンテナンス リリースには、次の変更が含まれています。  
  
-   クラスター化インデックスのサポートが追加されました。  
-   低速の Oracle スキーマ クエリ (RFC 5076207) を修正しました。  
-   固定コンソールから Azure に接続します。  
-   追加の表示 メニュー項目をログ、SSMA (RFC 5706203) にします。 
-   追加された製品利用統計情報。  
  
## <a name="july-2014"></a>2014 年 7 月  
SSMA for Oracle の 2014 年 7 月リリースには、次の変更が含まれています。  
  
-   Azure SQL DB のサポートが追加されました。  
-   拡張機能パックの機能は、Azure SQL DB をサポートするために、スキーマに移動します。  
-   Oracle の具体化されたビューのサポートが追加されました。  
-   SQL Server 2014 のメモリのサポートを追加では、テーブルが最適化されています。  
-   含まれるパフォーマンスの向上は、10 k を超えるデータベースのオブジェクトをテストします。  
-   多数のオブジェクトを処理するための追加の UI 機能強化。  
-   LOB スキーマの「既知」の強調表示を追加します。  
-   変換速度の向上が含まれています。  
-   UI でオブジェクトを表示するためのサポートが追加されましたがカウントされます。  
-   25% 以上削減レポート サイズ。
-   未解析のコンス トラクターに対して改善されたエラー メッセージ。  
  
## <a name="april-2014"></a>2014 年 4 月  
SSMA for Oracle の 2014 年 4 月リリースには、次の変更が含まれています。  
  
-   MS SQL Server 2014 のサポートが追加されました。  
-   Oracle 12 とクエリの最適化のサポートが追加されました。  
-   Azure への変換に関するバグを固定します。  
-   IE 10 で非表示レポート ページに関するバグを固定します。  
  
## <a name="january-2012"></a>2012 年 1 月  
SSMA for Oracle の 2012 年 1 月リリースには、次の変更が含まれています。  
  
-   NULL にデフォルトの RowType と RecordType の入力パラメーターのサポートが追加されました。  
  
## <a name="july-2011"></a>2011 年 7 月  
SSMA for Oracle の 2011 年 7 月リリースには、次の変更が含まれています。  
  
-   Oracle シーケンスへの変換のサポートを追加[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"Denali"シーケンス ジェネレーター。  
-   レポート データの移行中にエラーを改善しました。  
-   予約語を使用してステートメントの変換を向上します。  
-   関数の日付値の暗黙的な変換が向上します。  
  
## <a name="april-2011"></a>2011 年 4 月  
SSMA for Oracle の 2011 年 4 月リリースには、次の変更が含まれています。  
  
-   "SSMA for Oracle"製品の統合は、サポートする[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"Denali"  
-   接続してへの移行のサポートが追加されました[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"Denali"  
-   データの並列移行のサポート、強化されたクライアント側のデータ移行エンジン。  
-   強化されたデータの移行とパフォーマンスを単純な一括復旧モデルが記録されます。  
-   SSMA (v4.0 および v4.2) の以前のバージョンで作成されたプロジェクトの旧バージョンとの互換性サポートが追加されました。  
-   Oracle v5.0 製品のサイド バイ サイド (SxS) SSMA (v4.0 および v4.2) の以前のバージョンでの SSMA のインストールに機能が追加されました。  
-   Reporting (サブタイプ、VARRAY、入れ子になったテーブル、オブジェクトのテーブルおよびビューのオブジェクトを含む) ユーザー定義型と特殊なエラー メッセージの PL/SQL ブロックでその使用状況のサポートが追加されました。  

## <a name="july-2010"></a>2010 年 7 月  
SSMA for Oracle の 2010 年 7 月リリースには、次の変更が含まれています。  
  
-   SQL Server 2008 R2 への移行のサポートが追加されました。  
-   コマンドラインの実行用の新しい SSMA コンソール アプリケーションを追加します。  
-   サーバー側とクライアント側のデータ移行のエンジンの両方を使用してデータ移行のサポートが追加されました。  
-   データ移行で「カスタム選択」ステートメントのサポートが追加されました。  
-   Oracle 11 g R2 に移行するためのサポートが追加されました。  
  
## <a name="june-2008"></a>2008 年 6 月  
SSMA for Oracle の 2008 年 6 月リリースには、次の変更が含まれています。  
  
-   評価レポートは、シノニムの追加情報、解析可能なオブジェクト、パネルと SQL Server ロゴの削除、およびレイアウトの永続性の生ソースなどの機能強化に追加します。  
-   オブジェクトへの変換に追加された機能強化:  
    -   パッケージ DBMS_LOB、DBMS_SQL 変換を追加します。  
    -   変換の変更を結合します。  
    -   変更のコレクションとレコードの変換、フィールドごとに別個の変数を使用してリリースされる単純なケース内のレコードの変換ようになりました。  
    -   レコードとコレクションの実装の機能強化。  
    -   ウィンドウ集計関数が追加されます。  
    -   ROLLUP/CUBE 句を追加します。  
    -   NEXTVAL/CURVAL の機能強化。  
    -   SET 句でグループ化、列のセットをグループ化と ID をグループ化が追加されました。  
    -   MERGE ステートメントが追加されます。  
    -   新しい datetime 型およびレコードのコレクションとして追加された CLR データ型の変換をサポートします。  
-   テスト担当者の新機能を追加します。 テーブルをテスト担当者を使用してオブジェクトとしてテストできる、テスト_ケースで複数のテスト可能なオブジェクトの呼び出しの順序を変更することができます、ユーザーがパラメーターと戻り値は、プロシージャと関数のレコードとコレクションをテストできますおよびを確認する依存関係のアナライザーが追加されましたテーブルのみ使用されます。  
  
## <a name="august-2007"></a>2007 年 8 月  
SSMA for Oracle の 2007 年 8 月リリースには、次の変更が含まれています。  
  
-   新しいテスト担当者のコンポーネントでは、作成、管理、および変換後の SQL コードを確認するテスト_ケースを実行することができますを追加します。  
-   Oracle のサブタイプ、コレクション、およびローカル モジュールの変換のサポートが追加されましたが、SQL のコンバーターに追加されました。  
-   追加の同期の新機能では、SQL Server データベースと特定のオブジェクトを同期することができます。  
-   新しい変換オプションを追加します。  
  
## <a name="april-2007"></a>2007 年 4 月  
SSMA for Oracle の 2007 年 4 月リリースでは、最初のリリースをでした。
