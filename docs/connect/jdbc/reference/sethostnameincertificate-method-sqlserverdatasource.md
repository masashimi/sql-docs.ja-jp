---
title: setHostNameInCertificate メソッド (SQLServerDataSource) |Microsoft Docs
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
- setHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- setHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 2bcf4f2e-a103-4374-abc4-ffad4ce8e3c0
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 673ccc44b53898e56da29c2a46df5467233c7fa2
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784740"
---
# <a name="sethostnameincertificate-method-sqlserverdatasource"></a>setHostNameInCertificate メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の SSL (Secure Sockets Layer) 証明書の検証に使用されるホスト名が設定されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setHostNameInCertificate(java.lang.String hostNameInCertificate)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *hostNameInCertificate*  
  
 ホスト名を含む**文字列**です。  
  
## <a name="remarks"></a>Remarks  
 hostNameInCertificate 値を使用して、通信レイヤーが SSL で暗号化されているときに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の SSL 証明書を検証します。 既定値は、null です。  
  
 hostNameInCertificate プロパティが null に設定されているか、またはそれが指定されていない場合、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] では、serverName プロパティ値を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の SSL 証明書に対して検証が行われます。 hostNameInCertificate プロパティが任意の文字列または空の文字列 "" に設定されている場合、ドライバーはその値を使用してサーバーの SSL 証明書を検証します。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
