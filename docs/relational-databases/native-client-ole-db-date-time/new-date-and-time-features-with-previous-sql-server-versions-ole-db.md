---
title: 新しい日付と時刻の機能で以前の SQL Server バージョン (OLE DB) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 96976bac-018c-47cc-b1b2-fa9605eb55e5
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bb6ae27f2a936ab8b102a5e6e043e5b7b70c811c
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43099989"
---
# <a name="new-date-and-time-features-with-previous-sql-server-versions-ole-db"></a>以前のバージョンの SQL Server における、新しい日付または時刻の機能の動作 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  このトピックでは、強化された日付と時刻の機能を使用するクライアント アプリケーションのバージョンと通信する場合に想定される動作を説明します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]よりも前[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、クライアントのバージョンでコンパイルされたときに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client前[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]強化された日付と時刻の機能をサポートするサーバーへのコマンドを送信します。  
  
## <a name="down-level-client-behavior"></a>下位クライアントの動作  
 バージョンを使用するクライアント アプリケーション[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client より前[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]として新しい日付/時刻型を参照してください。 **nvarchar**列。 列のコンテンツはリテラル表現になります。 詳細については、の「データ形式: 文字列とリテラルをデータする"セクションを参照してください。 [OLE DB の日付と時刻の強化に対するデータ型のサポート](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)します。 列のサイズは、列に指定された有効桁数に対するリテラルの最大長です。  
  
 カタログ Api メタデータが返される、クライアントに返される下位データ型のコードで一貫性のある (たとえば、 **nvarchar**) と関連付けられている下位レベル形式 (たとえば、適切なリテラル形式)。 ただし、返されるデータ型名は、実際の [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] の型名です。  
  
 に対して下位クライアント アプリケーションを実行すると、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (またはそれ以降) サーバーの種類が構成されている日付/時刻へのスキーマ変更で、想定される動作は次のようにします。  
  
|OLE DB クライアントの型|SQL Server 2005 の型|SQL Server 2008 (またはそれ以降) の種類|結果の変換 (サーバーからクライアントへ)|パラメーターの変換 (クライアントからサーバーへ)|  
|------------------------|--------------------------|---------------------------------------|--------------------------------------------|-----------------------------------------------|  
|DBTYPE_DBDATE|DATETIME|date|[OK]|[OK]|  
|DBTYPE_DBTIMESTAMP|||時刻フィールドは 0 に設定されます。|時刻フィールドが 0 以外の場合は、IRowsetChange を文字列の切り捨てにより失敗します。|  
|DBTYPE_DBTIME||Time(0)|[OK]|[OK]|  
|DBTYPE_DBTIMESTAMP|||日付フィールドは現在の日付に設定されます。|IRowsetChange は、秒の小数部が 0 以外の場合、文字列の切り捨てにより失敗します。<br /><br /> 日付は無視されます。|  
|DBTYPE_DBTIME||Time(7)|失敗します (時刻リテラルが無効です)。|[OK]|  
|DBTYPE_DBTIMESTAMP|||失敗します (時刻リテラルが無効です)。|[OK]|  
|DBTYPE_DBTIMESTAMP||Datetime2 (3)|[OK]|[OK]|  
|DBTYPE_DBTIMESTAMP||datetime2 (7)|[OK]|[OK]|  
|DBTYPE_DBDATE|Smalldatetime|date|[OK]|[OK]|  
|DBTYPE_DBTIMESTAMP|||時刻フィールドは 0 に設定されます。|時刻フィールドが 0 以外の場合は、IRowsetChange を文字列の切り捨てにより失敗します。|  
|DBTYPE_DBTIME||Time(0)|[OK]|[OK]|  
|DBTYPE_DBTIMESTAMP|||日付フィールドは現在の日付に設定されます。|IRowsetChange は、秒の小数部が 0 以外の場合、文字列の切り捨てにより失敗します。<br /><br /> 日付は無視されます。|  
|DBTYPE_DBTIMESTAMP||Datetime2(0)|[OK]|[OK]|  
  
 OK は、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] で機能した場合には、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降でも引き続き機能することを意味します。  
  
 次の一般的なスキーマ変更のみが考慮されています。  
  
-   論理的にアプリケーションで日付値または時刻値のみが必要な場合に、新しい型を使用します。 アプリケーションが強制的に使用するただし、 **datetime**または**smalldatetime**のため、個別の日付と時刻型に使用可能なでした。  
  
-   追加の秒の小数部の有効桁数または精度を取得するために、新しい型を使用します。  
  
-   切り替え**datetime2**日付と時刻の優先されるデータ型は、このためです。  
  
 Icommandwithparameters::getparameterinfo またはスキーマ行セットから取得したサーバーのメタデータを使用して、icommandwithparameters::setparameterinfo をパラメーターの型情報を設定するアプリケーションが、クライアントでの変換に失敗、文字列ソース型の表現は、変換先の型の文字列表現を超えています。 たとえば、クライアントのバインディングが DBTYPE_DBTIMESTAMP を使用し、サーバーの列が date、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client は、"yyyy dd mm hh:mm:ss.fff"に値が変換されますが、サーバーのメタデータとして返されます**nvarchar (10)** します。 その結果発生するオーバーフローが、DBSTATUS_E_CATCONVERTVALUE の原因となります。 ような問題が発生するデータ変換を含む IRowsetChange、によって行セットのメタデータが結果セットのメタデータから設定されているためです。  
  
### <a name="parameter-and-rowset-metadata"></a>パラメーターと行セットのメタデータ  
 このセクションでは、クライアントのバージョンでコンパイルされたパラメーター、結果列、およびスキーマ行セットのメタデータがについて説明します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client より前[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]します。  
  
