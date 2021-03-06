---
title: C から SQL への変換 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC], C to SQL
ms.assetid: 7ac098db-9147-4883-8da9-a58ab24a0d31
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 430b8f3d0184e41a2882b867b64bf2ce3dbfc0cf
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43084555"
---
# <a name="datetime-data-type-conversions-from-c-to-sql"></a>datetime データ型の C から SQL への変換
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  このトピックでは、C 型から変換する際に考慮する問題を示します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日付/時刻型です。  
  
 次の表で説明する変換は、クライアントで行われる変換に当てはまります。 クライアントがサーバーで定義されているパラメーターとは異なる小数秒の有効桁数を指定する場合、クライアントの変換が成功可能性がありますが、サーバーはエラーを返しますと**SQLExecute**または**SQLExecuteDirect**が呼び出されます。 一方、ODBC で秒の小数部の切り捨てがエラーとして処理する具体的には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に丸める動作は、たとえば、丸め処理を行うときに発生しますから移動する**datetime2(6)** に**datetime2(2)**. datetime 列の値は 1/300 秒単位に丸められ、smalldatetime 列では、サーバーによって秒が 0 に設定されます。  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
||SQL_TYPE_DATE|SQL_TYPE_TIME|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_SS_TIMSTAMPOFFSET|SQL_CHAR|SQL_WCHAR|  
|SQL_C_DATE|1|-|-|1,6|1,5,6|1,13|1,13|  
|SQL_C_TIME|-|1|1|1,7|1,5,7|1,13|1,13|  
|SQL_C_SS_TIME2|-|1,3|1,10|1,7|1,5,7|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIME2_STRUCT)|なし|なし|1,10,11|なし|なし|なし|なし|  
|SQL_C_TYPE_TIMESTAMP|1,2|1,3,4|1,4,10|1,10|1,5,10|1,13|1,13|  
|SQL_C_SS_TIMESTAMPOFFSET|1,2,8|1,3,4,8|1,4,8,10|1,8,10|1,10|1,13|1,13|  
|SQL_C_BINARY(SQL_SS_TIMESTAMPOFFSET_STRUCT)|なし|なし|なし|なし|1,10,11|なし|なし|  
|SQL_C_CHAR/SQL_WCHAR (date)|9|9|9|9,6|9,5,6|なし|なし|  
|SQL_C_CHAR/SQL_WCHAR (time2)|9|9,3|9,10|9,7,10|9,5,7,10|なし|なし|  
|SQL_C_CHAR/SQL_WCHAR (datetime)|9,2|9,3,4|9,4,10|9,10|9,5,10|なし|なし|  
|SQL_C_CHAR/SQL_WCHAR (datetimeoffset)|9,2,8|9,3,4,8|9,4,8,10|9,8,10|9,10|なし|なし|  
|SQL_C_BINARY(SQL_DATE_STRUCT)|1,11|なし|なし|なし|なし|なし|なし|  
|SQL_C_BINARY(SQL_TIME_STRUCT)|なし|なし|なし|なし|なし|なし|なし|  
|SQL_C_BINARY(SQL_TIMESTAMP_STRUCT)|なし|なし|なし|なし|なし|なし|なし|  
  
## <a name="key-to-symbols"></a>記号の説明  
  
-   **-**: 変換がサポートされてありません。 "データ型の属性に関する制限に違反しました" というメッセージで SQLSTATE 07006 の診断レコードが生成されます。  
  
-   **1**: SQLSTATE 22007、メッセージ「無効な datetime 形式」診断レコードが生成される指定したデータが有効でない場合。  
  
-   **2**: 時刻フィールドは 0 である必要がありますか、診断レコードで SQLSTATE 22008 し、「分数が切り捨てられました」というメッセージが生成されます。  
  
-   **3**: 秒の小数部は 0 である必要がありますか、診断レコードで SQLSTATE 22008 し、「分数が切り捨てられました」というメッセージが生成されます。  
  
-   **4**: 日付部分は無視されます。  
  
