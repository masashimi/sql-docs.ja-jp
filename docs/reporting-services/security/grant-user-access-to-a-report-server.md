---
title: レポート サーバーへのユーザー アクセスを許可する | Microsoft Docs
ms.date: 05/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: security
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- removing role assignments
- permissions [Reporting Services], granting report server access
- roles [Reporting Services], assignments
- modifying role assignments
- deleting role assignments
ms.assetid: 2144c020-3253-4b47-8cda-e14c928bb471
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 285642926ae52e076d9c3012df16583c7896132e
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2018
ms.locfileid: "43279167"
---
# <a name="grant-user-access-to-a-report-server"></a>レポート サーバーへのユーザー アクセスを許可する

[!INCLUDE[ssrs-appliesto-sql2016-preview](../../includes/ssrs-appliesto-sql2016-preview.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、ロール ベースのセキュリティを使用して、レポート サーバーへのアクセス権がユーザーに付与されます。 新しいレポート サーバーをインストールした直後は、ローカル Administrators グループに属するユーザーにのみ、レポート サーバーのコンテンツと操作に対する権限が与えられます。 他のユーザーがレポート サーバーにアクセスできるようにするには、ロール割り当てを作成して、ユーザーまたはグループ アカウントを、一連のタスクが指定された定義済みのロールにマップする必要があります。

 **SharePoint モードのレポート サーバー:** SharePoint 統合モード用に構成されたレポート サーバーの場合は、SharePoint サイトから、SharePoint の権限を使ってアクセスを構成します。 レポート サーバーのコンテンツや操作にアクセスできるかどうかは、SharePoint サイト上の権限レベルによって決まります。 SharePoint サイトでの権限を付与できるのはサイト管理者だけです。 詳細については、「 [SharePoint サイトのレポート サーバー アイテムに対する権限の付与](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)」を参照してください。

 **ネイティブ モードのレポート サーバー:** このトピックでは、ネイティブ モードで構成されているレポート サーバーと、ロールにユーザーを割り当てる Web ポータルの使用方法に注目します。 ロールには次の 2 種類があります。

- アイテムレベルのロール : レポート サーバーのコンテンツ、サブスクリプション、レポート処理、レポート履歴などを表示、追加、および管理するためのロール。 アイテム レベルのロール割り当ては、ルート ノード ([ホーム] フォルダー)、または階層内でそれより下位にある特定のフォルダーやアイテムに対して定義できます。

- システムレベルのロール : 特定のアイテムではなく、サイト全体にわたる操作へのアクセスを許可します。 たとえば、レポート ビルダーや共有スケジュールを使用することが含まれます。

    この 2 種類のロールは相互補完的な関係にあり、組み合わせて使用する必要があります。 そのため、レポート サーバーにユーザーを追加するには、2 段階の処理が必要となります。 ユーザーをアイテムレベルのロールに割り当てる場合は、同時にシステムレベルのロールにも割り当てる必要があります。 ユーザーをロールに割り当てる際は、既に定義されているロールを選択する必要があります。 ロールを作成、変更、または削除するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]を使用します。 詳細については、「 [ロールを作成、削除、または変更する &#40;Management Studio&#41;](../../reporting-services/security/role-definitions-create-delete-or-modify.md)」を参照してください。

## <a name="before-you-start"></a>開始前の準備

ネイティブ モードのレポート サーバーにユーザーを追加する場合は、あらかじめ次の点を確認してください。

- レポート サーバー コンピューターのローカル Administrators グループのメンバーとしてログインする必要があります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] または Windows Server 2008 に配置する場合、レポート サーバーをローカルで管理するには追加の構成が必要となります。 詳細については、「[ローカル管理用のネイティブ モードのレポート サーバーの構成](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)」を参照してください。

- このタスクを他のユーザーに委任する場合は、ユーザー アカウントをコンテンツ マネージャー ロールとシステム管理者ロールにマップするためのロール割り当てを作成します。 コンテンツ マネージャーとシステム管理者の権限を与えられたユーザーは、レポート サーバーにユーザーを追加できます。

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]で、システム ロールおよびユーザー ロールに対して定義されているロールを確認し、それぞれのロールにどのようなタスクが含まれているかを確認します。 Web ポータルではタスクの説明が表示されません。そのため、ユーザーを追加する前に、各ロールについて理解しておく必要があります。

