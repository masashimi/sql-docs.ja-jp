---
title: SQL Server データベース警告の作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- database performance [SQL Server], alerts
- alerts [SQL Server], creating
- thresholds [SQL Server]
- database alerts [SQL Server]
- tuning databases [SQL Server], alerts
- monitoring performance [SQL Server], alerts
- monitoring server performance [SQL Server], alerts
- database monitoring [SQL Server], alerts
- server performance [SQL Server], alerts
ms.assetid: 0511136a-1b6b-4095-aa45-39e77b67aba2
caps.latest.revision: 21
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1dcbc89e580283335f0a969baa04322f38f7c71a
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2018
ms.locfileid: "43818298"
---
# <a name="create-a-sql-server-database-alert"></a>SQL Server データベース警告の作成
  システム モニターでは、システム モニターのカウンターがしきい値に達したときに発生する警告を作成できます。 警告が発せられると、システム モニターは、その警告状況を処理するために記述されたカスタム アプリケーションなどのアプリケーションを起動します。 たとえば、デッドロックの数が特定の値を超えたときに発生する警告を作成できます。  
  
 警告は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用して定義することもできます。 詳細については、「[警告](../../ssms/agent/alerts.md)」を参照してください。  
  
 システム モニターを使用した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース警告を設定する方法の詳細については、「[SQL Server データベースの警告のセットアップ &#40;Windows&#41;](../performance/set-up-a-sql-server-database-alert-windows.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [sp_add_alert &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql)  
  
  
