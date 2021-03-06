---
title: 利用状況モニターを開く方法 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Activity Monitor [SQL Server], setting the refresh interval
- refresh interval for Activity Monitor
- Activity Monitor [SQL Server], opening
- opening Activity Monitor
ms.assetid: 0a6eeb16-f02b-479d-9a60-543e40ebf46b
caps.latest.revision: 33
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4c823440cb47f8c1a6d8a020856214291bdac5a3
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2018
ms.locfileid: "43809758"
---
# <a name="open-activity-monitor-sql-server-management-studio"></a>利用状況モニターを開く方法 (SQL Server Management Studio)
  このトピックでは、に関する情報を取得、利用状況モニターを開く方法を説明します。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]プロセスおよびこれらのプロセスの現在のインスタンスに与える影響[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 また、利用状況モニターの更新間隔の設定方法についても説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **使用して、利用状況モニターを開きます。**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
-   **更新間隔を設定する方法:**  [SQL Server Management Studio](#Refresh)  
  
##  <a name="BeforeYouBegin"></a> 作業を開始する準備  
 利用状況モニターでは、監視対象となるインスタンスでクエリを実行し、[利用状況モニター] 表示ペインに表示する情報を取得します。 更新間隔を 10 秒未満に設定すると、これらのクエリを実行する時間がサーバーのパフォーマンスに影響を与える可能性があります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 利用状況モニターを表示するには、VIEW SERVER STATE 権限が必要です。 利用状況モニターの [データ ファイル I/O] セクションを表示するには、VIEW SERVER STATE に加えて、CREATE DATABASE、ALTER ANY DATABASE、VIEW ANY DEFINITION のいずれかの権限が必要です。  
  
 プロセスを強制終了するには、sysadmin 固定サーバー ロールまたは processadmin 固定サーバー ロールのメンバーである必要があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-open-activity-monitor-in-sql-server-management-studio"></a>SQL Server Management Studio で利用状況モニターを開くには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]標準ツールバーで、をクリックして**の利用状況モニター**します。  
  
2.  **[サーバーへの接続]** ダイアログ ボックスで、サーバー名と認証モードを選択して **[接続]** をクリックします。  
  
 また、Ctrl キーと Alt キーを押しながら A キーを押すと、いつでも利用状況モニターを表示できます。  
  
#### <a name="to-open-activity-monitor-in-object-explorer"></a>オブジェクト エクスプローラーで利用状況モニターを開くには  
  
-   オブジェクト エクスプ ローラーで、インスタンス名を右クリックし、**の利用状況モニター**します。  
  
#### <a name="to-open-activity-monitor-when-opening-sql-server-management-studio"></a>SQL Server Management Studio を開くときに利用状況モニターを開くには  
  
1.  **[ツール]** メニューの **[オプション]** をクリックします。  
  
2.  **[オプション]** ダイアログ ボックスで **[環境]** を展開し、 **[全般]** をクリックします。  
  
3.  **[スタートアップ時]** ボックスで **[オブジェクト エクスプローラーと利用状況モニターを開く]** をクリックします。  
  
4.  変更を有効にするには、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を閉じて再度開きます。  
  
###  <a name="Refresh"></a> 利用状況モニターの更新間隔を設定するには  
  
-   利用状況モニターを開きます。  
  
-   **[概要]** を右クリックして **[更新間隔]** をクリックし、利用状況モニターで新しいインスタンス情報を取得する間隔を選択します。  
  
  
