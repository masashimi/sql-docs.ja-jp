---
title: 監査変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.audittrans.f1
- sql13.dts.designer.audittransformation.f1
helpviewer_keywords:
- environment data in packages [Integration Services]
- Audit transformation
ms.assetid: 8c143682-9c81-4150-83d6-1d9678151d37
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: be17c584af2fc584be7d95ebcc4069fc9f545b97
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2018
ms.locfileid: "35331076"
---
# <a name="audit-transformation"></a>監査変換
  監査変換により、パッケージが実行される環境に関するデータをパッケージ内のデータ フローに含めることができます。 たとえば、パッケージ、コンピューター、および演算子の名前をデータ フローに追加できます。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] には、この情報を提供するシステム変数が含まれています。  
  
## <a name="system-variables"></a>システム変数  
 次の表では、監査変換で使用できるシステム変数について説明します。  
  
|システム変数|インデックス|[説明]|  
|---------------------|-----------|-----------------|  
|**ExecutionInstanceGUID**|0|パッケージの実行インスタンスを識別する GUID です。|  
|**PackageID**|@shouldalert|パッケージの一意識別子です。|  
|**PackageName**|2|パッケージの名前です。|  
|**VersionID**|3|パッケージのバージョンです。|  
|**ExecutionStartTime**|4|パッケージの実行を開始した時刻です。|  
|**MachineName**|5|コンピューター名|  
|**UserName**|6|パッケージを開始した人のログイン名です。|  
|**TaskName**|7|監査変換が関連付けられているデータ フロー タスクの名前です。|  
|**TaskId**|8|データ フロー タスクの一意識別子です。|  
  
## <a name="configuration-of-the-audit-transformation"></a>監査変換の構成  
 監査変換を構成するには、新しい出力列の名前を設定し、変換出力に追加します。次に、その出力列にシステム変数をマップします。 1 つのシステム変数は、複数の列にマップできます。  
  
 この変換は 1 つの入力と 1 つの出力をとります。 エラー出力はサポートされていません。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [変換のカスタム プロパティ](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 プロパティの設定方法の詳細については、「 [データ フロー コンポーネントのプロパティを設定する](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="audit-transformation-editor"></a>監査変換エディター
  監査変換により、パッケージが実行される環境に関するデータをパッケージ内のデータ フローに含めることができます。 たとえば、パッケージ、コンピューター、および演算子の名前をデータ フローに追加できます。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] には、この情報を提供するシステム変数が含まれています。  
  
### <a name="options"></a>および  
 **[出力列の名前]**  
 監査情報を格納する、新しい出力列の名前を入力します。  
  
 **[監査の種類]**  
 監査情報を得るために使用できるシステム変数を選択します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[実行インスタンスの GUID]**|パッケージの実行インスタンスを個別に識別する GUID を挿入します。|  
|**[パッケージ ID]**|パッケージを個別に識別する GUID を挿入します。|  
|**パッケージ名**|パッケージ名を挿入します。|  
|**[バージョン ID]**|パッケージのバージョンを個別に識別する GUID を挿入します。|  
|**[実行開始時刻]**|パッケージの実行が開始される時刻を挿入します。|  
|**コンピューター名**|パッケージを起動したコンピューターの名前を挿入します。|  
|**User name**|パッケージを起動したユーザーのログイン名を挿入します。|  
|**[タスク名]**|監査変換が関連付けられているデータ フロー タスクの名前を挿入します。|  
|**[タスク ID]**|監査変換が関連付けられているデータ フロー タスクを個別に識別する GUID を挿入します。|  
  
  
