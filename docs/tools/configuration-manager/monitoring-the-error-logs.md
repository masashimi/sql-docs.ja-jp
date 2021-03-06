---
title: エラー ログの監視 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server]
- database performance [SQL Server], errors
- Windows application logs [SQL Server]
- monitoring performance [SQL Server], errors
- server performance [SQL Server], errors
- comparing error and application log output
- errors [SQL Server], logs
- tuning databases [SQL Server], errors
- database monitoring [SQL Server], errors
- SQL Server error log
- logs [SQL Server], SQL Server error logs
- error logs [SQL Server]
- logs [SQL Server], Windows application logs
ms.assetid: e250336b-0695-44f6-a42f-23222f94e377
caps.latest.revision: 23
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: 5e4449d8e8bc1006833d79c914a1208528a08893
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2018
ms.locfileid: "42785207"
---
# <a name="monitoring-the-error-logs"></a>エラー ログの監視
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、特定のシステム イベントとユーザー定義イベントを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログと [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アプリケーション ログに記録します。 両方のログで、記録されるすべてのイベントのタイムスタンプが自動的に記録されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログの情報を使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に関連する問題のトラブルシューティングを行うことができます。  
  
 Windows アプリケーション ログでは、Windows オペレーティング システムで発生したイベントと、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] や [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントでのイベントの全体像が示されます。 Windows イベント ビューアーを使用すると、Windows アプリケーション ログを表示して情報をフィルター処理できます。 たとえば、情報、警告、エラー、および成功または失敗の監査などのイベントをフィルター処理できます。  
  
## <a name="comparing-error-and-application-log-output"></a>エラー ログとアプリケーション ログの出力の比較  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログと Windows アプリケーション ログの両方を使用して、問題の原因を特定できます。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログの監視中、原因に関する情報が含まれていないエラー メッセージが表示される場合があります。 これらのログの間でイベントの日付と時刻を比較することにより、可能性のある原因の範囲を絞り込むことができます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ログ ファイル ビューアーにより、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント、および Windows ログが 1 つの一覧に統合され、関連するサーバー イベントや [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] イベントの把握が容易になります。 詳細については、SQL Server オンライン ブックの「[ログ ファイルの表示]」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|[説明]|  
|-----------|-----------------|  
|[SQL Server エラー ログの表示](../../tools/configuration-manager/viewing-the-sql-server-error-log.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログとその表示方法について説明します。|  
|[Windows アプリケーション ログの表示](../../tools/configuration-manager/viewing-the-windows-application-log.md)|Windows アプリケーション ログとその表示方法について説明します。|  
  
  
