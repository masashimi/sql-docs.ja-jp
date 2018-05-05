---
title: エイリアス要素 (ASSL) |Microsoft ドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Alias Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Alias
helpviewer_keywords:
- Alias element
ms.assetid: 674fdb06-e33c-4f35-bd6a-d9bbb13ececa
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 83b37bf4be8f9b59dba886db11862b895c34fd72
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="alias-element-assl"></a>Alias 要素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  別名を定義、[アカウント](../../../analysis-services/scripting/objects/account-element-assl.md)要素。  
  
## <a name="syntax"></a>構文  
  
```xml  
  
<Aliases>  
      <Alias>...</Alias>  
</Aliases>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|説明|  
|--------------------|-----------------|  
|データ型と長さ|文字列|  
|既定値|なし|  
|Cardinality|0-n : 省略可能な要素で、出現する場合は複数回の出現が可能です|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|-------------|  
|親要素|[エイリアス](../../../analysis-services/scripting/collections/aliases-element-assl.md)|  
|子要素|なし|  
  
## <a name="remarks"></a>解説  
 値、**エイリアス**要素がによって定義されたアカウントの代替名として使用される、**アカウント**親要素、およびユーザー アカウントの種類と集計関数の組み合わせを識別するために役立ちますインターフェイスです。  
  
 親に対応する要素、**エイリアス**分析管理オブジェクト (AMO) オブジェクト モデルのコレクションが<xref:Microsoft.AnalysisServices.Account>です。  
  
## <a name="see-also"></a>参照  
 [プロパティ & #40 です。ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  