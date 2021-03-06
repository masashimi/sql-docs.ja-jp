---
title: Folder 要素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Folder Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.folder
- http://schemas.microsoft.com/analysisservices/2003/engine#Folder
- urn:schemas-microsoft-com:xml-analysis#Folder
helpviewer_keywords:
- Folder element
ms.assetid: 87b305b0-57e3-4ec3-9d80-f1bcf3ce7540
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9bc961679619f15211689b4f118f511edbadac8c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37283918"
---
# <a name="folder-element-xmla"></a>Folder 要素 (XMLA)
  更新がファイル システム ストレージの場所が含まれています、[場所](location-element-xmla.md)中に要素を[復元](../xml-elements-commands/restore-element-xmla.md)または[同期](../xml-elements-commands/synchronize-element-xmla.md)コマンド。  
  
## <a name="syntax"></a>構文  
  
```xml  
  
<Folders>  
   ...  
   <Folder>  
      <Original>...</Original>  
      <New>...</New>  
   </Folder>  
   ...  
</Folders>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|説明|  
|--------------------|-----------------|  
|データ型と長さ|なし|  
|既定値|なし|  
|Cardinality|0-n : 省略可能な要素で、出現する場合は複数回の出現が可能です|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|-------------|  
|親要素|[フォルダー](folders-element-xmla.md)|  
|子要素|[新しい](new-element-xmla.md)、[元](original-element-xmla.md)|  
  
## <a name="remarks"></a>コメント  
 `Folder` 要素が指定されている場合、`Restore` 要素の値に一致するバックアップ ファイル (`Synchronize` コマンドの場合) またはソース インスタンス上のデータベース (`Original` コマンドの場合) に含まれるオブジェクトの格納場所が、`New` 要素の値に変更されます。  
  
 バックアップと復元のオブジェクトの詳細については、次を参照してください。[データベースのバックアップ、復元、およびデータベースの同期&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)します。  
  
## <a name="see-also"></a>参照  
 [StorageLocation 要素&#40;ASSL&#41;](../../scripting/properties/storagelocation-element-assl.md)   
 [プロパティ&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
