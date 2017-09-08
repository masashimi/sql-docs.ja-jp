---
title: "RelationshipEndVisualizationProperties データ型 (ASSL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 11f9a10f-d36c-4faf-b595-3fe969d1935e
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9627f9a245230f13030b87ae63df47ec920c271a
ms.contentlocale: ja-jp
ms.lasthandoff: 09/01/2017

---
# <a name="relationshipendvisualizationproperties-data-type-assl"></a>RelationshipEndVisualizationProperties データ型 (ASSL)
  リレーションシップのリレーションシップ End を表すプリミティブ データ型を定義します。  
  
## <a name="syntax"></a>構文  
  
```xml  
  
<RelationshipEnd>  
   <FolderPosition>...</FolderPosition>  
   <ContextualNameRule>...</ContextualNameRule>  
   <DefaultDetailsPosition>...</DefaultDetailsPosition>  
   <DisplayKeyPosition>...</DisplayKeyPosition>  
   <CommonIdentifierPosition>...</CommonIdentifierPosition>  
   <IsDefaultMeasure>...</IsDefaultMeasure>  
   <IsDefaultImage>...</IsDefaultImage>  
   <SortPropertiesPosition>...</SortPropertiesPosition>  
</RelationshipEnd>  
```  
  
## <a name="data-type-characteristics"></a>データ型の特性  
  
|特性|説明|  
|--------------------|-----------------|  
|基本データ型|なし|  
|派生データ型|なし|  
  
## <a name="data-type-relationships"></a>データ型のリレーションシップ  
  
|リレーションシップ|要素|  
|------------------|-------------|  
|親要素|[RelationshipEnd](../../../analysis-services/scripting/data-type/relationshipend-data-type-assl.md)|  
|子要素|[FolderPosition](../../../analysis-services/xmla/xml-elements-properties/folderposition-element-xml.md)、 [ContextualNameRule](../../../analysis-services/xmla/xml-elements-properties/contextualnamerule-element-xml.md)、 [DefaultDetailsPosition](../../../analysis-services/xmla/xml-elements-properties/defaultdetailsposition-element-xml.md)、 [DisplayKeyPosition](../../../analysis-services/xmla/xml-elements-properties/displaykeyposition-element-xml.md)、 [CommonIdentifierPosition](../../../analysis-services/xmla/xml-elements-properties/commonidentifierposition-element-xml.md)、 [IsDefaultMeasure](../../../analysis-services/xmla/xml-elements-properties/isdefaultmeasure-element-xml.md)、 [IsDefaultImage](../../../analysis-services/xmla/xml-elements-properties/isdefaultimage-element-xml.md)、 [SortPropertiesPosition](../../../analysis-services/xmla/xml-elements-properties/sortpropertiesposition-element-xml.md)|  
|派生要素||  
  
## <a name="remarks"></a>解説  
 分析管理オブジェクト (AMO) オブジェクト モデルで対応する要素は<xref:Microsoft.AnalysisServices.RelationshipEnd>します。  
  
  