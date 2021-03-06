---
title: オプション (プレーン テキストのテキスト エディター タブ ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.Plain_Text.Tabs
ms.assetid: 07d82d10-bca9-4b37-abbb-58ef9bfb264b
caps.latest.revision: 21
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 6bce8fcc9ea458c3cf2408a3edeb497def4044b2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37275308"
---
# <a name="options-text-editor---plain-text---tabs-page"></a>[オプション] ([テキスト エディター]/[テキスト形式]/[タブ] ページ)
  特定の開発言語に関連付けられていないドキュメントを編集するときには、テキスト エディターが使用されます。このダイアログ ボックスを使用すると、テキスト エディターのタブの動作を変更できます。 この設定を表示するには、**[ツール]** メニューの **[オプション]** をクリックして、**[テキスト エディター]** フォルダーを展開し、さらに **[テキスト形式]** を展開して、**[タブ]** をクリックします。  
  
## <a name="setting-options-in-multiple-locations"></a>複数の場所でのオプション設定  
 テキスト形式エディターのオプションは、**[すべての言語] の [全般]** ダイアログで設定することもできます。 ただし、DMX エディターや MDX エディターなど、他の **エディターに対し、** [すべての言語] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] のダイアログを使用して異なるオプションを設定する場合は、ここで紹介したダイアログを使用してテキスト形式エディターのオプションを設定し直す必要があります。  
  
## <a name="indenting"></a>インデント  
 **なし**  
 Enter キーを押したときに作成される新しい行はインデントされません。 カーソルは、新しい行の 1 列目に置かれます。  
  
 **ブロック**  
 Enter キーを押したときに作成される新しい行が、直前のインデントされている行と同じ位置までインデントされます。  
  
 **スマート**  
 プレーンテキスト エディターではこの種の書式設定はサポートされません。  
  
## <a name="tabs"></a>タブ  
 **[タブ サイズ]**  
 タブ ストップ間の間隔をスペース数で設定します。 既定値は、スペースが 4 つです。  
  
 **インデントのサイズ**  
 自動インデントのサイズをスペース数で設定します。 既定値は、スペースが 4 つです。 指定されたサイズになるように、タブ文字、スペース文字、またはその両方が挿入されます。  
  
 **スペースを挿入します。**  
 タブ文字を使用せずにスペース文字だけを挿入してインデントします。 たとえば **[インデント サイズ]** が 5 に設定されている場合、Tab キーを押すか、**[書式設定]** ツール バーの **[インデント]** ボタンを押すごとに、5 つのスペース文字が挿入されます。  
  
 **タブを保持します。**  
 インデントするときにできる限り多くのタブ文字を挿入します。 それぞれのタブ文字が、**[タブ サイズ]** で指定された数のスペースを満たします。 **[インデント サイズ]** が **[タブ サイズ]** 値の倍数でない場合は、その差を埋めるためにスペース文字が追加されます。  
  
  
