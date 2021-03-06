---
title: XML 一括読み込みの例 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- overflow-field annotation
- ConnectionCommand property
- XMLFragment property
- relationship chains [SQLXML]
- multiple table bulk loading
- examples [SQLXML], XML Bulk Load
- overflow data [SQLXML]
- sql:datatype
- transaction mode [SQLXML]
- CheckConstraints property
- sql:overflow-field
- XML Bulk Load [SQLXML], examples
- TempFilePath property
- datatype annotation
- Transaction property
- KeepIdentity property
- Execute method
- streaming XML data
- xml data type [SQL Server], SQLXML
- bulk load [SQLXML], examples
ms.assetid: 970e4553-b41d-4a12-ad50-0ee65d1f305d
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c95ad1c22b7a54156d1a3ef602c4f015263f5161
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43079594"
---
# <a name="xml-bulk-load-examples-sqlxml-40"></a>XML 一括読み込みの例 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  以下の例では、Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の XML 一括読み込み機能について示します。 それぞれの例では、XSD スキーマと、同等の XDR スキーマを提供します。  
  
## <a name="bulk-loader-script-validateandbulkloadvbs"></a>一括読み込みスクリプト (ValidateAndBulkload.vbs)  
 次のスクリプトで記述された、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript)、XML DOM に XML ドキュメントを読み込みます; スキーマに対して検証するためと、ドキュメントが有効で実行、XML 一括ロードする負荷に XML を[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]テーブル。 このスクリプトは、後に示す個々の例で使用できます。  
  
> [!NOTE]  
>  XML 一括読み込みでは、データ ファイルから内容がアップロードされなくても警告またはエラーは返されません。 このため、一括読み込み操作を実行する前に XML データ ファイルを検証することをお勧めします。  
  
```vbs  
Dim FileValid  
  
set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=MyServer;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
  
'Validate the data file prior to bulkload  
Dim sOutput   
sOutput = ValidateFile("SampleXMLData.xml", "", "SampleSchema.xml")  
WScript.Echo sOutput  
  
If FileValid Then  
   ' Check constraints and initiate transaction (if needed)  
   ' objBL.CheckConstraints = True  
   ' objBL.Transaction=True  
  'Execute XML bulkload using file.  
  objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
  set objBL=Nothing  
End If  
  
Function ValidateFile(strXmlFile,strUrn,strXsdFile)  
  
   ' Create a schema cache and add SampleSchema.xml to it.  
   Dim xs, fso, sAppPath  
   Set fso = CreateObject("Scripting.FileSystemObject")   
   Set xs = CreateObject("MSXML2.XMLSchemaCache.6.0")  
   sAppPath = fso.GetFolder(".")   
   xs.Add strUrn, sAppPath & "\" & strXsdFile  
  
   ' Create an XML DOMDocument object.  
   Dim xd   
   Set xd = CreateObject("MSXML2.DOMDocument.6.0")  
  
   ' Assign the schema cache to the DOM document.  
   ' schemas collection.  
   Set xd.schemas = xs  
  
   ' Load XML document as DOM document.  
   xd.async = False  
   xd.Load sAppPath & "\" & strXmlFile  
  
   ' Return validation results in message to the user.  
   If xd.parseError.errorCode <> 0 Then  
        ValidateFile = "Validation failed on " & _  
             strXmlFile & vbCrLf & _  
             "=======" & vbCrLf & _  
             "Reason: " & xd.parseError.reason & _  
             vbCrLf & "Source: " & _  
             xd.parseError.srcText & _  
             vbCrLf & "Line: " & _  
             xd.parseError.Line & vbCrLf  
             FileValid = False  
    Else  
        ValidateFile = "Validation succeeded for " & _  
             strXmlFile & vbCrLf & _  
             "========" & _  
             vbCrLf & "Contents to be bulkloaded" & vbCrLf  
             FileValid = True  
    End If  
End Function  
```  
  
## <a name="a-bulk-loading-xml-in-a-table"></a>A. 単一テーブルでの XML の一括読み込み  
 この例は、のインスタンスへの接続を確立します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ConnectionString プロパティ (MyServer) で指定されています。 この例では、ErrorLogFile プロパティも指定します。 エラー出力は指定したファイル ("C:\error.log") に保存されます。ファイルの保存場所は変更することもできます。 マッピング スキーマ ファイル (SampleSchema.xml) と XML データ ファイル (SampleXMLData.xml) の両方に、Execute メソッドがパラメーターとして持つことにも注意してください。 一括読み込みが実行される場合で作成した Cust テーブル**tempdb**データベースは、XML データ ファイルの内容に基づいて新しいレコードが格納されます。  
  
#### <a name="to-test-a-sample-bulk-load"></a>一括読み込みのサンプルをテストするには  
  
1.  次のテーブルを作成します。  
  
    ```sql  
    CREATE TABLE Cust(CustomerID  int PRIMARY KEY,  
                      CompanyName varchar(20),  
                      City        varchar(20));  
    GO  
    ```  
  