-   **5**: タイム ゾーンは、クライアントのタイム ゾーンの設定に設定されます。  
  
-   **6**: 時間が 0 に設定されます。  
  
-   **7**: 現在の日付に日付を設定します。  
  
-   **8**: 時間は、クライアントのタイム ゾーンから UTC に変換されます。 この変換中にエラーが発生すると、"Datetime フィールド オーバーフロー" というメッセージで SQLSTATE 22008 の診断レコードが生成されます。  
  
-   **9**: 文字列が解析され、date、datetime、datetimeoffset、または最初に検出された句読点と残りのコンポーネントの存在によって、時刻の値に変換します。 次に、上の表に示した規則のうち、この処理で検出された変換元の型についての規則に従って、文字列は変換先の型に変換されます。 データの解析中にエラーが検出された場合、"キャストした文字コードが正しくありません" というメッセージで SQLSTATE 22018 の診断レコードが生成されます。 datetime 型および smalldatetime 型のパラメーターでは、年がこれらの型でサポートされる範囲外の場合、"datetime 形式が無効です" というメッセージで SQLSTATE 22007 の診断レコードが生成されます。  
  
     datetimeoffset では、UTC への変換が必要なくても、値は UTC への変換後の範囲内に収まっている必要があります。 TDS とサーバーは datetimeoffset 値の時刻を常に UTC 用に正規化するので、クライアントは、時刻部分が、UTC への変換後にサポートされる範囲内に収まっていることを確認する必要があるためです。 値が、サポートされている UTC の範囲内に収まっていない場合、"datetime 形式が無効です" というメッセージで SQLSTATE 22007 の診断レコードが生成されます。  
  
-   **10**: SQLSTATE 22008、メッセージ「形式の時刻が無効です」診断レコードが生成されたデータの損失を伴う切り捨てが発生した場合。 サーバーが使用する UTC の範囲で表すことができる範囲の外に値がある場合にも、このエラーが発生します。  
  
-   **11**: SQLSTATE 22003、メッセージ「数値が範囲外」診断レコードが生成されたデータのバイト長が、SQL 型が必要な構造体のサイズを等しくない場合。  
  
-   **12**: 生の TDS smalldatetime または datetime 形式でサーバーにデータが送信されるデータのバイトの長さが 4 または 8 の場合は、します。 データのバイト長が SQL_TIMESTAMP_STRUCT のサイズと完全に一致する場合、データは、datetime2 用の TDS 形式に変換されます。  
  
-   **13**: SQLSTATE 22001「文字列データの右側が切り捨てられました」というメッセージと診断レコードが生成されたデータの損失を伴う切り捨てが発生した場合。  
  
     秒の小数部桁数 (スケール) は、次の表に従って、変換先列のサイズから決定されます。  
  
    ||||  
    |-|-|-|  
    |型|暗黙の小数点以下桁数<br /><br /> 0|暗黙の小数点以下桁数<br /><br /> 1..9|  
    |SQL_C_TYPE_TIMESTAMP|19|21..29|  
  
     ただし、SQL_C_TYPE_TIMESTAMP では、データを損失することなく秒の小数部を 3 桁で表すことができる場合で、かつ、列のサイズが 23 以上である場合、ちょうど 3 桁になるように秒の小数部が生成されます。 この動作により、以前の ODBC ドライバーを使用して開発されたアプリケーションの下位互換性が保証されます。  
  
     テーブルの範囲よりサイズが大きい列の場合は、9 桁と見なされます。 この変換では、秒の小数点以下桁数が 9 桁まで許容されます。これは、ODBC で許容される最大桁数です。  
  
     列サイズ 0 は、ODBC では可変長文字型のサイズが無制限であることを意味します (SQL_C_TYPE_TIMESTAMP の 3 桁ルールが適用されなければ 9 桁)。 固定長文字型の列サイズ 0 を指定すると、エラーになります。  
  
-   **該当なし**: 既存[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]と以前の動作が維持されます。  
  
## <a name="see-also"></a>参照  
 [日付と時刻の強化&#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
