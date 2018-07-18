---
title: '[フルテキスト インデックス] ダイアログ ボックス (Visual Database Tools) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.fulltextindex
ms.assetid: ef45b585-2567-4abe-b421-9fd0994e0146
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ccb9c98771128e7793eac25e11e3de851fa6dce2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37315094"
---
# <a name="full-text-index-dialog-box-visual-database-tools"></a>[フルテキスト インデックス] ダイアログ ボックス (Visual Database Tools)
  このダイアログ ボックスを使用すると、データベース テーブルのテキスト ベースの列に対するフルテキスト検索用にフルテキスト インデックスを作成できます。 フルテキスト インデックスは、通常のインデックスに基づくため、最初に通常のインデックスを作成する必要があります。 通常のインデックスは、単一の非 null 列に作成する必要があります。大きな値を格納している列ではなく、小さな値を格納している列を選択するのが最も適切です。  
  
> [!NOTE]  
>  フルテキスト インデックスを作成する場合、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 、Enterprise Manager などの外部ツールを使用して、あらかじめデータベースのフルテキスト カタログを作成しておく必要があります。  
  
> [!NOTE]  
>  フルテキスト インデックスの機能は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで利用できるわけではありません。 エディションでサポートされている機能の一覧については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[機能は、SQL Server 2014 の各エディションでサポートされている](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)します。  
  
## <a name="options"></a>および  
 **[選択されたフルテキスト インデックス]**  
 既存のフルテキスト インデックスを一覧表示します。 インデックスを選択すると、右のグリッドにそのインデックスのプロパティが表示されます。 一覧が空の場合、テーブルにフルテキスト インデックスは定義されていません。  
  
 **[追加]**  
 新しいフルテキスト インデックスを作成します。  
  
 **削除**  
 **[選択されたフルテキスト インデックス]** ボックスの一覧で選択したフルテキスト インデックスを削除します。  
  
 **[全般] カテゴリ**  
 展開して **[列]** および **[フルテキスト カタログ名]** を表示します。  
  
 **[列]**  
 フルテキスト検索ができる列の名前を、コンマ区切りの一覧として表示します。 完全な一覧を表示するには、プロパティ フィールドの左側にある省略記号ボタン (**[...]**) をクリックします。  
  
 **Full-Text Catalog Name**  
 フルテキスト インデックスが格納されているフルテキスト カタログの名前を表示します。 インデックスを別のカタログに格納するには、カタログ名をクリックし、ドロップダウン リストから別のカタログを選択します。  
  
> [!NOTE]  
>  カタログは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または Enterprise Manager などの外部ツールで、あらかじめ作成しておく必要があります。  
  
 **[IDENTITY] カテゴリ**  
 展開してインデックスの名前フィールドを表示します。  
  
 **名前**  
 システムが指定したフルテキスト インデックスの名前を表示します。  
  
 **[テーブル デザイナー] カテゴリ**  
 展開してインデックスの実行方法を指定するプロパティを表示します。  
  
 **Active**  
 該当するフルテキスト インデックスを使用して、フルテキスト検索を現在実行できるかどうかを示します。  
  
 **[トラッキング設定の変更]**  
 該当するインデックスの変更履歴の状態を示します。[手動]、[自動]、または [オフ]。  
  
 **[クロールの完了]**  
 最近のクロールが完了したかどうかを示します。 このプロパティ値が [いいえ] の場合、クロールは現在進行中です。  
  
 **[現在または最近のクロールの終了日時]**  
 最近のクロールが終了した日時を表示します。  
  
 **[現在または最近のクロール内のエラー]**  
 現在のクロールまたは最近のクロールで発生したエラーの数を表示します。  
  
 **[インデックス バージョン]**  
 クロールが開始した時点での、テーブルのスキーマ バージョンを表示します。  
  
 **[現在または最近のクロール内の行]**  
 現在のクロールまたは最近のクロールで更新された行の数を表示します。  
  
 **[現在または最近のクロールの開始日時]**  
 現在のクロールまたは最近のクロールが開始した日時を表示します。  
  
 **[次のクロールのタイムスタンプ]**  
 次のクロールが開始する日時を表示します。  
  
 **[現在または最近のクロールの種類]**  
 現在のクロールまたは最近のクロールの型を表示します。[空き領域なし]、[インクリメンタル]、[更新]、または [自動伝達]。  
  
 **[一意のインデックス名]**  
 一意の単一列インデックスを持つ、データベース内のすべての列の名前を一覧表示します。 これらの列は、フルテキスト インデックスの作成に使用できます。  
  
## <a name="see-also"></a>参照  
 [フルテキスト インデックス作成ウィザードを使用してください。](../../relational-databases/search/use-the-full-text-indexing-wizard.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
  