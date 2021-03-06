---
title: アップロード ファイル ページ (レポート マネージャー) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7bb3166f-9374-4449-b66a-ffb77298507d
caps.latest.revision: 27
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f29cf01e446c30a69bb2c205d26965b9288ef7f3
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2018
ms.locfileid: "39083034"
---
# <a name="upload-file-page-report-manager"></a>[ファイルのアップロード] ページ (レポート マネージャー)
  ファイル システムからレポート サーバー データベースにファイルをパブリッシュするには、[ファイルのアップロード] ページを使用します。 アップロードされたファイルは、レポート サーバーのフォルダー階層に、アイテムとして表示されます。  
  
-   アップロードされた .rdl ファイルは、レポートとしてレポート サーバーにパブリッシュされます。  
  
-   アップロードされた .smdl ファイルにデータ ソース ビュー情報が含まれていた場合、このファイルはレポート モデルとしてパブリッシュされます。 データ ソース ビューへの参照が失われると、アップロード中にエラーが発生します。 .Smdl ファイルをアップロードする場合、データ ソース ビュー情報が不足している可能性がありますが、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]レポート モデル プロジェクト。 レポート モデル プロジェクトでは、データ ソース ビュー情報は、.smdl ファイル自体ではなく、独立したファイルに格納されます。  
  
     データ ソース ビュー情報を含む (およびアップロードが正常に実行される) モデル ファイルは、以前にレポート サーバーにパブリッシュされて、サーバーからファイル システムのファイルに保存されたものです。 モデルの [全般プロパティ] ページを開き、 **[編集]** をクリックしてモデルを開くと、モデルをファイルに保存できます。その後、そのファイルを新しいモデルとしてレポート サーバーにアップロードすることができます。 次にアップロードした .smdl ファイルには、モデルのパブリケーションに必要な情報がすべて含められます。  
  
-   アップロードする他のすべてのファイルの種類は、リソースとして格納されます。 これには、レポート データ ソース接続情報を含む .rds ファイルが含まれます。 .rds ファイルをアップロードしても、レポート サーバーで共有データ ソース アイテムは生成されません。  
  
 アイテムをアップロードすると、そのアイテムは現在のフォルダーに格納されます。 アップロードの完了後、異なる場所にアイテムを移動できます。  
  
> [!NOTE]  
>  この機能は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 エディションでサポートされている機能の一覧については[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]を参照してください[機能は、SQL Server 2014 の各エディションでサポートされている](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)します。  
  
## <a name="navigation"></a>ナビゲーション  
 ユーザー インターフェイス (UI) のこの場所に移動するには、次の手順に従います。  
  
### <a name="to-open-the-upload-file-page"></a>[ファイルのアップロード] ページを開くには  
  
1.  レポート マネージャーを開き、ファイルをアップロードするフォルダーに移動します。  
  
2.  ツール バーの **[ファイルのアップロード]** をクリックします。  
  
## <a name="options"></a>および  
 **アップロードするファイル**  
 ファイル システムからコピーするファイルへの完全修飾パスを表示します。  
  
 **[参照]**  
 ファイル システムからファイルを選択する場合にクリックします。  
  
 **名前**  
 ファイル名を入力します。この名前はレポート サーバーの名前空間に表示されます。 名前には、少なくとも 1 つの英数字が含まれている必要があります。 また、スペースおよび特定の記号を含めることもできます。 名前を指定するときに、; ? : \@ & = +, $ * \< > |"または/アイテムの名前を指定します。  
  
 **アイテムが存在する場合は上書き**  
 既存のアイテムを新しいバージョンと置き換える場合に、このチェック ボックスをオンにします。 既存のバージョンを上書きするには、新しいアイテムと既存のアイテムの名前が完全に一致している必要があります。  
  
## <a name="see-also"></a>参照  
 [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [[コンテンツ] ページ&#40;レポート マネージャー&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [レポート マネージャー F1 ヘルプ](../../2014/reporting-services/report-manager-f1-help.md)   
 [フォルダーへのファイルのアップロード](report-server/upload-files-to-a-folder.md)  
  
  
