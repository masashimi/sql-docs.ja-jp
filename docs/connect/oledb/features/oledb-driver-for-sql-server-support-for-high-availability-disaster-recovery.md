---
title: OLE DB Driver for SQL Server の高可用性、ディザスター リカバリーに関するサポート | Microsoft Docs
description: OLE DB Driver for SQL Server の高可用性、ディザスター リカバリーに関するサポート
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: ac2a123be5557069964edaddf0a3d6234fba6d19
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43027528"
---
# <a name="ole-db-driver-for-sql-server-support-for-high-availability-disaster-recovery"></a>OLE DB Driver for SQL Server の高可用性、ディザスター リカバリーに関するサポート
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  この記事では、SQL Server のサポートの OLE DB ドライバーをについて説明します (で追加された[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]) の[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]します。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の詳細については、「[可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)」、「[可用性グループの作成と構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)」、「[フェールオーバー クラスタリングと AlwaysOn 可用性グループ &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)」、および「[アクティブなセカンダリ: 読み取り可能なセカンダリ レプリカ &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)」を参照してください。  
  
 接続文字列で、特定の可用性グループの可用性グループ リスナーを指定できます。 フェールオーバーする可用性グループ内のデータベースに OLE DB Driver for SQL Server アプリケーションが接続されている場合、元の接続が切断されるため、フェールオーバー後にアプリケーションが動作を継続するには新しい接続を開く必要があります。  
  
 可用性グループ リスナーに接続しておらず、ホスト名に複数の IP アドレスが関連付けられている場合、OLE DB Driver for SQL Server では DNS エントリに関連付けられているすべての IP アドレスが順次繰り返し処理されます。 DNS サーバーが最初に返した IP アドレスがネットワーク インターフェイス カード (NIC) にバインドされていない場合、この処理に時間がかかる可能性があります。 可用性グループ リスナーに接続している場合、OLE DB Driver for SQL Server では同時にすべての IP アドレスとの間で接続の確立が試行されます。接続試行が成功した場合、ドライバーでは未解決の試行がすべて破棄されます。  
  
> [!NOTE]  
> 接続タイムアウト値を大きくし、接続再試行ロジックを実装することにより、アプリケーションが可用性グループに接続する確立が高まります。 また、可用性グループのフェールオーバーにより接続が失敗する可能性があるため、接続再試行ロジックを実装して、再接続されるまで、失敗した接続の再接続を試行する必要があります。  
  
## <a name="connecting-with-multisubnetfailover"></a>MultiSubnetFailover を使用した接続  
 SQL Server Always On 可用性グループ リスナーまたは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスに接続する際には、必ず **MultiSubnetFailover=Yes** を指定してください。 **MultiSubnetFailover** を使用することで、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のすべての Always On 可用性グループおよびフェールオーバー クラスター インスタンスに対して高速フェールオーバーが有効化され、単一サブネットおよびマルチサブネットの AlwaysOn トポロジにおけるフェールオーバー時間が大幅に短縮されます。 マルチサブネット フェールオーバーの際には、クライアントは複数の接続を並列で試行します。 サブネットのフェールオーバー中に OLE DB Driver for SQL Server は TCP 接続を再試行します。  
  
 **MultiSubnetFailover** 接続プロパティを指定すると、アプリケーションが可用性グループまたはフェールオーバー クラスター インスタンスに配置され、OLE DB Driver for SQL Server ではすべての IP アドレスに対して接続を試行することで、プライマリ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス上のデータベースに接続が試行されます。 接続に対して **MultiSubnetFailover=Yes** を指定した場合、クライアントは、オペレーティング システムの既定の TCP 再送信間隔より短い間隔で TCP 接続を再試行します。 これにより、Always On 可用性グループまたはフェールオーバー クラスター インスタンスのフェールオーバー後、再接続されるまでの時間を短縮することができます。単一サブネットとマルチサブネットの可用性グループ インスタンスおよびフェールオーバー クラスター インスタンスに適用することができます。  
  
 接続文字列キーワードの詳細については、「[OLE DB Driver for SQL Server での接続文字列キーワードの使用](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)」を参照してください。  
  
 可用性グループ リスナーまたはフェールオーバー クラスター インスタンス以外に接続するときに **MultiSubnetFailover=Yes** を指定するとパフォーマンスが低下する可能性があるため、このような指定はサポートされていません。  
  
 可用性グループまたはフェールオーバー クラスター インスタンス内のサーバーに接続する際には、次のガイドラインに従います。  
  