#### <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 DBPARAMINFO 構造体を次の情報を返します、 *prgParamInfo*パラメーター。  
  
|パラメーターの型|wType|ulParamSize|bPrecision|bScale|  
|--------------------|-----------|-----------------|----------------|------------|  
|日付|DBTYPE_WSTR|10|~0|~0|  
|time|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
 上記の値の範囲は連続していない場合があることに注意してください。たとえば、"8,10..16" には 9 は含まれません。 有効桁数が 0 より大きい場合は、小数点が追加されるためです。  
  
#### <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 返される列を次に示します。  
  
|列の型|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE、DBCOLUMN_DATETIMEPRECISION|  
|-----------------|--------------------|--------------------------|-------------------------|--------------------------------------------------|  
|日付|DBTYPE_WSTR|10|NULL|NULL|  
|time|DBTYPE_WSTR|8, 10..16|NULL|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|NULL|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|NULL|NULL|  
  
#### <a name="columnsinfogetcolumninfo"></a>ColumnsInfo::GetColumnInfo  
 DBCOLUMNINFO 構造体には、次の情報が返されます。  
  
|パラメーターの型|wType|ulColumnSize|bPrecision|bScale|  
|--------------------|-----------|------------------|----------------|------------|  
|日付|DBTYPE_WSTR|10|~0|~0|  
|time(1..7)|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
### <a name="schema-rowsets"></a>スキーマ行セット  
 このセクションでは、新しいデータ型のパラメーター、結果列、およびスキーマ行セットのメタデータについて説明します。 この情報は、便利なツールを使用して開発されたクライアント プロバイダーがあるはよりも前[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client。  
  
#### <a name="columns-rowset"></a>COLUMNS 行セット  
 日付型または時刻型に対して返される列の値を次に示します。  
  
|列の型|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|DATETIME_PRECISION|  
|-----------------|----------------|--------------------------------|------------------------------|-------------------------|  
|日付|DBTYPE_WSTR|10|20|NULL|  
|time|DBTYPE_WSTR|8, 10..16|16,20..32|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|NULL|NULL|3|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|NULL|  
  
#### <a name="procedureparameters-rowset"></a>PROCEDURE_PARAMETERS 行セット  
 日付型または時刻型に対して返される列の値を次に示します。  
  
|列の型|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|TYPE_NAME<br /><br /> LOCAL_TYPE_NAME|  
|-----------------|----------------|--------------------------------|------------------------------|--------------------------------------|  
|日付|DBTYPE_WSTR|10|20|日付|  
|time|DBTYPE_WSTR|8, 10..16|16,20..32|time|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|smalldatetime|  
|DATETIME|DBTYPE_DBTIMESTAMP|NULL|NULL|DATETIME|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|datetime2|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|datetimeoffset|  
  
#### <a name="providertypes-rowset"></a>PROVIDER_TYPES 行セット  
 日付/時刻型に対して返される行を次に示します。  
  
|型 -><br /><br /> [列]|日付|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|日付|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_WSTR|DBTYPE_WSTR|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_WSTR|DBTYPE_WSTR|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|‘|‘|‘|‘|‘|‘|  
|LITERAL_SUFFIX|‘|‘|‘|‘|‘|‘|  
|CREATE_PARAMS|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|日付|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|MAXIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_TRUE|VARIANT_FALSE|VARIANT_FALSE|  
|IS_FIXEDLENGTH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
  
## <a name="down-level-server-behavior"></a>下位サーバーの動作  
 前のバージョンのサーバーに接続されているときに[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、(たとえば、icommandwithparameters::setparameterinfo または itabledefinition::createtable) で新しいサーバーの型名を使用しようとすると、DB_E_BADTYPENAME になります。  
  
 型名を使用せずに新しい型がパラメーターまたは結果にバインドされている場合に、新しい型を使用してサーバーの型を暗黙的に指定するか、サーバーの型からクライアントの型への有効な変換がないと、DB_E_ERRORSOCCURRED が返されます。また、実行時に使用されるアクセサーのバインドの状態に DBBINDSTATUS_UNSUPPORTED_CONVERSION が設定されます。  
  
 接続時に、サーバーのバージョンに対して、クライアントでのバッファーの型からサーバーの型への変換がサポートされている場合は、クライアントのすべてのバッファーの型を使用できます。 このコンテキストで*サーバーの種類*icommandwithparameters::setparameterinfo をで指定されたまたは icommandwithparameters::setparameterinfo が呼び出されていない場合は、バッファーの種類が含まれる型のことを意味します。 つまり、クライアントでサポートされるサーバーの型への変換が成功した場合、DBTYPE_DBTIME2 および DBTYPE_DBTIMESTAMPOFFSET は、下位サーバーで使用するか、DataTypeCompatibility=80 の場合に使用することができます。 当然ながら、サーバーの型が正しくないと、実際のサーバーの型への暗黙的な変換を実行できない場合にサーバーからエラーが報告されます。  
  
## <a name="sspropinitdatatypecompatibility-behavior"></a>SSPROP_INIT_DATATYPECOMPATIBILITY の動作  
 SSPROP_INIT_DATATYPECOMPATIBILITY が SSPROPVAL_DATATYPECOMPATIBILITY_SQL2000 に設定されている場合、新しい日付/時刻型と関連付けられているメタデータと表示されますクライアントをダウンレベル クライアントでは、」の説明に従って[の一括コピーの変更強化された日付/時刻型&#40;OLE DB および ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)します。  
  
## <a name="comparability-for-irowsetfind"></a>IRowsetFind での比較  
 新しい日付型または時刻型に対しては、すべての比較演算子を使用できます。これは、日付型または時刻型ではなく文字列型と見なされるためです。  
  
## <a name="see-also"></a>参照  
 [日付と時刻の強化機能 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
