---
title: サブスクライバーの種類 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.subscribertypes.f1
ms.assetid: a70656cb-21c9-4489-be77-ccd396747e3b
caps.latest.revision: 28
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d35f130d3a7ac5cdd13682ee431336c66eba2cc6
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43074232"
---
# <a name="subscriber-types"></a>サブスクライバーの種類
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  マージ レプリケーションを使用すると、パブリケーションがサポートする必要があるサブスクライバーの種類を指定することができます。 サブスクライバーの種類を選択することで、パブリケーションが使用できる機能を決定する *パブリケーションの互換性レベル*が設定されます。  
  
 パブリケーション スナップショットが作成された後は、パブリケーションの互換性レベルは、 **[パブリケーションのプロパティ]** ダイアログ ボックスの **[全般]** ページ上で高く (より制限) することができますが、互換性レベルを低くすることはできません。  
  
## <a name="options"></a>[変数]  
 このパブリケーションでサポートする必要がある各サブスクライバーの種類を選択します。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 パブリケーションはすべての機能を使用することができます。  
  
 [!INCLUDE[ssEW](../../includes/ssew-md.md)]  
 パブリケーションは、スナップショット ファイルが文字形式 (これは、スナップショット エージェントによって自動的に処理されます) である必要があります。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] には、互換性レベルとは別の制限事項もあります。  
  
 このオプションが選択されている場合、Web 同期オプションはこのパブリケーションで有効です。 Web 同期の詳細については、「 [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データとデータベース オブジェクトのパブリッシュ](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [View and Modify Distributor and Publisher Properties (ディストリビューターとパブリッシャーのプロパティの表示および変更)](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [プロパティ リファレンス &#40;レプリケーション&#41;](../../relational-databases/replication/properties-reference-replication.md)  
  
  
