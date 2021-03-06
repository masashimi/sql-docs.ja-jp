---
title: DQS ドメインに対してサポートされる SQL Server のデータ型と SSIS のデータ型 | Microsoft Docs
ms.custom: ''
ms.date: 11/08/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4931143a-b84d-478b-9b45-174128d36ed3
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e7e297690f6b2a6c14d4b280905a0fa888d0b4ed
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2018
ms.locfileid: "35311121"
---
# <a name="supported-sql-server-and-ssis-data-types-for-dqs-domains"></a>DQS ドメインに対してサポートされる SQL Server のデータ型と SSIS のデータ型

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  SQL Server と SQL Server Integration Services (SSIS) にはさまざまなデータ型が存在しますが、DQS ドメインのデータ型は Date、Decimal、Integer、String の 4 つだけです。 SQL Server と SSIS のデータ型には、DQS でサポートされないものも存在します。 ソース データを DQS ドメインにマッピングし、データ品質アクティビティを実行できるのは、ソースのデータ型が DQS でサポートされていて、なおかつ DQS ドメインのデータ型と一致する場合だけです。 このトピックでは、SQL Server と SSIS のデータ型のうち、DQS ドメインの 4 つのデータ型にそれぞれマッピングできる、サポートされるデータ型について取り上げます。  
  
> [!NOTE]  
>  .xlsx および .xls ファイルでは、ソース列のデータ型は最初の 8 行で最も多く使用されているデータ型によって決定されます。 セルがそのデータ型に従っていない場合、セルの値は null になります。 同様に、.csv ファイルでは、ソース列のデータ型は最初の 8 行で最も多く使用されているデータ型によって決定されます。  
  
##  <a name="SQLServer"></a> サポートされる SQL Server のデータ型  
 次の表は、DQS ドメインの各データ型について、サポートされる SQL Server のデータ型を示しています。  
  
|DQS ドメインのデータ型|サポートされる SQL Server のデータ型|  
|--------------------------|------------------------------------|  
|date|日付|  
|Decimal|Decimal<br /><br /> FLOAT<br /><br /> money<br /><br /> NUMERIC<br /><br /> REAL<br /><br /> SMALLMONEY|  
|Integer|BIGINT<br /><br /> ssNoversion<br /><br /> smallint<br /><br /> TINYINT|  
|String|char<br /><br /> NCHAR<br /><br /> NVARCHAR<br /><br /> varchar|  
  
 その他の SQL Server データ型は、DQS ではサポートされません。 SQL Server データ型については、「[データ型 &#40;Transact-SQL&#41;](../t-sql/data-types/data-types-transact-sql.md)」をご覧ください。  
  
##  <a name="SSIS"></a> サポートされる SSIS のデータ型  
 次の表は、DQS ドメインの各データ型について、サポートされる SSIS のデータ型を示しています。  
  
|DQS ドメインのデータ型|サポートされる SSIS のデータ型|  
|--------------------------|------------------------------|  
|date|DT_DATE|  
|Decimal|DT_DECIMAL<br /><br /> DT_NUMERIC<br /><br /> DT_R4<br /><br /> DT_R8|  
|Integer|DT_I1<br /><br /> DT_I2<br /><br /> DT_I4<br /><br /> DT_I8<br /><br /> DT_U1<br /><br /> DT_U2<br /><br /> DT_U4<br /><br /> DT_U8|  
|String|DT_STR<br /><br /> DT_WSTR|  
  
 その他の SSIS データ型は、DQS ではサポートされません。 SSIS のすべてのデータ型については、「 [Integration Services Data Types](../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ドメインの管理](../data-quality-services/managing-a-domain.md)  
  
  
