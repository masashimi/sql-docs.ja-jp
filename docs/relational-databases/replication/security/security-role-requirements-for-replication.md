---
title: レプリケーションのセキュリティ ロール要件 | Microsoft Docs
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
helpviewer_keywords:
- security [SQL Server replication], roles
- roles [SQL Server], replication
ms.assetid: b324a80f-4319-4cb2-847b-1910c49d90e0
caps.latest.revision: 35
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ba534e77e3a91e9b36ef54645b70497f5ff4de79
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2018
ms.locfileid: "37352774"
---
# <a name="security-role-requirements-for-replication"></a>レプリケーションのセキュリティ ロール要件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  レプリケーションでは、ユーザーのログインがマップされているロールに基づいて、ユーザーが実行できる操作が制限されます。 レプリケーションでは、 **sysadmin** 固定サーバー ロール、 **db_owner** 固定データベース ロール、およびパブリケーション アクセス リスト (PAL) 内のログインに、特定の権限が許可されています。  
  
## <a name="security-role-requirements-for-replication-setup"></a>レプリケーション セットアップのセキュリティ ロール要件  
 次の表に、一般的なレプリケーション セットアップ タスクに必要な認証レベルをまとめます。  
  
|セットアップ タスク|必要なメンバーシップ|  
|----------------|----------------------------|  
|ディストリビューター、パブリッシャー、またはサブスクライバーの有効化。|パブリッシャーの**sysadmin** サーバー ロール。|  
|レプリケーション用のデータベースの有効化。|パブリッシャーの**sysadmin** サーバー ロール。|  
|パブリケーションの作成。|パブリッシャーのパブリケーション データベースの**db_owner** データベース ロールまたはパブリッシャーの **sysadmin** サーバー ロール。|  
|パブリケーション プロパティの表示。|パブリッシャーの PAL のメンバー、パブリッシャーのパブリケーション データベースの **db_owner** データベース ロール、またはパブリッシャーの **sysadmin** サーバー ロール。|  
|サブスクリプションの作成。|パブリッシャーのパブリケーション データベースの**db_owner** データベース ロールまたはパブリッシャーの **sysadmin** サーバー ロール。<br /><br /> サブスクライバーのサブスクリプション データベースの**db_owner** データベース ロールまたはサブスクライバーの **sysadmin** サーバー ロール。|  
|エージェント プロファイルの構成。|ディストリビューターの**sysadmin** サーバー ロール。|  
  
## <a name="security-role-requirements-for-replication-maintenance"></a>レプリケーション メンテナンスのセキュリティ ロール要件  
 次の表に、一般的なレプリケーション メンテナンス タスクに必要な認証レベルをまとめます。  
  
|メンテナンス タスク|必要なメンバーシップ|  
|----------------------|----------------------------|  
|ディストリビューター、パブリッシャー、またはサブスクライバーの変更または削除。|該当するサーバーの**sysadmin** サーバー ロール。|  
|パブリケーションの変更または削除。|パブリッシャーのパブリケーション データベースの**db_owner** データベース ロールまたはパブリッシャーの **sysadmin** サーバー ロール。|  
|パブリッシャーでのサブスクリプションの変更または削除。|パブリッシャーのパブリケーション データベースの**db_owner** データベース ロールまたはパブリッシャーの **sysadmin** サーバー ロール。|  
|サブスクライバーでのサブスクリプションの変更または削除。|サブスクライバーのサブスクリプション データベースの**db_owner** データベース ロールまたはサブスクライバーの **sysadmin** サーバー ロール。|  
|サブスクリプションへの再初期化マークの設定。|プッシュ サブスクリプション : パブリッシャーのパブリケーション データベースの **db_owner** データベース ロールまたはパブリッシャーの **sysadmin** サーバー ロール。<br /><br /> プル サブスクリプション : サブスクライバーのサブスクリプション データベースの **db_owner** データベース ロールまたはサブスクライバーの **sysadmin** サーバー ロール。|  
|レプリケーション モニターを使用した、レプリケーションの利用状況、エラー、および履歴の表示。 **sysadmin** サーバー ロールのメンバーでないユーザーは、エージェントのプロファイル、スケジュールなどを変更できません。|ディストリビューターのディストリビューション データベースの**replmonitor** データベース ロールまたはディストリビューターの **sysadmin** サーバー ロール。|  
|レプリケーション エージェントのメンテナンス。|該当するデータベースの**db_owner** データベース ロールまたは該当するサーバーの **sysadmin** サーバー ロール。<br /><br /> エージェントが **sysadmin** ロールのユーザーによって作成され、そのエージェントに対してプロキシ アカウントが指定されていない場合、エージェントは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント アカウントのコンテキストで実行されます。 この場合、 **db_owner** ロールのユーザーは、エージェントに関連付けられているジョブを変更できません。|  
|レプリケーション エージェントの起動または停止。|エージェント ジョブの所有者または該当するサーバーの **sysadmin** サーバー ロール。|  
  
## <a name="see-also"></a>参照  
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [セキュリティと保護 &#40;レプリケーション&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
