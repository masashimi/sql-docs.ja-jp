---
title: 共有データ ソース アイテムをセキュリティで保護する | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: security
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
- security [Reporting Services], data sources
ms.assetid: 7299e498-0a1a-4821-a22a-5199bb773ce0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5553797f786ae889d767d9f1cea3cde363466830
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2018
ms.locfileid: "43269182"
---
# <a name="secure-shared-data-source-items"></a>共有データ ソース アイテムをセキュリティで保護する
  共有データ ソース アイテムにセキュリティを設定して、そのアイテムへのアクセスを有効または無効にすることができます。  
  
 共有データ ソースにアクセスするための最低限の権限 (たとえば、 **閲覧者** ロールにより与えられる権限) を持っているユーザーは、レポート自体の表示を承認されていれば、アイテムを使用するレポートの一覧を表示できます。  
  
 それ以上の権限 (たとえば、 **コンテンツ マネージャー** ロールにより与えられる権限) を持つユーザーは、共有データ ソースのプロパティを表示および設定できます。  
  
 セキュリティを設定するには、共有データ ソースへのアクセス権を与えられたユーザー アカウントまたはグループ アカウントを指定するロールの割り当てを作成します。 共有データ ソース アイテムへのアクセス権を持つユーザーは、名前、説明、接続文字列、および資格情報を変更できます。  
  
## <a name="tasks-and-access-to-items"></a>タスクおよびアイテムへのアクセス  
 ロールの割り当てを作成するときに、以下のタスクを持つロールを使用して、ユーザーとグループに適切な権限を割り当てます。  
  
|使用するタスク|ユーザーに権限を与える操作|  
|----------------------|---------------------------------|  
|データ ソースの表示|フォルダー階層内の共有データ ソース アイテムを表示します。 このタスクがないと、アイテムがユーザーに表示されず、利用可能なデータ ソースをユーザーが認識できなくなる可能性があります。|  
|データ ソースの管理|名前、説明、および接続情報を表すプロパティを表示します。 このタスクは、フォルダー階層内の共有データ ソース アイテムの表示にも使用します。 このタスクを選択した場合は、"データ ソースの表示" タスクを省略できます。|  
|アイテムへのセキュリティの設定|共有データ ソースへのアクセスを制御するロールの割り当てを作成および変更します。 このタスクは、"データ ソースの表示" タスク、または "データ ソースの管理" タスクのいずれかと併用する必要があります。 それ以外の場合、ユーザーはアイテムを選択できないので効果がありません。|  
  
## <a name="see-also"></a>参照  
 [レポート データ ソースを管理する](../../reporting-services/report-data/manage-report-data-sources.md)   
 [フォルダーをセキュリティで保護する](../../reporting-services/security/secure-folders.md)   
 [レポートとリソースの保護](../../reporting-services/security/secure-reports-and-resources.md)   
 [ネイティブ モードのレポート サーバーに対する権限の許可](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Reporting Services データ ソースに資格情報を保存する](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
  
