---
title: データベース ファイルの移動 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], moving database files
- files [SQL Server], moving
- data files [SQL Server], moving
- file moving [SQL Server]
- moving full-text catalogs
- moving databases
- full-text catalogs [SQL Server], moving
- moving database files
- scheduled disk maintenance [SQL Server]
- moving files
- relocating database files
- planned database relocations [SQL Server]
- databases [SQL Server], moving
ms.assetid: 89f01b10-5fae-4ed8-b0fb-a4b9f540fd28
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a92b002e6590903ae90f584e7b87d565df7272fe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32925017"
---
# <a name="move-database-files"></a>データベース ファイルの移動
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) ステートメントの FILENAME 句で新しいファイルの場所を指定して、システムおよびユーザー データベースを移動することができます。 データ ファイル、ログ ファイル、およびフルテキスト カタログ ファイルもこの方法で移動できます。 データベース ファイルの移動は、次の状況で便利な場合があります。  
  
-   障害復旧。 たとえば、ハードウェア障害により、データベースが問題のあるモードになっている場合や、シャットダウンされた場合など。  
  
-   計画に従った再配置。  
  
-   スケジュールされたディスク メンテナンスとしての再配置。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|Description|  
|-----------|-----------------|  
|[ユーザー データベースの移動](../../relational-databases/databases/move-user-databases.md)|ユーザー データベース ファイルおよびフルテキスト カタログ ファイルを新しい場所に移動する手順について説明します。|  
|[システム データベースの移動](../../relational-databases/databases/move-system-databases.md)|システム データベース ファイルを新しい場所に移動する手順について説明します。|  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [データベースのデタッチとアタッチ &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  
