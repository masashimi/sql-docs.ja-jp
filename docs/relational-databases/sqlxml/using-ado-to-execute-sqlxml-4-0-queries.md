---
title: SQLXML 4.0 を実行するために ADO を使用してクエリを実行します。マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- query testers [SQLXML]
- test scripts
- ADO [SQLXML]
- queries [SQLXML], ADO
- SQLXML, ADO
ms.assetid: 3d54e3bb-7c5f-427e-82f8-1403a54c4f53
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8e9243bac63901649e1794cdfe2c3d190ebb2435
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43063284"
---
# <a name="using-ado-to-execute-sqlxml-40-queries"></a>ADO を使用した、SQLXML 4.0 クエリの実行
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  以前のバージョンの SQLXML では、SQLXML IIS 仮想ディレクトリと SQLXML ISAPI フィルターを使用して、HTTP ベースのクエリを実行することができました。 SQLXML 4.0 では、重複する類似の機能が [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のネイティブ XML Web サービスに付属しているため、これらのコンポーネントが削除されました。  
  
 SQLXML 4.0 では、代わりに Microsoft Data Access Components (MDAC) 2.6 以降で最初に導入された ADO (ActiveX Data Objects) への SQLXML 拡張を使用して、COM ベースのアプリケーションで SQLXML 4.0 を使用してクエリを実行することができます。  
  
 このトピックでは、Visual Basic Scripting Edition (VBScript) アプリケーション (.vbs ファイル名拡張子を持つスクリプト) の一部として SQLXML と ADO を使用してを示します。 SQLXML 4.0 のドキュメントにあるサンプル クエリを作成しテストするときには、ここで紹介する最初の設定手順を参考にしてください。  
  
## <a name="creating-the-sqlxml-40-test-script"></a>SQLXML 4.0 テスト スクリプトの作成  
 ここでは、VBScript (.vbs) ファイル Sqlxml4test.vbs を作成します。このファイルを使用すると、ADO 2.6 以降の SQLXML ADO 拡張を使用して SQLXML クエリを実行できます。  
  
#### <a name="to-create-the-sqlxml-40-query-tester-using-ado-vbscript"></a>ADO を使用した SQLXML 4.0 クエリのテスト スクリプト (VBScript) を作成するには  
  
1.  次のコードをコピーして、テキスト ファイルに貼り付け、 Sqlxml4test.vbs として保存します。  
  
    ```  
    WScript.Echo "Query process may take a few seconds to complete. Please be patient."  
  
    ' Note that for SQL Server Native Client to be used as the data provider,  
    ' it needs to be installed on the client computer first. Also, SQLXML extensions   
    ' for ADO are used and available in MDAC 2.6 or later.  
  
    'Set script variables.  
    inputFile = "@@FILE_NAME@@"  
    strServer = "@@SERVER_NAME@@"  
    strDatabase = "@@DATABASE_NAME@@"  
    dbGuid = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  
    ' Establish ADO connection to SQL Server and   
    ' create an instance of the ADO Command object.  
    Set conn = CreateObject("ADODB.Connection")  
    Set cmd = CreateObject("ADODB.Command")  
    conn.Open "Provider=SQLXMLOLEDB.4.0;Data Provider=SQLNCLI11;Server=" & strServer & _  
              ";Database=" & strDatabase & ";Integrated Security=SSPI"  
    Set cmd.ActiveConnection = conn  
  
    ' Create the input stream as an instance of the ADO Stream object.  
    Set inStream = CreateObject("ADODB.Stream")  
    inStream.Open  
    inStream.Charset = "utf-8"  
    inStream.LoadFromFile inputFile  
  
    ' Set ADO Command instance to use input stream.  
    Set cmd.CommandStream = inStream  
  
    ' Set the command dialect.  
    cmd.Dialect = dbGuid  
  
    ' Set a second ADO Stream instance for use as a results stream.   
    Set outStream = CreateObject("ADODB.Stream")  
    outStream.Open  
  
    ' Set dynamic properties used by the SQLXML ADO command instance.   
    cmd.Properties("XML Root").Value = "ROOT"  
    cmd.Properties("Output Encoding").Value = "UTF-8"  
  
    ' Connect the results stream to the command instance and execute the command.  
    cmd.Properties("Output Stream").Value = outStream  
    cmd.Execute , , 1024  
  
    ' Echo cropped/partial results to console.  
    WScript.Echo Left(outStream.ReadText, 1023)  
  
    inStream.Close  
    outStream.Close  
    ```  
  
2.  テストするサンプルとテスト環境に合わせて、次のスクリプト値を更新します。  
  
    -   "`@@FILE_NAME@@`" をテンプレート ファイルの名前に置き換えます。  
  
    -   "`@@SERVER_NAME@@`" を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をローカルで実行している場合は "`(local)`" など) に置き換えます。  
  
    -   "`@@DATABASE_NAME@@`" をデータベースの名前 ("`AdventureWorks2012`" や "`tempdb`" など) に置き換えます。  
  
     ローカル コンピューターに作成するサンプル用の具体的な指示に従って、必要であれば他の値も更新します。  
  
3.  ファイルを保存して閉じます。  
  
4.  ローカル コンピューターに作成するサンプル ファイルの一部として、XML テンプレートやスキーマなどの必要な追加ファイルが作成されたことを確認します。 これらのファイルは、テスト スクリプト ファイル (Sqlxml4test.vbs) を保存したディレクトリに置く必要があります。  
  
5.  次に、SQLXML 4.0 テスト スクリプトの使用方法について説明します。  
  
## <a name="using-the-sqlxml-40-test-script"></a>SQLXML 4.0 テスト スクリプトの使用  
 Sqlxml4test.vbs ファイルを使用して、このドキュメントで提供されるサンプル クエリをテストするには、次の手順に従います。  
  
#### <a name="to-use-the-sqlxml-40-query-tester"></a>SQLXML 4.0 クエリのテスト スクリプトの使用  
  
1.  次の方法で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client がインストールされていること確認します。  
  
    1.  **開始** メニューの 作成 をポイント**設定**、 をクリックし、**コントロール パネルの **。  
  
    2.  [コントロール パネル] を開くには**の追加とプログラムの削除**  
  
    3.  現在インストールされているプログラムの一覧であることを確認**Microsoft SQL Server ネイティブ クライアント**リストに表示されます。  
  
        > [!NOTE]  
        >  インストールする必要がある場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ネイティブ クライアントを参照してください[SQL Server ネイティブ クライアントをインストールする](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)です。  
  
2.  クライアント コンピューターにインストールされている MDAC のバージョンが 2.6 以降であることを確認します。 MDAC のバージョン情報を確認する必要がある場合は、MDAC Component Checker ツールを使用します。このツールは Microsoft の Web サイト (www.microsoft.com) から無償でダウンロードできます。 詳細については、Microsoft の Web サイトで "MDAC Component Checker" を検索してください。  
  
3.  スクリプトを実行します。  
  
     VBScript ファイルを実行するには、コマンド ラインで Cscript.exe を指定するか、Sqlxml4test.vbs ファイルをダブルクリックして Windows Script Host (WScript.exe) を呼び出します。  
  
     スクリプトを実行すると、警告メッセージが表示され、返されたクエリの結果を出力として表示するまでには時間がかかる場合があることが示されます。 出力が表示されたら、サンプルの結果例と内容を比較します。  
  
  
