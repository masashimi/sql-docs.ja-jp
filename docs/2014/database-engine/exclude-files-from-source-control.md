---
title: ファイルをソース管理から除外 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- excluding files from source control
- source controls [SQL Server Management Studio], file exclusions
ms.assetid: 7dcb6514-db5c-49eb-8b5a-2c766ce39aa7
caps.latest.revision: 21
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: aa1379d18c84db90207e68d548219740ac8d60af
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2018
ms.locfileid: "43811868"
---
# <a name="exclude-files-from-source-control"></a>ソース管理からのファイルの除外
  使用することで作業しているソリューションにソース管理サービスを必要としないファイルが含まれている場合、**ソース管理から除外する**コマンド ファイルをソース管理から除外します。 ファイルを除外すると、そのファイルは [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe データベースに残りますが、プロジェクトと共にチェックインまたはチェックアウトされなくなります。  
  
 使用する必要があります、**ソース管理から除外する**生成されたファイルに対してのみコマンド。 生成されたファイルは、いずれかのことが完全に再作成して[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]ソリューションで別のファイルの内容を基にします。  
  
### <a name="to-exclude-a-file-from-source-control"></a>ソース管理からファイルを除外するには  
  
1.  ソリューション エクスプローラーで、除外するファイルを選択します。  
  
2.  **ファイル**メニューで、**ソース管理**、 をクリックし、**除外** *\<ファイル名 >* **からソース管理**します。  
  
## <a name="see-also"></a>参照  
 [ソース管理の基礎](../../2014/database-engine/source-control-basics.md)   
 [ソース管理オプションを設定します。](../../2014/database-engine/set-source-control-options.md)   
 [ソース管理接続の変更](../../2014/database-engine/change-source-control-connections.md)  
  
  
