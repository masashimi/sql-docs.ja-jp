---
title: Detail プロパティを使用したエラー処理 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-exception-handling
ms.suite: pro-bi
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- exceptions [Reporting Services], Detail property
- Detail property
- InnerText property
ms.assetid: 4392633d-b46b-41e6-bc12-efb64e166704
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ffab4097077a95dada228f816a9b0daf79c20fdf
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2018
ms.locfileid: "43280448"
---
# <a name="using-the-detail-property-to-handle-specific-errors"></a>Detail プロパティを使用したエラー処理
  例外を細かく分類するために、[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] によって、SOAP 例外の **Detail** プロパティの子要素の **InnerText** プロパティにある追加のエラー情報が返されます。 **Detail** プロパティは **XmlNode** オブジェクトであるため、次のコードを使って **Message** 子要素の内部テキストにアクセスできます。  
  
 **Detail** プロパティに含まれる有効なすべての子要素の一覧については、「[Detail プロパティ](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)」を参照してください。 詳細については、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK ドキュメントの「Detail プロパティ」を参照してください。  
  
```vb  
Try  
' Code for accessing the report server  
Catch ex As SoapException  
   ' The exception is a SOAP exception, so use  
   ' the Detail property's Message element.  
   Console.WriteLine(ex.Detail("Message").InnerXml)  
End Try  
```  
  
```csharp  
try  
{  
   // Code for accessing the report server  
}  
catch (SoapException ex)  
{  
   // The exception is a SOAP exception, so use  
   // the Detail property's Message element.  
   Console.WriteLine(ex.Detail["Message"].InnerXml);  
}  
```  
  
```vb  
Try  
' Code for accessing the report server  
Catch ex As SoapException  
   If ex.Detail("ErrorCode").InnerXml = "rsInvalidItemName" Then  
   End If ' Perform an action based on the specific error code  
End Try  
```  
  
```csharp  
try  
{  
   // Code for accessing the report server  
}  
catch (SoapException ex)  
{  
   if (ex.Detail["ErrorCode"].InnerXml == "rsInvalidItemName")  
   {  
      // Perform an action based on the specific error code  
   }  
}  
```  
  
 次のコード行によって、SOAP 例外で返される特定のエラー コードがコンソールに書き込まれます。 また、エラー コードを評価して特定のアクションを実行することもできます。  
  
```vb  
Console.WriteLine(ex.Detail("ErrorCode").InnerXml)  
```  
  
```csharp  
Console.WriteLine(ex.Detail["ErrorCode"].InnerXml);  
```  
  
## <a name="see-also"></a>参照  
 [Reporting Services における例外処理の概要](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException クラス](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [SoapException エラー テーブル](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md)  
  
  
