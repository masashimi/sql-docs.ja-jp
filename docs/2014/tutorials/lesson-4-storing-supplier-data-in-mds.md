---
title: 'レッスン 4: MDS の仕入先データを格納する |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bacd9eaf-4d12-4f25-aec7-d785dec1b623
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 778e28463c8fcb6b46a59e5929801dd56c819186
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393314"
---
# <a name="lesson-4-storing-supplier-data-in-mds"></a>レッスン 4: MDS に仕入先データを格納する
  マスター データ サービス (MDS) は、マスター データ管理用の SQL Server ソリューションです。 マスター データ管理 (MDM) とは、データの非トランザクション リストを探索および定義するために組織が必要とする作業を表します。  
  
 モデルはマスター データ サービス内の最上位レベルの編成単位で、マスター データの構造を整理します。 MDS を実装すると、1 つ以上のモデルを作成することができ、各モデルで類似データがグループ化されます。 マスター データは通常、4 つのカテゴリ (人、場所、物、概念) のうちの 1 つに分類されます。 たとえば、製品関連のデータを含む Product モデルや、顧客関連のデータを含む Customer モデルを作成できます。 参照してください[モデル (マスター データ サービス)](http://msdn.microsoft.com/library/ee633746.aspx)の詳細。  
  
 モデルには 1 つ以上のエンティティを含めることができます。 各エンティティには属性 (列) とメンバー (行) があります。 各行にはマスター データが含まれます。 このレッスンでは、Supplier および State という 2 つのエンティティを持つ Suppliers モデルを作成します。 Supplier エンティティには、Code、Name、Contact First Name、Contact Last Name、Contact Email Address、Address Line、City、State、Zip、および Country の属性があります。 参照してください[属性 (マスター データ サービス)](http://msdn.microsoft.com/library/ee633745.aspx)詳細については詳細属性に関する一般にします。 Code および Name 属性は、Cleansed and Matched Suppliers Excel ファイルの SupplierID および Supplier Name 列に対応します。  
  
 ドメイン ベースの属性とは、別のエンティティからのメンバーによって値が設定される属性です。 ドメイン ベースの属性では、ユーザーは有効でない属性値を入力できません。 属性値は、別のエンティティによって設定されるドロップダウン リストからのみ選択できます。 このチュートリアルでは、Supplier エンティティの State 属性は State エンティティからの値を含むドメイン ベースの属性です。 Supplier エンティティの State 属性の値は、State エンティティのいずれかの値にのみ変更できます。 参照してください[ドメイン ベース属性](../master-data-services/domain-based-attributes-master-data-services.md)の詳細。  
  
 MDS 内の派生階層は、モデル内に存在するドメイン ベースの属性のリレーションシップにから派生します。 このチュートリアルでは、Supplier エンティティと State エンティティ間の派生階層を作成します。 派生階層を作成すると、マスター データ マネージャーのブラウザーに状態の一覧が表示されます。 一覧から状態をクリックすると、選択した状態の仕入先が右ペインに表示されます。 このリレーションシップに基づいて派生階層を後で作成します。 参照してください[派生階層](../master-data-services/derived-hierarchies-master-data-services.md)の詳細。  
  
 DQS でナレッジ ベースを作成し、仕入先データのクレンジングと照合に使用して、結果を Cleansed and Matched Supplier Data.xls ファイルに保存しました。 このレッスンでは、クレンジングおよび照合済みのデータを MDS にアップロードします。 DQS にはデータ (メタデータ) に関するナレッジだけが含まれ、MDS はデータ自体 (マスター セット) を保存します。 たとえば、DQS に複数の仕入先に関するナレッジが含まれている場合でも、MDS は会社が使用する仕入先のみを管理します。  
  
 このレッスンでは、次のタスクを行います。  
  
1.  作成、 **Suppliers**モデル**MDS**を使用して、**マスター データ マネージャー Web アプリケーション**します。  
  
2.  オープン**Cleansed and Matched Supplier Data.xls** Excel で使用、 **MDS アドインの Excel**という名前のエンティティを作成する**業者**MDS にデータをアップロードします。  
  
3.  使用して、データが MDS で作成されたことを確認、**マスター データ マネージャー**します。  
  
4.  という名前のエンティティを作成**状態**し、更新、**状態**属性の**Supplier**エンティティによって、ドメイン ベースの属性を**の状態**エンティティ。 このすべてを使用して操作を行う、 **MDS アドインの Excel**します。  
  
5.  使用してドメイン ベースの属性が作成されたことを確認**マスター データ マネージャー**の値を更新し、**名前**の属性、**状態**エンティティ。  
  
6.  使用して行った更新を表示**マスター データ マネージャー**で**Excel**します。  
  
7.  値を読み込む、**状態**にエンティティ**Excel** 、値を追加しを使用して、追加の確認し**マスター データ マネージャー**します。  
  
8.  作成し、ドメイン ベースの属性リレーションシップを使用して派生階層を使用して、 **Supplier**エンティティと**状態**(Supplier エンティティの State 属性は State エンティティの種類のエンティティ) を使用して**マスター データ マネージャー**します。  
  
## <a name="next-step"></a>次の手順  
 [タスク 1: マスター データ マネージャーを使用して Suppliers モデルを作成する](../../2014/tutorials/task-1-creating-suppliers-model-using-master-data-manager.md)  
  
  
