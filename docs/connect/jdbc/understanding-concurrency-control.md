---
title: 同時実行制御の理解 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 98b7dabe-9b12-4e1d-adeb-e5b5cb0c96f3
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0ff86dbb264194a0d4693d88c6eb14cc629d344
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785473"
---
# <a name="understanding-concurrency-control"></a>同時実行制御について
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  同時実行制御とは、複数のユーザーが同時に行を更新しているときにデータベースの整合性を維持するために使用される、さまざまな手法を表します。 不適切な同時実行は、ダーティ リード、ファントム読み取り、反復不能読み取りなどの問題につながります。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] は、これらの問題を解決するために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって使用されるすべての同時実行手法へのインターフェイスを提供します。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の同時実行の詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「同時実行データ アクセスの管理」を参照してください。  
  
## <a name="remarks"></a>Remarks  
 JDBC ドライバーは、以下に示す同時実行の種類をサポートしています。  
  
|同時実行の種類|特性|行ロック|[説明]|  
|----------------------|---------------------|---------------|-----------------|  
|CONCUR_READ_ONLY|[読み取り専用]|いいえ|カーソルを使用して更新することはできません。また、結果セットを構成する行にはロックが設定されません。|  
|CONCUR_UPDATABLE|オプティミスティック読み取り、書き込み|いいえ|データベースで、行の競合が発生する可能性が低いと想定されます。 行の整合性は、タイムスタンプの比較によって検証されます。|  
|CONCUR_SS_SCROLL_LOCKS|ペシミスティック読み取り、書き込み|[ユーザー アカウント制御]|データベースで、行の競合が発生する可能性が高いと想定されます。 行の整合性は、行のロックによって保証されます。|  
|CONCUR_SS_OPTIMISTIC_CC|オプティミスティック読み取り、書き込み|いいえ|データベースで、行の競合が発生する可能性が低いと想定されます。 行の整合性は、タイムスタンプの比較によって検証されます。<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降の場合、テーブルにタイムスタンプ列が含まれていなければ、サーバーはこの同時実行の種類を CONCUR_SS_OPTIMISTIC_CCVAL に変更します。<br /><br /> [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] の場合、基になるテーブルにタイムスタンプ列があれば、OPTIMISTIC WITH VALUES が指定されていても、OPTIMISTIC WITH ROW VERSIONING が使用されます。 OPTIMISTIC WITH ROW VERSIONING が指定されていて、テーブルにタイムスタンプがない場合は、OPTIMISTIC WITH VALUES が使用されます。|  
|CONCUR_SS_OPTIMISTIC_CCVAL|オプティミスティック読み取り、書き込み|いいえ|データベースで、行の競合が発生する可能性が低いと想定されます。 行の整合性は、行データの比較によって検証されます。|  
  
## <a name="result-sets-that-are-not-updateable"></a>更新不可能な結果セット  
 更新可能な結果セットは、行の挿入、更新、および削除が可能な結果セットです。 次の場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は更新可能なカーソルを作成できません。 "結果セットは更新可能ではありません" という意味の例外が生成されます。  
  
|原因|[説明]|Remedy|  
|-----------|-----------------|------------|  
|ステートメントが JDBC 2.0 (以降) の構文を使用して作成されていない|JDBC 2.0 では、ステートメントを作成するための新しい方法が導入されました。 JDBC 1.0 の構文を使用した場合、結果セットは既定で読み取り専用になります。|ステートメントを作成するときに、結果セットの種類と同時実行を指定します。|  
|ステートメントが TYPE_SCROLL_INSENSITIVE を使用して作成されている|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、静的スナップショット カーソルを作成します。 このカーソルは、他のユーザーによる行の更新からカーソルを保護するために、基になるテーブル行から切り離されています。|TYPE_SCROLL_SENSITIVE、TYPE_SS_SCROLL_KEYSET、TYPE_SS_SCROLL_DYNAMIC、または TYPE_FORWARD_ONLY を CONCUR_UPDATABLE と共に使用し、静的カーソルが作成されないようにします。|  
|テーブル デザインにより KEYSET カーソルまたは DYNAMIC カーソルが使用できなくなっている|基になるテーブルに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が行を一意に識別できる一意キーがありません。|一意キーをテーブルに追加し、各行を一意に識別できるようにします。|  
  
## <a name="see-also"></a>参照  
 [JDBC ドライバーによる結果セットの管理](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  
