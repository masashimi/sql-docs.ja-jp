---
title: オブジェクトからのポリシー ベースの管理ポリシーの評価 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: b9e9d646-4894-4dee-a02a-0c71a8dc020e
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5db720bfb03e2b210bd0f5887340552f5218db38
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2018
ms.locfileid: "43812018"
---
# <a name="evaluate-a-policy-based-management-policy-from-an-object"></a>オブジェクトからのポリシー ベースの管理ポリシーの評価
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でサーバー インスタンス、データベース、またはデータベース オブジェクトからポリシーを評価する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **以下を使用してオブジェクトからポリシーを評価するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 作業を開始する準備  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   実行モードは、ポリシーの一部として定義されており、 **[ポリシーの評価]** ダイアログ ボックスで変更することはできません。  
  
-   **[ポリシーの評価]** ダイアログ ボックスには、データベース オブジェクトに適したポリシーのみが表示されます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-evaluate-a-policy-from-an-object"></a>オブジェクトからポリシーを評価するには  
  
1.  オブジェクト エクスプローラーで、サーバー インスタンス、データベース、またはデータベース オブジェクトを右クリックし、 **[ポリシー]** をポイントして、 **[評価]** をクリックします。  
  
2.  **[ポリシーの評価]** ダイアログ ボックスで、1 つ以上のポリシーを選択し、 **[評価]** をクリックしてポリシーを評価モードで実行します。 これにより対象セットの準拠レポートが生成されますが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が再構成されたり、今後の準拠が適用されたりすることはありません。 選択したポリシーに準拠せず、ポリシー ベースの管理で再構成可能なプロパティを持つ対象の場合は、 **[適用]** をクリックしてポリシーへの準拠を適用できます。 **[ポリシーの評価]** ダイアログ ボックスで使用可能なオプションの詳細については、「 [Evaluate Policies Dialog Box, Policy Selection Page](evaluate-policies-dialog-box-policy-selection-page.md)」、「 [Evaluate Policies Dialog Box, Evaluation Results Page](evaluate-policies-dialog-box-evaluation-results-page.md)」、および「 [Results Detailed View Dialog Box](results-detailed-view-dialog-box.md)」を参照してください。  
  
3.  完了したら、 **[閉じる]** をクリックします。  
  
  
