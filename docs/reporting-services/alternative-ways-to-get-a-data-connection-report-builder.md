---
title: 別の方法でデータ接続を取得する (レポート ビルダー) | Microsoft Docs
ms.date: 06/15/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.suite: pro-bi
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: aebc5f3d-97d5-4d54-b525-753fed073a9a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7b421f79dd45efdb7b9c0942b6611e88a0dbd7b9
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2018
ms.locfileid: "43272168"
---
# <a name="alternative-ways-to-get-a-data-connection-report-builder"></a>別の方法でデータ接続を取得する (レポート ビルダー)
データ接続には、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースなどの外部データ ソースに接続するときに必要な情報が含まれます。 通常、使用する接続情報と資格情報の種類はデータ ソースの所有者から提供されます。  
  
データ接続を指定するには、レポート サーバーの共有データ ソースを使用するか、特定のレポートでのみ使用する埋め込みデータ ソースを作成します。  
  
ほとんどのチュートリアルでは埋め込みデータ ソースを使用しますが、共有データ ソースにアクセスできる場合は、代わりに共有データ ソースを使用できます。  
  
## <a name="getting-a-data-connection-from-a-shared-data-source"></a>共有データ ソースのデータ接続の取得  
レポート サーバーに使用可能な共有データ ソースがあり、それらを使用する権限がある場合は、埋め込みデータ ソースの代わりにそれらの共有データ ソースを使用できます。 共有データ ソースを探し、それらを使用するために必要な資格情報を指定する手順を次に示します。  
  
共有データ ソースを使用するには、レポート サーバーを参照して共有データ ソースを選択します。 通常、レポート サーバーの URL はレポート サーバー管理者から提供されます。  
  
### <a name="to-specify-a-data-connection-from-a-list-of-shared-data-sources"></a>共有データ ソースの一覧からデータ接続を指定するには  
  
1.  [新しいテーブル/マトリックス] または [新しいグラフ] ウィザードの **[データセットの選択]** ページで、**[データセットの作成]** を選択し、**[次へ]** をクリックします。 **[データ ソースへの接続の選択]** ページが開きます。  
  
2.  データ ソースの一覧から、アクセスする権限があるデータ ソースを選択します。  
  
3.  データ ソースに接続できることを確認するために、**[接続テスト]** をクリックします。 "接続が正常に作成されました" というメッセージが表示されます。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  **[次へ]** をクリックします。  
  
    必要に応じて、資格情報を入力します。 資格情報をローカルに保存するには、**[接続時にパスワードを保存する]** を選択します。 このオプションを選択しない場合、レポートを実行するたびに資格情報が要求されます。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-specify-a-data-connection-by-browsing-to-a-shared-data-source-on-a-report-server"></a>レポート サーバーの共有データ ソースを参照してデータ接続を指定するには  
  
1.  [新しいテーブル/マトリックス] または [新しいグラフ] ウィザードの **[データセットの選択]** ページで、**[データセットの作成]** を選択し、**[次へ]** をクリックします。 **[データ ソースへの接続の選択]** ページが開きます。  
  
2.  **[参照]** をクリックします。 **[データ ソースの選択]** ダイアログ ボックスが表示されます。  
  
3.  **[検索対象]** ドロップダウン リストから **[最近使ったサイトとサーバー]** を選択します。 データ ソース ウィンドウでサーバーの URL をクリックし、**[開く]** をクリックします。  
  
    データ ソースまたはモデルの一覧が表示されます。  
  
4.  または、**[名前]** にレポート サーバーの URL を入力します。 **[開く]** をクリックします。  
  
    レポート ビルダーがレポート サーバーに接続され、ルート フォルダーにある使用可能なデータ ソースが読み込まれます。  
  
5.  接続するための必要な権限があるデータ ソースが格納されたフォルダーに移動し、データ ソースを選択して **[開く]** をクリックします。  
  
    **[データ ソースへの接続の選択]** ページに戻ります。  
  
6.  データ ソースに接続できることを確認するために、 **[接続テスト]** をクリックします。  
  
    "接続が正常に作成されました" というメッセージが表示されます。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  **[次へ]** をクリックします。  
  
8.  ユーザー名とパスワードを要求された場合は、資格情報を入力します。 資格情報をローカルに保存するには、**[接続時にパスワードを保存する]** を選択します。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
[レポート データセット (SSRS)](../reporting-services/report-data/report-datasets-ssrs.md)  
[レポート ビルダー チュートリアル](../reporting-services/report-builder-tutorials.md) 
  

