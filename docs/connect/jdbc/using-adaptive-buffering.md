---
title: アダプティブ バッファリングの使用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 92d4e3be-c3e9-4732-9a60-b57f4d0f7cb7
caps.latest.revision: 53
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d0a4d3409d9d87bfaca810405e542130a90a471b
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2018
ms.locfileid: "42786117"
---
# <a name="using-adaptive-buffering"></a>アダプティブ バッファリングの使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

アダプティブ バッファリングは、サーバー カーソルのオーバーヘッドを発生させることなく、あらゆる種類の大きな値のデータを取得できるように設計されています。 アプリケーションでは、ドライバーによってサポートされるすべてのバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でアダプティブ バッファリング機能を使用できます。

通常、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] がクエリを実行するときは、すべての結果をサーバーからアプリケーション メモリに取り出します。 この方法では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でのリソースの消費が最小化されますが、非常に大きな結果を生成するクエリの場合は、JDBC アプリケーションで OutOfMemoryError がスローされることがあります。

アプリケーションで非常に大きな結果を処理できるようにするために、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] はアダプティブ バッファリングを提供しています。 ドライバーでアダプティブ バッファリングを使用すると、ステートメントの実行結果を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から取得する処理が、すべて一度にではなく、アプリケーションの必要に応じて行われます。 また、アプリケーションからアクセスできなくなった結果は、ドライバーによって直ちに破棄されます。 アダプティブ バッファリングは次のような場合に効果的です。

- **クエリが非常に大きな結果セットを生成する:** アプリケーションでは、メモリに格納できる行よりも多くの行を生成する SELECT ステートメントを実行できます。 以前のリリースでは、OutOfMemoryError を避けるために、サーバー カーソルを使用する必要がありました。 アダプティブ バッファリングは、サーバー カーソルを使用することなく、任意の大きな結果セットを順方向専用かつ読み取り専用で渡せるようにします。

- **クエリが非常に大きな** [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) **列または** [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) **OUT パラメーター値を生成する:** アプリケーションでは、アプリケーション メモリに完全に含めるには大きすぎる単一の値 (列または OUT パラメーター) を取得できます。 アダプティブ バッファリングはにより、getAsciiStream、getBinaryStream または getCharacterStream メソッドを使用して、ストリームとして、このような値を取得するクライアント アプリケーションです。 アプリケーションは、ストリームから読み取るときと同じようにして、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から値を取得します。

> [!NOTE]  
> アダプティブ バッファリングでは、必要な量のデータだけが、JDBC ドライバーによってバッファリングされます。 ドライバーにバッファーのサイズを制御したり制限したりするためのパブリック メソッドは備わっていません。

## <a name="setting-adaptive-buffering"></a>アダプティブ バッファリングの設定

JDBC Driver 2.0 以降では、ドライバーの既定の動作は "**adaptive**" です。 つまり、アプリケーションから明示的に要求しなくても、アダプティブ バッファリングの動作が適用されます。 ただし、バージョン 1.2 リリースでは、"**full**" が既定のバッファリング モードであるため、アプリケーションから明示的にアダプティブ バッファリング モードを要求する必要があります。

アプリケーションがステートメントの実行でアダプティブ バッファリングを使用するように要求できる方法は 3 つあります。

- アプリケーションは、接続プロパティを設定できる**responseBuffering** "adaptive"にします。 接続プロパティの設定の詳細については、次を参照してください。[接続プロパティの設定](../../connect/jdbc/setting-the-connection-properties.md)します。

- アプリケーションで、[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) オブジェクトの [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md) メソッドを使用して、その [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) オブジェクトを通じて作成されたすべての接続の応答バッファリング モードを設定できます。

- アプリケーションで、[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) クラスの [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) メソッドを使用して、特定のステートメント オブジェクトの応答バッファリング モードを設定できます。

JDBC Driver Version 1.2 を使用している場合、[setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) メソッドを使用するには、Statement オブジェクトを [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) クラスにキャストする必要があります。 コード例では、[読み取り大規模なデータ サンプル](../../connect/jdbc/reading-large-data-sample.md)と[ストアド プロシージャのサンプルを使用して大規模なデータの読み取り](../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md)この古い使用法を示します。

ただし、JDBC ドライバー Version 2.0 では、実装されているクラス階層を意識することなく、[isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) メソッドおよび [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) メソッドを使用して、ベンダー固有の機能にアクセスできます。 コード例を参照してください、[大規模なデータ サンプルの更新](../../connect/jdbc/updating-large-data-sample.md)トピック。

## <a name="retrieving-large-data-with-adaptive-buffering"></a>アダプティブ バッファリングによる大きなデータの取得

get\<Type>Stream メソッドを使用して大きな値を 1 回読み取り、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって返された順序で ResultSet 列および CallableStatement OUT パラメーターにアクセスする場合、アダプティブ バッファリングにより、結果を処理するときのアプリケーション メモリの使用量を最小限に抑えることができます。 アダプティブ バッファリングを使用すると、次のようになります。

- [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) クラスおよび [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) クラスで定義されている get\<Type>Stream メソッドは、既定では 1 回だけ読み取るストリームを返します。ただし、アプリケーションによってマークされていれば、このストリームをリセットできます。 アプリケーションでストリームの `reset` を行う必要がある場合、まずそのストリームに対して `mark` メソッドを呼び出す必要があります。

- [SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md) クラスおよび [SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md) クラスで定義されている get\<Type>Stream メソッドは、`mark` メソッドを呼び出すことなく、常にストリームの開始位置に位置を変更できるストリームを返します。

