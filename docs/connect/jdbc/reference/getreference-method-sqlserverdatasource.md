---
title: getReference メソッド (SQLServerDataSource) |Microsoft Docs
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
- SQLServerDataSource.getReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b3fb1a97-86ee-4977-adca-c35ae199dbb3
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6a34933b8f210e7591da73bb3f9a44bc67246dd7
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785960"
---
# <a name="getreference-method-sqlserverdatasource"></a>getReference メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) オブジェクトへの参照が返されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public javax.naming.Reference getReference()  
```  
  
## <a name="return-value"></a>戻り値  
 参照オブジェクト。  
  
## <a name="remarks"></a>Remarks  
 この getReference メソッドは、javax.naming.Referenceable インターフェイスの getReference メソッドによって指定されます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 がリリースされる前は、SQLServerDataSource オブジェクトの SQLServerDataSource.setTrustStorePassword が呼び出された場合、対応するパスワードが、SQLServerDataSource.getReference から返されるオブジェクトに内包される形で開示され、結果、そのオブジェクトを使用することによって、別の接続を確立することが可能でした。 JDBC Driver 3.0 では、SQLServerDataSource.getReference から返されたオブジェクトにパスワードを設定してから、そのオブジェクトとの接続を確立する必要があります。  
  
 また、SQLServerDataSource.setTrustStorePassword を設定してから、データ ソースのプロパティをバインドする場合は、SQLServerDataSource.setTrustStorePassword を呼び出してから接続を取得する必要があります。 例を次に示します。  
  
```  
ctx = new InitialContext(System.getProperties());  
  
SQLServerDataSource ds1 = (SQLServerDataSource) ctx.lookup(jndiName);  
  
ds1.setTrustStorePassword("XXXXX");  
Connection con = ds1.getConnection("user", "XXXXXX");  
  
ctx.rebind(jndiName, ds1);  
SQLServerDataSource ds2 = (SQLServerDataSource) ctx.lookup(jndiName);  
ds2.setTrustStorePassword("XXXXX");   // reset the truststore password  
con = ds2.getConnection("user", "XXXXXX");   // provide userid and password again  
```  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
