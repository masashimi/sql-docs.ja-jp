---
title: クライアントが使用するサーバーの別名の作成または削除 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- server alias
helpviewer_keywords:
- aliases [SQL Server], deleting
- aliases [SQL Server], creating
ms.assetid: b687e376-ee33-470d-b65a-87246bfefe6f
caps.latest.revision: 26
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b8bd808902d6f479606aecc2ba6eb601d5464748
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32864537"
---
# <a name="create-or-delete-a-server-alias-for-use-by-a-client"></a>クライアントが使用するサーバーの別名の作成または削除
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で SQL Server 構成マネージャーを使用して、サーバー別名を作成または削除する方法について説明します。 別名は、接続のために使用できる代替名です。 別名は、接続文字列の必須要素をカプセル化したものであり、ユーザーが選択した名前でそれらの要素を公開できます。 別名は、任意のクライアント アプリケーションで使用できます。 サーバーの別名を作成すると、クライアント コンピューターはさまざまなネットワーク プロトコルを使用して複数のサーバーに接続できます。プロトコルおよび接続の詳細をそれぞれ指定する必要はありません。 また、さまざまなネットワーク プロトコルを、たとえ頻繁に使用する必要がないプロトコルであっても常に有効にしておくことができます。 既定以外のポート番号または名前付きパイプで受信するようにサーバーを構成し、SQL Server Browser サービスを無効にした場合は、新しいポート番号または名前付きパイプを指定する別名を作成してください。  
  
##  <a name="SSMSProcedure"></a> SQL Server 構成マネージャーの使用  
  
#### <a name="to-create-an-alias"></a>別名を作成するには  
  
1.  SQL Server 構成マネージャーで、 **[SQL Server Native Client の構成]** を展開し、 **[別名]** を右クリックして、 **[新しい別名]** をクリックします。  
  
2.  **[別名]** ボックスに別名を入力します。 クライアント アプリケーションは、接続時にこの名前を使用します。  
  
3.  **[サーバー]** ボックスに、サーバーの名前または IP アドレスを入力します。 名前付きインスタンスの場合は、インスタンス名を追加します。  
  
4.  **[プロトコル]** ボックスで、この別名に使用されるプロトコルを選択します。 プロトコルを選択すると、オプション プロパティ ボックスのタイトルが、[ポート番号]、[パイプ名]、または [接続文字列] に変わります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーのヘルプに記載されている接続文字列は、独自の接続文字列を作成するプログラマにとって役立つことがあります。 この情報にアクセスするには、 **[新しい別名]** ダイアログ ボックスで、F1 キーを押するか、 **[ヘルプ]** をクリックします。  
  
> [!NOTE]  
>  構成されている別名で間違ったサーバーやインスタンスに接続する場合は、関連付けられているネットワーク プロトコルを無効にし、次にこれを再び有効にします。 これによりキャッシュされた接続情報がクリアされ、クライアントに正しく接続できます。  
  
#### <a name="to-delete-an-alias"></a>別名を削除するには  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーで、 **[SQL Server Native Client の構成]** を展開し、 **[別名]** をクリックします。  
  
2.  詳細ペインで、削除する別名を右クリックし、 **[削除]** をクリックします。  
  
  
