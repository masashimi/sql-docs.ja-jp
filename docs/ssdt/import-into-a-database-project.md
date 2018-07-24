---
title: データベース プロジェクトへのインポート | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.SQLPROJECTIMPORTSNAPSHOTSUMMARYDIALOG.DIALOG
- SQL.DATA.TOOLS.SQLPROJECTIMPORTDATABASESUMMARYDIALOG.DIALOG
- SQL.DATA.TOOLS.IMPORTSCRIPTWIZARD.SUMMARY
ms.assetid: d0a0a394-6cb6-416a-a25f-9babf8ba294a
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: af8ee2d569c44d19e518c1dafacddb958c66cc88
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2018
ms.locfileid: "39087744"
---
# <a name="import-into-a-database-project"></a>データベース プロジェクトへのインポート
[インポート] を使用すると、ライブ データベースや .dacpac から新しいオブジェクトをプロジェクトに取り込んだり、スクリプトの新しい定義でプロジェクト内の既存のオブジェクトを更新したりできます。 次の 3 つの方法の動作には、注意が必要な相違点がいくつかあります。これらの方法について以下で説明します。  
  
**[インポート] メニュー**  
  
![SSDT の [インポート] メニュー](../ssdt/media/ssdt-import.gif "SSDT の [インポート] メニュー")  
  
**このトピックのセクション**  
  
[インポート元: データベースまたはデータ層アプリケーション (*.dacpac)](#bkmk_import_source_db)  
  
[インポート元: スクリプト (*.sql)](#bkmk_import_source_script)  
  
[暗号化されたオブジェクトのインポート](#bkmk_import_encrypted)  
  
## <a name="bkmk_import_source_db"></a>インポート元: データベースまたはデータ層アプリケーション (*.dacpac)  
データベースや .dacpac ファイルからスキーマをインポートする機能を使用できるのは、プロジェクト内でスキーマ オブジェクトが定義されていない場合のみです。 これには、RefactorLog、または配置前や配置後のスクリプトは含まれません。  
  
インポート時に、オブジェクトの定義は、SSDT で構成する新しいオブジェクトに関する既定値を使用してスクリプト化され、プロジェクト ファイルに含まれます。新しいオブジェクトには、トップ レベル オブジェクト用の新しいファイル、親と同じファイルで定義された階層の子、可能な場合はインラインで定義されたテーブル/列の制約が含まれます。 各オブジェクトの表示設定と制御に対象に絞る場合は、[インポート] ではなく [スキーマ比較] を使用してください。  
  
インポート元に配置前スクリプトと配置後スクリプト、RefactorLog、または SQLCMD 変数の定義が含まれている場合、これらはプロジェクトにインポートされます。 これらの成果物のいずれかが既にプロジェクトに含まれている場合、インポートされたファイルは、プロジェクトの **[インポート時に無視]** フォルダーに追加されます。  
  
**[インポート時に無視] フォルダー**  
  
![SSDT の [インポート時に無視] フォルダー](../ssdt/media/ssdt-ignoredonimport.gif "SSDT の [インポート時に無視] フォルダー")  
  
## <a name="bkmk_import_source_script"></a>インポート元: スクリプト (*.sql)  
インポート元のオブジェクトのうち、プロジェクト内に存在*しない*オブジェクトはすべて追加され、プロジェクト内*に存在する*オブジェクトはすべて、プロジェクト内のオブジェクト定義を上書きします。  
  
> [!NOTE]  
> この方法には、既知のバグが 2 つありますが、今後のリリースで修復される予定です。  
>   
> -   テーブル/列の制約がプロジェクトのテーブル定義内の CREATE TABLE ステートメントの外部で定義されている場合は、インポートにより、制約がインラインになるようにテーブル定義が上書きされます。 ただし、不一致の制約はそのまま残るため、プロジェクト内で制約が重複します。  
> -   インポート元のスクリプトのマスター キーまたはデータベース暗号化キーは、既にプロジェクトに存在する場合、インポート時に複製されます。 プロジェクトをビルドするには、重複するキーを削除してください。  
  
スクリプトからのインポート プロセスでは、配置前スクリプトと配置後スクリプト、SQLCMD 変数、または RefactorLog ファイルが認識されません。 インポート時に検出される、このようにサポートされていないコンストラクターは、プロジェクトの **Scripts** フォルダー内の **ScriptsIgnoredOnImport.sql** ファイルに配置されます。  
  
詳しくは、SSDT チーム フォーラム ([http://social.msdn.microsoft.com/Forums/en-US/ssdt/threads](http://social.msdn.microsoft.com/Forums/en-US/ssdt/threads)) をご覧ください。  
  
## <a name="bkmk_import_encrypted"></a>暗号化されたオブジェクトのインポート  
暗号化されたオブジェクトをデータベース プロジェクトにインポートする際、必ずしも、オブジェクト定義の本体を完全にサーバーから取得できるとは限りません。 このように、インポートの動作は、このクラスのオブジェクトを処理する際に異なる場合があります。  
  
定義本体を完全に取得できないと、オブジェクトのヘッダーとフッターは、本体のダミーと共にスクリプト化されます。 この現象は、インポートしたり、インポート元がライブ データベースまたはデータベースから抽出された .dacpac に指定されているスキーマ比較を使用したりすると発生する場合があります。  
  
**本体のダミーを含むスクリプト**  
  
![本体のダミーを含むスクリプト](../ssdt/media/ssdt-procwithencryption.gif "本体のダミーを含むスクリプト")  
  
オブジェクトの定義全体が利用可能で取得できる場合は、インポートとスキーマ比較により、そのままプロジェクトになります。 この現象は、スクリプト、データベース プロジェクトからビルドされた .dacpac、または別のデータベース プロジェクトからプロジェクトを更新すると発生します。  
  