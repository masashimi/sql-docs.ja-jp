---
title: Transact-SQL での OLE オートメーション オブジェクト | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: stored-procedures
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], OLE Automation
- batches [SQL Server], OLE Automation
- OLE Automation [SQL Server]
- OLE Automation [SQL Server], about OLE Automation
ms.assetid: a887d956-4cd0-400a-aa96-00d7abd7c44b
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6c63b36cbd83e00a9fee04ceae3e4968fe367fec
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43109556"
---
# <a name="ole-automation-objects-in-transact-sql"></a>Transact-SQL での OLE オートメーション オブジェクト
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[tsql](../../includes/tsql-md.md)][!INCLUDE[tsql](../../includes/tsql-md.md)] バッチ、ストアド プロシージャ、およびトリガーの中で OLE オートメーション オブジェクトを参照できるいくつかのシステム ストアド プロシージャが組み込まれています。 これらのシステム ストアド プロシージャは拡張ストアド プロシージャとして動作します。また、これらのストアド プロシージャから実行される OLE オートメーション オブジェクトは、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] アドレス空間の中で拡張ストアド プロシージャと同じように動作します。  
  
 OLE オートメーション ストアド プロシージャでは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] バッチから SQL DMO オブジェクトやカスタム OLE オートメーション オブジェクト ( **IDispatch** インターフェイスを公開しているオブジェクトなど) を参照できます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] を使用して作成するカスタム インプロセス OLE サーバーには、 **On Error GoTo** サブルーチンと **On Error GoTo** サブルーチン用に **On Error GoTo** ステートメントで指定されたエラー ハンドラーを実装する必要があります。 **Class_Initialize** サブルーチンと **Class_Terminate** サブルーチンで処理されないエラーが発生すると、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスでのアクセス違反など、予期しないエラーが発生する可能性があります。 また、その他のサブルーチン用のエラー ハンドラーも用意しておくことをお勧めします。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] で OLE オートメーション オブジェクトを使用する場合は、まず、**sp_OACreate[!INCLUDE[ssDE](../../includes/ssde-md.md)] システム ストアド プロシージャを呼び出して、** のインスタンスのアドレス空間にそのオブジェクトのインスタンスを作成します。  
  
 オブジェクトのインスタンスを作成した後、次のストアド プロシージャを呼び出してオブジェクトのプロパティ、メソッド、およびエラー情報を処理します。  
  
-   **sp_OAGetProperty** はプロパティの値を取得します。  
  
-   **sp_OASetProperty** はプロパティの値を設定します。  
  
-   **sp_OAMethod** はメソッドを呼び出します。  
  
-   **sp_OAGetErrorInfo** は最新のエラー情報を取得します。  
  
 オブジェクトが必要なくなったら、 **sp_OADestroy** を呼び出し、 **sp_OACreate**で作成したオブジェクトのインスタンスの割り当てを解除します。  
  
 OLE オートメーション オブジェクトは、プロパティ値とメソッドを使用してデータを返します。 **sp_OAGetProperty** と **sp_OAMethod** は、これらのデータ値を結果セットの形で返します。  
  
 OLE オートメーション オブジェクトのスコープはバッチです。 そのオブジェクトへのすべての参照は、単一のバッチ、ストアド プロシージャ、またはトリガー内に含まれている必要があります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の OLE オートメーション オブジェクトからオブジェクトを参照する場合、参照するオブジェクトに含まれる他のオブジェクトも参照できます。 たとえば、SQL-DMO の **SQLServer** オブジェクトを使用すると、参照先のサーバーに含まれているデータベースとテーブルを参照できます。  
  
## <a name="related-content"></a>関連コンテンツ  
 [オブジェクト階層構文 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/object-hierarchy-syntax-transact-sql.md)  
  
 [セキュリティ構成](../../relational-databases/security/surface-area-configuration.md)  
  
 [Ole Automation Procedures サーバー構成オプション](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)  
  
 [sp_OACreate &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oacreate-transact-sql.md)  
  
 [sp_OAGetProperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oagetproperty-transact-sql.md)  
  
 [sp_OASetProperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oasetproperty-transact-sql.md)  
  
 [sp_OAMethod &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oamethod-transact-sql.md)  
  
 [sp_OAGetErrorInfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oageterrorinfo-transact-sql.md)  
  
 [sp_OADestroy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oadestroy-transact-sql.md)  
  
  
