---
title: "SQL Server のプライバシーの補足情報 | Microsoft Docs"
ms.date: 2/19/2018
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-non-specified
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: 
helpviewer_keywords: 
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 4ab0d870af9ca795562c1bc9382540e95dfea119
ms.sourcegitcommit: 03021482208259e6c67599b47df23fbbe8f3a393
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2018
---
# <a name="sql-server-privacy-supplement"></a>SQL Server のプライバシーの補足情報
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事は、SQL Server で使用されるさまざまなデータ オブジェクトの動作と、個人または機密情報を渡すためのオブジェクトの使用方法をまとめたものです。 この記事のデータ分類は、SQL Server オンプレミス製品のバージョンにのみ適用されます。 次のアイテムには適用されません。

- Azure SQL データベース
- SQL Server Management Studio (SSMS)
- SQL Server Data Tools (SSDT)
- SQL Operations Studio

*許可される使用シナリオ*の定義。 この記事のコンテキストでは、Microsoft は、"許可される使用シナリオ" を Microsoft によって開始されたアクションまたはアクティビティとして定義します。

***

>## <a name="access-control"></a>アクセス制御

SQL Server のインストール内のログイン、ユーザー、またはアカウントをセキュリティで保護するために使用される資格情報関連の情報。

### <a name="examples-of-access-control"></a>アクセス制御の例

- パスワード
- 証明書

### <a name="permitted-usage-scenarios"></a>許可される使用シナリオ

|シナリオ  |アクセスの制限  |リテンション期間の要件 |
|---------|---------|---------|
|使用状況のフィードバックを通じて、これらの資格情報がユーザー コンピューターの外に出ることはありません。     |-         |-         |
|クラッシュ ダンプにはアクセス制御データが含まれている可能性があります。     |-         |クラッシュ ダンプ: 最大 30 日。         |
|顧客が手動で挿入する場合を除き、ユーザー フィードバックを通じて、これらの資格情報がユーザー コンピューターの外に出ることはありません。    |サードパーティによるアクセスなしの Microsoft の内部使用に制限されます。         |ユーザー フィードバック: 最大 1 年         |
 |
>## <a name="customer-content"></a>顧客のコンテンツ

顧客のコンテンツは、直接または間接的に、ユーザー テーブル内に格納されるデータとして定義されます。 データには、ユーザー テーブル内に格納される可能性のあるクエリ テキスト内の統計またはユーザー リテラルが含まれます。

### <a name="examples-of-customer-content"></a>顧客のコンテンツの例

- ユーザー テーブルの行内に格納されるデータ値。
- ユーザー テーブルの行内の値のコピーを含む統計オブジェクト。
- リテラル値を含むクエリ テキスト。

### <a name="permitted-usage-scenarios"></a>許可される使用シナリオ
|シナリオ  |アクセスの制限  |リテンション期間の要件 |
|---------|---------|---------|
|使用状況のフィードバックを通じて、このデータがユーザー コンピューターの外に出ることはありません。 |- |- |
|クラッシュ ダンプには顧客のコンテンツが含まれ、Microsoft に送信される場合があります。 |- |クラッシュ ダンプ: 最大 30 日。 |
|同意した顧客は、顧客のコンテンツを含むユーザー フィードバックを Microsoft に送信できます。 |サードパーティによるアクセスなしの Microsoft の内部使用に制限されます。 Microsoft は元の顧客にデータを公開できます。 |ユーザー フィードバック: 最大 1 年 |

>## <a name="end-user-identifiable-information-euii"></a>エンド ユーザーを特定できる情報 (EUII)

ユーザーから受信したデータ、または製品の使用時に生成されたデータ。
- 個々のユーザーにリンク可能。
- コンテンツを含まない。

### <a name="examples-end-user-identifiable-information"></a>エンド ユーザーを特定できる情報の例

- インターフェイスの識別。 完全な IP アドレス
- コンピューター名
- ログイン/ユーザー名
- 電子メール アドレスのローカル部分 (joe@contoso.com)
- 場所情報
- 顧客の識別

### <a name="permitted-usage-scenarios"></a>許可される使用シナリオ

|シナリオ  |アクセスの制限  |リテンション期間の要件|
|---------|---------|---------|
|使用状況のフィードバックを通じて、このデータがユーザー コンピューターの外に出ることはありません。 |- |- |
|クラッシュ ダンプには EUII が含まれ、Microsoft に送信される場合があります。 |- |クラッシュ ダンプ: 最大 30 日 |
|顧客の識別 ID は、ユーザーがサブスクライブしている新しいハイブリッドおよびクラウド機能を提供するために Microsoft に送信される可能性があります。 |- |現在、このようなハイブリッドまたはクラウド機能は存在しません。|
|同意した顧客は、顧客のコンテンツを含むユーザー フィードバックを Microsoft に送信できます。|サードパーティによるアクセスなしの Microsoft の内部使用に制限されます。 Microsoft は元の顧客にデータを公開できます。 |ユーザー フィードバック: 最大 1 年 |

