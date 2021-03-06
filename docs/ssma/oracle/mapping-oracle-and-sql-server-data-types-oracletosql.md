---
title: Oracle と SQL Server データ型 (OracleToSQL) のマッピング |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Type Mapping Inheritance
ms.assetid: 05da1495-63b9-47b7-86e2-6746394a2d8a
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 6948b81ca2460d4de74393aa880f95fe3f11dfb1
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394568"
---
# <a name="mapping-oracle-and-sql-server-data-types-oracletosql"></a>Oracle と SQL Server データ型のマッピング (OracleToSQL)
Oracle データベースの型が異なる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースの型。 Oracle データベースのオブジェクトを変換する際に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オブジェクトの場合、oracle からのデータ型をマップする方法を指定する必要があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 既定のデータ型マッピングをそのまま使用できるまたはマッピングをカスタマイズするには、次のセクションで示すようにします。  
  
## <a name="default-mappings"></a>既定のマッピング  
SSMA では、データ型マッピングの既定セットがあります。 既定のマッピングの一覧で、次を参照してください。[プロジェクト設定&#40;型マッピングの&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md)します。  
  
## <a name="type-mapping-inheritance"></a>継承のマッピングの種類  
プロジェクト レベル、オブジェクトのカテゴリ レベル (などすべてストアド プロシージャの場合)、またはオブジェクト レベルでは、型マッピングをカスタマイズすることができます。 設定は、下位のレベルでオーバーライドされない限りより高いレベルから継承されます。 たとえば、マップする**smallmoney**に**money**オブジェクトまたはカテゴリ レベルでマッピングをカスタマイズしない限り、このマッピング プロジェクト レベルでは、プロジェクト内のすべてのオブジェクトが使用されます。  
  
表示すると、**型マッピングの**SSMA、バック グラウンドのタブが色分けされ、どの型のマッピングは、継承を表示します。 型マッピングの背景は、継承された型のマッピング、および現在のレベルで指定されているすべてのマッピングのホワイト黄色です。  
  
## <a name="customizing-data-type-mappings"></a>データ型マッピングのカスタマイズ  
次の手順では、プロジェクト、データベース、またはオブジェクト レベルでのデータ型をマップする方法を示します。  
  
**データ型をマップするには**  
  
1.  プロジェクト全体のデータ型マッピングをカスタマイズするには、開く、**プロジェクト設定** ダイアログ ボックス。  
  
    1.  **ツール**メニューの **プロジェクト設定**します。  
  
    2.  左側のウィンドウで次のように選択します。**型マッピングの**します。  
  
        右側のウィンドウでは、型マッピングの表とボタンが表示されます。  
  
    または、データの種類をカスタマイズするデータベース、テーブル、ビュー、またはストアド プロシージャのレベルにあるマッピング オブジェクトのデータベース、またはオブジェクト カテゴリの場合は、Oracle メタデータ エクスプ ローラーで選択。  
  
    1.  Oracle メタデータ エクスプ ローラーでフォルダーまたはカスタマイズするオブジェクトを選択します。  
  
    2.  右側のウィンドウでをクリックして、**型マッピングの**タブ。  
  
2.  新しいマッピングを追加するには、次の操作を行います。  
  
    1.  **[追加]** をクリックします。  
  
    2.  **ソースの種類**、Oracle データ型にマップを選択します。  
  
    3.  型には、長さが必要とする場合は、内でマッピングの最小限のデータ長を指定、**から**ボックスと内の最大データ長、**に**ボックス。  
  
        これにより、同じデータ型の値が小さくなりより大きなデータのマッピングをカスタマイズできます。  
  
    4.  **ターゲットの種類**、ターゲットを選択して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データ型。  
  
        一部の種類には、対象のデータ型の長さが必要です。 必要な場合は、入力内の新しいデータ長、**置き換えます**ボックス。  
  
    5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  データ型のマッピングを変更するには、次の操作を行います。  
  
    1.  **[編集]** をクリックします。  
  
    2.  **ソースの種類**、Oracle データ型にマップを選択します。  
  
    3.  型には、長さが必要とする場合は、内でマッピングの最小限のデータ長を指定、**から**ボックスと内の最大データ長、**に**ボックス。  
  
        これにより、同じデータ型の値が小さくなりより大きなデータのマッピングをカスタマイズできます。  
  
    4.  **ターゲットの種類**、ターゲットを選択して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データ型。  
  
        一部の種類には、対象のデータ型の長さが必要です。 必要な場合は、入力内の新しいデータ長、**で置き換えます**ボックスで、し、 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  カスタム データ型のマッピングを削除するには、次の操作を行います。  
  
    1.  削除するデータ型マッピングを格納する型マッピングの一覧で、行を選択します。  
  
    2.  **[削除]** をクリックします。  
  
        継承のマッピングを削除することはできません。 ただし、継承のマッピングは、特定のオブジェクトまたはオブジェクト カテゴリのカスタム マッピングによって上書きされます。  
  
## <a name="next-steps"></a>次の手順  
移行プロセスの次の手順は、いずれかに[評価レポートを作成する](assessing-oracle-schemas-for-conversion-oracletosql.md)または[Oracle データベースのオブジェクトを SQL Server の構文に変換](converting-oracle-schemas-oracletosql.md)します。 評価レポートを作成する場合、Oracle のオブジェクトは、評価時に自動的に変換されます。  
  
## <a name="see-also"></a>参照  
[SQL Server にデータベースを移行する Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
