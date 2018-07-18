---
title: トランザクション レプリケーションの更新可能なサブスクリプション | Microsoft Docs
ms.custom: ''
ms.date: 03/31/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, about updatable subscriptions
- queued updating subscriptions [SQL Server replication]
- immediate updating subscriptions
- subscriptions [SQL Server replication], updatable
- updatable subscriptions
ms.assetid: 8eec95cb-3a11-436e-bcee-bdcd05aa5c5a
caps.latest.revision: 57
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 38e7b5970295bec4170c8658c254214f40d250ff
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37268668"
---
# <a name="updatable-subscriptions-for-transactional-replication"></a>Updatable Subscriptions for Transactional Replication
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 トランザクション レプリケーションでは、更新可能なサブスクリプションおよびピア ツー ピア レプリケーションによるサブスクライバーでの更新をサポートしています。 2 種類の更新可能なサブスクリプションを以下に示します。  
  
-   即時更新。 サブスクライバーのデータを更新するために、パブリッシャーとサブスクライバーを接続する必要があります。  
  
-   キュー更新。サブスクライバーのデータを更新するために、パブリッシャーとサブスクライバーを接続する必要はありません。 サブスクライバーまたはパブリッシャーがオフラインでも更新できます。  
  
 サブスクライバーでデータが更新されると、更新はまずパブリッシャーに反映され、次に他のサブスクライバーに反映されます。 即時更新を使用した場合、変更は 2 フェーズ コミット プロトコルを使用して即時に反映されます。 キュー更新を使用した場合、変更はキューに格納されます。キューに登録されたトランザクションは、ネットワーク接続が可能であればいつでも、パブリッシャーで非同期に適用されます。 更新は非同期的にパブリッシャーに反映されるので、同じデータがそのパブリッシャーまたは別のサブスクライバーによって更新済みになると、更新の適用時に競合が生じる可能性があります。 競合の解決方法はパブリケーションの作成時に設定され、この方法に従って競合が検出されて解決されます。  
  
 パブリケーションの新規作成ウィザードで更新可能なサブスクリプションによるトランザクション パブリケーションを作成する場合は、即時更新およびキュー更新の両方が有効になります。 ストアド プロシージャによるパブリケーションを作成する場合は、どちらか一方または両方のオプションを有効にすることができます。 パブリケーションに対してサブスクリプションを作成する場合は、使用する更新モードを指定します。 必要に応じて、更新モードを切り替えることができます。 詳細については、以下の「更新モードの切り替え」を参照してください。  
  
 トランザクション パブリケーションの更新可能なサブスクリプションを有効にするには、「 [Enable Updating Subscriptions for Transactional Publications](../publish/enable-updating-subscriptions-for-transactional-publications.md)」をご覧ください。  
  
 トランザクション パブリケーションに対して更新可能なサブスクリプションを作成するを参照してください[Create an Updatable Subscription to Transactional Publication。](../create-updatable-subscription-transactional-publication-transact-sql.md)  
  
## <a name="switching-between-update-modes"></a>更新モードの切り替え  
 更新可能なサブスクリプションを使用する場合に、サブスクリプションに 1 つの更新モードを指定し、アプリケーションで別の更新モードが必要な場合はそちらに切り替えるように指定できます。 たとえば、サブスクリプションで即時更新を使用するが、システム障害でネットワークに接続できなくなった場合には、キュー更新に切り替えるように指定することができます。  
  
> [!NOTE]  
>  レプリケーションでは、自動的に更新モードの切り替えを行いません。 SQL Server Management Studio で更新モードを設定するか、アプリケーションから [sp_setreplfailovermode &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql) を呼び出してモードを切り替える必要があります。  
  
 即時更新からキュー更新へ切り替えた場合、サブスクライバーとパブリッシャーが接続され、キュー リーダー エージェントがキューにあるすべての保留メッセージをパブリッシャーに適用するまで、即時更新に戻すことはできません。  
  
 **更新モードを切り替えるには**  
  
 更新モードを切り替えるには、両方の更新モードに対してパブリケーションとサブスクリプションを有効にしてから、必要に応じてこれらを切り替える必要があります。 詳細については、「  
