---
title: 権限借用情報 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 42319d60-ccd0-46b8-af0b-f0968c390d8a
caps.latest.revision: 9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1a0f2b5914c31c3cacce4bfb8887ebde73e0d932
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37181019"
---
# <a name="impersonation-information"></a>[権限借用情報]
  **[権限借用情報]** ページを使用して、Analysis Services がデータ ソースに接続する際に使用される資格情報を指定します。  
  
## <a name="options"></a>および  
 **特定の Windows ユーザー名とパスワードを使用します。**  
 このオプションを選択すると、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] オブジェクトにより、指定の Windows ユーザー アカウントのセキュリティ資格情報が使用されます。 処理、ROLAP クエリ、不一致バインド、ローカル キューブ、マイニング モデル、リモート パーティション、リンク オブジェクト、ターゲットからソースへの同期に、指定した資格情報が使用されます。 ただし、データ マイニング拡張機能 (DMX) の OPENQUERY ステートメントについては、このオプションが無視され、現在のユーザーの資格情報が使用されます。  
  
 **ユーザー名**  
 選択した [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] オブジェクトで使用するユーザー アカウントのドメインと名前を入力します。 次の形式を使用します。  
  
 *\<ドメイン名 >* **\\** *\<ユーザー アカウント名 >*  
  
 このオプションは、 **[特定のユーザー名とパスワードを使用する]** がオンになっている場合にのみ有効になります。  
  
 **Password**  
 選択した [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] オブジェクトで使用するユーザー アカウントのパスワードを入力します。  
  
 このオプションは、 **[特定のユーザー名とパスワードを使用する]** がオンになっている場合にのみ有効になります。  
  
 **[サービス アカウントを使用する]**  
 このオプションを選択すると、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] オブジェクトを管理する [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] サービスに関連付けられているセキュリティ資格情報が使用されます。 処理、ROLAP クエリ、リモート パーティション、リンク オブジェクト、ターゲットからソースへの同期に、サービス アカウント資格情報が使用されます。 ただし、データ マイニング拡張機能 (DMX) の OPENQUERY ステートメントでは、ローカル キューブとマイニング モデルに現在のユーザーの資格情報が使用されます。 不一致バインドに対しては、このオプションはサポートされません。  
  
 **[現在のユーザーの資格情報を使用する]**  
 このオプションを選択すると、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] オブジェクトにより、不一致バインド、DMX OPENQUERY、ローカル キューブ、マイニング モデルに現在のユーザーのセキュリティ資格情報が使用されます。 処理、ROLAP クエリ、リモート パーティション、リンク オブジェクト、ターゲットからソースへの同期に対しては、このオプションはサポートされません。  
  
 **継承**  
 このオプションを選択すると、データベース レベルで定義されている権限借用の動作が使用されます。この動作は、サーバー管理者が `DataSourceImpersonation` データベース プロパティを使用して設定します。  
  
## <a name="see-also"></a>参照  
 [多次元モデルのデータ ソース](multidimensional-models/data-sources-in-multidimensional-models.md)   
 [サポートされるデータ ソース&#40;SSAS 多次元&#41;](multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  
