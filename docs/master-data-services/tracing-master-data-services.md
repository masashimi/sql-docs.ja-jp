---
title: トレース (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 45823fc8-723a-49f2-9a11-94d241245cfd
caps.latest.revision: 7
author: leolimsft
ms.author: lle
manager: erikre
ms.openlocfilehash: d7c90b45352ff3afe78891c6849b04d69ab58175
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2018
ms.locfileid: "38984694"
---
# <a name="tracing-master-data-services"></a>トレース (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Web.config ファイルには、次のようにトレース セクションが含まれています。 これは、 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]  
  
```  
<sources>  
      <!-- Adjust the switch value to control the types of messages that should be logged.   
           http://msdn.microsoft.com/library/system.diagnostics.sourcelevels  
           Use the a switchValue of Verbose to generate a full log. Please be aware that   
           the trace file can get quite large very quickly -->  
      <source name="MDS" switchType="System.Diagnostics.SourceSwitch" switchValue="Warning, ActivityTracing">  
        <listeners>  
          <!-- Set a directory path where the service account you chose while setting up Master Data Services has read and write privileges.  
               Default path is Logs in WebApplication folder, for example C:\Program Files\Microsoft SQL Server\130\Master Data Services\WebApplication  
               New log file will be created every day or every 10 mb.  
               When directory size hits the 200mb limitation, the oldest file will be deleted.-->  
          <add name="FileTraceListener"  
               type="Microsoft.MasterDataServices.Core.Logging.FileTraceListener, Microsoft.MasterDataServices.Core"   
               initializeData="DirectoryPath = Logs; FileSizeInMb = 10; MaxDirectorySizeInMb = 200"/>  
          <remove name="Default"/>  
        </listeners>  
      </source>  
    </sources>  
  
```  
  
 既定のトレース動作を次に示します。  
  
-   トレースは、Warning メッセージと ActivityTracing メッセージに対して有効になっています。  
  
     詳細については、「 [SourceLevels 列挙体](https://msdn.microsoft.com/library/system.diagnostics.sourcelevels)」を参照してください。  
  
-   ログは、WebApplication フォルダーの下の Logs フォルダーに保存されます。 既定の場所は、C:\Program Files\Microsoft SQL Server\130\Master Data Services\WebApplication\Logs です。  
  
-   日ごと、または 10 MB に達するたびにファイルが作成されます。  
  
-   ディレクトリのサイズが 200 MB に達すると、最も古いログが削除されます。  
  
-   ログの形式は CSV です。 次の表に、ログの形式について説明します。  
  
    |要素|[説明]|  
    |-------------|-----------------|  
    |[時刻]|トレースのエントリが発生した時刻。|  
    |CorrelationID|要求ごとに 1 つの関連付け ID が割り当てられます。 この要求によってトリガーされるすべてのトレースは、同じ関連付け ID を共有します。<br /><br /> UI でエラーが発生すると、エラー メッセージに関連付け ID が表示されます。|  
    |演算|要求操作の名前。 要求が Web UI 要求の場合、URL が操作名になります。 要求が API 要求の場合、サービス名が操作名になります。|  
    |レベル|このトレース エントリのレベル。|  
    |メッセージ|トレースのメッセージ本文。|  
  
## <a name="external-resources"></a>外部リソース  
 msdn.com のブログ記事「 [Troubleshooting Logging Improvement (トラブルシューティングのためのログ記録の改善)](http://go.microsoft.com/fwlink/p/?LinkId=615377)」  
  
  