-   単一サブネットまたはマルチサブネットに接続する場合に **MultiSubnetFailover** 接続プロパティを使用すると、パフォーマンスを向上させることができます。  
  
-   可用性グループに接続するには、接続文字列でサーバーとして、可用性グループの可用性グループ リスナーを指定します。  
  
-   64 個を超える数の IP アドレスが構成された [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスに接続すると、接続エラーが発生します。  
  
-   **MultiSubnetFailover** 接続プロパティを使用するアプリケーションの動作は、認証の種類 ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証、Kerberos 認証、または Windows 認証) の影響を受けません。  
  
-   **loginTimeout** の値を増やすことで、フェールオーバー時間に対応し、アプリケーションの接続試行回数を減らすことができます。  
  
-   分散トランザクションはサポートされていません。  
  
読み取り専用のルーティングが無効である場合、次の状況では可用性グループのセカンダリ レプリカの場所には接続できません。  
  
1.  セカンダリ レプリカの場所が、接続を許可するように構成されていない。  
  
2.  アプリケーションに **ApplicationIntent=ReadWrite** (後述します) が使用されているが、セカンダリ レプリカの場所が読み取り専用アクセスとして構成されている。  
  
プライマリ レプリカが読み取り専用ワークロードを拒否するように構成されているとき、接続文字列に **ApplicationIntent=ReadOnly** が含まれていると、接続は失敗します。  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>データベース ミラーリングの使用からマルチサブネット クラスターの使用へのアップグレード  
接続文字列に **MultiSubnetFailover** および **Failover_Partner** の接続キーワードが存在する場合、接続エラーが発生します。 また、**MultiSubnetFailover** が使用されているとき、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] から、データベース ミラーリング ペアに属していることを示すフェールオーバー パートナー応答が返された場合にも、エラーが発生します。  
  
現在、データベース ミラーリングを使用している OLE DB Driver for SQL Server アプリケーションをマルチサブネットのシナリオにアップグレードする場合、**Failover_Partner** 接続プロパティを削除して **MultiSubnetFailover** に置き換え、それを **Yes** に設定し、接続文字列内のサーバー名を可用性グループ リスナーの名前に置き換えます。 接続文字列で **Failover_Partner** および **MultiSubnetFailover=Yes** が使用されている場合、ドライバーでエラーが発生します。 ただし、接続文字列に **Failover_Partner** と **MultiSubnetFailover=No** (または **ApplicationIntent=ReadWrite**) が使用されている場合、アプリケーションはデータベース ミラーリングを使用します。  
  
ドライバーは、可用性グループのプライマリ データベースでデータベース ミラーリングが使用されている場合、および可用性グループ リスナーではなくプライマリ データベースに接続する接続文字列内で **MultiSubnetFailover=Yes** が使用されている場合、エラーを返します。  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="ole-db"></a>OLE DB (OLE DB)  
両方をサポートする、OLE DB Driver for SQL Server、 **ApplicationIntent**と**MultiSubnetFailover**キーワード。   
  
2 つの OLE DB 接続文字列キーワードがサポートするために追加された[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]OLE DB driver for SQL Server:  
  
-   **ApplicationIntent** 
-   **MultiSubnetFailover**  
  
 SQL Server 用の OLE DB ドライバーの接続文字列キーワードの詳細については、次を参照してください。 [OLE DB Driver for SQL Server での接続文字列キーワードの使用](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)します。  

### <a name="application-intent"></a>アプリケーションの目的 

対応する接続プロパティは次のとおりです。  
  
-   **SSPROP_INIT_APPLICATIONINTENT**  
  
-   **DBPROP_INIT_PROVIDERSTRING**  
  
