---
title: Invocation 要素 (ASSL) |Microsoft ドキュメント
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a6bd0e8f75edf7562a85f670176eb11376900285
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2018
ms.locfileid: "34035703"
---
# <a name="invocation-element-assl"></a>Invocation 要素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  指定する方法、[アクション](../../../analysis-services/scripting/objects/action-element-assl.md)呼び出す必要があります。  
  
## <a name="syntax"></a>構文  
  
```xml  
  
<Action>  
   ...  
   <Invocation>...</Invocation>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|説明|  
|--------------------|-----------------|  
|データ型と長さ|String (列挙型)|  
|既定値|*対話型*|  
|Cardinality|0-1 : 省略可能な要素で、出現する場合は 1 回だけの出現が可能です|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|-------------|  
|親要素|[操作](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|子要素|なし|  
  
## <a name="remarks"></a>解説  
 アクションの起動は、クライアント アプリケーションに依存します。 **呼び出し**アクションの処理する必要がありのインスタンスに示されない要素をクライアント アプリケーションに提案[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]操作を呼び出す方法です。  
  
 この要素の値は、次の表のいずれかの文字列に制限されます。  
  
|値|説明|  
|-----------|-----------------|  
|*対話型*|ユーザーが対話形式で起動します。|  
|*OnOpen*|クライアント アプリケーションがオブジェクトを開いたときに起動します。|  
|*バッチ*|バッチ処理コマンドによって起動します。|  
  
 許可される値に対応する列挙**呼び出し**分析管理オブジェクト (AMO) オブジェクト モデルは<xref:Microsoft.AnalysisServices.Action>します。  
  
## <a name="see-also"></a>参照  
 [プロパティ & #40 です。ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