- 必要であれば、ロールをカスタマイズするか、新しいロールを定義して必要なタスクを追加します。 たとえば、個々のアイテムにカスタム セキュリティ設定を使用する場合は、フォルダーの閲覧権限を付与した新しいロール定義を作成する必要があります。

### <a name="to-add-a-user-or-group-to-a-system-role"></a>ユーザーまたはグループをシステム ロールに追加するには

1. [Web ポータル](../web-portal-ssrs-native-mode.md)を起動します。

2. 右上にある*歯車*アイコンを選択します。

3. **[サイトの設定]** を選択します。

4. **[セキュリティ]** を選択します。

5. **[グループまたはユーザーの追加]** を選択します。

6. **[グループまたはユーザー]** で、Windows ドメインのユーザー アカウントまたはグループ アカウントを \<ドメイン>\\<アカウント\> の形式で入力します。 

    > [!NOTE]
    > フォーム認証やカスタム セキュリティを使用している場合は、その環境に合った適切な形式でユーザー アカウントまたはグループ アカウントを指定します。

7. システム ロールを選択し、**[OK]** を選択します。

    ロールは累積されます。したがって、システム管理者とシステム ユーザーを両方とも選択した場合、そのユーザーまたはグループは、これら両方のロールのタスクを実行できるようになります。

8. 割り当てを作成するユーザーまたはグループが他にもある場合は、以上の手順を繰り返します。

### <a name="to-add-a-user-or-group-to-an-item-role"></a>ユーザーまたはグループをアイテム ロールに追加するには

1. **Web ポータル** を起動し、ユーザーまたはグループを追加するレポート アイテムを探します。

2. アイテムの **[...]** (省略記号) を選択します。

3. ドロップダウン メニューで、**[管理]** を選択します。

4. **[セキュリティ]** を選択します。

5. **[グループまたはユーザーの追加]** を選択します。

    > [!NOTE]
    > アイテムが現在、親アイテムからセキュリティを継承している場合は、ツール バーの **[セキュリティをカスタマイズする]** をクリックしてセキュリティの設定を変更します。 次いで **[グループまたはユーザーの追加]** を選択します。

6. **[グループまたはユーザー]** で、Windows ドメインのユーザー アカウントまたはグループ アカウントを \<ドメイン>\\<アカウント\> の形式で入力します。 フォーム認証やカスタム セキュリティを使用している場合は、その環境に合った適切な形式でユーザー アカウントまたはグループ アカウントを指定します。

7. ユーザーまたはグループがアイテムにアクセスする方法を表すロールの定義を 1 つ以上選択して、**[OK]** を選択します。

8. 割り当てを作成するユーザーまたはグループが他にもある場合は、以上の手順を繰り返します。

## <a name="next-steps"></a>次の手順

[ロールの割り当てを作成および管理する](../../reporting-services/security/create-and-manage-role-assignments.md)   
[[新しいロールの割り当て]: [ロールの割り当てを編集] ページ (レポート マネージャー)](http://msdn.microsoft.com/library/3319ced0-4b86-42af-b18d-da41a625113c)   
[[セキュリティのプロパティ] ページ、アイテム (レポート マネージャー)](http://msdn.microsoft.com/library/351b8503-354f-4b1b-a7ac-f1245d978da0)   
[ロールの割り当て](../../reporting-services/security/role-assignments.md)   
[ロールの定義](../../reporting-services/security/role-definitions.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](http://go.microsoft.com/fwlink/?LinkId=620231)
