---
title: スナップショットの形式の指定 (SQL Server Management Studio) | Microsoft Docs
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
- snapshots [SQL Server replication], formats
- snapshot replication [SQL Server], formats
ms.assetid: 7c95f545-731a-4743-9acb-0b325ef9b98b
caps.latest.revision: 38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7038fa61c81248886c7f45d062f0ea4496d74fc9
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2018
ms.locfileid: "37358744"
---
# <a name="specify-snapshot-format-sql-server-management-studio"></a>スナップショットの形式の指定 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  スナップショットの形式は、**[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[スナップショット]** ページで指定します。 このダイアログ ボックスへのアクセス方法の詳細については、「[パブリケーション プロパティの表示および変更](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)」を参照してください。  
  
### <a name="to-specify-snapshot-format"></a>スナップショットの形式を指定するには  
  
1.  **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスの **[スナップショット]** ページで、**[ネイティブ SQL Server - サブスクライバーはすべて SQL Server を実行しているサーバーである必要があります]** または **[文字 - パブリッシャーまたはサブスクライバーで SQL Server が実行されていない場合は必須]** を選択します。  
  
    > [!NOTE]  
    >  このパブリケーションで [!INCLUDE[ssEW](../../../includes/ssew-md.md)] データベースまたは[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以外のデータベースへのサブスクリプションをサポートする必要がある場合を除き、ネイティブ形式を選択することをお勧めします。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [スナップショットのプロパティの構成 &#40;レプリケーション Transact-SQL プログラミング&#41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [パブリケーションとアーティクルのプロパティの変更](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [スナップショットを使用したサブスクリプションの初期化](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