2.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleSchema.xml として保存します。 このファイルに次の XSD スキーマを追加します。  
  
    ```xml  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
       <xsd:element name="ROOT" sql:is-constant="1" >  
         <xsd:complexType>  
           <xsd:sequence>  
             <xsd:element name="Customers" sql:relation="Cust" maxOccurs="unbounded">  
               <xsd:complexType>  
                 <xsd:sequence>  
                   <xsd:element name="CustomerID"  type="xsd:integer" />  
                   <xsd:element name="CompanyName" type="xsd:string" />  
                   <xsd:element name="City"        type="xsd:string" />  
                 </xsd:sequence>  
               </xsd:complexType>  
             </xsd:element>  
           </xsd:sequence>  
          </xsd:complexType>  
         </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleXMLData.xml として保存します。 このファイルには、次の XML ドキュメントを追加します。  
  
    ```xml  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Sean Chai</CompanyName>  
        <City>New York</City>  
      </Customers>  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Tom Johnston</CompanyName>  
         <City>Los Angeles</City>  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Institute of Art</CompanyName>  
        <City>Chicago</City>  
      </Customers>  
    </ROOT>  
    ```  
  
4.  任意のテキスト エディターまたは XML エディターでファイルを作成し、ValidateAndBulkload.vbs として保存します。 このファイルに、このトピックの冒頭で示した VBScript コードを追加します。 接続文字列は、適切なサーバー名に変更します。 Execute メソッドにパラメーターとして指定されているファイルの適切なパスを指定します。  
  
5.  VBScript コードを実行します。 XML 一括読み込みによって、XML が Cust テーブルに読み込まれます。  
  
 これは、同等の XDR スキーマです。  
  
```xml  
  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers"  sql:relation="Cust" >  
      <element type="CustomerID"  sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City"        sql:field="City" />  
  
   </ElementType>  
</Schema>  
```  
  
## <a name="b-bulk-loading-xml-data-in-multiple-tables"></a>B. 複数テーブルでの XML データの一括読み込み  
 XML ドキュメントから成る、この例では、 **\<顧客 >** と**\<順序 >** 要素。  
  
```xml  
<ROOT>  
  <Customers>  
    <CustomerID>1111</CustomerID>  
    <CompanyName>Sean Chai</CompanyName>  
    <City>NY</City>  
    <Order OrderID="1" />  
    <Order OrderID="2" />  
  </Customers>  
  <Customers>  
    <CustomerID>1112</CustomerID>  
    <CompanyName>Tom Johnston</CompanyName>  
     <City>LA</City>    
    <Order OrderID="3" />  
  </Customers>  
  <Customers>  
    <CustomerID>1113</CustomerID>  
    <CompanyName>Institute of Art</CompanyName>  
    <Order OrderID="4" />  
  </Customers>  
</ROOT>  
```  
  
 この例の一括では、2 つのテーブルに XML データを読み込みます**Cust**と**CustOrder**:  
  
-   Cust (CustomerID、CompanyName、City)  
  
-   CustOrder (OrderID、CustomerID)  
  
 次の XSD スキーマでは、これらのテーブルの XML ビューが定義されています。 スキーマ間の親子リレーションシップを指定します、 **\<顧客 >** と**\<順序 >** 要素。  
  
```xml  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="ROOT" sql:is-constant="1" >  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Customers" sql:relation="Cust" >  
          <xsd:complexType>  
            <xsd:sequence>  
              <xsd:element name="CustomerID"  type="xsd:integer" />  
              <xsd:element name="CompanyName" type="xsd:string" />  
              <xsd:element name="City"        type="xsd:string" />  
              <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
                <xsd:complexType>  
                  <xsd:attribute name="OrderID" type="xsd:integer" />  
                </xsd:complexType>  
              </xsd:element>  
             </xsd:sequence>  
          </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 主キー/外部キー リレーションシップ間上記で指定した XML 一括読み込みで、  **\<Cust >** と **\<CustOrder >** を一括要素は、両方のテーブルにデータを読み込む.  
  
#### <a name="to-test-a-sample-bulk-load"></a>一括読み込みのサンプルをテストするには  
  
1.  2 つのテーブルを作成する**tempdb**データベース。  
  
    ```sql  
    USE tempdb;  
    CREATE TABLE Cust(  
           CustomerID  int PRIMARY KEY,  
           CompanyName varchar(20),  
           City        varchar(20));  
    CREATE TABLE CustOrder(        OrderID     int PRIMARY KEY,   
            CustomerID int FOREIGN KEY REFERENCES Cust(CustomerID));  
    ```  
  
2.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleSchema.xml として保存します。 このファイルに、この例で示した XSD スキーマを追加します。  
  
3.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleData.xml として保存します。 このファイルに、この例で前に示した XML ドキュメントを追加します。  
  
4.  任意のテキスト エディターまたは XML エディターでファイルを作成し、ValidateAndBulkload.vbs として保存します。 このファイルに、このトピックの冒頭で示した VBScript コードを追加します。 接続文字列は、適切なサーバー名とデータベース名に変更します。 Execute メソッドにパラメーターとして指定されているファイルの適切なパスを指定します。  
  
5.  上の VBScript コードを実行します。 XML 一括読み込みによって、XML ドキュメントが Cust テーブルと CustOrder テーブルに読み込まれます。  
  
 これは、同等の XDR スキーマです。  
  
```xml  
  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust" >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
<sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
</Schema>  
```  
  
## <a name="c-using-chain-relationships-in-the-schema-to-bulk-load-xml"></a>C. スキーマでチェーン リレーションシップを使用して XML の一括読み込みを行う  
 この例では、XML 一括読み込みにおいて、マッピング スキーマで指定されている M:N リレーションシップを使用し、M:N リレーションシップを表すテーブルにデータを読み込む方法を示します。  
  
 たとえば、次の XSD スキーマを考えてみます。  
  
