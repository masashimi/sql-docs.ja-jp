---
title: SQL Server フェールオーバー クラスターでのレポート サーバー データベースのホスト | Microsoft Docs
ms.date: 03/30/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: 7bd5f019-2857-452f-a023-cc3b9e93aec4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 21d0a7867e5a9d85fc36a9e305de77b00c9f5b95
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2018
ms.locfileid: "43266220"
---
# <a name="host-a-report-server-database-in-a-sql-server-failover-cluster"></a>SQL Server フェールオーバー クラスターでのレポート サーバー データベースのホスト
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対して複数のディスクを使用できるように、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、フェールオーバー クラスタリングをサポートしています。 フェールオーバー クラスタリングは、レポート サーバー データベースでのみサポートされています。つまり、フェールオーバー クラスターの一部としてレポート サーバー サービスを実行することはできません。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターでレポート サーバー データベースをホストするには、クラスターを事前にインストールして構成しておく必要があります。 その後、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールの [データベースのセットアップ] ページでレポート サーバー データベースを作成するときに、そのフェールオーバー クラスターをサーバー名として選択できます。  
  
 レポート サーバー サービスはフェールオーバー クラスターに参加できませんが、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] フェールオーバー クラスターをインストールしたコンピューターに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールできます。 レポート サーバーは、フェールオーバー クラスターとは別に実行されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー インスタンスの一部であるコンピューターにレポート サーバーをインストールした場合、レポート サーバー データベースにフェールオーバー クラスターを使用する必要はありません。別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを使用してデータベースをホストできます。  
  
## <a name="see-also"></a>参照  
 [レポート サーバー データベース &#40;SSRS ネイティブ モード&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
 [レポート サーバー データベースの作成 &#40;SSRS構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)  
  
  
