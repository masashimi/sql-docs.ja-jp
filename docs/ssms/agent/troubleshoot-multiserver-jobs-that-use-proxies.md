---
title: プロキシを使用するマルチサーバー ジョブのトラブルシューティング | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- proxies [SQL Server Agent], multiserver jobs
- jobs [SQL Server Agent], multiserver jobs using proxies
ms.assetid: fc579bd3-010c-4f72-8b5c-d0cc18a1f280
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5a08b1c5d3685a4d4193cc7f7b40b59af27ef878
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2018
ms.locfileid: "42774432"
---
# <a name="troubleshoot-multiserver-jobs-that-use-proxies"></a>プロキシを使用するマルチサーバー ジョブのトラブルシューティング
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

プロキシに関連付けられているステップを持つ分散ジョブは、対象サーバーのプロキシ アカウントのコンテキストで実行されます。 プロキシ アカウントを使用するジョブ ステップをマスター サーバーからダウンロードする際、それらのジョブ ステップにエラーが発生した場合は、 **msdb** データベースの **sysdownloadlist** テーブルにある **error_message** 列に次のエラー メッセージが出力されていないか確認してください。  
  
-   "ジョブ ステップではプロキシ アカウントが必要ですが、対象サーバーで一致するプロキシが無効です。"  
  
    このエラーを解決するには、**\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL.***\<n*>** \SQLServerAgent\AllowDownloadedJobsToMatchProxyName** レジストリ サブキーを **1 (true)** に設定します。 既定では、このサブキーは **0** (**false**) に設定されます。 **MSSQL.**\<*n*> の値はインスタンス名です (例: **MSSQL.1**、**MSSQL.3**)。  
  
-   "プロキシ アカウントが見つかりませんでした。"  
  
    このエラーを解決するには、対象サーバー上にプロキシ アカウントが存在し、ジョブ ステップを実行するマスター サーバー プロキシ アカウントと同じ名前が付けられているかどうかを確認します。  
  
> [!CAUTION]  
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
## <a name="see-also"></a>参照  
[マルチサーバー環境の作成](../../ssms/agent/create-a-multiserver-environment.md)  
  