```xml  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrderOD"  
          parent="Ord"  
          parent-key="OrderID"  
          child="OrderDetail"  
          child-key="OrderID" />  
  
    <sql:relationship name="ODProduct"  
          parent="OrderDetail"  
          parent-key="ProductID"  
          child="Product"  
          child-key="ProductID"   
          inverse="true"/>  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="ROOT" sql:is-constant="1" >  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Ord"   
                     sql:key-fields="OrderID" >  
          <xsd:complexType>  
            <xsd:sequence>  
             <xsd:element name="Product"  
                          sql:relation="Product"   
                          sql:key-fields="ProductID"  
                          sql:relationship="OrderOD ODProduct">  
               <xsd:complexType>  
                 <xsd:attribute name="ProductID" type="xsd:int" />  
                 <xsd:attribute name="ProductName" type="xsd:string" />  
               </xsd:complexType>  
             </xsd:element>  
           </xsd:sequence>  
           <xsd:attribute name="OrderID"   type="xsd:integer" />   
           <xsd:attribute name="CustomerID"   type="xsd:string" />  
         </xsd:complexType>  
       </xsd:element>  
      </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 スキーマを指定します、 **\<順序 >** を持つ要素を**\<製品 >** 子要素。 **\<順序 >** 要素は、Ord テーブルにマップし、 **\<製品 >** 要素は、データベースの Product テーブルにマップされます。 指定されたチェーン リレーションシップでは、 **\<製品 >** 要素は、OrderDetail テーブルで表される M:N リレーションシップを識別します。 つまり、1 つの注文には複数の製品が含まれ、1 つの製品は複数の注文に含まれるという関係です。  
  
 このスキーマで XML ドキュメントの一括読み込みを行うと、Ord テーブル、Product テーブル、および OrderDetail テーブルにレコードが追加されます。  
  
#### <a name="to-test-a-working-sample"></a>実際のサンプルをテストするには  
  
1.  次の 3 つのテーブルを作成します。  
  
    ```sql  
    CREATE TABLE Ord (  
             OrderID     int  PRIMARY KEY,  
             CustomerID  varchar(5));  
    GO  
    CREATE TABLE Product (  
             ProductID   int PRIMARY KEY,  
             ProductName varchar(20));  
    GO  
    CREATE TABLE OrderDetail (  
           OrderID     int FOREIGN KEY REFERENCES Ord(OrderID),  
           ProductID   int FOREIGN KEY REFERENCES Product(ProductID),  
                       CONSTRAINT OD_key PRIMARY KEY (OrderID, ProductID));  
    GO  
    ```  
  
2.  この例の最初で提供されているスキーマを SampleSchema.xml として保存します。  
  
3.  次のサンプル XML データを SampleXMLData.xml として保存します。  
  
    ```xml  
    <ROOT>    
      <Order OrderID="1" CustomerID="ALFKI">  
        <Product ProductID="1" ProductName="Chai" />  
        <Product ProductID="2" ProductName="Chang" />  
      </Order>  
      <Order OrderID="2" CustomerID="ANATR">  
        <Product ProductID="3" ProductName="Aniseed Syrup" />  
        <Product ProductID="4" ProductName="Gumbo Mix" />  
      </Order>  
    </ROOT>  
    ```  
  
4.  任意のテキスト エディターまたは XML エディターでファイルを作成し、ValidateAndBulkload.vbs として保存します。 このファイルに、このトピックの冒頭で示した VBScript コードを追加します。 接続文字列は、適切なサーバー名とデータベース名に変更します。 この例のソース コードで、次の行のコメント指定をはずします。  
  
    ```vbs  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    ```  
  
5.  VBScript コードを実行します。 XML 一括読み込みによって、XML ドキュメントが Ord テーブルと Product テーブルに読み込まれます。  
  
## <a name="d-bulk-loading-in-identity-type-columns"></a>D. ID 型の列に一括読み込みを行う  
 この例では、一括読み込みでの ID 型列の扱いについて説明します。 この例では、3 つのテーブル (Ord、Product、OrderDetail) にデータの一括読み込みが行われます。  
  
 これらのテーブルには、次の条件が設定されています。  
  
-   Ord テーブルの OrderID は ID 型の列です。  
  
-   Product テーブルの ProductID は ID 型の列です。  
  
-   OrderDetail の OrderID および ProductID 列は、Ord テーブルおよび Product テーブル内の対応する主キー列を参照する外部キー列です。  
  
 この例のテーブル スキーマを次に示します。  
  
```  
Ord (OrderID, CustomerID)  
Product (ProductID, ProductName)  
OrderDetail (OrderID, ProductID)  
```  
  
 この XML 一括読み込みの例で、一括読み込みオブジェクト モデルの KeepIdentity プロパティが false に設定します。 このため、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、Product テーブルおよび Ord テーブルの ProductID 列および OrderID 列に ID 値がそれぞれ生成されます。一括読み込みの対象ドキュメントで指定されている値は無視されます。  
  
 この場合、XML 一括読み込みでは、テーブル間の主キー/外部キーのリレーションシップが識別されます。 一括読み込みでは、主キーのあるテーブルにレコードが挿入された後、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で生成された ID 値が、外部キー列のあるテーブルに格納されます。 次の XML 一括読み込みの例では、次の順序でテーブルにデータが挿入されます。  
  
1.  Product  
  
2.  Ord  
  
3.  OrderDetail  
  
    > [!NOTE]  
    >  この処理ロジックでは、Products テーブルと Orders テーブルで生成された ID 値を後で OrderDetails テーブルに挿入できるよう、XML 一括読み込みによってこれらの値が保持されます。 これにはまず、XML 一括読み込みで中間テーブルが作成され、このテーブルにデータが格納されます。格納された値は、後で削除されます。  
  
#### <a name="to-test-a-working-sample"></a>実際のサンプルをテストするには  
  
1.  これらのテーブルを作成します。  
  
    ```  
    CREATE TABLE Ord (  
             OrderID     int identity(1,1)  PRIMARY KEY,  
             CustomerID  varchar(5));  
    GO  
    CREATE TABLE Product (  
             ProductID   int identity(1,1) PRIMARY KEY,  
             ProductName varchar(20));  
    GO  
    CREATE TABLE OrderDetail (  
           OrderID     int FOREIGN KEY REFERENCES Ord(OrderID),  
           ProductID   int FOREIGN KEY REFERENCES Product(ProductID),  
                       CONSTRAINT OD_key PRIMARY KEY (OrderID, ProductID));  
    GO  
    ```  
  
2.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleSchema.xml として保存します。 このファイルには、この XSD スキーマを追加します。  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
     <xsd:annotation>  
       <xsd:appinfo>  
        <sql:relationship name="OrderOD"  
              parent="Ord"  
              parent-key="OrderID"  
              child="OrderDetail"  
              child-key="OrderID" />  
        <sql:relationship name="ODProduct"  
              parent="OrderDetail"  
              parent-key="ProductID"  
              child="Product"  
              child-key="ProductID"   
              inverse="true"/>  
       </xsd:appinfo>  
     </xsd:annotation>  
  
      <xsd:element name="Order" sql:relation="Ord"   
                                sql:key-fields="OrderID" >  
       <xsd:complexType>  
         <xsd:sequence>  
            <xsd:element name="Product" sql:relation="Product"   
                         sql:key-fields="ProductID"  
                         sql:relationship="OrderOD ODProduct">  
              <xsd:complexType>  
                 <xsd:attribute name="ProductID" type="xsd:int" />  
                 <xsd:attribute name="ProductName" type="xsd:string" />  
              </xsd:complexType>  
            </xsd:element>  
         </xsd:sequence>  
            <xsd:attribute name="OrderID"   type="xsd:integer" />   
            <xsd:attribute name="CustomerID"   type="xsd:string" />  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleXMLData.xml として保存します。 次の XML ドキュメントを追加します。  
  
    ```  
    <ROOT>    
      <Order OrderID="11" CustomerID="ALFKI">  
        <Product ProductID="11" ProductName="Chai" />  
        <Product ProductID="22" ProductName="Chang" />  
      </Order>  
      <Order OrderID="22" CustomerID="ANATR">  
         <Product ProductID="33" ProductName="Aniseed Syrup" />  
        <Product ProductID="44" ProductName="Gumbo Mix" />  
      </Order>  
    </ROOT>  
    ```  
  
4.  任意のテキスト エディターまたは XML エディターでファイルを作成し、ValidateAndBulkload.vbs として保存します。 このファイルに次の VBScript コードを追加します。 接続文字列は、適切なサーバー名とデータベース名に変更します。 パラメーターとして使用されるファイルの適切なパスを指定、 **Execute**メソッド。  
  
    ```  
    Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "C:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction = False  
    objBL.KeepIdentity = False  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    Set objBL = Nothing  
    MsgBox "Done."  
    ```  
  
5.  VBScript コードを実行します。 XML 一括読み込みによって、適切なテーブルにデータが読み込まれます。  
  
## <a name="e-generating-table-schemas-before-bulk-loading"></a>E. 一括読み込み前にテーブル スキーマを生成する  
 一括読み込み前にテーブルが存在しない場合、XML 一括読み込みでテーブルを作成するように指定できます。 この TRUE に SQLXMLBulkLoad オブジェクトの SchemaGen プロパティを設定します。 また、必要に応じて、既存のテーブルを削除して再 SGDropTables プロパティを TRUE に設定して作成するための XML 一括読み込みを要求できます。 次の VBScript の例では、これらのプロパティの使用法を示します。  
  
 また、この例では、これらの他に次の 2 つのプロパティを TRUE に設定します。  
  
-   CheckConstraints です。 : このプロパティを TRUE に設定すると、テーブルに指定されている制約違反が、テーブルに挿入されるデータによって発生するのを回避できます。この場合の制約は、Cust テーブルと CustOrder テーブル間に指定されている PRIMARY KEY/FOREIGN KEY 制約です。 制約違反が発生すると、一括読み込みは失敗します。  
  
-   XMLFragment します。 : サンプル XML ドキュメント (データ ソース) はフラグメントであり、単一の最上位要素が含まれていません。したがって、このプロパティを TRUE に設定する必要があります。  
  
 この VBScript コードは次のとおりです。  
  
```  
Dim objBL   
Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
  
