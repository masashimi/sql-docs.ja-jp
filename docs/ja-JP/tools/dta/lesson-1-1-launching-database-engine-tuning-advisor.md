---
title: データベース エンジン チューニング アドバイザーの起動 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-query-tuning
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- tuning databases [SQL Server]
- Database Engine Tuning Advisor [SQL Server], starting
ms.assetid: 4abc0e10-96fd-4e46-93d6-d7ee03eec844
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 545a7f2e9758bb5221bbaec9c35516cef66596ab
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2018
---
# <a name="lesson-1-1---launching-database-engine-tuning-advisor"></a>レッスン 1-1: データベース エンジン チューニング アドバイザーの起動
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] まず、データベース エンジン チューニング アドバイザーのグラフィカル ユーザー インターフェイス (GUI) を開きます。 初回起動時には、 **sysadmin** 固定サーバー ロールのメンバーがデータベース エンジン チューニング アドバイザーを起動し、アプリケーションを初期化する必要があります。 初期化が完了すると、 **db_owner** 固定データベース ロールのメンバーがデータベース エンジン チューニング アドバイザーを使用し、所有するデータベースをチューニングできるようになります。 データベース エンジン チューニング アドバイザーの初期化の詳細については、「 [データベース エンジン チューニング アドバイザーの起動および使用](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)」を参照してください。  
  
### <a name="open-the-database-engine-tuning-advisor-gui"></a>データベース エンジン チューニング アドバイザーの GUI を開く  
  
1.  Windows の **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** をポイントします。次に、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]] をポイントし、 **[パフォーマンス ツール]** をポイントして、 **[データベース エンジン チューニング アドバイザー]** をクリックします。  
  
2.  **[サーバーへの接続]** ダイアログ ボックスで既定の設定を確認し、 **[接続]** をクリックします。  
  
既定では、次の図に示す構成でデータベース エンジン チューニング アドバイザーが開きます。  
  
![データベース エンジン チューニング アドバイザーの既定のウィンドウ](../../tools/dta/media/defaultdtagui.gif "データベース エンジン チューニング アドバイザーの既定のウィンドウ")  
  
> [!NOTE]  
> タブおよび **[セッション名]** ボックスに、コンピューターおよび接続しているインスタンスの名前が表示されます。 タブおよびボックスには、現在の日付と時刻も表示されます。  
  
データベース エンジン チューニング アドバイザーの GUI を初めて開くと、2 つのメイン ペインが表示されます。  
  
-   左側のセッション モニターには、この [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで実行されたすべてのチューニング セッションが表示されます。 データベース エンジン チューニング アドバイザーを開くと、セッション モニターの最上部に新しいセッションが表示されます。 隣のペインで、このセッションに名前を付けることができます。 初期状態では既定のセッションのみが表示されます。 このセッションは、データベース エンジン チューニング アドバイザーが自動的に作成する既定のセッションです。 データベースのチューニングが完了すると、接続している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで実行されたすべてのチューニング セッションが、新しいセッションの下に一覧表示されます。 セッション名を変更する、セッションを閉じる、削除する、またはクローンを作成するときは、チューニング セッションを右クリックします。 リスト内で右クリックすると、名前順、状態順、または作成時間順にセッションを並べ替えることができます。新しいセッションも作成できます。 このペインの下部には、選択したチューニング セッションの詳細が表示されます。 **[項目別]** ボタンをクリックすると、詳細情報がカテゴリ別に分類され、表示されます。 **[アルファベット順]** ボタンをクリックすると、詳細情報がアルファベット順に表示されます。 このペインの右側の境界を左方向にドラッグすることで、セッション モニターを非表示にすることもできます。 再度表示するには、ペインの境界を右方向にドラッグします。 セッション モニターは以前のチューニング セッションを表示できるほか、似ている定義を使用して新しいセッションを作成するために使用できます。 また、セッション モニターを使用してチューニング推奨設定を評価することもできます。 詳細については、「 [データベース エンジン チューニング アドバイザーからの出力の表示および操作](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)」を参照してください。 このチュートリアルに戻るには、ブラウザーの **[戻る]** ボタンを使用します。  
  
-   右側のペインには、 **[全般]** タブと **[チューニング オプション]** タブがあります。 これらのタブでデータベース エンジン チューニング セッションを定義します。 **[全般]** タブでは、チューニング セッション名の入力、使用するワークロード ファイルまたはテーブルの指定、およびこのセッションでチューニングするデータベースとテーブルの選択を行います。 ワークロードとは、チューニングするデータベースに対して実行する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのセットです。 データベースをチューニングする際には、トレース ファイル、トレース テーブル、 [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト、または XML ファイルがワークロード入力として使用されます。 **[チューニング オプション]** タブでは、物理データベース設計構造 (インデックスまたはインデックス付きビュー) を選択し、その分析時に適用するパーティション分割方法を指定できます。 また、ワークロードのチューニングにあてる最大時間を指定することもできます。 既定のワークロード チューニング時間は 1 時間です。  
  
> [!NOTE]  
> [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリ エディターから [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] スクリプトをインポートする場合、XML ファイルからスクリプトを取り込むことができます。 詳細については、「 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] データベース エンジン チューニング アドバイザーからの出力の表示および操作 [」の](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)クエリ エディターからデータベース エンジン チューニング アドバイザーを起動する方法に関するセクションを参照してください。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
[ツール オプションとレイアウトの設定](../../tools/dta/lesson-1-2-setting-tool-options-and-layout.md)  
  
  
  