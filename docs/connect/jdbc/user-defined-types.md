---
title: ユーザー定義の種類 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 19a71b27-b788-43a3-a76d-fe3001a6f016
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 55db7c7c903f4b22a85f9762f13f845ea7ea17ba
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2018
ms.locfileid: "42786116"
---
# <a name="user-defined-types"></a>ユーザー定義型

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

ユーザー定義型 (UDT) は [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] で導入されました。以来、開発者は共通言語ランタイム (CLR) のオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに格納することによってサーバーのスカラー型システムを拡張できるようになりました。 UDT は複数の要素を持つことができ、動作を定義できます。この点は、1 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム データ型から構成される従来の別名データ型と異なります。 従来、UDT のサイズは最大 8 KB に制限されていました。 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] では、64 KB を超える UDT のサポートが追加されました。 バージョン 3.0 以降の JDBC Driver も、UserDefined 形式を指定する場合に、64 KB を超える UDT をサポートするようになりました。

8,000 バイト以下の UDT の動作は従来と変わりませんが、8,000 バイトを超える UDT もサポートされるようになり、そのサイズは "無制限" として報告されます。

## <a name="see-also"></a>参照

[JDBC ドライバーのデータ型について](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)
