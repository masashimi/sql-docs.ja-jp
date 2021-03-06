---
title: 機能強化された日付型と時刻型向けの一括コピーの変更 (OLE DB) | Microsoft Docs
description: 機能強化された日付型と時刻型向けの一括コピーの変更 (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, bulk copy operations
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 16ab7dd1f4a083c51108ef86ff9c9428df1649da
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43029561"
---
# <a name="bulk-copy-changes-for-enhanced-date-and-time-types-ole-db"></a>機能強化された日付型と時刻型向けの一括コピーの変更 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  この記事では、OLE DB driver for SQL Server バルク コピー機能をサポートするために日付/時刻の機能強化について説明します。  
  
## <a name="format-files"></a>フォーマット ファイル  
 フォーマット ファイルを対話形式で作成する場合に、日付型と時刻型の指定に使用する入力、および対応するホスト ファイル データ型名を次の表に示します。  
  
|ファイル ストレージ型|ホスト ファイル データ型|"フィールド <field_name> [\<default>] のファイル ストレージ型を入力してください" というプロンプトへの応答|  
|-----------------------|-------------------------|-----------------------------------------------------------------------------------------------------|  
|DATETIME|SQLDATETIME|d|  
|Smalldatetime|SQLDATETIM4|D|  
|date|SQLDATE|de|  
|Time|SQLTIME|te|  
|Datetime2|SQLDATETIME2|d2|  
|Datetimeoffset|SQLDATETIMEOFFSET|do|  
  
 XML フォーマット ファイルの XSD への追加内容を次に示します。  
  
```  
<xs:complexType name="SQLDATETIME2">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLDATETIMEOFFSET">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLDATE">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLTIME">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
```  
  
## <a name="character-data-files"></a>文字データ ファイル  
 「データ形式: 文字列とリテラルをデータする"セクションで説明した文字のデータ ファイルで日付と時刻値が表される[OLE DB の日付と時刻の強化に対するデータ型のサポート](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)OLE DB 用です。  
  
 ネイティブ データ ファイルでは、4 つの新しい型の日付と時刻の値は、小数点以下桁数が 7 桁の TDS 表現として表されます (これが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によってサポートされている最大であり、bcp データ ファイルはこれらの列の小数点以下桁数を格納しないためです)。 既存の **datetime** 型および **smalldatetime** 型や、それらの TDS (表形式のデータ ストリーム) 表現のストレージに変更はありません。  
  
 OLE DB の場合、さまざまなストレージ型のストレージ サイズは次のとおりです。  
  
|ファイル ストレージ型|ストレージ サイズ (バイト単位)|  
|-----------------------|---------------------------|  
|DATETIME|8|  
|smalldatetime|4|  
|日付|3|  
|time|6|  
|datetime2|9|  
|datetimeoffset|11|  
 
  
## <a name="bcp-types-in-msoledbsqlh"></a>Msoledbsql.h 内の BCP 型  
 次の種類は、msoledbsql.h で定義されます。 これらの型が渡され、 *eUserDataType* ibcpsession::bcpcolfmt OLE DB でのパラメーター。  
  
|ファイル ストレージ型|ホスト ファイル データ型|Msoledbsql.h ibcpsession::bcpcolfmt で使用するために入力します。|ReplTest1|  
|-----------------------|-------------------------|-----------------------------------------------------------|-----------|  
|DATETIME|SQLDATETIME|BCP_TYPE_SQLDATETIME|0x3d|  
|Smalldatetime|SQLDATETIM4|BCP_TYPE_SQLDATETIM4|0x3a|  
|date|SQLDATE|BCP_TYPE_SQLDATE|0x28|  
|Time|SQLTIME|BCP_TYPE_SQLTIME|0x29|  
|Datetime2|SQLDATETIME2|BCP_TYPE_SQLDATETIME2|0x2a|  
|Datetimeoffset|SQLDATETIMEOFFSET|BCP_TYPE_SQLDATETIMEOFFSET|0x2b|  
  
## <a name="bcp-data-type-conversions"></a>BCP データ型変換  
 次の表に、変換情報を示します。  
  
 **OLE DB に関するメモ** 次の変換は、IBCPSession によって実行されます。 IRowsetFastLoad で定義されている OLE DB 変換を使用して[サーバーにクライアントから変換](../../oledb/ole-db-date-time/conversions-performed-from-client-to-server.md)します。 次に示すクライアントでの変換が実行されると、datetime 値は 1/300 秒単位に丸められ、smalldatetime 値の秒は 0 に設定されます。 datetime の丸め処理は、時間と分に適用されますが、日付には適用されません。  
  
|変換先 --><br /><br /> From|日付|time|smalldatetime|DATETIME|datetime2|datetimeoffset|char|wchar|  
|------------------------|----------|----------|-------------------|--------------|---------------|--------------------|----------|-----------|  
|date|1|-|1、6|1、6|1、6|1、5、6|1、3|1、3|  
|Time|なし|1、10|1、7、10|1、7、10|1、7、10|1、5、7、10|1、3|1、3|  
|Smalldatetime|1、2|1、4、10|1|1|1、10|1、5、10|1、11|1、11|  
|DATETIME|1、2|1、4、10|1、12|1|1、10|1、5、10|1、11|1、11|  
|Datetime2|1、2|1、4、10|1、12|1、10|1、10|1、5、10|1、3|1、3|  
|Datetimeoffset|1、2、8|1、4、8、10|1、8、10|1、8、10|1、8、10|1、10|1、3|1、3|  
|Char/wchar (date)|9|-|9、6、12|9、6、12|9、6|9、5、6|なし|なし|  
|Char/wchar (time)|-|9、10|9、7、10、12|9、7、10、12|9、7、10|9、5、7、10|なし|なし|  
|Char/wchar (datetime)|9、2|9、4、10|9、10、12|9、10、12|9、10|9、5、10|なし|なし|  
|Char/wchar (datetimeoffset)|9、2、8|9、4、8、10|9、8、10、12|9、8、10、12|9、8、10|9、10|なし|なし|  
  
#### <a name="key-to-symbols"></a>記号の説明  
  
|記号|意味|  
|------------|-------------|  
|-|変換はサポートされていません。<br />|  
|1|指定したデータが有効でない場合、エラーが通知されます。 datetimeoffset 値の場合は、UTC への変換が必要なくても、時刻部分は UTC への変換後の範囲内に収まっている必要があります。 TDS とサーバーは datetimeoffset 値の時刻を常に UTC 用に正規化するためです。 したがって、クライアントは、時刻部分が、UTC への変換後にサポートされる範囲内に収まっていることを確認する必要があります。|  
|2|時刻部分は無視されます。|  
|3|データの損失を伴う切り捨てが行われると、エラーが通知されます。 datetime2 に関しては、次の表に示すように、秒の小数点以下桁数は変換先の列のサイズによって決まります。 テーブルの範囲よりサイズが大きい列の場合は、9 桁と見なされます。 この変換では、秒の小数点以下桁数が 9 桁まで許容されます。これは、OLE DB で許容される最大桁数です。<br /><br /> **型:** DBTIME2<br /><br /> **暗黙の小数点以下桁数 0** 8<br /><br /> **暗黙の小数点以下桁数 1..9** 1..9<br /><br /> <br /><br /> **型:** DBTIMESTAMP<br /><br /> **暗黙の小数点以下桁数 0:** 19<br /><br /> **暗黙の小数点以下桁数 1..9:** 21..29<br /><br /> <br /><br /> **型:** DBTIMESTAMPOFFSET<br /><br /> **暗黙の小数点以下桁数 0:** 26<br /><br /> **暗黙の小数点以下桁数 1..9:** 28..36|  
|4|日付部分は無視されます。|  
|5|タイム ゾーンは UTC (00:00 など) に設定されます。|  
|6|時刻は 0 に設定されます。|  
|7|日付は 1900-01-01 に設定されます。|  
|8|タイム ゾーン オフセットは無視されます。|  
|9|文字列は解析され、最初に検出された句読点、および残りの部分があるかどうかに応じて、date 値、datetime 値、datetimeoffset 値、time 値のいずれかに変換されます。 次に、この記事の最後にある表に示した規則のうち、この処理で検出された変換元の型についての規則に従って、文字列は変換先の型に変換されます。 エラーを発生させずに渡されるデータを解析できない場合に、またはいずれかの部分が、許容範囲外の場合またはリテラルの型から対象の型への変換が存在しない場合は、エラーが通知されます。 Datetime および smalldatetime 型のパラメーターの年がこれらの型がサポート範囲外の場合、エラーが通知されます。<br /><br /> datetimeoffset では、UTC への変換が必要なくても、値は UTC への変換後の範囲内に収まっている必要があります。 TDS とサーバーは datetimeoffset 値の時刻を常に UTC 用に正規化するので、クライアントは、時刻部分が、UTC への変換後にサポートされる範囲内に収まっていることを確認する必要があるためです。 値が、サポートされている UTC の範囲内にない場合は、エラーが通知されます。|  
|10|クライアント サーバーへの変換から、データ損失を伴う切り捨てが発生した場合、エラーが通知されます。 サーバーが使用する UTC の範囲で表すことができる範囲の外に値がある場合にも、このエラーが発生します。 サーバーからクライアントへの変換で、秒または秒の小数部の切り捨てが行われた場合は、警告のみが発生します。|  
|11|クライアント サーバーへの変換から、データ損失を伴う切り捨てが発生した場合、エラーが通知されます。|
|12|秒は 0 に設定され、秒の小数部は破棄されます。 切り捨てエラーは発生しません。|  
|なし|既存の [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以前のバージョンの動作が維持されます。|  
  
## <a name="see-also"></a>参照     
 [日付と時刻の強化機能 &#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