objBL.CheckConstraints=true  
objBL.XMLFragment = True  
objBL.SchemaGen = True  
objBL.SGDropTables = True  
  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
Set objBL = Nothing  
```  
  
#### <a name="to-test-a-working-sample"></a>実際のサンプルをテストするには  
  
1.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleSchema.xml として保存します。 このファイルに、前の例「スキーマでチェーン リレーションシップを使用して XML の一括読み込みを行う」で示した XSD スキーマを追加します。  
  
2.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleXMLData.xml として保存します。 このファイルに、前の例「スキーマでチェーン リレーションシップを使用して XML の一括読み込みを行う」で示した XML ドキュメントを追加します。 削除、\<ルート > (フラグメントになります) をドキュメントからの要素。  
  
3.  任意のテキスト エディターまたは XML エディターでファイルを作成し、ValidateAndBulkload.vbs として保存します。 このファイルに、この例で示した VBScript コードを追加します。 接続文字列は、適切なサーバー名とデータベース名に変更します。 Execute メソッドにパラメーターとして指定されているファイルの適切なパスを指定します。  
  
4.  VBScript コードを実行します。 XML 一括読み込みによって、指定されたマッピング スキーマを基に必要なテーブルが作成され、このテーブルにデータの一括読み込みが行われます。  
  
## <a name="f-bulk-loading-from-a-stream"></a>F. ストリームから一括読み込みを行う  
 XML 一括読み込みオブジェクト モデルの Execute メソッドは、2 つのパラメーターを受け取ります。 最初のパラメーターはマッピング スキーマ ファイルであり、 もう 1 つのパラメーターは、データベースに読み込まれる XML データを指定するものです。 XML 一括読み込みの Execute メソッドに XML データを渡す 2 つの方法はあります。  
  
-   ファイル名をパラメーターとして指定する。  
  
-   XML データを含むストリームを渡す。  
  
 この例では、ストリームから一括読み込みを行う方法を示します。  
  
 VBScript はまず SELECT ステートメントが実行され、Northwind データベースの Customers テーブルから顧客情報が取得されます。 SELECT ステートメントには、FOR XML 句 (と ELEMENTS オプション) が指定されているため、クエリを実行すると、次の形式の、要素中心の XML ドキュメントが返されます。  
  
```  
<Customer>  
  <CustomerID>..</CustomerID>  
  <CompanyName>..</CompanyName>  
  <City>..</City>  
