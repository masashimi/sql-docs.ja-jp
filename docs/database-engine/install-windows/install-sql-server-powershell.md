---
title: SQL Server PowerShell のインストール | Microsoft Docs
ms.custom: ''
ms.date: 09/05/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 854c0b2f-02d2-46a4-a8cc-6b7a5d191cf8
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: da469052df30187baf290965e0a76fda48ae8cc7
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2018
ms.locfileid: "40410379"
---
# <a name="install-sql-server-powershell"></a>SQL Server PowerShell のインストール
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell のコンポーネントは、セットアップによって自動的に構成されます。  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを使用して、Windows PowerShell に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サポートを提供するソフトウェアをインストールします。 PowerShell サポートを必要とする任意の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能を選択すると、セットアップにより次の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell コンポーネントがインストールされます。  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell スナップイン。スナップインは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用の以下の 2 種類の Windows PowerShell サポートを実装する dll ファイルです。  
  
  - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コマンドレットのセット。 コマンドレットは特定の操作を実装するコマンドです。 たとえば、 **Invoke-Sqlcmd** では、 [!INCLUDE[tsql](../../includes/tsql-md.md)] sqlcmd **ユーティリティを使用して実行することもできる** スクリプトまたは XQuery スクリプトが実行され、 **Invoke-PolicyEvaluation** では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトがポリシー ベースの管理ポリシーに準拠しているかどうかが報告されます。  
  
  - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロバイダー。 プロバイダーでは、ファイル システム パスと同様のパスを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの階層内を移動できます。 各オブジェクトは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理オブジェクト モデルのクラスに関連付けられています。 クラスのメソッドやプロパティを使用して、オブジェクトの操作を実行できます。 たとえば、パスでデータベース オブジェクトに移動した場合、Microsoft.SqlServer.Managment.SMO.Database クラスのメソッドとプロパティを使用してデータベースを管理できます。  
 
- **のスナップインを読み込むために Windows PowerShell のセッションにインポートされる** sqlps [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] モジュール。  
 
- [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、オブジェクト エクスプローラー ツリーからの Windows PowerShell セッションの起動をサポートします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、Windows PowerShell ジョブ ステップをサポートします。  
  
Windows Server 2012 以降と Windows 8 以降には、PowerShell がインストールされ構成されています。 Windows PowerShell のインストールの詳細については、「[Windows PowerShell のインストール](http://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell)」を参照してください。  

詳細については、以下をご覧ください。   

- [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