[更新可能トランザクション サブスクリプションの更新モードの切り替え](../administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)  
  
### <a name="considerations-for-using-updatable-subscriptions"></a>更新可能なサブスクリプションの使用に関する注意点  
  
-   更新サブスクリプションまたはキュー更新サブスクリプションに対してパブリケーションを有効にすると、このオプションをパブリケーションに対して無効にできません (サブスクリプションで使用する必要がない場合でも同様)。 このオプションを無効にするには、パブリケーションを削除し、新しいパブリケーションを作成する必要があります。  
  
-   データの再パブリッシュはサポートされていません。  
  
-   レプリケーションでは、追跡のため、パブリッシュされたテーブルに **msrepl_tran_version** 列を追加します。 この追加の列によりすべて`INSERT`ステートメントは、列リストを含める必要があります。  
  
-   更新サブスクリプションをサポートするパブリケーションのテーブルでスキーマ変更を行うには、パブリッシャーおよびサブスクライバーでのテーブルの利用をすべて停止し、スキーマ変更を行う前に、保留中のデータの変更をすべてのノードに反映させる必要があります。 これにより、未完了のトランザクションが保留中のスキーマ変更と競合しません。 スキーマ変更がすべてのノードに反映されたら、パブリッシュされたテーブルの操作を再開できます。 詳細については、「[レプリケーション トポロジの停止 &#40;レプリケーション Transact-SQL プログラミング&#41;](../administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)」を参照してください。  
  
-   更新モードを切り替える場合、サブスクリプションが初期化された後で、少なくとも 1 回はキュー リーダー エージェントを実行する必要があります (既定では、キュー リーダー エージェントは連続的に実行されます)。  
  
-   サブスクライバー データベースが行方向にパーティション分割され、そのパーティションにパブリッシャーではなくサブスクライバーの行が入る場合は、サブスクライバーはそれ以前に存在した行を更新することはできません。 これらの行を更新しようとすると、エラーが返されます。 行はテーブルから削除され、パブリッシャーで追加されます。  
  
### <a name="updates-at-the-subscriber"></a>サブスクライバーでの更新  
  
-   サブスクライバーでの更新は、サブスクリプションの有効期限が切れていたり、アクティブでない場合でも、パブリッシャーに反映されます。 そのようなサブスクリプションは、削除または再初期化してください。  
  
-   場合`TIMESTAMP`または`IDENTITY`列を使用して、基本データ型としてレプリケートされる、これらの列の値はサブスクライバーで更新しない必要があります。  
  
-   サブスクライバーの更新または挿入できません`text`、`ntext`または`image`値ため、レプリケーションの変更の追跡トリガー内で挿入または削除されたテーブルから読み取ることはできません。 同様に、サブスクライバーを更新または挿入できません`text`または`image`を使用して値`WRITETEXT`または`UPDATETEXT`データが、パブリッシャーによって上書きされるためです。 代わりに、パーティション、`text`と`image`を個別の列がテーブルし、トランザクション内で 2 つのテーブルを変更します。  
  
     サブスクライバーでラージ オブジェクトを更新するデータ型を使用して、 `varchar(max)`、 `nvarchar(max)`、`varbinary(max)`の代わりに`text`、 `ntext`、および`image`それぞれのデータ型します。  
  
-   一意なキー (主キーを含む) に対する更新によって重複が生じる場合 (たとえば、 `UPDATE <column> SET <column> =<column>+1` などの形式による更新)、その更新を行うことはできません。その更新は一意性違反のため拒否されます。 これは、個人としてレプリケーションによって、サブスクライバーで行われた set 更新が反映される`UPDATE`の影響を受ける各行のステートメント。  
  
-   サブスクライバー データベースが行方向にパーティション分割されていて、行を含むパーティションがサブスクライバーにはあっても、パブリッシャーにはない場合、この既存の行をサブスクライバーは更新できません。 これらの行を更新しようとすると、エラーが返されます。 この行は、テーブルから削除し、再び挿入する必要があります。  
  
### <a name="user-defined-triggers"></a>ユーザー定義トリガー  
  
-   サブスクライバーでアプリケーションがトリガーを必要とする場合、パブリッシャーおよびサブスクライバーで `NOT FOR REPLICATION` オプションを使用してトリガーを定義する必要があります。 これにより、トリガーは元のデータの変更に対してのみ起動され、その変更がレプリケートされるときには起動されません。  
  
     ユーザー定義トリガーは、レプリケーション トリガーがテーブルを更新するときには起動されません。 これは、プロシージャを呼び出す`sp_check_for_sync_trigger`ユーザー定義トリガーの本文にします。 詳細については、「[sp_check_for_sync_trigger &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-check-for-sync-trigger-transact-sql)」を参照してください。  
  
### <a name="immediate-updating"></a>即時更新  
  
-   即時更新サブスクリプションでは、サブスクライバーでの変更は、パブリッシャーに反映され、Microsoft 分散トランザクション コーディネーター (MS DTC) を使用して適用されます。 パブリッシャーおよびサブスクライバーに MS DTC がインストールおよび構成されていることを確認してください。 詳細については、Windows のマニュアルを参照してください。  
  
-   即時更新サブスクリプションで使用されるトリガーでは、変更をレプリケートするためにパブリッシャーへ接続する必要があります。  
  
-   パブリケーションで、即時更新サブスクリプションおよびパブリケーション内のアーティクルに対する列フィルターが許容する場合は、既定値を持たず NULL にできない列をフィルター選択により除外することはできません。  
  
### <a name="queued-updating"></a>キュー更新  
  
-   キュー更新サブスクリプションを受け入れるトランザクション パブリケーションの一部として、マージ パブリケーションのテーブルをパブリッシュすることはできません。  
  
-   主キーはすべてのキューでレコードを見つけるために使用されるので、キュー更新では主キーの列を更新しないでください。 競合の解決方法がサブスクライバー優先であるとき、主キーの更新には注意が必要です。 主キーの更新をパブリッシャーとサブスクライバーの両方で行うと、その結果は 2 つの行がそれぞれ異なる主キーを持つことになります。  
  
-   データ型の列の`SQL_VARIANT`: データの挿入や更新サブスクライバーで、これは次のように、キュー リーダー エージェントによってするときにマップ、サブスクライバーからキューにコピーされます。  
  
    -   `BIGINT`、 `DECIMAL`、 `NUMERIC`、 `MONEY`、および`SMALLMONEY`にマップされます`NUMERIC`します。  
  
    -   `BINARY` `VARBINARY`にマップされます`VARBINARY`データ。  
  
### <a name="conflict-detection-and-resolution"></a>競合の検出と解決  
  
-   サブスクライバー優先の競合ポリシーの場合、主キー列への更新に対して、競合解決方法はサポートされません。  
  
-   外部キーの制約違反による競合は、レプリケーションでは解決されません。  
  
    -   競合が予想されず、データが正常にパーティション分割されている (サブスクライバーは同じ行を更新しない) 場合は、パブリッシャーおよびサブスクライバーで外部キーの制約を使用できます。  
  
    -   競合が予想され、"サブスクライバー優先" の競合解決方法を使用する場合は、パブリッシャーまたはサブスクライバーで外部キーの制約は使用しないでください。"パブリッシャー優先" の競合解決方法を使用する場合は、サブスクライバーで外部キーの制約は使用しないでください。  
  
## <a name="see-also"></a>参照  
 [Peer-to-Peer Transactional Replication](peer-to-peer-transactional-replication.md)   
 [トランザクション レプリケーションで使用するパブリケーションの種類](publication-types-for-transactional-replication.md)   
 [データとデータベース オブジェクトのパブリッシュ](../publish/publish-data-and-database-objects.md)   
 [パブリケーションのサブスクライブ](../subscribe-to-publications.md)  
  
  