</Customer>  
...  
```  
  
 スクリプト、XML ストリームとしてに渡します Execute メソッドの 2 番目のパラメーターとして。 Execute メソッドの大部分は、Cust テーブルにデータを読み込みます。  
  
 このスクリプトは、TRUE を SchemaGen プロパティと SGDropTables プロパティを TRUE に設定ため、XML 一括読み込みは、指定されたデータベースに Cust テーブルを作成します。 テーブルが存在する場合は、最初にテーブルが削除された後に再作成されます。  
  
 この VBScript の例を次に示します。  
  
```  
Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
Set objCmd = CreateObject("ADODB.Command")  
Set objConn = CreateObject("ADODB.Connection")  
Set objStrmOut = CreateObject ("ADODB.Stream")  
  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile     = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.SchemaGen        = True  
objBL.SGDropTables     = True  
objBL.XMLFragment      = True  
' Open a connection to the instance of SQL Server to get the source data.  
  
objConn.Open "provider=SQLOLEDB;server=(local);database=tempdb;integrated security=SSPI"  
Set objCmd.ActiveConnection = objConn  
objCmd.CommandText = "SELECT CustomerID, CompanyName, City FROM Customers FOR XML AUTO, ELEMENTS"  
  
' Open the return stream and execute the command.  
Const adCRLF = -1  
Const adExecuteStream = 1024  
objStrmOut.Open  
objStrmOut.LineSeparator = adCRLF  
objCmd.Properties("Output Stream").Value = objStrmOut  
objCmd.Execute , , adExecuteStream  
objStrmOut.Position = 0  
  
' Execute bulk load. Read source XML data from the stream.  
objBL.Execute "SampleSchema.xml", objStrmOut  
  
Set objBL = Nothing  
```  
  
 次の XSD マッピング スキーマでは、テーブルの作成に必要な情報が指定されます。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:element name="ROOT" sql:is-constant="true" >  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element ref="Customers"/>  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
<xsd:element name="Customers" sql:relation="Cust" >  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element name="CustomerID"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(5)"/>  
      <xsd:element name="CompanyName"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(40)"/>  
      <xsd:element name="City"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(40)"/>  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
</xsd:schema>  
```  
  
 XDR スキーマの場合は次のようになります。  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
    </ElementType>  
</Schema>  
```  
  
### <a name="opening-a-stream-on-an-existing-file"></a>既存のファイルのストリームを開く  
 既存の XML データ ファイルのストリームを開き、(ファイル名をパラメーターとして渡す) ではなく、Execute メソッドにパラメーターとして、ストリームを渡すことができますも。  
  
 ストリームをパラメーターとして渡す Visual Basic の例を次に示します。  
  
```  
Private Sub Form_Load()  
Dim objBL As New SQLXMLBulkLoad  
Dim objStrm As New ADODB.Stream  
Dim objFileSystem As New Scripting.FileSystemObject  
Dim objFile As Scripting.TextStream  
  
MsgBox "Begin BulkLoad..."  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.SchemaGen = True  
objBL.SGDropTables = True  
' Here again a stream is specified that contains the source data   
' (instead of the file name). But this is just an illustration.  
' Usually this is useful if you have an XML data   
' stream that is created by some other means that you want to bulk   
' load. This example starts with an XML text file, so it may not be the   
' best to use a stream (you can specify the file name directly).  
' Here you could have specified the file name itself.   
Set objFile = objFileSystem.OpenTextFile("c:\SampleData.xml")  
objStrm.Open  
objStrm.WriteText objFile.ReadAll  
objStrm.Position = 0  
objBL.Execute "c:\SampleSchema.xml", objStrm  
  
Set objBL = Nothing  
MsgBox "Done."  
End Sub  
```  
  
 アプリケーションをテストするには、次の XML ドキュメントをファイル (SampleData.xml) に保存し、この例で提供されている XSD スキーマと共に使用します。  
  
 XML ソース データ (SampleData.xml) は次のとおりです。  
  
```  
<ROOT>  
  <Customers>  
    <CustomerID>1111</CustomerID>  
    <CompanyName>Hanari Carnes</CompanyName>  
    <City>NY</City>  
    <Order OrderID="1" />  
    <Order OrderID="2" />  
  </Customers>  
  
  <Customers>  
    <CustomerID>1112</CustomerID>  
    <CompanyName>Toms Spezialitten</CompanyName>  
     <City>LA</City>  
    <Order OrderID="3" />  
  </Customers>  
  <Customers>  
    <CustomerID>1113</CustomerID>  
    <CompanyName>Victuailles en stock</CompanyName>  
    <Order CustomerID= "4444" OrderID="4" />  
