---
title: SQLGetDescRec |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLGetDescRec function
ms.assetid: f3389ff2-f3be-4035-9fb5-c9ebc2f15025
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 522cacc5005848f207c3a17ab90a26172bc6291d
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43060900"
---
# <a name="sqlgetdescrec"></a>SQLGetDescRec
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  このトピックで説明する固有の sqlgetdescrec による機能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client。  
  
## <a name="sqlgetdescrec-and-table-valued-parameters"></a>SQLGetDescRec とテーブル値パラメーター  
 SQLGetDescRec は、テーブル値パラメーターおよびテーブル値パラメーター列の属性の値を取得できます。 *RecNumber* SQLGetDescRec のパラメーターに対応、 *ParameterNumber* SQLBindParameter のパラメーター。  
  
 テーブル値パラメーター列は、記述子のヘッダー フィールド SQL_SOPT_SS_PARAM_FOCUS に、SQL_DESC_TYPE が SQL_SS_TABLE に設定されているレコードの序数が設定される場合のみ使用できます。 SQL_SOPT_SS_PARAM_FOCUS の詳細についての詳細については、次を参照してください。 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)します。  
  
 SQLGetDescRec には、次のデータが返されます。  
  
|パラメーター|テーブル値パラメーター|テーブル値パラメーター列とその他のパラメーター|  
|---------------|-----------------------------|----------------------------------------------------------|  
|*名前*|ストアド プロシージャ呼び出しの場合は仮パラメーター名。それ以外の場合は長さが 0 の文字列。|テーブル値パラメーター列の名前。|  
|*TypePtr*|SQL_DESC_TYPE。 テーブル値パラメーターの場合、これは SQL_SS_TABLE です。|SQL_DESC_TYPE|  
|*SubTypePtr*|未定義。|SQL_DESC_DATETIME_INTERVAL_CODE (SQL_DATETIME 型または SQL_INTERVAL 型のレコードの場合)。|  
|*LengthPtr*|0|SQL_DESC_OCTET_LENGTH|  
|*PrecisionPtr*|0|SQL_DESC_PRECISION|  
|*ScalePtr*|0|SQL_DESC_SCALE|  
|*NullablePtr*|1|SQL_DESC_NULLABLE|  
  
 テーブル値パラメーターの詳細については、次を参照してください。[テーブル値パラメーター &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)します。  
  
## <a name="sqlgetdescrec-support-for-enhanced-date-and-time-features"></a>SQLGetDescRec による機能強化された日付と時刻のサポート  
 日付型または時刻型に対して返される値を次に示します。  
  
||*TypePtr*|*SubTypePtr*|*LengthPtr*|*PrecisionPtr*|*ScalePtr*|  
|-|---------------|------------------|-----------------|--------------------|----------------|  
|DATETIME|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|日付|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|time|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 詳細については、次を参照してください。[日付と時刻の強化&#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)します。  
  
## <a name="sqlgetdescrec-support-for-large-clr-udts"></a>SQLGetDescRec による大きな CLR UDT のサポート  
 **SQLGetDescRec**大きなの CLR ユーザー定義型 (Udt) をサポートしています。 詳細については、次を参照してください。 [Large CLR User-Defined 型&#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)します。  
  
## <a name="see-also"></a>参照  
 [SQLGetDescRec](http://go.microsoft.com/fwlink/?LinkId=80707)   
 [ODBC API 実装の詳細](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
