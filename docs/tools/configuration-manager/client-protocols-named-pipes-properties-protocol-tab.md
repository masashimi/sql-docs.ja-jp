---
title: クライアント プロトコル - [名前付きパイプのプロパティ] ダイアログ ボックス ([プロトコル] タブ) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- pipes [SQL Server], connecting to
- Named Pipes [SQL Server], default pipe
- client protocols [SQL Server]
ms.assetid: 30fbae62-2f2e-4d36-9c6e-3444fff68781
caps.latest.revision: 23
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: fa9108c526fc957a77938200a881535cf2afafa9
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2018
ms.locfileid: "42786517"
---
# <a name="client-protocols---named-pipes-properties-protocol-tab"></a>クライアント プロトコル - [名前付きパイプのプロパティ] ダイアログ ボックス ([プロトコル] タブ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーでは、 **[名前付きパイプのプロパティ]** ダイアログ ボックスの **[プロトコル]** タブを使用して、既定のパイプに関する説明の表示や変更を行います。 別のパイプに接続するには、そのパイプを **[既定のパイプ]** ボックスに入力してください。 接続文字列の詳細については、「 [Creating a Valid Connection String Using Named Pipes](http://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)」を参照してください。  
  
## <a name="options"></a>[変数]  
 **[既定のパイプ]**  
 名前付きパイプ Net-Library が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の対象インスタンスに接続するために使用する既定のパイプを指定します。 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は `\\.\pipe\sql\query`  
  
 既定のパイプに接続するには、 `sql\query`  
  
 **有効**  
 指定できる値は **[はい]** か **[いいえ]** のいずれかです。  
  
## <a name="see-also"></a>参照  
 [ネットワーク プロトコルの選択](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)  
  
  
