---
title: テンプレート、XSL、およびスキーマ (SQLXML 4.0) をキャッシュします。マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLXML, caching
- cache [SQLXML]
- memory [SQLXML]
ms.assetid: 80b4fa79-243f-442c-9f22-74ad66186501
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 90249141ab30ce5eb5803b29b687423d4ef17227
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43101571"
---
# <a name="caching-templates-xsl-and-schemas-sqlxml-40"></a>テンプレート、XSL、およびスキーマのキャッシュ (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  パフォーマンス向上のため、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 ではテンプレート、XSL、およびスキーマのキャッシュがサポートされています。  
  
 SQLXML 4.0 ではすべてのスキーマとテンプレート、および (http:// または ftp:// にあるファイルを除く) XSL ファイルをキャッシュでき、 キャッシュされたファイルは処理が実行されている間メモリに残ります。 処理が終了すると、すべてのキャッシュは失われます。 したがって、クエリごとに 1 つの処理を実行する場合は、キャッシュがそれほどメリットにならない場合もあります。  
  
 ここでは、キャッシュの詳細について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [テンプレートのキャッシュ&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)  
 テンプレートのキャッシュ用のレジストリ キーについて説明します。  
  
 [XSL のキャッシュ&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
 XSL のキャッシュ用のレジストリ キーについて説明します。  
  
 [スキーマ キャッシュ&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)  
 スキーマのキャッシュに関する SQLXML サイド バイ サイド インストールについて説明し、スキーマのキャッシュ用のレジストリ キーを提供します。  
  
  
