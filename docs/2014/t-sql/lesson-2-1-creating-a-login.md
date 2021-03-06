---
title: ログインの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- creating a login
ms.assetid: a2512310-bdb6-41dc-858a-e866b2b58afc
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: d62f8c381fb11dc34de1e51e56e7aefa3e85e17e
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43017528"
---
# <a name="creating-a-login"></a>ログインの作成
  [!INCLUDE[ssDE](../includes/ssde-md.md)]にアクセスするには、ユーザーのログインが必要です。 ログインは、ユーザーの ID を Windows のアカウントまたは Windows グループのメンバーとして表すか、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のみに存在する [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]ログインを使用することができます。 できるだけ Windows 認証を使用してください。  
  
 既定では、コンピューターの管理者には [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]へのフル アクセス権が与えられます。 このレッスンでは、これより特権の少ないユーザーが必要なので、コンピューターに新しいローカルの Windows 認証アカウントを作成します。 そのためには、コンピューターの管理者であることが条件となります。 その後、この新しいユーザーに [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]へのアクセス権を与えます。  
  
### <a name="to-create-a-new-windows-account"></a>新しい Windows アカウントを作成するには  
  
1.  をクリックして**開始**、 をクリックして**実行**で、**を開く**ボックスに「 `%SystemRoot%\system32\compmgmt.msc /s`、順にクリックします**ok**コンピュータの管理プログラムを開きます。  
  
2.  **[システム ツール]** の **[ローカル ユーザーとグループ]** を展開し、**[ユーザー]** を右クリックして、**[新しいユーザー]** をクリックします。  
  
3.  **[ユーザー名]** ボックスに、「 **Mary**」と入力します。  
  
4.  **[パスワード]** および **[パスワードの確認入力]** ボックスに強力なパスワードを入力し、**[作成]** をクリックして、新しいローカルの Windows ユーザーを作成します。  
  
### <a name="to-create-a-login"></a>ログインを作成するには  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]のクエリ エディター ウィンドウで、次のコードを入力して実行します。 `computer_name` は自分のコンピューター名に置き換えます。 `FROM WINDOWS` は Windows がユーザーを認証することを示します。 オプションの `DEFAULT_DATABASE` 引数は、接続文字列で別のデータベースを指定しない限り、 `Mary` を `TestData` データベースに接続します。 このステートメントでは、セミコロンが [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントのオプションの終了文字として使用されています。  
  
    ```  
    CREATE LOGIN [computer_name\Mary]  
        FROM WINDOWS  
        WITH DEFAULT_DATABASE = [TestData];  
    GO  
    ```  
  
     これでユーザー名 `Mary`が承認され、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のこのインスタンスへのアクセスがコンピューターによって認証されます。 コンピューターに [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスが複数ある場合は、 `Mary` がアクセスする各インスタンスでログインを作成する必要があります。  
  
    > [!NOTE]  
    >  `Mary` はドメインのアカウントではないため、このユーザー名はこのコンピューターでしか認証できません。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [データベースへのアクセス権の付与](lesson-2-2-granting-access-to-a-database.md)  
  
## <a name="see-also"></a>参照  
 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)   
 [認証モードの選択](../relational-databases/security/choose-an-authentication-mode.md)  
  
  
