---
title: catalog.execution_property_override_values | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 83cbdd6f-ddde-47bf-abde-36bd24272621
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 787baa21f2039647084b271a7cb63c681b6e7438
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2018
ms.locfileid: "35409834"
---
# <a name="catalogexecutionpropertyoverridevalues"></a>catalog.execution_property_override_values
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  パッケージの実行中に設定されたプロパティ オーバーライド値を表示します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|property_id|**bigint**|プロパティ オーバーライド値の一意の ID。|  
|execution_id|**bigint**|実行のインスタンスの一意の ID。|  
|property_path|**nvarchar (4000)**|パッケージ内のプロパティのパス。|  
|property_value|**nvarchar(max)**|プロパティのオーバーライド値。|  
|sensitive|**bit**|値が 1 のとき、プロパティはセンシティブで、格納されるときに暗号化されます。 値が 0 のとき、プロパティはセンシティブではなく、値はプレーンテキストで格納されます。|  
  
## <a name="remarks"></a>Remarks  
 このビューには、**[パッケージの実行]** ダイアログの **[詳細設定]** タブの **[プロパティのオーバーライド]** セクションを使用してプロパティ値がオーバーライドされた実行ごとに行が表示されます。 プロパティのパスは、パッケージ タスクの **[パッケージのパス]** プロパティから取得されます。  
  
## <a name="permissions"></a>アクセス許可  
 このビューには、次の権限のいずれかが必要です。  
  
-   実行のインスタンスの READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
> [!NOTE]  
>  サーバー上で操作を実行する権限がある場合は、操作に関する情報を表示する権限もあります。 行レベルのセキュリティが適用されるため、表示する権限がある行のみが表示されます。  
  
  
