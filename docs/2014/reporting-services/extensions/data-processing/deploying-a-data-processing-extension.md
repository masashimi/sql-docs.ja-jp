---
title: データ処理拡張機能の配置 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: e5c0b5a9-1386-47cb-aade-96653ecfaa54
caps.latest.revision: 34
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 88fcfd2d87238a31562d17b0811d94485a9d1ad9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37242252"
---
# <a name="deploying-a-data-processing-extension"></a>データ処理拡張機能の配置
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のデータ処理拡張機能は、作成して [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] ライブラリにコンパイルした後、レポート サーバーおよびレポート デザイナーで検出できるようにする必要があります。 これは、適切なディレクトリに拡張機能をコピーし、適切な [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 構成ファイルにエントリを追加するだけで簡単に行うことができます。  
  
## <a name="configuration-file-extension-element"></a>構成ファイルの Extension 要素  
 レポート サーバーまたはレポート デザイナーに配置するデータ処理拡張機能は、構成ファイルに **Extension** 要素として入力する必要があります。 構成ファイルは、レポート サーバーの場合は RSReportServer.config、レポート デザイナーの場合は RSReportDesigner.config です。  
  
 次の表では、データ処理拡張機能の **Extension** 要素の属性について説明します。  
  
|属性|説明|  
|---------------|-----------------|  
|`Name`|拡張機能の一意な名前。たとえば、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ処理拡張機能に対して "SQL"、OLE DB データ処理拡張機能に対して "OLEDB"。 `Name` 属性の最大文字数は 255 文字です。 名前は、構成ファイルの **Extension** 要素内にあるすべてのエントリの間で一意にする必要があります。|  
|`Type`|アセンブリの名前と共に完全修飾名前空間を含むコンマ区切りの一覧。|  
|`Visible`|`false` の値は、データ処理拡張機能がユーザー インターフェイスに表示されないことを示します。 属性が含まれない場合、既定値は`true`します。|  
  
 RSReportServer.config ファイルまたは RSReportDesigner.config ファイルの詳細については、「[Reporting Services 構成ファイル](../../report-server/reporting-services-configuration-files.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[データ処理拡張機能をレポート サーバーに配置する方法](deploying-a-data-processing-extension-to-a-report-server.md)|レポート サーバーにデータ処理拡張機能を配置する方法について説明します。|  
|[データ処理拡張機能をレポート デザイナーに配置する方法](deploying-a-data-processing-extension-to-report-designer.md)|レポート デザイナーにデータ処理拡張機能を配置する方法について説明します。|  
  
## <a name="see-also"></a>参照  
 [Reporting Services の拡張機能](../reporting-services-extensions.md)   
 [データ処理拡張機能の実装](implementing-a-data-processing-extension.md)   
 [Reporting Services 拡張機能ライブラリ](../reporting-services-extension-library.md)  
  
  
