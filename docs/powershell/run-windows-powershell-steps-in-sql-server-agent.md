---
title: SQL Server エージェントでの Windows PowerShell ステップの実行 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: scripting
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f25f7549-c9b3-4618-85f2-c9a08adbe0e3
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ce07cf1898291221f0c33111468d3f8e7187ce6c
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2018
ms.locfileid: "42775663"
---
# <a name="run-windows-powershell-steps-in-sql-server-agent"></a>SQL Server エージェントでの Windows PowerShell ステップの実行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

SQL Server エージェントを使用して、スケジュールされた時刻に SQL Server PowerShell スクリプトを実行します。  
  
**SQL Server エージェントから PowerShell を実行するには:**  [PowerShell ジョブ ステップ](#PShellJob)と [コマンド プロンプト ジョブ ステップ](#CmdExecJob)  
  
> [!NOTE]
> SQL Server PowerShell モジュールには **SqlServer** と **SQLPS** の 2 つがあります。 **SQLPS** モジュールは (後方互換性のため) SQL Server のインストールに含まれていますが、今後更新されることはありません。 最新の PowerShell モジュールは **SqlServer** モジュールです。 **SqlServer** モジュールには **SQLPS** のコマンドレットの更新バージョンだけでなく、最新の SQL 機能をサポートする新しいコマンドレットも含まれています。  
> SQL Server Management Studio (SSMS) には前のバージョンの **SqlServer** が含まれて*いました*が、SSMS の 16.x バージョンのみです。 PowerShell を SSMS 17.0 以降で使用するには、**SqlServer** モジュールを PowerShell ギャラリーからインストールする必要があります。
> **SqlServer** モジュールをインストールする場合は、「[SQL Server PowerShell のインストール](download-sql-server-ps-module.md)」を参照してください。


[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェントのジョブ ステップにはいくつかの種類があります。 それぞれの種類は、レプリケーション エージェントやコマンド プロンプト環境など、特定の環境を実装するサブシステムに関連付けられています。 Windows PowerShell スクリプトのコードを作成した後、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェントを使用して、スケジュールされた時刻に実行されるジョブや [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] イベントに応答して実行されるジョブにそのスクリプトを含めることができます。 コマンド プロンプト ジョブ ステップまたは PowerShell ジョブ ステップを使用して、Windows PowerShell スクリプトを実行できます。  
  
1.  PowerShell ジョブ ステップを使用して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェント サブシステムに **sqlps** ユーティリティを実行させます。このユーティリティは、PowerShell 2.0 を起動し、 **sqlps** モジュールをインポートします。  
  
2.  コマンド プロンプト ジョブ ステップを使用して PowerShell.exe を実行し、 **sqlps** モジュールをインポートするスクリプトを指定します。  
  
###  <a name="LimitationsRestrictions"></a> 制限事項と制約事項  
  
> [!CAUTION]  
>  **sqlps** モジュールで PowerShell を実行する [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェント ジョブ ステップでは、それぞれ、約 20 MB のメモリを消費するプロセスが起動されます。 大量の Windows PowerShell ジョブ ステップを同時実行すると、パフォーマンスに悪影響が及びます。  
  
##  <a name="PShellJob"></a> PowerShell ジョブ ステップの作成  
 **PowerShell ジョブ ステップを作成するには**  
  
1.  **[SQL Server エージェント]** を展開し、新しいジョブを作成するか、既存のジョブを右クリックして **[プロパティ]** をクリックします。 ジョブの作成に関する詳細については、「 [ジョブの作成](../ssms/agent/create-jobs.md)」を参照してください。  
  
2.  **[ジョブのプロパティ]** ダイアログで **[ステップ]** ページをクリックし、 **[新規作成]** をクリックします。  
  
3.  **[新しいジョブ ステップ]** ダイアログの **[ステップ名]** ボックスにジョブ ステップ名を入力します。  
  
4.  **[種類]** ボックスの一覧で **[PowerShell]** をクリックします。  
  
5.  **[実行するアカウント名]** ボックスの一覧で、ジョブで使用する資格情報を備えたプロキシ アカウントをクリックします。  
  
6.  **[コマンド]** ボックスに、ジョブ ステップで実行する PowerShell スクリプト構文を入力します。 または、 **[開く]** をクリックしてスクリプト構文が記述されたファイルを選択します。  
  
7.  **[詳細設定]** ページをクリックして、ジョブ ステップのオプションのうち、ジョブ ステップが成功または失敗した場合のアクション、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェントによるジョブ ステップの再試行回数、および再試行間隔を設定します。  
  
##  <a name="CmdExecJob"></a> コマンド プロンプト ジョブ ステップの作成  
 **CmdExec ジョブ ステップを作成するには**  
  
1.  **[SQL Server エージェント]** を展開し、新しいジョブを作成するか、既存のジョブを右クリックして **[プロパティ]** をクリックします。 ジョブの作成に関する詳細については、「 [ジョブの作成](../ssms/agent/create-jobs.md)」を参照してください。  
  
2.  **[ジョブのプロパティ]** ダイアログで **[ステップ]** ページをクリックし、 **[新規作成]** をクリックします。  
  
3.  **[新しいジョブ ステップ]** ダイアログの **[ステップ名]** ボックスにジョブ ステップ名を入力します。  
  
4.  **[種類]** ボックスの一覧の **[オペレーティング システム (CmdExec)]** をクリックします。  
  
5.  **[実行するアカウント名]** ボックスの一覧で、ジョブで使用する資格情報を備えたプロキシ アカウントをクリックします。 既定では、CmdExec ジョブ ステップは SQL Server エージェント サービス アカウントのコンテキストで実行されます。  
  
6.  **[コマンド成功時のプロセス終了コード]** ボックスに、0 ～ 999999 の値を入力します。  
  
7.  **[コマンド]** ボックスに、実行する PowerShell スクリプトを指定するパラメーターと共に powershell.exe を入力します。  
  
8.  **[詳細設定]** ページをクリックして、ジョブが成功または失敗した場合の操作、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェントによるジョブ ステップ実行の試行回数、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェントでジョブ ステップの出力を書き込むファイルなど、ジョブ ステップのオプションを設定します。 **sysadmin** 固定サーバー ロールのメンバーだけが、オペレーティング システム ファイルにジョブ ステップの出力を書き込むことができます。  
  
## <a name="see-also"></a>参照  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
