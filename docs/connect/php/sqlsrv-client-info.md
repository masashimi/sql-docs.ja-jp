---
title: "sqlsrv_client_info |Microsoft ドキュメント"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- sqlsrv_client_info
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_client_info
- sqlsrv_client_info
ms.assetid: 3e2d3679-436a-45d8-8bdc-7c633b65a720
caps.latest.revision: 47
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 491e88383643747ccd43aa5a171fffd326347528
ms.contentlocale: ja-jp
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvclientinfo"></a>sqlsrv_client_info
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

接続とクライアントの履歴に関する情報を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
sqlsrv_client_info( resource $conn)  
```  
  
#### <a name="parameters"></a>パラメーター  
*$conn*: クライアントが接続する接続リソースです。  
  
## <a name="return-value"></a>戻り値  
次の表で説明するキーを持つ連想配列、また接続リソースが null の場合、 **false** です。  
  
**PHP for SQL Server バージョン 3.2 および 3.1 用**:  
  
|[キー]|説明|  
|-------|---------------|  
|DriverDllName|MSODBCSQL11.DLL (SQL Server 用 ODBC Driver 11)|  
|DriverODBCVer|ODBC version (xx.yy)|  
|DriverVer|次の SQL Server DLL バージョン用 ODBC Driver 11:<br /><br />xx.yy.zzzz ([!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]バージョン 3.2 または 3.1)|  
|ExtensionVer|次の php_sqlsrv.dll バージョン:<br /><br />3.2.xxxx.x (の[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]バージョン 3.2)<br /><br />3.1.xxxx.x (の[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]バージョン 3.1)|  
  
**PHP for SQL Server バージョン 3.0 および 2.0 用**:  
  
|[キー]|説明|  
|-------|---------------|  
|DriverDllName|SQLNCLI10 です。DLL ([!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]バージョン 2.0)|  
|DriverODBCVer|ODBC version (xx.yy)|  
|DriverVer|次の SQL Server Native Client DLL バージョン:<br /><br />10.50.xxx ([!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]バージョン 2.0)|  
|ExtensionVer|次の php_sqlsrv.dll バージョン:<br /><br />2.0.xxxx.x ([!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]バージョン 2.0)|  
  
## <a name="example"></a>例  
次の例では、コマンドラインからこの例を実行すると、クライアント情報がコンソールに書き込まれます。 この例では、SQL Server がローカル コンピューターにインストールされていることを前提にしています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$conn = sqlsrv_connect( $serverName);  
  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
if( $client_info = sqlsrv_client_info( $conn))  
{  
       foreach( $client_info as $key => $value)  
      {  
              echo $key.": ".$value."\n";  
      }  
}  
else  
{  
       echo "Client info error.\n";  
}  
  
/* Close connection resources. */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>参照  
[SQLSRV ドライバー API リファレンス](../../connect/php/sqlsrv-driver-api-reference.md)  
[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)  
  
