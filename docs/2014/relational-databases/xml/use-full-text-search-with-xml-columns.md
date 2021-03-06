---
title: XML 列でのフルテキスト検索の使用 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- xml columns [full-text search]
- indexes [full-text search]
ms.assetid: 8096cfc6-1836-4ed5-a769-a5d63b137171
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 54bf7f5993962bb885d16a513cf34c49bda0de0a
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2018
ms.locfileid: "43888568"
---
# <a name="use-full-text-search-with-xml-columns"></a>XML 列でのフルテキスト検索の使用
  XML 列にフルテキスト インデックスを作成して XML 値のコンテンツにインデックスを設定できますが、XML マークアップは無視されます。 要素タグはトークンの境界として使用されます。 インデックスは次の項目に設定されます。  
  
-   XML 要素のコンテンツ。  
  
-   最上位レベルの要素の XML 属性のコンテンツ (属性値が数値でない場合)。  
  
 可能であれば、次のようにしてフルテキスト検索と XML インデックスを組み合わせることができます。  
  
1.  まず、SQL フルテキスト検索を使用して、対象の XML 値をフィルター処理します。  
  
2.  次に、XML 列の XML インデックスを使用する XML 値にクエリを実行します。  
  
## <a name="example-combining-full-text-search-with-xml-querying"></a>例 : フルテキスト検索と XML クエリの組み合わせ  
 XML 列でフルテキスト インデックスを作成した後、XML 値が書名に語 "custom" を含んでいることを次のクエリで確認します。  
  
```  
SELECT *   
FROM   T   
WHERE  CONTAINS(xCol,'custom')   
AND    xCol.exist('/book/title/text()[contains(.,"custom")]') =1  
```  
  
 **contains()** メソッドによって、フルテキスト インデックスを使用してドキュメントのどこかに語 "custom" を含んでいる XML 値をサブセットとして取り出します。 **exist()** 句により、書名に語 "custom" が使用されていることを確認します。  
  
 **contains()** を使用するフルテキスト検索と XQuery **contains()** は意味が異なります。 前者はステミングによるトークンの照合で、後者は部分文字列の照合です。 したがって、書名に "run" が使用されている文字列を検索する場合、フルテキストの **contains()** と XQuery の **contains()** をいずれも満たす "run"、"runs"、および "running" が検出されます。 ただし、この例のクエリでは語 "customizable" が書名に使用されていても、XQuery の **contains()** は満たしますがフルテキストの **contains()** で失敗するので検出されません。 一般に純粋な部分文字列の検索を行うには、フルテキストの **contains()** 句を削除する必要があります。  
  
 さらに、フルテキスト検索ではステマーが使用されますが、XQuery の **contains()** はリテラルの照合です。 両者の違いを次の例で示します。  
  
## <a name="example-full-text-search-on-xml-values-using-stemming"></a>例 : ステミングを使用した XML 値のフルテキスト検索  
 上記の例で行った XQuery **contains()** による確認は、通常は省略できません。 次のクエリについて考えてみます。  
  
```  
SELECT *   
FROM   T   
WHERE  CONTAINS(xCol,'run')   
```  
  
 ドキュメント内で語 "ran" が使用されていると、ステミングによりこの検索条件に一致します。 XQuery では検索コンテキストは確認されません。  
  
 フルテキスト インデックスが作成されたリレーショナル列に AXSD を使用して XML を分解した場合、XML ビューに XPath クエリを実行しても基になるテーブルのフルテキスト検索は行われません。  
  
## <a name="see-also"></a>参照  
 [XML インデックス &#40;SQL Server&#41;](xml-indexes-sql-server.md)  
  
  
