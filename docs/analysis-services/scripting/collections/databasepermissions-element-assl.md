---
title: "DatabasePermissions 要素 (ASSL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DatabasePermissions Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DatabasePermissions
helpviewer_keywords:
- DatabasePermissions element
ms.assetid: c4ce0da3-f7ba-4f11-8cd8-236c32992aaf
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2fe4aeb00e4daed509e4a1d5daa24f65c7ac2b26
ms.contentlocale: ja-jp
ms.lasthandoff: 09/01/2017

---
# <a name="databasepermissions-element-assl"></a>DatabasePermissions 要素 (ASSL)
  コレクションを格納[DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md)要素に関連付けられた、[データベース](../../../analysis-services/scripting/objects/database-element-assl.md)要素。  
  
## <a name="syntax"></a>構文  
  
```xml  
  
<Database>  
   ...  
   <DatabasePermissions>  
      <DatabasePermission>...</DatabasePermission>  
      </DatabasePermissions>  
      ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|説明|  
|--------------------|-----------------|  
|データ型と長さ|なし|  
|既定値|なし|  
|Cardinality|0-1 : 省略可能な要素で、出現する場合は 1 回だけの出現が可能です|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|-------------|  
|親要素|[データベース](../../../analysis-services/scripting/objects/database-element-assl.md)|  
|子要素|[DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md)|  
  
## <a name="remarks"></a>解説  
 分析管理オブジェクト (AMO) オブジェクト モデルで対応する要素は<xref:Microsoft.AnalysisServices.DatabasePermissionCollection>します。  
  
## <a name="see-also"></a>参照  
 [Permission データ型 & #40 です。ASSL &#41;](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)   
 [コレクション & #40 です。ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  