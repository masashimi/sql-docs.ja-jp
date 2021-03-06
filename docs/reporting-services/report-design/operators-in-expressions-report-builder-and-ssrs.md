---
title: 式で使用される演算子 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: d22dc8b6-4353-40e7-91a1-65e8dae6325d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0a098567515f7f5884c787c288ea01b09bb34c06
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2018
ms.locfileid: "43266728"
---
# <a name="operators-in-expressions-report-builder-and-ssrs"></a>式で使用される演算子 (レポート ビルダーおよび SSRS)
  演算子は、式に含まれる 1 つ以上の項に適用される操作を表す記号です。 式でサポートされている演算子のカテゴリには、算術、比較、連結、論理 (ビット)、およびビット シフトがあります。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="arithmetic"></a>算術  
 算術演算子は、1 つの式に含まれる 2 つの項に対して数学的な操作を実行します。  
  
|演算子|[説明]|  
|--------------|-----------------|  
|^|一方の数値をもう一方の数値で累乗します。|  
|*|2 つの値を乗算します。|  
|/|2 つの数値の商を計算し、結果を浮動小数点で返します。|  
|\|2 つの数値の商を計算し、結果を整数で返します。|  
|Mod|除算による整数の剰余を返します。 たとえば、7 Mod 5 の場合、7 を 5 で割ると余りは 2 なので、7 Mod 5 = 2 となります。|  
|+|2 つの数値を加算します。|  
|-|2 つの数式の差を返すか、項が負の値であることを示します。|  
  
### <a name="comparison"></a>比較  
 比較演算子は、2 つの式が同じかどうかをテストします。  
  
|演算子|[説明]|  
|--------------|-----------------|  
|<|より小さい。|  
|\<=|以下。|  
|>|より大きい。|  
|>=|以上。|  
|=|等しい。|  
|<>|等しくない。|  
|Like|指定された文字列が指定されたパターンと一致するかどうかを判断します。 パターンは、標準の文字とワイルドカード文字を含むことができます。 パターン検索時に、標準の文字は文字列に指定された文字と正確に一致する必要があります。 しかし、ワイルドカード文字は文字列の任意の部分と一致することができます。 = や != などの文字列比較演算子を使用する場合と比べて、ワイルドカード文字を使用する方がより柔軟に LIKE 演算子を使用できます。<br /><br /> 次の表に、ワイルドカードとして使用できる文字を示します。<br /><br /> %: 0 個以上の文字で構成される任意の文字列です。<br /><br /> _: 任意の 1 文字です。<br /><br /> [ ]: 指定した範囲 (たとえば [a-f]) またはセット (たとえば [aeiou]) 内の任意の 1 文字です。<br /><br /> [^]: 指定した範囲 (たとえば [^a-f]) またはセット (たとえば [^aeiou]) 内にない任意の 1 文字です。|  
|Is|2 つのオブジェクト参照を比較します。|  
  
### <a name="string-concatenation"></a>文字列連結  
 文字列連結では、式に含まれる 2 番目の文字列が 1 番目の文字列の最後に追加されます。 その他の文字列操作では、組み込み関数を使用してください。  
  
|演算子|[説明]|  
|--------------|-----------------|  
|&|2 つの文字列を連結します。|  
|+|2 つの文字列を連結します。|  
  
### <a name="logical-and-bitwise"></a>論理演算子とビット演算子  
 論理演算子およびビット演算子は、式に含まれる 2 つの整数項の間の論理操作を実行します。  
  
|演算子|[説明]|  
|--------------|-----------------|  
|And|2 つのブール式の場合は論理積、2 つの数値式の場合はビットごとの積を求めます。|  
|Not|ブール式の場合は論理否定、数値式の場合はビットごとの否定を求めます。|  
|スイッチまたは|2 つのブール式の場合は論理和、2 つの数値の場合はビットごとの和を求めます。|  
|Xor|2 つのブール式の場合は排他的論理演算、2 つの数値式の場合はビットごとの排他を求めます。|  
|AndAlso|2 つの式の論理積を求めます。|  
|OrElse|2 つの式の論理和を求めます。|  
  
### <a name="bit-shift"></a>ビット シフト  
 ビットごとの演算子は、式に含まれる 2 つの整数項の間のビット操作を実行します。  
  
|演算子|[説明]|  
|--------------|-----------------|  
|<\<|ビット パターン上で算術左シフトを実行します。|  
|>>|ビット パターン上で算術右シフトを実行します。|  
  
## <a name="see-also"></a>参照  
 [[式] ダイアログ ボックス](http://msdn.microsoft.com/library/e6c74ccb-4594-4d4f-b958-618d710e34eb)   
 [式 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [式の例 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [式で使用されるデータ型 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [[式] ダイアログ ボックス &#40;レポート ビルダー&#41;](http://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)  
  
  
