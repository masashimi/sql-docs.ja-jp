---
title: '[SQL スクリプトの生成](レプリケーション オブジェクト) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.generatesqlscript.f1
helpviewer_keywords:
- Generate SQL Script dialog box
ms.assetid: b7ccc34e-1c22-44b8-8eb5-f6423af3164e
caps.latest.revision: 24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c8090f6d41acbcb48ef5c40eef273655cbb7fb41
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2018
ms.locfileid: "37358714"
---
# <a name="generate-sql-script-replication-objects"></a>[SQL スクリプトの生成](レプリケーション オブジェクト)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  レプリケーション スクリプトには、パブリケーションやサブスクリプションなど、スクリプト化されたレプリケーション コンポーネントを実装するために必要な [!INCLUDE[tsql](../../includes/tsql-md.md)] システム ストアド プロシージャが含まれます。 トポロジ内のすべてのレプリケーション コンポーンネントは、ディザスター リカバリー計画の一部としてスクリプト化され、スクリプトはタスクの繰り返しの自動化にも使用することができます。 レプリケーションでは、レプリケーション オブジェクトをスクリプト化するための次の 2 つのダイアログ ボックスが用意されています。  
  
-   **[SQL スクリプトの生成]** ダイアログ ボックスは、 **msCoName** の [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]フォルダーと、すべてのサブ フォルダーのショートカット メニューから利用可能です。 このダイアログ ボックスを使用して、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス上のすべてのレプリケーション オブジェクトのスクリプトを作成できます。  
  
-   **[SQL スクリプトの生成 \<ObjectName>]** ダイアログ ボックスは、パブリケーションおよびサブスクリプションのショートカット メニューから利用可能です。 このダイアログ ボックスを使用して、個々のオブジェクトのスクリプトを作成できます。  
  
 これらのダイアログ ボックスでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の単一のインスタンスにオブジェクトのスクリプトを作成します。ダイアログ ボックスは、他のインスタンスに接続して関連するオブジェクトのスクリプトを作成することはありません。  
  
## <a name="generate-sql-script-options"></a>[SQL スクリプトの生成] ダイアログ ボックスのオプション  
 **[ディストリビューターのプロパティ]**  
 ディストリビューターの有効化または無効化、ディストリビューターに関連付けられたパブリッシャーの追加または削除、およびディストリビューション データベースの作成または削除を行うため、ストアド プロシージャのスクリプトを作成します。  
  
 **[次のデータ ソースのパブリケーション]**  
 パブリッシュの有効化または無効化と、パブリケーション、アーティクル、プッシュ サブスクリプション、およびレプリケーション ジョブの作成または削除を行うため、ストアド プロシージャのスクリプトを作成します。  
  
 **[次のデータ ソース内のサブスクリプション]**  
 プル サブスクリプションとレプリケーション ジョブの作成または削除を行うため、ストアド プロシージャのスクリプトを作成します。  
  
 **[コンポーネントを作成または有効にする]** と **[コンポーネントを削除または無効にする]**  
 スクリプトにレプリケーション オブジェクトの作成または削除を行うコマンドを含めるかどうかを指定します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、コンポーネントの有効化と無効化を行うために、ダイアログ ボックスを使用してスクリプト セットを作成することを推奨します。  
  
 **[レプリケーション ジョブ]**  
 ストアド プロシージャの呼び出しに加えて、レプリケーション ジョブのスクリプトを作成します。 このオプションは、ディストリビューターからスクリプトを作成する場合にのみ利用可能です。  
  
 レプリケーション ストアド プロシージャは実行時に必要なジョブを作成します。そのため、このオプションを選択する必要はありません。 ただし、作成したジョブを記録しておくと、個々のジョブを再作成する必要が生じた場合に役に立ちます。  
  
## <a name="generate-sql-script-objectname-options"></a>[SQL スクリプトの生成 \<ObjectName>] ダイアログ ボックスのオプション  
 **[コンポーネントを作成または有効にする]** と **[コンポーネントを削除または無効にする]**  
 スクリプトにレプリケーション オブジェクトの作成または削除を行うコマンドを含めるかどうかを指定します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、コンポーネントの有効化と無効化を行うために、ダイアログ ボックスを使用してスクリプト セットを作成することを推奨します。  
  
 **[レプリケーション ジョブ]**  
 このオプションは、 **[SQL スクリプトの生成]** ダイアログ ボックスからのみ利用可能です。  
  
## <a name="see-also"></a>参照  
 [レプリケーションのスクリプト作成](../../relational-databases/replication/scripting-replication.md)  
  
  