</Customers>  
</ROOT>  
```  
  
 これは、同等の XDR スキーマです。  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
             <sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
</Schema>  
```  
  
## <a name="g-bulk-loading-in-overflow-columns"></a>G. オーバーフロー列に一括読み込みを行う  
 マッピング スキーマが使用して、オーバーフロー列を指定するかどうか、 **sql:overflow-フィールド**注釈、XML 一括読み込みは、この列に、ソース ドキュメントからすべての未使用データをコピーします。  
  
 この XSD スキーマを検討してください。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  <xsd:element name="Customers" sql:relation="Cust"  
                                sql:overflow-field="OverflowColumn" >  
   <xsd:complexType>  
     <xsd:sequence>  
       <xsd:element name="CustomerID"  type="xsd:integer" />  
       <xsd:element name="CompanyName" type="xsd:string" />  
       <xsd:element name="City"        type="xsd:string" />  
       <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
         <xsd:complexType>  
          <xsd:attribute name="OrderID" type="xsd:integer" />  
          <xsd:attribute name="CustomerID" type="xsd:integer" />  
         </xsd:complexType>  
       </xsd:element>  
     </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 このスキーマでは、Cust テーブルにオーバーフロー列 (OverflowColumn) が指定されています。 その結果、すべての未使用 XML データの各**\<顧客 >** 要素は、この列に追加されます。  
  
> [!NOTE]  
>  すべての abstract 要素 (要素の**抽象 ="true"** が指定されて)、すべての属性が禁止されています (対象の属性**禁止されています ="true"** が指定されて) XML の一括でオーバーフローと解釈ロード テストとは、指定されている場合は、オーバーフロー列に追加されます。 それ以外の場合は無視されます。  
  
#### <a name="to-test-a-working-sample"></a>実際のサンプルをテストするには  
  
1.  2 つのテーブルを作成する**tempdb**データベース。  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust (  
                  CustomerID     int         PRIMARY KEY,  
                  CompanyName    varchar(20) NOT NULL,  
                  City           varchar(20) DEFAULT 'Seattle',  
                  OverflowColumn nvarchar(200));  
    GO  
    CREATE TABLE CustOrder (  
                  OrderID    int PRIMARY KEY,  
                  CustomerID int FOREIGN KEY   
                                 REFERENCES Cust(CustomerID));  
    GO  
    ```  
  
2.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleSchema.xml として保存します。 このファイルに、この例で示した XSD スキーマを追加します。  
  
3.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleXMLData.xml として保存します。 このファイルに次の XML ドキュメントを追加します。  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City><![CDATA[NY]]> </City>  
        <Junk>garbage in overflow</Junk>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
      </Customers>  
  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Toms Spezialitten</CompanyName>  
         <![CDATA[LA]]>   
        <!-- <xyz><address>111 Maple, Seattle</address></xyz>   -->  
        <Order OrderID="3" />  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
    </Customers>  
    </ROOT>  
    ```  
  
4.  任意のテキスト エディターまたは XML エディターでファイルを作成し、ValidateAndBulkload.vbs として保存します。 このファイルに次の Microsoft Visual Basic Scripting Edition (VBScript) コードを追加します。 接続文字列は、適切なサーバー名とデータベース名に変更します。 Execute メソッドにパラメーターとして指定されているファイルの適切なパスを指定します。  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  VBScript コードを実行します。  
  
 これは、同等の XDR スキーマです。  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"   
                       sql:overflow-field="OverflowColumn"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
             <sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
</Schema>  
```  
  
## <a name="h-specifying-the-file-path-for-temp-files-in-transaction-mode"></a>H. トランザクション モードで一時ファイル用のファイル パスを指定する  
 トランザクション モードで一括読み込みを行うときに (つまり、トランザクションのプロパティ設定されている場合に TRUE)、設定することも必要があります TempFilePath プロパティが true で、次の条件のいずれかの場合。  
  
-   リモート サーバーに一括読み込みを行う。  
  
-   トランザクション モードで作成される一時ファイルの格納に、TEMP 環境変数で指定されているパスとは別のローカル ドライブまたはフォルダーを使用する。  
  
 たとえば、次の VBScript コードでは、SampleXMLData.xml ファイルからデータベース テーブルに、トランザクション モードでデータの一括読み込みが行われます。 TempFilePath プロパティを指定するには、トランザクション モードで生成される一時ファイルのパスを設定しています。  
  
```  
set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.Transaction=True  
objBL.TempFilePath="\\Server\MyDir"  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
set objBL=Nothing  
```  
  
> [!NOTE]  
>  一時ファイルのパスは、対象の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスのサービス アカウントと、一括読み込みアプリケーションを実行するアカウントからの共有アクセスが可能な場所にする必要があります。 ローカル サーバーに一括読み込みでない限り、一時ファイルのパスが UNC パスを指定する必要があります (など\\\servername\sharename)。  
  
#### <a name="to-test-a-working-sample"></a>実際のサンプルをテストするには  
  
1.  このテーブルを作成**tempdb**データベース。  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust (     CustomerID uniqueidentifier,   
          LastName  varchar(20));  
    GO  
    ```  
  
2.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleSchema.xml として保存します。 次の XSD スキーマをファイルに追加します。  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
  
      <xsd:element name="Customers" sql:relation="Cust" >  
       <xsd:complexType>  
         <xsd:attribute name="CustomerID"  type="xsd:string" />  
         <xsd:attribute name="LastName" type="xsd:string" />  
       </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleXMLData.xml として保存します。 このファイルに次の XML ドキュメントを追加します。  
  
    ```  
    <ROOT>  
    <Customers CustomerID="6F9619FF-8B86-D011-B42D-00C04FC964FF"   
               LastName="Smith" />  
    </ROOT>  
    ```  
  
