---
title: 分散再生のインストールの修復 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6fcd8ca8-1ceb-457d-9545-096c74e274d7
caps.latest.revision: 9
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8d5baee6d121becc970dd6c7e6d0a82f47e4a2ec
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304982"
---
# <a name="repair-a-distributed-replay-installation"></a>分散再生のインストールの修復
  分散再生コンポーネント (コントローラーまたはクライアント) を修復すると、次の処理が行われます。  
  
1.  ディスク上に関連付けられたすべてのファイルを再インストールし、既存のファイルを置き換えます。  
  
2.  対応するサービス アカウントが削除された場合、Windows サービス アカウントを再作成します。  
  
 修復操作を利用してコンポーネントを追加または削除することはできません。 コンポーネントを追加または削除を確認するかの機能ツリーに対応する要素をオフに、**機能の選択**ページ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]セットアップします。  
  
### <a name="to-repair-a-failed-installation-of-distributed-replay"></a>分散再生のインストールの失敗を修復するには  
  
1.  **開始**] メニューのをクリックして**コントロール パネルの [**、し、ダブルクリック**プログラム追加と削除**します。  
  
2.  選択[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]で、**のアンインストールまたは変更するプログラム**ウィンドウで、し、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]ダイアログ ボックスで、をクリックして**修復**。  
  
3.  手順に従って、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]ウィザード、し、**機能の選択**を修復するには、[分散再生コンポーネントを選択] ページで、 **[次へ]。**。  
  
4.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] インストール ウィザードを完了すると、選択した 分散再生の機能が修復されます。  
  
  
