---
title: IsDefaultMeasure 要素 (XML) |Microsoft ドキュメント
ms.custom: ''
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 523cf3d7-9df0-4f9d-8486-9109de8d3cca
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3739cf8669385a6f60a5141f53566599da285569
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="isdefaultmeasure-element-xml"></a>IsDefaultMeasure 要素 (XML)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  このリレーションシップを他のテーブルまでナビゲートし、属性 DefaultMeasure を持っているメンバーをフェッチすることにより、このエンティティの既定のメジャーを取得できることを示します。  
  
## <a name="syntax"></a>構文  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <IsDefaultMeasure>...</IsDefaultMeasure>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|説明|  
|--------------------|-----------------|  
|データ型と長さ|ブール値|  
|既定値|オプション|  
|Cardinality|0-1 : 省略可能な要素で、出現する場合は 1 回だけ出現します|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|-------------|  
|親要素|[RelationshipEndVisualizationProperties](../../../analysis-services/scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|子要素|なし|  
  
## <a name="remarks"></a>解説  
 **RelationshipEndVisualizationProperties** 、要素、 **IsDefaultMeasure**要素は、のもう一方の端に移動して、このエンティティの既定のメジャーを取得することであることを示しますこのリレーションシップです。 既定値の**false**取得される既定のメジャーがないことを示します。  
  
  