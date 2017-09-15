---
title: "ユーザー入力の検証 |Microsoft ドキュメント"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8aa867b0-e6f0-49eb-93d3-817ae2ed8f77
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9f46806c35bffcc9cacd77483f6a4cfe01153d5a
ms.contentlocale: ja-jp
ms.lasthandoff: 09/09/2017

---
# <a name="validating-user-input"></a>ユーザー入力の検証
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  データにアクセスするアプリケーションを作成する場合は、すべてのユーザー入力について、悪意がないと確認されるまでは、悪意があるものと見なす必要があります。 そうしないと、アプリケーションは攻撃に対して脆弱になる可能性があります。 発生する可能性がある攻撃の 1 つの型と呼ばれる SQL インジェクションのインスタンスに後で渡される文字列に悪意のあるコードを追加する場所[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]を解析して実行します。 この攻撃を防ぐには、パラメータを持つストアド プロシージャを可能な限り使用し、ユーザー入力を常に検証する必要があります。  
  
 サーバーへの無駄なラウンド トリップを行わないようにするには、ユーザー入力の検証をクライアント コードで行うことが重要です。 同様に、ストアド プロシージャへのパラメータをサーバー上で検証し、有効でない入力や、クライアント側の検証をバイパスする入力を検出することも重要です。  
  
 SQL インジェクションとその回避方法に関する詳細については、「SQL インジェクション」を参照してください[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]オンライン ブック。 ストアド プロシージャのパラメーターの検証の詳細については、次を参照してください。"ストアド プロシージャ ([!INCLUDE[ssDE](../../includes/ssde_md.md)])"と下位のトピックでは[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]オンライン ブック。  
  
## <a name="see-also"></a>参照  
 [JDBC ドライバー アプリケーションをセキュリティで保護します。](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  