4.  任意のテキスト エディターまたは XML エディターでファイルを作成し、ValidateAndBulkload.vbs として保存します。 このファイルに次の VBScript コードを追加します。 接続文字列は、適切なサーバー名とデータベース名に変更します。 Execute メソッドにパラメーターとして指定されているファイルの適切なパスを指定します。 また、TempFilePath プロパティの適切なパスを指定します。  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    objBL.TempFilePath="\\server\folder"  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  VBScript コードを実行します。  
  
     スキーマは、対応するを指定する必要があります**sql:datatype**の**CustomerID**ときに属性の値は、 **CustomerID**中かっこ ({が含まれる GUID として指定されますおよび}) など。  
  
    ```  
    <ROOT>  
    <Customers CustomerID="{6F9619FF-8B86-D011-B42D-00C04FC964FF}"   
               LastName="Smith" />  
    </ROOT>  
    ```  
  
     これは、更新されたスキーマです。  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
  
      <xsd:element name="Customers" sql:relation="Cust" >  
       <xsd:complexType>  
         <xsd:attribute name="CustomerID"  type="xsd:string"   
                        sql:datatype="uniqueidentifier" />  
         <xsd:attribute name="LastName" type="xsd:string" />  
       </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
     ときに**sql:datatype**として列の型を識別する指定**uniqueidentifier**、一括読み込み操作は、中かっこを削除します ({および}) から、 **CustomerID**値列に挿入します。  
  
 これは、同等の XDR スキーマです。  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
<ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
</ElementType>  
<ElementType name="Customers" sql:relation="Cust" >  
  <AttributeType name="CustomerID"  sql:datatype="uniqueidentifier" />  
  <AttributeType name="LastName"   />  
  
  <attribute type="CustomerID" />  
  <attribute type="LastName"   />  
</ElementType>  
</Schema>  
```  
  
## <a name="i-using-an-existing-database-connection-with-the-connectioncommand-property"></a>I. 既存のデータベース接続で ConnectionCommand プロパティを使用する  
 既存の ADO 接続を使用して、XML の一括読み込みを行うことができます。 これは、データ ソースに実行する多くの操作のうちの 1 つとして XML 一括読み込みを行う場合に便利です。  
  
 ConnectionCommand プロパティでは、ADO コマンド オブジェクトを使用して既存の ADO 接続を使用することができます。 この Visual Basic の例を次に示します。  
  
```  
Private Sub Form_Load()  
Dim objBL As New SQLXMLBulkLoad4  
Dim objCmd As New ADODB.Command  
Dim objConn As New ADODB.Connection  
  
'Open a connection to an instance of SQL Server.  
objConn.Open "provider=SQLOLEDB;data source=(local);database=tempdb;integrated security=SSPI"  
'Ask the Command object to use the connection just established.  
Set objCmd.ActiveConnection = objConn  
  
'Tell Bulk Load to use the active command object that is using the Connection obj.  
objBL.ConnectionCommand = objCmd  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
'The Transaction property must be set to True if you use ConnectionCommand.  
objBL.Transaction = True  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
Set objBL = Nothing  
End Sub  
```  
  
#### <a name="to-test-a-working-sample"></a>実際のサンプルをテストするには  
  
1.  2 つのテーブルを作成する**tempdb**データベース。  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust(  
                   CustomerID   varchar(5) PRIMARY KEY,  
                   CompanyName  varchar(30),  
                   City         varchar(20));  
    GO  
    CREATE TABLE CustOrder(  
                   CustomerID  varchar(5) references Cust (CustomerID),  
                   OrderID     varchar(5) PRIMARY KEY);  
    GO  
    ```  
  
2.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleSchema.xml として保存します。 次の XSD スキーマをファイルに追加します。  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
    <xsd:annotation>  
      <xsd:appinfo>  
        <sql:relationship name="CustCustOrder"  
              parent="Cust"  
              parent-key="CustomerID"  
              child="CustOrder"  
              child-key="CustomerID" />  
      </xsd:appinfo>  
    </xsd:annotation>  
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
      <xsd:element name="Customers" sql:relation="Cust" >  
       <xsd:complexType>  
         <xsd:sequence>  
           <xsd:element name="CustomerID"  type="xsd:integer" />  
           <xsd:element name="CompanyName" type="xsd:string" />  
           <xsd:element name="City"        type="xsd:string" />  
           <xsd:element name="Order"   
                              sql:relation="CustOrder"  
                              sql:relationship="CustCustOrder" >  
             <xsd:complexType>  
              <xsd:attribute name="OrderID" type="xsd:integer" />  
              <xsd:attribute name="CustomerID" type="xsd:integer" />  
             </xsd:complexType>  
           </xsd:element>  
         </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleXMLData.xml として保存します。 このファイルに次の XML ドキュメントを追加します。  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City>NY</City>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
      </Customers>  
  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Toms Spezialitten</CompanyName>  
         <City>LA</City>  
        <Order OrderID="3" />  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
    </Customers>  
    </ROOT>  
    ```  
  
4.  Visual Basic (標準 EXE) アプリケーションと、上のコードを作成し、 プロジェクトに次の参照を追加します。  
  
    ```  
    Microsoft XML BulkLoad for SQL Server 4.0 Type Library  
    Microsoft ActiveX Data objects 2.6 Library  
    ```  
  
5.  アプリケーションを実行します。  
  
 これは、同等の XDR スキーマです。  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
         <sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
</Schema>  
```  
  
