---
title: ': _ _Construct |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3ee53aff-6fe4-44cd-a15b-51770c98c712
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 848a06e1b383b1416396111bf4d0e907bfba3568
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2018
ms.locfileid: "42786500"
---
# <a name="pdoconstruct"></a>PDO::__construct
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースへの接続を作成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
PDO::__construct($dsn [,$username [,$password [,$driver_options ]]] )  
```  
  
#### <a name="parameters"></a>パラメーター  
*$dsn*: プレフィックス名 (常に `sqlsrv`)、コロン、および、Server キーワードを含む文字列です。 たとえば、 `"sqlsrv:server=(local)"`のようにします。 オプションで他の接続キーワードを指定することも可能です。 Server キーワードおよびその他の接続キーワードの詳細については、「 [Connection Options](../../connect/php/connection-options.md) 」を参照してください。 *$dsn* は全体が引用符で囲まれているので、各接続キーワードは個別に囲まないようにする必要があります。  
  
*$username*: 省略可です。 ユーザー名を含む文字列です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用して接続する場合、ログイン ID を指定します。 Windows 認証を使用して接続するには、 `""`を指定します。  
  
*$password*: 省略可です。 ユーザー パスワードを含む文字列です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用して接続する場合、パスワードを指定します。 Windows 認証を使用して接続するには、 `""`を指定します。  
  
*$ を指定する*: 省略可能です。 PDO ドライバー マネージャーの属性および [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] に固有のドライバー属性 (PDO::SQLSRV_ATTR_ENCODING、PDO::SQLSRV_ATTR_DIRECT_QUERY) を指定できます。 無効な属性では、例外は生成されません。 無効な属性を [PDO::setAttribute](../../connect/php/pdo-setattribute.md)と共に指定すると、例外が生成されます。  
  
## <a name="return-value"></a>戻り値  
PDO オブジェクトを返します。 失敗した場合は、PDOException オブジェクトを返します。  
  
## <a name="exceptions"></a>例外  
PDOException  
  
## <a name="remarks"></a>Remarks  
インスタンスを null に設定して、接続オブジェクトを閉じることができます。  
  
接続後、pdo::errorcode には 00000 の代わりに 01000 が表示されます。  
  
何らかの理由で PDO::__construct が失敗する場合、PDO::ATTR_ERRMODE が PDO::ERRMODE_SILENT に設定されていても例外がスローされます。  
  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  
  
## <a name="example"></a>例  
この例では、Windows 認証を使用してサーバーに接続し、データベースを指定する方法を示します。  
  
```  
<?php  
   $c = new PDO( "sqlsrv:Server=(local) ; Database = AdventureWorks ", "", "", array(PDO::SQLSRV_ATTR_DIRECT_QUERY => true));   
  
   $query = 'SELECT * FROM Person.ContactType';   
   $stmt = $c->query( $query );   
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ) {   
      print_r( $row );   
   }  
   $c = null;   
?>  
```  
  
## <a name="example"></a>例  
この例では、サーバーへの接続方法を示します。後でデータベースを指定します。  
  
```  
<?php  
   $c = new PDO( "sqlsrv:server=(local)");  
  
   $c->exec( "USE AdventureWorks");  
   $query = 'SELECT * FROM Person.ContactType';  
   $stmt = $c->query( $query );  
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
      print_r( $row );  
   }  
   $c = null;  
?>  
```  
  
## <a name="see-also"></a>参照  
[PDO クラス](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
