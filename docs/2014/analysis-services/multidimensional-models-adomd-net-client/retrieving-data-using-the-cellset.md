---
title: セルセットを使用してデータの取得 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- CellSet object
- retrieving data
- data retrieval [ADOMD.NET], CellSet object
ms.assetid: 77e4ee58-882d-4012-91a3-0565f18a4882
caps.latest.revision: 41
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 69e53cab56cf22d6627fd8039e6a46735d934ca7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37178899"
---
# <a name="retrieving-data-using-the-cellset"></a>セルセットを使用したデータの取得
  分析データを取得する際、対話性と柔軟性に最も優れている方法が <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> オブジェクトです。 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> オブジェクトは階層データおよびメタデータのインメモリ キャッシュであり、これらのデータの元の次元を保持します。 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> オブジェクトは、接続された状態でも、接続されていない状態でもスキャンすることができます。 非接続状態でもアクセス可能なことから、<xref:Microsoft.AnalysisServices.AdomdClient.CellSet> オブジェクトを使用すれば、データやメタデータを任意の順序で表示することができ、データ取得の最も包括的なオブジェクト モデルといえます。 一方で、<xref:Microsoft.AnalysisServices.AdomdClient.CellSet> オブジェクトはオーバーヘッドが非常に大きく、最も低速な ADOMD.NET データ取得オブジェクト モデルでもあります。  
  
## <a name="retrieving-data-in-a-connected-state"></a>接続状態でのデータの取得  
 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> オブジェクトを使用してデータを取得するには、次の手順を実行します。  
  
1.  **オブジェクトの新しいインスタンスを作成します。**  
  
     <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> オブジェクトの新しいインスタンスを作成するには、<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> オブジェクトの <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteCellSet%2A> または <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> メソッドを呼び出します。  
  
2.  **メタデータを特定します。**  
  
     データを取得する以外に、ADOMD.NET はセルセットのメタデータも取得します。 コマンドによってクエリが実行され、<xref:Microsoft.AnalysisServices.AdomdClient.CellSet> が返されるとすぐに、さまざまなオブジェクトを通じてメタデータを取得できるようになります。 このメタデータは、クライアント アプリケーションがセルセット データを表示したり、セルセット データを操作したりする際に必要となります。 たとえば、多くのクライアント アプリケーションには、セルセット内の指定した位置をドリル ダウンし、子の位置を階層的に表示するための機能が備わっています。  
  
     ADOMD.NET では、<xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Axes%2A> オブジェクトの <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.FilterAxis%2A> プロパティおよび <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> プロパティは、返されたセルセット内のクエリおよびスライサー軸のメタデータをそれぞれ表します。 これら 2 つのプロパティは、<xref:Microsoft.AnalysisServices.AdomdClient.Axis> オブジェクトへの参照を返します。さらに、このオブジェクトには、各軸上での位置が含まれています。  
  
     各 <xref:Microsoft.AnalysisServices.AdomdClient.Axis> オブジェクトは、その軸で使用可能な組のセットを表す <xref:Microsoft.AnalysisServices.AdomdClient.Position> オブジェクトのコレクションを格納します。 各 <xref:Microsoft.AnalysisServices.AdomdClient.Position> オブジェクトは、1 つの組を表しています。この組は、<xref:Microsoft.AnalysisServices.AdomdClient.Member> オブジェクトのコレクションによって表される 1 つまたは複数のメンバーを含みます。  
  
3.  **セルセット コレクションからデータを取得します。**  
  
     メタデータを取得する以外に、ADOMD.NET はセルセットのデータも取得します。 コマンドによってクエリが実行され、<xref:Microsoft.AnalysisServices.AdomdClient.CellSet> が返されるとすぐに、<xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Cells%2A> の <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> コレクションを使用してデータを取得できるようになります。 このコレクションには、クエリのすべての軸の交差部分について計算された値が含まれます。 したがって、各交差部分 (セル) にアクセスするためのインデクサーがいくつかあります。 インデクサーの一覧については、「<xref:Microsoft.AnalysisServices.AdomdClient.CellCollection.Item%2A>」を参照してください。  
  
### <a name="example-of-retrieving-data-in-a-connected-state"></a>接続状態でのデータの取得例  
 次の例では、ローカル サーバーへの接続を確立し、その接続に対してコマンドを実行します。 この例では、`CellSet` オブジェクト モデルを使用して結果を解析します。列のキャプション (メタデータ) は最初の軸から取得され、各行のキャプション (メタデータ) は 2 つ目の軸から取得されます。また、交差部分のデータは、<xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Cells%2A> コレクションを使用して取得されます。  
  
 [!code-csharp[Adomd.NetClient#ReturnCommandUsingCellSet](../../snippets/csharp/SQL14/adomd.net/adomd.netclient/cs/adomdexample.cs#returncommandusingcellset)]  
  
## <a name="retrieving-data-in-a-disconnected-state"></a>非接続状態でのデータの取得  
 前のクエリで返された XML を読み込むことにより、接続中でなくても、<xref:Microsoft.AnalysisServices.AdomdClient.CellSet> オブジェクトを使用して分析データを包括的に参照することができます。  
  
> [!NOTE]  
>  <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> オブジェクトからアクセスできるオブジェクトのプロパティの中には、非接続状態では使用できないものがあります。 詳細については、「<xref:Microsoft.AnalysisServices.AdomdClient.CellSet.LoadXml%2A>」を参照してください。  
  
### <a name="example-of-retrieving-data-in-a-disconnected-state"></a>非接続状態でのデータの取得例  
 次の例は、このトピックで前述したメタデータとデータの例に似ています。 ただし、この例のコマンドは、<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> への呼び出しを使用して実行され、結果は `System.Xml.XmlReader` として返されます。 その後、<xref:Microsoft.AnalysisServices.AdomdClient.CellSet> メソッドと共にこの `System.Xml.XmlReader` を使用して <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.LoadXml%2A> オブジェクトを設定します。 この例では `System.Xml.XmlReader` をすぐに読み込みますが、データをセルセットに読み込む前に、リーダーからハード ディスクに格納された XML をキャッシュするか、なんらかの方法でデータを別のアプリケーションに転送することもできます。  
  
 [!code-csharp[Adomd.NetClient#DemonstrateDisconnectedCellset](../../snippets/csharp/SQL14/adomd.net/adomd.netclient/cs/adomdexample.cs#demonstratedisconnectedcellset)]  
  
## <a name="see-also"></a>参照  
 [分析データ ソースからデータを取得します。](retrieving-data-from-an-analytical-data-source.md)   
 [AdomdDataReader を使用してデータを取得します。](retrieving-data-using-the-adomddatareader.md)   
 [XmlReader を使用したデータの取得](retrieving-data-using-the-xmlreader.md)  
  
  