アプリケーションでアダプティブ バッファリングを使用する場合、get\<Type>Stream メソッドによって取得される値は、1 回だけ取得できます。 同じオブジェクトの get\<Type>Stream メソッドを呼び出した後に、同じ列またはパラメーターで任意の get\<Type>Stream メソッドを呼び出すと、"このデータはアクセスされており、この列またはパラメーターに対しては使用できません" という意味のメッセージで例外がスローされます。

> [!NOTE]
> 結果セットの処理の途中で ResultSet.close() への呼び出しには、Microsoft JDBC Driver for SQL Server を読み取って、残りのすべてのパケットを破棄が必要です。 クエリには、大規模なデータ セットが返された場合、およびネットワーク接続速度が遅い場合は特に、かなりの時間がかかります。

## <a name="guidelines-for-using-adaptive-buffering"></a>アダプティブ バッファリングを使用するうえでのガイドライン

アプリケーションによるメモリ使用量を最小限に抑えるには、開発者は次の重要なガイドラインに従う必要があります。

- アプリケーションが非常に大きな結果セットを処理できるようにするために、接続文字列プロパティ **selectMethod=cursor** を使用しないようにします。 アダプティブ バッファリング機能を使用すると、アプリケーションがサーバー カーソルを使用することなく、非常に大きな順方向専用の読み取り専用結果セットを処理することが可能になります。 **selectMethod=cursor** を設定する場合、その接続で生成された順方向専用、読み取り専用のすべての結果セットに影響が及ぶ点に注意してください。 つまり、わずかな行数の短い結果セットを定期的に処理するようなアプリケーションでは、結果セットごとにサーバー カーソルを作成し、読み取って、閉じる操作を繰り返すことになって、クライアント側とサーバー側の両方でリソース消費が (**selectMethod** を **cursor** に設定しなかった場合と比較して) 増えることになります。

- 大きなテキストまたはバイナリ値を getBlob または getClob メソッドではなく、getAsciiStream、getBinaryStream または getCharacterStream メソッドを使用してストリームとして読み取ります。 Version 1.2 リリース以降の [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) クラスには、この目的のための新しい get\<Type>Stream メソッドがあります。

- 大きな値を含む可能性がある列は、SELECT ステートメント内で列リストの最後に配置し、[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) の get\<Type>Stream メソッドを使用して、選択された順序で列にアクセスします。

- 大きな値を含む可能性がある OUT パラメーターは、[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) の作成に使用する SQL のパラメーターの一覧の最後で宣言します。 また、[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) の get\<Type>Stream メソッドを使用して、宣言された順序で OUT パラメーターにアクセスします。

- 同じ接続で複数のステートメントを同時に実行しないでください。 前のステートメントの結果を処理する前に別のステートメントを実行すると、処理されない結果がアプリケーションのメモリにバッファリングされることがあります。

- いくつかあります。 を使用した**selectMethod = カーソル**の代わりに**responseBuffering = adaptive**など、より便利になります。

  - 読み取り専用の結果セットを使用して入力すると、ユーザーはいくつかの後の行ごとの読み取りなどの時間がかかり、順方向専用、アプリケーションが処理する場合**selectMethod = カーソル**の代わりに**responseBuffering = adaptive**可能性がありますによるリソース使用量を減らす[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。

  - 同じ接続で順方向専用、読み取り専用の複数の結果セットを同時に処理するようなアプリケーションでは、**responseBuffering=adaptive** の代わりに **selectMethod=cursor** を使用することで、ドライバーがこれらの結果セットを処理する際に必要となるメモリ量を減らすことができます。

  どちらのケースも、サーバー カーソルを作成し、読み取って、閉じるという処理のオーバーヘッドを考慮する必要があります。

スクロール可能な結果セットと順方向専用の更新可能な結果セットの推奨事項を以下に補足します。

- スクロール可能な結果セット : 行をブロック単位でフェッチする場合、常に [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) メソッドで指定された行数がメモリに読み込まれます。これは、アダプティブ バッファリングが有効になっていたとしても変わりません。 スクロールによって OutOfMemoryError が発生した場合は、フェッチされる行数を減らすことによって対処できます。フェッチ サイズの行数を減らすには、[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) メソッドを呼び出します。必要であれば、行数を 1 に設定することも検討してください。 それでも OutOfMemoryError を回避できない場合は、あまり大きな列がスクロール可能な結果セットに含まれないようにします。

- 順方向専用の更新可能な結果セット: 行をブロック単位でフェッチする場合、その接続でアダプティブ バッファリングが有効になっていたとしても、通常は [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) メソッドで指定された行数がメモリに読み込まれます。 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの [next](../../connect/jdbc/reference/next-method-sqlserverresultset.md) メソッドを呼び出すと OutOfMemoryError が発生する場合は、フェッチされる行数を減らすことによって対処できます。フェッチ サイズの行数を減らすには、[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) メソッドを呼び出します。必要であれば、行数を 1 に設定することも検討してください。 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトの [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) メソッドを "**adaptive**" パラメーターで呼び出した後、ステートメントを実行することによって、行のバッファリングを強制的に抑制することもできます。 結果セットはスクロールできないため、アプリケーションから、いずれかの get\<Type>Stream メソッドで大きな列の値にアクセスした場合、アプリケーションが読み取りを始めると直ちに、ドライバーが、順方向専用、読み取り専用の結果セットの場合とまったく同じように、その値を破棄します。

## <a name="see-also"></a>参照

[JDBC ドライバーによるパフォーマンスと信頼性の強化](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
