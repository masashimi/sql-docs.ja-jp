---
title: Integration Services プロジェクト変換ウィザード |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ssis.migrationwizard.f1
ms.assetid: a192b094-4d0f-4c21-b911-460ec844a49f
caps.latest.revision: 16
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a5c547623597e72e4c6ae144baed226dbf88af60
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2018
ms.locfileid: "37219652"
---
# <a name="integration-services-project-conversion-wizard"></a>Integration Services プロジェクト変換ウィザード
  **Integration Services プロジェクト変換ウィザード** で、プロジェクトをプロジェクト配置モデルに変換します。  
  
> [!NOTE]  
>  プロジェクトに含まれている 1 つ以上のデータ ソースは、プロジェクトの変換が完了すると削除されます。 プロジェクト内のパッケージで共有可能なデータ ソースへの接続を作成するには、プロジェクト レベルで接続マネージャーを追加します。 詳細については、「 [Add, Delete, or Share a Connection Manager in a Package](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md)」(パッケージでの接続マネージャーの追加、削除、または共有) を参照してください。  
  
 **目的に合ったトピックをクリックしてください**  
  
-   [Integration Services プロジェクト変換ウィザードを開く](#open_dialog)  
  
-   [[パッケージの場所の指定] ページのオプションの設定](#locate)  
  
-   [[パッケージの選択] ページのオプションの設定](#selectPackages)  
  
-   [[配置先の選択] ページのオプションの設定](#destination)  
  
-   [[プロジェクト プロパティの指定] ページのオプションの設定](#projectProperties)  
  
-   [[パッケージ実行タスクの更新] ページのオプションの設定](#executePackage)  
  
-   [[構成の選択] ページのオプションの設定](#configurations)  
  
-   [[パラメーターの作成] ページのオプションの設定](#createParameters)  
  
-   [[パラメーターの構成] ページのオプションの設定](#configureParameters)  
  
-   [[確認] ページのオプションの設定](#review)  
  
-   [[変換の実行] のオプションの設定](#conversion)  
  
##  <a name="open_dialog"></a> Integration Services プロジェクト変換ウィザードを開く  
 **Integration Services プロジェクト変換** ウィザードを開くには、次のいずれかの操作を行います。  
  
-   [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]でプロジェクトを開き、ソリューション エクスプローラーでプロジェクトを右クリックし、 **[プロジェクト配置モデルに変換]** をクリックします。  
  
-   オブジェクト エクスプローラーの [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]で、 **[プロジェクト]** ノードを右クリックし、 **[パッケージのインポート]** を選択します。  
  
 **Integration Services プロジェクト変換ウィザード** を [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] または [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]のいずれから実行するかによって、ウィザードが実行する変換タスクは異なります。 詳細については、「 [Integration Services サーバーへのプロジェクトの配置](../../2014/integration-services/deploy-projects-to-integration-services-server.md)」を参照してください。  
  
##  <a name="locate"></a> [パッケージの場所の指定] ページのオプションの設定  
  
> [!NOTE]  
>  **[パッケージの場所の指定]** ページは、ウィザードを [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]から実行した場合にのみ使用可能です。  
  
 **[ソース]** ボックスの一覧の **[ファイル システム]** を選択すると、次のオプションがページに表示されます。 パッケージがファイル システムに存在する場合は、このオプションを選択します。  
  
 **フォルダー**  
 パッケージのパスを入力するか、 **[参照]** をクリックしてパッケージに移動します。  
  
 **[ソース]** ボックスの一覧の **[SSIS パッケージ ストア]** を選択すると、次のオプションがページに表示されます。 パッケージ ストアの詳細については、「[パッケージの管理 &#40;SSIS サービス&#41;](service/package-management-ssis-service.md)」を参照してください。  
  
 **[サーバー]**  
 サーバー名を入力するか、またはサーバーを選択します。  
  
 **フォルダー**  
 パッケージのパスを入力するか、 **[参照]** をクリックしてパッケージに移動します。  
  
 **[ソース]** ボックスの一覧の **[Microsoft SQL Server]** を選択すると、次のオプションがページに表示されます。 パッケージが Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]に存在する場合は、このオプションを選択します。  
  
 **[サーバー]**  
 サーバー名を入力するか、またはサーバーを選択します。  
  
 **[Windows 認証を使用する]**  
 Microsoft Windows 認証モードを使用すると、ユーザーは Windows ユーザー アカウントを使用して接続できます。 Windows 認証を使用すると、ユーザー名とパスワードを入力する必要がなくなります。  
  
 **[SQL Server 認証を使用する]**  
 指定されたログイン名とパスワードを使用して、信頼関係の低い接続から接続した場合、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ログイン アカウントが設定されているかどうか、指定されたパスワードが以前に記録されたパスワードと一致しているかどうかを確認することで接続の認証を行います。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] にログイン アカウントが設定されていない場合、認証は失敗し、エラー メッセージが返されます。  
  
 **ユーザー名**  
 SQL Server 認証を使用する場合に、ユーザー名を指定します。  
  
 **Password**  
 SQL Server 認証を使用する場合に、パスワードを指定します。  
  
 **フォルダー**  
 パッケージのパスを入力するか、 **[参照]** をクリックしてパッケージに移動します。  
  
##  <a name="selectPackages"></a> [パッケージの選択] ページのオプションの設定  
 **[パッケージ名]**  
 パッケージ ファイルを一覧表示します。  
  
 **ステータス**  
 パッケージをパッケージ配置モデルに変換する準備ができているかどうかを示します。  
  
 **メッセージ**  
 パッケージに関連付けられているメッセージが表示されます。  
  
 **Password**  
 パッケージに関連付けられているパスワードが表示されます。 パスワードのテキストは表示されません。  
  
 **[選択項目に適用]**  
 クリックすると、 **[パスワード]** ボックスのパスワードが選択したパッケージに適用されます。  
  
 **[更新]**  
 パッケージの一覧を更新します。  
  
##  <a name="destination"></a> [配置先の選択] ページのオプションの設定  
 このページで、新規プロジェクト配置ファイル (.ispac) の名前とパスを指定するか、既存のファイルを選択します。  
  
> [!NOTE]  
>  **[配置先の選択]** ページは、ウィザードを [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]から実行した場合にのみ使用可能です。  
  
 **[出力パス]**  
 配置ファイルのパスを入力するか、 **[参照]** をクリックしてファイルに移動します。  
  
 **プロジェクト名**  
 プロジェクト名を入力します。  
  
 **保護レベル**  
 保護レベルを選択します。 詳しくは、「 [Access Control for Sensitive Data in Packages](security/access-control-for-sensitive-data-in-packages.md)」をご覧ください。  
  
 **[プロジェクトの説明]**  
 プロジェクトの説明を入力します (省略可)。  
  
##  <a name="projectProperties"></a> [プロジェクト プロパティの指定] ページのオプションの設定  
  
> [!NOTE]  
>  **[プロジェクト プロパティの指定]** ページは、ウィザードを [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]から実行した場合にのみ使用可能です。  
  
 **プロジェクト名**  
 プロジェクト名を一覧表示します。  
  
 **保護レベル**  
 プロジェクトに含まれるパッケージの保護レベルを選択します。 保護レベルの詳細については、「 [パッケージ内の機微なデータへのアクセス制御](security/access-control-for-sensitive-data-in-packages.md)」を参照してください。  
  
 **[プロジェクトの説明]**  
 プロジェクトの説明 (省略可能) を入力します。  
  
##  <a name="executePackage"></a> [パッケージ実行タスクの更新] ページのオプションの設定  
 プロジェクト ベースの参照を使用するには、パッケージに含まれているパッケージ実行タスクを更新します。 詳細については、「 [パッケージ実行タスク エディター](../../2014/integration-services/execute-package-task-editor.md)」を参照してください。  
  
 **[親パッケージ]**  
 パッケージ実行タスクを使用して子パッケージを実行するパッケージの名前を一覧表示します。  
  
 **[タスク名]**  
 パッケージ実行タスクの名前を一覧表示します。  
  
 **[元の参照]**  
 子パッケージの現在のパスを一覧表示します。  
  
 **[参照の割り当て]**  
 プロジェクトに格納されている子パッケージを選択します。  
  
##  <a name="configurations"></a> [構成の選択] ページのオプションの設定  
 パラメーターで置き換えるパッケージ構成を選択します。  
  
 **[パッケージ]**  
 パッケージ ファイルを一覧表示します。  
  
 **型**  
 XML 構成ファイルなど、構成の種類を一覧表示します。  
  
 **[構成文字列]**  
 構成ファイルのパスを一覧表示します。  
  
 **ステータス**  
 構成の状態メッセージが表示されます。 メッセージ テキスト全体を表示するには、メッセージをクリックします。  
  
 **[構成の追加]**  
 他のプロジェクトに含まれているパッケージ構成を、パラメーターで置き換える (使用可能な) 構成の一覧に追加します。 ファイル システムまたは SQL Server に格納された構成を選択できます。  
  
 **[更新]**  
 構成の一覧を更新する場合にクリックします。  
  
 **[変換後にすべてのパッケージから構成を削除する]**  
 このオプションを選択して、プロジェクトからすべての構成を削除することをお勧めします。  
  
 このオプションを選択しない場合は、パラメーターで置き換えるために選択した構成のみが削除されます。  
  
##  <a name="createParameters"></a> [パラメーターの作成] ページのオプションの設定  
 各構成プロパティのパラメーター名とスコープを選択します。  
  
 **[パッケージ]**  
 パッケージ ファイルを一覧表示します。  
  
 **[パラメーター名]**  
 パラメーター名を一覧表示します。  
  
 **Scope**  
 パラメーターのスコープ (パッケージまたはプロジェクト) を選択します。  
  
##  <a name="configureParameters"></a> [パラメーターの構成] ページのオプションの設定  
 **名前**  
 パラメーター名を一覧表示します。  
  
 **Scope**  
 パラメーターのスコープを一覧表示します。  
  
 **[値]**  
 パラメーター値を一覧表示します。  
  
 パラメーター プロパティを構成するには、値フィールドの横にある参照ボタンをクリックします。  
  
 **[パラメーターの詳細の設定]** ダイアログ ボックスで、パラメーター値を編集できます。 パッケージの実行時にパラメーター値を指定する必要があるかどうかを指定することもできます。  
  
 **の** [構成] **ダイアログ ボックスの** [パラメーター] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]ページの値を変更するには、パラメーターの横にある参照ボタンをクリックします。 **[パラメーター値の設定]** ダイアログ ボックスが表示されます。  
  
 また、 **[パラメーターの詳細の設定]** ダイアログ ボックスには、パラメーター値のデータ型や元のパラメーターが一覧表示されます。  
  
##  <a name="review"></a> [確認] ページのオプションの設定  
 プロジェクトの変換に関して選択したオプションを確認するには、 **[確認]** ページを使用します。  
  
 **Previous**  
 オプションを変更する場合にクリックします。  
  
 **[変換]**  
 プロジェクトをプロジェクト配置モデルに変換する場合にクリックします。  
  
##  <a name="conversion"></a> [変換の実行] のオプションの設定  
 [変換の実行] ページには、プロジェクトの変換の状態が表示されます。  
  
 **操作**  
 特定の変換手順を一覧表示します。  
  
 **結果**  
 各変換手順の状態を一覧表示します。 状態メッセージをクリックすると、詳細が表示されます。  
  
 プロジェクトの変換は、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]でプロジェクトを保存しないと保存されません。  
  
 **[レポートの保存]**  
 プロジェクトの変換の概要を .xml ファイルに保存する場合にクリックします。  
  
## <a name="see-also"></a>参照  
 [Integration Services サーバーへのプロジェクトの配置](../../2014/integration-services/deploy-projects-to-integration-services-server.md)  
  
  
