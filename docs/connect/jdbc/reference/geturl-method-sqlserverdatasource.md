---
title: getURL メソッド (SQLServerDataSource) |Microsoft ドキュメント
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
- SQLServerDataSource.getURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dd0d5d2c-91fe-4b0f-a162-69d898ba176e
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0a506fbfd0c35ae57d2d027724b4d671092398de
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32838907"
---
# <a name="geturl-method-sqlserverdatasource"></a>getURL メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データ ソースへの接続に使用する URL を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.String getURL()  
```  
  
## <a name="return-value"></a>戻り値  
 A**文字列**URL を格納しています。  
  
## <a name="remarks"></a>解説  
 セキュリティ上の理由から、含める必要はありません、パスワードが指定された URL で、 [setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)メソッドです。 これは、サードパーティの Java アプリケーション サーバーでは、データ ソースの構成用ユーザー インターフェイスに、URL プロパティの値セットが表示されることが非常に多いためです。 代わりに、使用、 [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)パスワードの値を設定します。 Java アプリケーション サーバーで、データ ソース内に設定されたパスワードが構成用ユーザー インターフェイスに表示されなくなります。  
  
> [!NOTE]  
>  GetURL メソッドを呼び出す前に、setURL メソッドが呼び出されない場合 getURL、既定値を返しますの"jdbc:sqlserver://"です。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
