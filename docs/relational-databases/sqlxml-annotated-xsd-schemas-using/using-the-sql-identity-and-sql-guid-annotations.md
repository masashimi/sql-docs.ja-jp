---
title: Sql:identity 注釈と sql:guid 注釈の使用 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sql:guid
- annotated XSD schemas, IDENTITY-type columns
- annotated XSD schemas, GUID values
- DiffGrams [SQLXML], annotations
- identity annotation
- XSD schemas [SQLXML], GUID values
- GUIDs [SQLXML]
- guid annotation
- sql:identity
- IDENTITY-type column
- XSD schemas [SQLXML], IDENTITY-type columns
- updategrams [SQLXML], GUID values
ms.assetid: 7661dfd0-6573-4692-a8f1-3597adcd33c4
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 33bc05d0161caa2dacdc42a86f0255775fe69e79
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43058264"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>sql:identity 注釈と sql:guid 注釈の使用
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  指定することができます、 **sql:identity 注釈**と**sql:guid**でデータベース列にマップされる任意のノードの XSD スキーマで注釈[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 アップデート グラムの形式をサポートしていますが、 **updg: id で**と**updg:guid**属性、DiffGram 形式はありません。 **Updg: id で**属性、IDENTITY 型の列を更新中に、動作を定義します。 **Updg:guid**属性から GUID 値を取得できます。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をアップデート グラムで使用します。 詳細と実際のサンプルは、次を参照してください。[を挿入するデータを使用して XML アップデート グラム&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)します。  
  
 **Sql:identity 注釈**と**sql:guid**注釈は Diffgram にこの機能を拡張します。  
  
 DiffGram を実行すると、DiffGram がアップデートグラムに変換された後、アップデートグラムが実行されます。 指定することによって、 **sql:identity 注釈**と**sql:guid**アップデート グラムの動作を定義するには、XSD スキーマでの注釈。 したがって、すべての注釈はアップデートグラムのコンテキストで記述します。 これらの注釈は DiffGram とアップデートグラムの両方で使用できますが、アップデートグラムには ID 値と GUID 値をより効率的に処理する機能が既に用意されています。  
  
 **Sql:identity 注釈**と**sql:guid**複合コンテンツ要素に注釈を定義することができます。  
  
## <a name="sqlidentity-annotation"></a>sql:identity 注釈  
 指定することができます、 **sql:identity 注釈**IDENTITY 型のデータベース列にマップされる任意のノードの XSD スキーマに注釈。 この注釈の値では、IDENTITY 型の列の更新方法として、アップデートグラムで提供される値を使用するか、値を無視するかを定義します。値を無視する場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で生成される値が列に使用されます。  
  
 **Sql:identity 注釈**注釈には 2 つの値を割り当てることができます。  
  
 ignore  
 アップデートグラムで列に提供される値を無視し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で生成される ID 値を使用します。  
  
 useValue  
 アップデートグラムで提供される値を使用して、IDENTITY 型列を更新します。 アップデートグラムでは、列が ID 値かどうかは確認されません。  
  
 アップデート グラムで IDENTITY 型の列の値を指定する場合、 **sql:identity 注釈 ="useValue"** スキーマで指定する必要があります。  
  
## <a name="sqlguid-annotation"></a>sql:guid 注釈  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で GUID 値を生成し、その値をアップデートグラムで使用できます。 Diffgram のコンテキストで使用することができます、 **sql:guid** SQL Server によって生成される GUID 値を使用するかどうかを指定するか、その列のアップデート グラムで提供される値を使用する注釈。  
  
 **Sql:guid**注釈には 2 つの値を割り当てることができます。  
  
 generate  
 更新操作で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で生成される GUID を列に使用することを指定します。  
  
 useValue  
 アップデートグラムで提供される値を列に使用することを指定します。 これが既定値です。  
  
  
