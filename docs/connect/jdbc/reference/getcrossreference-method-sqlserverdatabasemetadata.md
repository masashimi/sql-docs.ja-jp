---
title: getCrossReference メソッド (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getCrossReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 099dd0bf-b017-479d-9696-f5b06f4c6bf9
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 06b89ccbb7884b7f4d3af6aeeedde3d4f25d9ae5
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2018
ms.locfileid: "42786466"
---
# <a name="getcrossreference-method-sqlserverdatabasemetadata"></a>getCrossReference メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  主キー テーブルの主キー列を参照する外部キー テーブルの外部キー列の記述を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.ResultSet getCrossReference(java.lang.String cat1,  
                                            java.lang.String schem1,  
                                            java.lang.String tab1,  
                                            java.lang.String cat2,  
                                            java.lang.String schem2,  
                                            java.lang.String tab2)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *cat1*  
  
 主キーを含むテーブルのカタログ名を格納する**文字列**です。  
  
 *schem1*  
  
 主キーを含むテーブルのスキーマ名を格納する**文字列**です。  
  
 *tab1*  
  
 主キーを含むテーブルのテーブル名を格納する**文字列**です。  
  
 *cat2*  
  
 外部キーを含むテーブルのカタログ名を格納する**文字列**です。  
  
 *schem2*  
  
 外部キーを含むテーブルのスキーマ名を格納する**文字列**です。  
  
 *tab2*  
  
 外部キーを含むテーブルのテーブル名を格納する**文字列**です。  
  
## <a name="return-value"></a>戻り値  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getCrossReference メソッドは、java.sql.DatabaseMetaData インターフェイスで getCrossReference メソッドによって指定されます。  
  
 getCrossReference メソッドによって返される結果セットには、次の情報が含まれます。  
  
|[オブジェクト名]|型|[説明]|  
|----------|----------|-----------------|  
|PKTABLE_CAT|**String**|主キー テーブルを含むカタログの名前です。|  
|PKTABLE_SCHEM|**String**|主キー テーブルのスキーマの名前です。|  
|PKTABLE_NAME|**String**|主キー テーブルの名前です。|  
|PKCOLUMN_NAME|**String**|主キーの列名です。|  
|FKTABLE_CAT|**String**|外部キー テーブルを含むカタログの名前です。|  
|FKTABLE_SCHEM|**String**|外部キー テーブルのスキーマの名前です。|  
|FKTABLE_NAME|**String**|外部キー テーブルの名前です。|  
|FKCOLUMN_NAME|**String**|外部キーの列名です。|  
|KEY_SEQ|**short**|複数列の主キーにおける列のシーケンス番号です。|  
|UPDATE_RULE|**short**|SQL の操作が更新であるとき、外部キーに適用される動作です。 次のいずれかの値を指定できます。<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|DELETE_RULE|**short**|SQL の操作が削除であるとき、外部キーに適用される動作です。 次のいずれかの値を指定できます。<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|FK_NAME|**String**|外部キーの名前です。|  
|PK_NAME|**String**|主キーの名前です。|  
|DEFERRABILITY|**short**|外部キーの制限の評価を、コミット時まで遅延できるかどうかを示します。 次のいずれかの値を指定できます。<br /><br /> importedKeyInitiallyDeferred (5)<br /><br /> importedKeyInitiallyImmediate (6)<br /><br /> importedKeyNotDeferrable (7)|  
  
> [!NOTE]  
>  getCrossReference メソッドによって返されるデータの詳細については、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックの「sp_fkeys (Transact-SQL)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、getCrossReference メソッドを使用して、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] サンプル データベースにおける Person.Contact テーブルと HumanResources.Employee テーブル間の主キーと外部キーの関係に関する情報を返す方法を示します。  
  
```  
public static void executeGetCrossReference(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getCrossReference("AdventureWorks", "Person", "Contact", null, "HumanResources", "Employee");  
      ResultSetMetaData rsmd = rs.getMetaData();  
  
      // Display the result set data.  
      int cols = rsmd.getColumnCount();  
      while(rs.next()) {  
         for (int i = 1; i <= cols; i++) {  
            System.out.println(rs.getString(i));  
         }  
      }  
      rs.close();  
   }   
  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
