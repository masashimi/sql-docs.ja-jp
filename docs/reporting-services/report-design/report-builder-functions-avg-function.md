---
title: Avg 関数 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: f1276c4c-bb44-44c0-a1bf-386a0c340003
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 857c0a7a5b7113adef4e43adcacc28b11f7e06f8
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2018
ms.locfileid: "43276544"
---
# <a name="report-builder-functions---avg-function"></a>レポート ビルダー関数 - Avg 関数
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のページ分割されたレポートでは、式で指定された NULL 以外のすべての数値の平均を、指定されたスコープで評価して返します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>構文  
  
```  
  
Avg(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *式 (expression)*  
 (**浮動小数点**) この集計関数の実行対象の式です。  
  
 *スコープ (scope)*  
 (**文字列**) 省略可。 集計関数の適用先となるレポート アイテムを含むデータセット、グループ、またはデータ領域の名前です。 *scope* を指定しない場合、現在のスコープが使用されます。  
  
 *再帰*  
 (**列挙型**) 省略可。 **Simple** (既定値) または **RdlRecursive**です。 集計を再帰的に実行するかどうかを指定します。  
  
## <a name="return-type"></a>戻り値の型  
 10 進数型の式には **Decimal** 値が、その他すべての式には **Double** 値が返されます。  
  
## <a name="remarks"></a>Remarks  
 式で指定されたデータセットは、同じデータ型である必要があります。 複数の数値データ型のデータを同じデータ型に変換するには、 **CInt**、 **CDbl** 、 **CDec**などの変換関数を使用します。 詳細については、「 [データ型変換関数](http://go.microsoft.com/fwlink/?LinkId=96142)」を参照してください。  
  
 *scope* の値は文字列定数である必要があり、式にすることはできません。 外部の集計または他の集計を指定しない集計では、 *scope* は現在のスコープまたはコンテナー スコープを参照する必要があります。 集計の集計では、入れ子になった集計に、子のスコープを指定できます。  
  
 *Expression* には、入れ子になった集計関数への呼び出しを含めることができます。ただし、次に示すように、これには例外および条件があります。  
  
-   入れ子集計の*Scope* は、外部集計のスコープと同じであるか、そのスコープに含まれている必要があります。 式内のすべてのスコープについては、1 つのスコープがそれ以外のすべてのスコープに対する子であるようなリレーションシップが必要です。  
  
-   入れ子集計の*Scope* には、データセット名は使用できません。  
  
-   *Expression* には、 **First**、 **Last**、 **Previous**、または **RunningValue** の各関数を含めることができません。  
  
-   *Expression* には、 *recursive*を指定する入れ子集計を含めることができません。  
  
 詳細については、「[集計関数リファレンス &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)」および「[合計、集計、および組み込みコレクションの式のスコープ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)」を参照してください。  
  
 再帰的集計については、「[複数の再帰型階層グループの作成 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の 2 つのコード例では、 `Cost` という名前のデータセットに含まれる `Inventory`フィールド内のすべての値の平均が返されます。  
  
```  
=Avg(Fields!Cost.Value, "Inventory")   
  OR    
=Avg (CDbl(Fields!Cost.Value), "Inventory")  
```  
  
## <a name="see-also"></a>参照  
 [レポートでの式の使用 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [式の例 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [式で使用されるデータ型 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [合計、集計、および組み込みコレクションの式のスコープ (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
