---
title: SQL Server レプリケーションのインストール | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- components [SQL Server replication]
- command line installations [SQL Server replication]
- installing replication
- replication [SQL Server], installing
- command prompt [SQL Server replication]
ms.assetid: c50ad078-060b-4a8d-ad45-9e31a8d85729
caps.latest.revision: 41
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: c80d68173537d667573def56992bb1d9255490af
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2018
ms.locfileid: "40406521"
---
# <a name="install-sql-server-replication"></a>SQL Server レプリケーションのインストール

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

レプリケーション コンポーネントのインストールは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール ウィザードまたはコマンド プロンプトを使用して行うことができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をインストールする場合、または既存のインスタンスを変更する場合はレプリケーションをインストールします。  
  
レプリケーション コンポーネントのインストール後、レプリケーションを使用する前にサーバーを構成する必要があります。 詳細については、 [オンライン ブックの「](../../relational-databases/replication/configure-distribution.md) ディストリビューションの構成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 」を参照してください。  
  
>[!IMPORTANT]  
>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の既存のインスタンスを変更するときにレプリケーション コンポーネントをインストールする場合は、インストール完了後に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを停止して再起動する必要があります。 この操作により、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがレプリケーション エージェント サブシステムを認識し、ジョブ ステップからレプリケーション エージェントを呼び出すことができるようになります。  
  
## <a name="installing-replication-by-using-setup"></a>セットアップ プログラムによるレプリケーションのインストール  
**の新しいインスタンスをインストールするときにレプリケーションをインストールするには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
- レプリケーション管理オブジェクト (RMO) を含めてレプリケーション コンポーネントをインストールするには、インストール ウィザードの **[機能の選択]** ページで **[SQL Server レプリケーション]** を選択します。  
  
## <a name="installing-replication-from-the-command-prompt"></a>コマンド プロンプトによるレプリケーションのインストール  
 **の新しいインスタンスをインストールするときにレプリケーションをインストールするには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
- 「[コマンド プロンプトからの SQL Server のインストール](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server のインストール](../../database-engine/install-windows/install-sql-server.md)   
 [コマンド プロンプトからの SQL Server のインストール](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [SQL Server の各エディションでサポートされる機能](../../sql-server/editions-and-components-of-sql-server-2017.md)  
  
  
