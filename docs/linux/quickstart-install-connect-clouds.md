---
title: クラウドでの SQL Server の概要 |Microsoft Docs
description: このクイック スタートでは、任意のクラウドでの Linux 上の SQL Server を実行する方法を示します。
author: annashres
ms.author: annashres
manager: craigg
ms.date: 10/25/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 638df74c4288f8f1b67232ff99cfd90393a52380
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2018
ms.locfileid: "46713174"
---
# <a name="quickstart-run-the-sql-server-in-the-cloud"></a>クイック スタート: クラウドで SQL Server を実行します。

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

このクイック スタートで SQL Server を Red Hat Enterprise Linux (RHEL)、SUSE Linux Enterprise Server (SLES)、または任意のクラウドでの Ubuntu にインストールされます。 Azure で Linux の SQL Server を実行する場合は、「[Azure Portal での Linux SQL Server 仮想マシンのプロビジョニング](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)」に移動してください。

    > [!NOTE]
    > If you choose to run a paid edition of SQL Server then you need to bring your own license (BYOL)

## <a name="amazon-web-services"></a>アマゾン ウェブ サービス
1.  マーケットプレースから Linux AMI を、少なくとも 2 gb のメモリで作成します。 
    * [RHEL 7.3 以降](https://aws.amazon.com/marketplace/pp/B00KWBZVK6)
    * [SLES v12 SP2](https://aws.amazon.com/marketplace/pp/B00PMM99PI)
    * [Ubuntu 16.04](https://aws.amazon.com/marketplace/pp/B01JBL2M0O)
1.  AMI に ssh で接続します
1.  選択した Linux ディストリビューションのクイック スタートに従ってください。 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  リモート接続を構成します。 
    * [Amazon EC2 コンソール]( https://console.aws.amazon.com/ec2/) を開きます。
    * ナビゲーション ウィンドウで、**セキュリティ グループ** を選択します。 
    * **受信、編集、規則の追加** を選択します
    * SQL Server がリッスンするポートでトラフィックを許可する受信規則を追加します。(既定の TCP ポートは 1433)

    
## <a name="digital-ocean"></a>Digital Ocean
1. [コントロール パネル](https://cloud.digitalocean.com/login) にログインし、ドロップレットの作成をクリックします。
1. 少なくとも 2 GB のメモリの Ubuntu 16.04 のドロップレットを選択します。
1. ドロップレットに ssh で接続します
1. [Ubuntu のクイック スタート](quickstart-install-connect-ubuntu.md) を参照します
1. リモート接続を構成します。
    * コントロール パネルの上部の、**ネットワーク** のリンクをクリックし、**ファイアウォール** を選択します。
    * SQL Server がリッスンするポートでトラフィックを許可する受信規則を追加します。(既定の TCP ポートは 1433)
    
## <a name="google-cloud-platform"></a>Google Cloud Platform
1.  クラウド ランチャーから少なくとも 2 GB のメモリのLinux イメージを作成します。 
    * [RHEL 7.3 以降](https://console.cloud.google.com/launcher/details/rhel-cloud/rhel-7)
    * [SLES v12 SP2](https://console.cloud.google.com/launcher/details/suse-cloud/sles-12)
    * [Ubuntu 16.04](https://console.cloud.google.com/launcher/details/ubuntu-os-cloud/ubuntu-xenial)
1.  イメージに ssh で接続します
1.  選択した Linux ディストリビューションのクイック スタートに従ってください。 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  リモート接続を構成します。 
    * [ファイアウォール規則](https://console.cloud.google.com/networking/firewalls) に移動します。
    * SQL Server がリッスンするポートでトラフィックを許可する受信規則の追加 (既定の tcp: 1433)