OLE DB Driver for SQL Server アプリケーションは、アプリケーションの目的を指定するのに方法のいずれかを使用できます。  
  
 -   **IDBInitialize::Initialize**  
 **IDBInitialize::Initialize** は、あらかじめ構成された一連のプロパティを使用して、データ ソースを初期化し、データ ソース オブジェクトを作成します。 アプリケーション インテントは、プロバイダーのプロパティとして指定するか、拡張プロパティ文字列の一部として指定します。  
  
 -   **IDataInitialize::GetDataSource**  
 **IDataInitialize::GetDataSource** は **Application Intent** キーワードを格納できる入力接続文字列を受け取ります。  
  
 -   **IDBProperties::SetProperties**  
 **ApplicationIntent** プロパティ値を設定するには、**IDBProperties::SetProperties** を呼び出して、"**ReadWrite**" または "**ReadOnly**" の値で **SSPROP_INIT_APPLICATIONINTENT** プロパティを渡すか、または "**ApplicationIntent=ReadOnly**" または "**ApplicationIntent=ReadWrite**" を含む値で **DBPROP_INIT_PROVIDERSTRING** プロパティを渡します。  
  
アプリケーション インテントは、**[データ リンク プロパティ]** ダイアログ ボックスの [すべて] タブの [アプリケーション インテントのプロパティ] フィールドで指定できます。  
  
暗黙的な接続が確立された場合、その接続には、親の接続のアプリケーション インテント設定が使用されます。 同様に、同じデータ ソースから作成されたセッションはいずれも、そのデータ ソースのアプリケーション インテント設定を継承します。  
  
### <a name="multisubnetfailover"></a>MultiSubnetFailover

対応する接続プロパティは次のとおりです。  
  
-   **SSPROP_INIT_MULTISUBNETFAILOVER**  
  
-   **DBPROP_INIT_PROVIDERSTRING**  

OLE DB Driver for SQL Server アプリケーションは、MultiSubnetFailover オプションを設定するのに、次のメソッドのいずれかを使用できます。  

 -   **IDBInitialize::Initialize**  
 **IDBInitialize::Initialize** は、あらかじめ構成された一連のプロパティを使用して、データ ソースを初期化し、データ ソース オブジェクトを作成します。 アプリケーション インテントは、プロバイダーのプロパティとして指定するか、拡張プロパティ文字列の一部として指定します。  
  
 -   **IDataInitialize::GetDataSource**  
 **IDataInitialize::GetDataSource** は **MultiSubnetFailover** キーワードを格納できる入力接続文字列を受け取ります。  

-   **IDBProperties::SetProperties**  
設定する、 **MultiSubnetFailover**プロパティ値、呼び出し**idbproperties::setproperties**を渡して、 **SSPROP_INIT_MULTISUBNETFAILOVER** の値を持つプロパティ**VARIANT_TRUE**または**VARIANT_FALSE**または**DBPROP_INIT_PROVIDERSTRING**プロパティ値が含まれている"**MultiSubnetFailover = Yes**「または」**MultiSubnetFailover = No**"。

#### <a name="example"></a>例

```
DBPROP rgPropMultisubnet;

rgPropMultisubnet.dwPropertyID = SSPROP_INIT_MULTISUBNETFAILOVER;
rgPropMultisubnet.dwOptions = DBPROPOPTIONS_REQUIRED;
rgPropMultisubnet.dwStatus = DBPROPSTATUS_OK;
rgPropMultisubnet.colid = DB_NULLID;
V_VT(&(rgPropMultisubnet.vValue)) = VT_BOOL;
V_BOOL(&(rgPropMultisubnet.vValue)) = VARIANT_TRUE;

DBPROPSET PropSet;

PropSet.rgProperties = &rgPropMultisubnet;
PropSet.cProperties = 1;
PropSet.guidPropertySet = DBPROPSET_SQLSERVERDBINIT;
IDBProperties* pIDBProperties = NULL;
hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void **)&pIDBProperties);
pIDBProperties->SetProperties(1, &PropSet);
```

## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server の機能](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [OLE DB Driver for SQL Server での接続文字列キーワードの使用](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)  
  
  
