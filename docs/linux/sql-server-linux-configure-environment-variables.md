---
title: 環境変数で SQL Server の設定を構成する |Microsoft ドキュメント
description: このトピックでは、環境変数を使用して、Linux で SQL Server 2017 の特定の設定を構成する方法について説明します。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 6388b284939ed439e02cc8d1ee9f5df6246812fd
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2018
ms.locfileid: "46713614"
---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>Linux 上の SQL Server の設定を環境変数で構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Linux 上の SQL Server 2017 を構成するのには、いくつかの別の環境変数を使用できます。 これらの変数は、2 つのシナリオで使用されます。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Linux 上の SQL Server 2019 CTP 2.0 を構成するのには、いくつかの別の環境変数を使用できます。 これらの変数は、2 つのシナリオで使用されます。

::: moniker-end

- `mssql-conf setup` コマンドで初期セットアップを構成。
- 新しい [Docker の SQL Server コンテナー](quickstart-install-connect-docker.md) を構成。

> [!TIP]
> これらのシナリオのセットアップ後に SQL Server を構成する必要がある場合は、次を参照してください。 [mssql-conf ツールを使用して Linux 上の SQL Server を構成](sql-server-linux-configure-mssql-conf.md)

## <a name="environment-variables"></a>環境変数

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

| 環境変数 | 説明 |
|-----|-----|
| **ACCEPT_EULA** | 任意の値 (たとえば、' Y') を設定すると SQL Server のライセンス契約に同意します。 |
| **MSSQL_SA_PASSWORD** | SA ユーザーのパスワードを構成します。 |
| **MSSQL_PID** | SQL Server のエディションまたはプロダクト キーを設定します。 有効な値は次のとおりです。 </br></br>**Evaluation**</br>**Developer**</br>**Express**</br>Web</br>**Standard**</br>**Enterprise**</br>**プロダクト キー**</br></br>プロダクト キーを指定する場合は、###-###-###-###-###、この '#' は、数値または文字の形式でなければなりません。|
| **MSSQL_LCID** | SQL Server に使用する言語 ID を設定します。 たとえば 1036 はフランス語です。 |
| **MSSQL_COLLATION** | SQL Server の既定の照合順序を設定します。 照合順序には、言語 id (LCID) の既定のマッピングが上書きされます。 |
| **MSSQL_MEMORY_LIMIT_MB** | SQL Server が使用できる最大メモリサイズ (MB) を設定します。 既定は、合計物理メモリの 80% となります。 |
| **MSSQL_TCP_PORT** | SQL Server がリッスンする TCP ポート (既定は 1433) を構成します。 |
| **MSSQL_IP_ADDRESS** | IP アドレスを設定します。 現時点では、IP アドレスは IPv4 スタイル (0.0.0.0) にする必要があります。 |
| **MSSQL_BACKUP_DIR** | 既定のバックアップ ディレクトリの場所を設定します。 |
| **MSSQL_DATA_DIR** | 新しい SQL Server データベースのデータ ファイル (.mdf) が作成されるディレクトリを変更します。 |
| **MSSQL_LOG_DIR** | 新しい SQL Server データベースのログ (.ldf) ファイルの作成されるディレクトリを変更します。 |
| **MSSQL_DUMP_DIR** | 既定の SQL Server のメモリ ダンプおよび、その他のトラブルシューティング ファイルを保存するディレクトリを変更します。 |
| **MSSQL_ENABLE_HADR** | 可用性グループを有効にします。 たとえば、'1' が有効になっているし、'0' が無効になっています |
| **MSSQL_AGENT_ENABLED** | SQL Server エージェントを有効にします。 たとえば、'true' を有効にし、'false' は無効になっています。 既定では、エージェントが無効です。  |
| **MSSQL_MASTER_DATA_FILE** | Master データベースのデータ ファイルの場所を設定します。 |
| **MSSQL_MASTER_LOG_FILE** | Master データベース ログ ファイルの場所を設定します。 |
| **MSSQL_ERROR_LOG_FILE** | エラー ログ ファイルの場所を設定します。 |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