## <a name="j-bulk-loading-in-xml-data-type-columns"></a>J. xml データ型の列に一括読み込みを行う  
 マッピング スキーマが指定されている場合、 [xml データ型](../../../t-sql/xml/xml-transact-sql.md)列を使用して、 **sql:datatype ="xml"** 注釈、XML 一括読み込みはこれにソース ドキュメントからマップされたフィールドの XML 子要素をコピーすることができます列です。  
  
 次の XSD スキーマを考えてみます。この XSD スキーマでは、サンプル データベース AdventureWorks の Production.ProductModel テーブルのビューがマップされます。 このテーブルでの CatalogDescription フィールド**xml**データ型にマッピングされますが、  **\<Desc >** 要素を使用して、 **sql:field**と**sql:データ型"xml"を =** 注釈。  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
           xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
           xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">   
  <xsd:element name="ProductModel"  sql:relation="Production.ProductModel" >  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Name" type="xs:string"></xsd:element>  
        <xsd:element name="Desc" sql:field="CatalogDescription" sql:datatype="xml">  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element name="ProductDescription">  
              <xsd:complexType>  
                <xsd:sequence>  
                  <xsd:element name="Summary" type="xs:anyType"/>  
                </xsd:sequence>  
              </xsd:complexType>  
            </xsd:element>  
          </xsd:sequence>  
        </xsd:complexType>  
        </xsd:element>   
     </xsd:sequence>  
     <xsd:attribute name="ProductModelID" sql:field="ProductModelID" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
#### <a name="to-test-a-working-sample"></a>実際のサンプルをテストするには  
  
1.  サンプル データベース AdventureWorks がインストールされていることを確認します。  
  
2.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleSchema.xml として保存します。 このファイルに上の XSD スキーマをコピーして貼り付け、ファイルを保存します。  
  
3.  任意のテキスト エディターまたは XML エディターでファイルを作成し、SampleXMLData.xml として保存します。 このファイルに次の XML ドキュメントをコピーして貼り付け、前の手順と同じフォルダーに保存します。  
  
    ```  
    <ProductModel ProductModelID="2005">  
        <Name>Mountain-100 (2005 model)</Name>  
        <Desc><?xml-stylesheet href="ProductDescription.xsl" type="text/xsl"?>  
            <p1:ProductDescription xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
                  xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"   
                  xmlns:wf="http://www.adventure-works.com/schemas/OtherFeatures"   
                  xmlns:html="http://www.w3.org/1999/xhtml"   
                  xmlns="">  
                <p1:Summary>  
                    <html:p>Our top-of-the-line competition mountain bike.   
          Performance-enhancing options include the innovative HL Frame,   
          super-smooth front suspension, and traction for all terrain.  
                            </html:p>  
                </p1:Summary>  
                <p1:Manufacturer>  
                    <p1:Name>AdventureWorks</p1:Name>  
                    <p1:Copyright>2002-2005</p1:Copyright>  
                    <p1:ProductURL>HTTP://www.Adventure-works.com</p1:ProductURL>  
                </p1:Manufacturer>  
                <p1:Features>These are the product highlights.   
                     <wm:Warranty>  
                        <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
                        <wm:Description>parts and labor</wm:Description>  
                    </wm:Warranty><wm:Maintenance>  
                        <wm:NoOfYears>10 years</wm:NoOfYears>  
                        <wm:Description>maintenance contract available through your dealer or any AdventureWorks retail store.</wm:Description>  
                    </wm:Maintenance><wf:wheel>High performance wheels.</wf:wheel><wf:saddle>  
                        <html:i>Anatomic design</html:i> and made from durable leather for a full-day of riding in comfort.</wf:saddle><wf:pedal>  
                        <html:b>Top-of-the-line</html:b> clipless pedals with adjustable tension.</wf:pedal><wf:BikeFrame>Each frame is hand-crafted in our Bothell facility to the optimum diameter   
          and wall-thickness required of a premium mountain frame.   
          The heat-treated welded aluminum frame has a larger diameter tube that absorbs the bumps.</wf:BikeFrame><wf:crankset> Triple crankset; alumunim crank arm; flawless shifting. </wf:crankset></p1:Features>  
                <!-- add one or more of these elements... one for each specific product in this product model -->  
                <p1:Picture>  
                    <p1:Angle>front</p1:Angle>  
                    <p1:Size>small</p1:Size>  
                    <p1:ProductPhotoID>118</p1:ProductPhotoID>  
                </p1:Picture>  
                <!-- add any tags in <specifications> -->  
                <p1:Specifications> These are the product specifications.  
                       <Material>Almuminum Alloy</Material><Color>Available in most colors</Color><ProductLine>Mountain bike</ProductLine><Style>Unisex</Style><RiderExperience>Advanced to Professional riders</RiderExperience></p1:Specifications>  
            </p1:ProductDescription>  
        </Desc>  
    </ProductModel>  
    ```  
  
4.  任意のテキスト エディターまたは XML エディターでファイルを作成し、BulkloadXml.vbs として保存します。 このファイルに次の VBScript コードをコピーして貼り付け、 前の XML データ ファイルとスキーマ ファイルを保存したフォルダーに保存します。  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=MyServer;database=AdventureWorks;integrated security=SSPI"  
  
    Dim fso, sAppPath  
    Set fso = CreateObject("Scripting.FileSystemObject")   
    sAppPath = fso.GetFolder(".")   
  
    objBL.ErrorLogFile = sAppPath & "\error.log"  
  
    'Execute XML bulkload using file.  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  スクリプト BulkloadXml.vbs を実行します。  
  
  
