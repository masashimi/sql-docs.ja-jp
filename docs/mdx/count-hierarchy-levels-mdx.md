---
title: Count (階層レベル) (MDX) |Microsoft ドキュメント
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 657ce658704b519c31dfaa2186429a7df4110308
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "34739541"
---
# <a name="count-hierarchy-levels-mdx"></a>Count (階層レベル) (MDX)


  階層内のレベル数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Hierarchy_Expression.Levels.Count  
```  
  
## <a name="arguments"></a>引数  
 *Hierarchy_Expression*  
 階層を返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>コメント  
 階層内のレベル数を返します。`[All]` レベルがある場合はこれも含みます。  
  
> [!IMPORTANT]  
>  表示可能な階層がディメンション内に 1 つしかない場合は、ディメンション名がその 1 つしかない階層に解決されるため、その階層はディメンション名でも階層名でも参照できます。 たとえば、`Measures.Levels.Count`有効な MDX 式は、Measures ディメンション内の唯一の階層に解決されるためです。  
  
## <a name="example"></a>例  
 次の例は、Adventure Works キューブ内のユーザー定義階層 Product Categories 内のレベル数を返します。  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Product Categories].Levels.Count   
Select Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [カウント&#40;ディメンション&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)   
 [カウント&#40;組&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [カウント&#40;設定&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [MDX 関数リファレンス&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