| 環境変数 | 説明 |
|-----|-----|
| **ACCEPT_EULA** | 任意の値 (たとえば、' Y') を設定すると SQL Server のライセンス契約に同意します。 |
| **MSSQL_SA_PASSWORD** | SA ユーザーのパスワードを構成します。 |
| **MSSQL_PID** | SQL Server のエディションまたはプロダクト キーを設定します。 有効な値は次のとおりです。 </br></br>**Evaluation**</br>**Developer**</br>**Express**</br>Web</br>**Standard**</br>**Enterprise**</br>**プロダクト キー**</br></br>プロダクト キーを指定する場合は、###-###-###-###-###、この '#' は、数値または文字の形式でなければなりません。|
| **MSSQL_LCID** | SQL Server に使用する言語 ID を設定します。 たとえば 1036 はフランス語です。 |
| **MSSQL_COLLATION** | SQL Server の既定の照合順序を設定します。 照合順序には、言語 id (LCID) の既定のマッピングが上書きされます。 |
| **MSSQL_MEMORY_LIMIT_MB** | SQL Server が使用できる最大メモリサイズ (MB) を設定します。 既定は、合計物理メモリの 80% となります。 |
| **MSSQL_TCP_PORT** | SQL Server がリッスンする TCP ポート (既定は 1433) を構成します。 |
| **MSSQL_IP_ADDRESS** | IP アドレスを設定します。 現時点では、IP アドレスは IPv4 スタイル (0.0.0.0) にする必要があります。 |
| **MSSQL_BACKUP_DIR** | 既定のバックアップ ディレクトリの場所を設定します。 |
| **MSSQL_DATA_DIR** | 新しい SQL Server データベースのデータ ファイル (.mdf) が作成されるディレクトリを変更します。 |
| **MSSQL_LOG_DIR** | 新しい SQL Server データベースのログ (.ldf) ファイルの作成されるディレクトリを変更します。 |
| **MSSQL_DUMP_DIR** | 既定の SQL Server のメモリ ダンプおよび、その他のトラブルシューティング ファイルを保存するディレクトリを変更します。 |
| **MSSQL_ENABLE_HADR** | 可用性グループを有効にします。 たとえば、'1' が有効になっているし、'0' が無効になっています |
| **MSSQL_AGENT_ENABLED** | SQL Server エージェントを有効にします。 たとえば、'true' を有効にし、'false' は無効になっています。 既定では、エージェントが無効です。  |
| **MSSQL_MASTER_DATA_FILE** | Master データベースのデータ ファイルの場所を設定します。 |
| **MSSQL_MASTER_LOG_FILE** | Master データベース ログ ファイルの場所を設定します。 |
| **MSSQL_ERROR_LOG_FILE** | エラー ログ ファイルの場所を設定します。 |

::: moniker-end

## <a name="example-initial-setup"></a>例: 初期セットアップ

この例では構成した環境変数で `mssql-conf setup` を実行します。 次の環境変数が指定されます。

- **ACCEPT_EULA**使用許諾契約書を受け入れます。
- **MSSSQL_PID** 非運用環境で利用できる、フリーライセンスの Developer Edition の SQL Server を指定します。
- **MSSQL_SA_PASSWORD**強力なパスワードを設定します。
- **MSSQL_TCP_PORT** SQL Server がリッスンする TCP ポートを 1234 として設定します。

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="example-docker"></a>例: Docker

この docker コマンドの例では、新しい SQL Server のコンテナーを作成するのに次の環境変数を使用します。

- **ACCEPT_EULA**使用許諾契約書を受け入れます。
- **MSSSQL_PID** 非運用環境で利用できる、フリーライセンスの Developer Edition の SQL Server を指定します。
- **MSSQL_SA_PASSWORD**強力なパスワードを設定します。
- **MSSQL_TCP_PORT** SQL Server がリッスンする TCP ポートを 1234 として設定します。 つまり、この例では、ポート 1433 (既定値) をホスト ポートにマップする代わりに、このカスタム TCP ポートを `-p 1234:1234` コマンドでマップしなければなりません。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Linux/macos で Docker を実行している場合は、単一引用符を使って次の構文を使用します。

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

Windows で Docker を実行している場合は、二重引用符で次の構文を使用します。

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

> [!NOTE]
> コンテナーで実稼働のエディションを実行するためのプロセスは若干異なります。 詳細については、次を参照してください。[実稼働のコンテナー イメージを実行](sql-server-linux-configure-docker.md#production)

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Linux/macos で Docker を実行している場合は、単一引用符を使って次の構文を使用します。

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
```

Windows で Docker を実行している場合は、二重引用符で次の構文を使用します。

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
```

::: moniker-end

## <a name="next-steps"></a>次の手順

記載されていない、その他の SQL Server の設定は、次を参照してください。 [mssql-conf ツールを使用して Linux 上の SQL Server を構成](sql-server-linux-configure-mssql-conf.md)

Linux 上に SQL Server をインストールして実行する方法の詳細については、次を参照してください。 [Linux 上に SQL Server をインストール](sql-server-linux-setup.md)
