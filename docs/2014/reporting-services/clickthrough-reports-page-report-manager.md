---
title: クリックスルー レポート ページ (レポート マネージャー) |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.modelproperties.drilthroughreports.f1
ms.assetid: e96cdeba-452b-45a8-9bcf-b75d76261e31
caps.latest.revision: 20
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 20c212e7829a04e1c6261a8818cebf7534d2529a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37244352"
---
# <a name="clickthrough-reports-page-report-manager"></a>[クリックスルー レポート] ページ (レポート マネージャー)
  クリックスルー レポートは、レポート内に含まれている対話的なデータをユーザーがクリックしたときに、関連するデータのテーブルを表示するレポートです。 これらのレポートは、レポートの作成に使用したモデルに含まれている情報に基づいて、レポート サーバーによって生成されます。 レポート サーバーによって生成されるクリックスルー レポートを使用しない場合は、カスタム レポートを作成し、レポート サーバーにパブリッシュして、そのモデルで定義されている対話的なデータ ポイントにマップすることができます。 カスタム レポートは、レポート ビルダーで同じモデルを使用して作成し、レポート サーバーにパブリッシュする必要があります。 カスタム レポートをモデル内のアイテムにマップするには、レポート マネージャーの [クリックスルー レポート] ページを使用します。  
  
 [クリックスルー レポート] ページには、定義済みのパブリッシュされたレポート ビルダーのレポートを、モデル内の特定のエンティティ、フォルダー、およびアイテムにマップする方法が用意されています。 レポートをモデル内の特定のアイテムにマップすると、そのアイテムに移動したユーザーは、レポート サーバーによって生成された一時レポートではなく、カスタム レポートを取得できます。  
  
 カスタム レポートを提供する場合、レポートの単一インスタンスおよび複数インスタンスの両方のバージョンを含める必要があります。 単一インスタンスまたは複数インスタンスのどちらのレポートが実行時にユーザーに表示されるかは、ユーザーが特定のエンティティに移動するために使用するデータ パスで決まります。 レポートのどちらかのバージョンが必要ないということを、事前に知ることができない場合があります。  
  
 エンティティにマップするカスタム レポートは、レポート サーバー フォルダー階層を通して安全性が確保されています。 モデル アイテムをレポートにマップした場合、そのレポートに移動したユーザーがレポートを使用できないときは、カスタム レポートではなく、レポート サーバーによって生成された一時レポートがそのユーザーに提供されます。  
  
 アクセス可能な任意のレポートを選択できますが、構成する対象のモデル用に作成されたレポートのみを選択してください。  
  
> [!NOTE]  
>  クリックスルー レポートはすべてのエディションで使用できません[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]します。 エディションでサポートされている機能の一覧については[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]を参照してください[機能は、SQL Server 2014 の各エディションでサポートされている](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)します。 組織で実行している [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のエディションが不明な場合は、データベース管理者に問い合わせてください。  
  
## <a name="navigation"></a>ナビゲーション  
 ユーザー インターフェイス (UI) のこの場所に移動するには、次の手順に従います。  
  
###### <a name="to-open-the-clickthrough-reports-page"></a>[クリックスルー レポート] ページを表示するには  
  
1.  レポート マネージャーを開き、クリックスルー レポートをエンティティにマップする対象のモデルを探します。  
  
2.  モデルの上にマウス ポインターを移動し、下矢印をクリックします。  
  
3.  ドロップダウン メニューの **[管理]** をクリックします。 この操作により、モデルの **[全般]** プロパティ ページが開きます。  
  
4.  **[クリックスルー]** タブをクリックします。  
  
## <a name="options"></a>および  
 **モデル アイテムの階層**  
 カスタマイズされたレポートを提供する、対象のモデル名前空間内のエンティティ、フォルダー、およびアイテムを表示します。  
  
 **単一インスタンス レポート**  
 ユーザーの移動によって単一インスタンス データのビューが必要な場合は、使用するカスタム レポートを指定します。 参照ボタンをクリックして、使用するレポートを選択します。  
  
 **複数インスタンスのレポート**  
 ユーザーの移動によって複数インスタンス データのビューが必要な場合は、使用するカスタム レポートを指定します。 参照ボタンをクリックして、使用するレポートを選択します。  
  
## <a name="see-also"></a>参照  
 [レポートのパブリッシュ](../../2014/reporting-services/publish-reports.md)  
  
  