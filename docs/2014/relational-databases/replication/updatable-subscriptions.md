---
title: '[更新可能なサブスクリプション] | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.updatablesubscriptions.f1
ms.assetid: 8e9a13a0-6b24-47c6-9d83-3cbaf08f673d
caps.latest.revision: 21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 05dec7535b1614aeaa34ce06099c16a3df66a146
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37195002"
---
# <a name="updatable-subscriptions"></a>[更新可能なサブスクリプション]
  トランザクション レプリケーションの場合、レプリケートされたデータは読み取り専用として扱う必要がありますが、更新可能なサブスクリプションを使用することにより、レプリケートされたデータを [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブスクライバーで変更できます。 サブスクライバーでデータを変更する必要がある場合は、要件に応じて次のいずれかのオプションを選択してください。  
  
|更新可能なサブスクリプション タイプ|要件|  
|---------------------------------|------------------|  
|即時更新|サブスクライバーのデータを更新するために、パブリッシャーとサブスクライバーを接続します。|  
|キュー更新|サブスクライバーのデータを更新するために、パブリッシャーとサブスクライバーを接続する必要はありません。 更新をオフラインで実行し、後からパブリッシャーとサブスクライバーの間で同期させることができます。|  
  
## <a name="options"></a>および  
 **[以下のサブスクライバーの変更内容をレプリケートします]**  
 更新可能にする必要のある各サブスクライバーの **[レプリケート]** 列のチェック ボックスをオンにします。 これらの更新可能なサブスクライバーに対して、 **[パブリッシャーでのコミット]** 列のドロップダウン リスト ボックスから適切なオプションを選択します。  
  
-   即時更新サブスクリプションに対して **[変更を同時にコミットする]** を選択します。  
  
-   キュー更新サブスクリプションに対して **[変更をキューに登録し、可能な場合はコミット]** を選択します。  
  
## <a name="see-also"></a>参照  
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [Create a Push Subscription](create-a-push-subscription.md)   
 [Subscribe to Publications](subscribe-to-publications.md)   
 [Updatable Subscriptions for Transactional Replication](transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
