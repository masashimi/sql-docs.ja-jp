---
title: rsModelGenerationError - Reporting Services エラー | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: troubleshooting
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- rsModelGenerationError
ms.assetid: 3a0ad63f-87f9-4ca1-b0c2-c85fa991634a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 47d9432f9a2032119a85e9fd70203ef132bc503d
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2018
ms.locfileid: "43265369"
---
# <a name="rsmodelgenerationerror---reporting-services-error"></a>rsModelGenerationError - Reporting Services エラー
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|rsRenderingError|  
|イベント ソース|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|コンポーネント|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|メッセージ テキスト|モデルの生成中にエラーが発生しました。 (rsModelGenerationError) (ReportingServicesLibrary) %1|  
  
## <a name="explanation"></a>説明  
 レポート モデルを生成できませんでした。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 SP1 以前のバージョンでは、このエラーは、System.Data.DataSet オブジェクトでデータベース スキーマ内のテーブルまたはリレーションシップを処理できない場合に表示される可能性があります。たとえば、1 つのテーブル内の同じ列に 2 つの外部キーが定義されている場合などです。  
  
## <a name="user-action"></a>ユーザーの操作  
 このメッセージが表示される原因となった具体的な理由を特定するには、\Microsoft SQL Server\\<SQL Server Instance\>\Reporting Services\LogFiles にあるレポート サーバーのログ ファイルを確認します。  
  
## <a name="internal-only"></a>内部使用のみ  
  
