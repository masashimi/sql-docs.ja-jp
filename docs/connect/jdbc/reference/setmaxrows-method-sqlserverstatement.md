---
title: setMaxRows メソッド (SQLServerStatement) |Microsoft Docs
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
- SQLServerStatement.setMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cccc0667-589b-4655-8ea8-14ae8b2eb9dc
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 292eb65a07cea177804bb2685147b05dd4cc961e
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785108"
---
# <a name="setmaxrows-method-sqlserverstatement"></a>setMaxRows メソッド (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  任意の [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトが含むことのできる最大行数の制限が、渡された数値に設定されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setMaxRows(int max)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *max*  
  
 最大行数を示す **int** です。制限しない場合は 0 です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この setMaxRows メソッドは、java.sql.Statement インターフェイスの setMaxRows メソッドによって指定されます。  
  
 この setMaxRows メソッドは、スクロール可能な動的カーソルには影響しません。 大きな結果セットから行が返される可能性がある場合に、返される行数を制限するには、アプリケーションで SELECT TOP N SQL 構文を使用してください。  
  
 setMaxRows メソッドが呼び出されると、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] ではアプリケーションのクエリの実行時に SET ROWCOUNT SQL ステートメントが実行されます。 これにより、そのクエリによって返される行の数だけでなく、そのクエリで実行されるすべての [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントによって影響を受ける行の最大数も JDBC ドライバーによって制限されます。 アプリケーションで最上位の [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトに対してのみ制限を設定する必要がある場合は、setMaxRows メソッドではなく、SELECT TOP N SQL 構文をクエリで使用してください。  
  
 SET ROWCOUNT SQL ステートメントの詳細については、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックの「[SET ROWCOUNT (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=139522)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
