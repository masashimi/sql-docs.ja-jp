---
title: データベース ダイアグラム デザイナーの設定 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vdt.diagnostic.InstallSqlDiagramSupport
helpviewer_keywords:
- Database Diagram Designer
- database diagrams [SQL Server], Database Diagram Designer
- diagrams [SQL Server], Database Diagram Designer
ms.assetid: 927321ee-b459-4f5b-9719-4a7a95639143
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3f3448116821aa161ecb46aa920d1f2613e18438
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2018
ms.locfileid: "43816508"
---
# <a name="set-up-database-diagram-designer-visual-database-tools"></a>データベース ダイアグラム デザイナーの設定 (Visual Database Tools)
  データベース ダイアグラム デザイナーを使用するには、 **db_owner** ロールのメンバーによって、ダイアグラムへのアクセスを制御するようにあらかじめ設定しておく必要があります。  
  
### <a name="to-set-up-database-diagramming"></a>データベース ダイアグラムを設定するには  
  
1.  オブジェクト エクスプローラーから、データベース ノードを展開します。  
  
2.  データベース接続のデータベース ダイアグラム ノードを展開します。  
  
3.  データベースのダイアグラム化を設定するかどうかをたずねるメッセージが表示されたら、 **[はい]** を選択します。  
  
    > [!NOTE]  
    >  これにより、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースにデータベース ダイアグラム テーブル、システム ストアド プロシージャ、およびシステム関数が作成されます。  
  
4.  Visual Studio では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに次のオブジェクトが作成されます。  
  
    1.  sysdiagrams テーブル  
  
    2.  sp_alterdiagram ストアド プロシージャ  
  
    3.  sp_creatediagram ストアド プロシージャ  
  
    4.  sp_dropdiagram ストアド プロシージャ  
  
    5.  sp_renamediagram ストアド プロシージャ  
  
    6.  fn_diagramobjects 関数  
  
    7.  sp_helpdiagrams ストアド プロシージャ  
  
    8.  sp_helpdiagramsdefinition ストアド プロシージャ  
  
    9. sp_upgraddiagrams ストアド プロシージャ  
  
## <a name="see-also"></a>参照  
 [データベース ダイアグラムの所有権について&#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [データベース ダイアグラムの以前のエディション アップグレード&#40;Visual Database Tools&#41;](upgrade-database-diagrams-from-previous-editions-visual-database-tools.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-authorization-transact-sql)  
  
  