>## <a name="internet-based-services-data"></a>インターネット ベースのサービス データ

SQL Server の使用許諾契約ごとに、インターネット ベースのサービスを提供するために必要なデータです。

### <a name="examples-of-internet-based-services-data"></a>インターネット ベースのサービス データの例

- コンピューター仕様の情報
- ブラウザーの名前/バージョン
- SQL Server のバージョン
- 言語コード
- 特定のオクテットが削除された IP アドレス
- マップ データ

### <a name="permitted-usage-scenarios"></a>許可される使用シナリオ

|シナリオ  |アクセスの制限  |リテンション期間の要件|
|---------|---------|---------| 
|機能の改善および/または現在の機能のバグの修正のために Microsoft で使用される可能性があります。 |サードパーティによるアクセスなしの Microsoft の内部使用に制限されます。 Microsoft は元の顧客にデータを公開できます。  たとえば、ダッシュボードを使用します。 |最短 90 日から最長 3 年 |
|同意した顧客は、顧客のコンテンツを含むユーザー フィードバックを Microsoft に送信できます。 |サードパーティによるアクセスなしの Microsoft の内部使用に制限されます。 |同意した顧客は、顧客のコンテンツを含むユーザー フィードバックを Microsoft に送信できます。 |
|Power View および SQL Reporting Services マップ アイテムの場合、Bing Maps を使用するためにデータが送信される可能性があります。 |セッション データに制限されます。 |- |

>## <a name="system-metadata"></a>システム メタデータ

サーバーの実行中に生成されるデータです。  このデータには顧客のコンテンツは含まれません。

### <a name="examples-of-system-metadata"></a>システム メタデータの例

顧客のコンテンツ、顧客のアクセス制御、または EUII が含まれない場合に考慮されるシステム メタデータを以下に示します。

- データベース GUID
- コンピューター名のハッシュ
- インスタンス名のハッシュ
- アプリケーション名のハッシュ
- 動作/使用状況データ
- SQL カスタマー エクスペリエンス向上プログラム データ (SQLCEIP)
- サーバー構成データ (sp_configure の設定など)
- 機能構成データ
- イベント名とエラー コード

### <a name="permitted-usage-scenarios"></a>許可される使用シナリオ

|シナリオ  |アクセスの制限  |リテンション期間の要件|
|---------|---------|---------|
|機能の改善および/または現在の機能のバグの修正のために Microsoft で使用される可能性があります。|サードパーティによるアクセスなしの Microsoft の内部使用に制限されます。 |最短 90 日から最長 3 年 |
|顧客への提案の際に使用される可能性があります。  たとえば、"製品の使用状況に基づいて、パフォーマンスの向上のため、機能 X の使用を検討してください" というように提案されます。 |Microsoft は、ダッシュボードなどを通じて、元の顧客にデータを公開できます。 |顧客データのセキュリティ ログ: 最短 3 年から最長 6 年 |
将来の製品計画のために Microsoft で使用される可能性があります。 |Microsoft はこの情報を他のハードウェアおよびソフトウェア ベンダーと共有し、Microsoft ソフトウェアでの製品の実行方法を改善する場合があります。 |最短 90 日から最長 3 年|
|出力される使用状況に関するフィードバックに基づいてクラウド ベース サービスを提供するために、Microsoft で使用される可能性があります。 たとえば、組織内のすべての SQL Server インストールでの機能の使用状況を示す顧客のダッシュボードなどです。 |Microsoft は、ダッシュボードなどを通じて、元の顧客にデータを公開できます。 |最短 90 日から最長 3 年 |
|同意した顧客は、顧客のコンテンツを含むユーザー フィードバックを Microsoft に送信できます。 |サードパーティによるアクセスなしの Microsoft の内部使用に制限されます。 Microsoft は元の顧客にデータを公開できます。 |ユーザー フィードバック: 最大 1 年 |

>## <a name="object-metadata"></a>オブジェクト メタデータ

サーバー、データベース、テーブル、およびその他のリソースの説明または構成を行うために使用されるデータ。  オブジェクト メタデータにはデータベース テーブルと列の名前が含まれますが、データベース行のコンテンツや他の顧客のコンテンツは含まれません。 顧客は、オブジェクト メタデータ フィールドのエンド ユーザーを特定できる情報などの個人データを配置したり、これらのフィールドに個人データを格納したりするように設計されたアプリケーションを作成することはできません。

### <a name="examples-of-object-metadata"></a>オブジェクト メタデータの例

- SQL Server データベース名
- テーブル名と列名
- 統計名

### <a name="permitted-usage-scenarios"></a>許可される使用シナリオ

|シナリオ  |アクセスの制限  |リテンション期間の要件|
|---------|---------|---------|
|機能の改善および/または現在の機能のバグの修正のために Microsoft で使用される可能性があります。 |サードパーティによるアクセスなしの Microsoft 内部使用に制限されます。 |最短 90 日から最長 3 年|

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]