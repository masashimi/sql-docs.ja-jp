---
title: "SQLGetData (デスクトップ データベース ドライバー) |Microsoft ドキュメント"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e091bf31e034eaabb9c87931bc6b128f5bdeba84
ms.contentlocale: ja-jp
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (デスクトップ データベース ドライバー)
この関数は、その後、列が取得された順序に関係なくバインドされた列があるかどうか、任意の列からデータを取得できます。  
  
> [!NOTE]  
>  \*pcbValue **SQLGetData**返す可能性があります 2 倍の数文字を実際に使用できる Jet 4.0 データベースで 510 文字より長く ANSI データをバインドする場合。 以下の 510 文字値では、実際の cbValue を返します。