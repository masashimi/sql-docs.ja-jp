---
title: CREATE LOGIN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE_LOGIN_TSQL
- CREATE LOGIN
- LOGIN_TSQL
- LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- passwords [SQL Server], logins
- mapping logins [SQL Server]
- logins [SQL Server], creating
- CREATE LOGIN statement
- permissions [SQL Server], logins
- Windows domain accounts [SQL Server]
- re-hashing passwords
- certificates [SQL Server], logins
ms.assetid: eb737149-7c92-4552-946b-91085d8b1b01
caps.latest.revision: 101
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6a5f2edc15c171a80c16ccc77f11bf7673571d53
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "43074475"
---
# <a name="create-login-transact-sql"></a>CREATE LOGIN (Transact-SQL)

SQL Server、SQL Database、SQL Data Warehouse、または Parallel Data Warehouse データベースのログインを作成します。 特定のバージョンの構文、引数、注釈、権限、例を表示するには、以下のいずれかのタブをクリックします。

構文表記規則の詳細については、「[Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)」を参照してください。 

## <a name="click-a-product"></a>製品をクリックしてください

次の行から興味がある製品名をクリックしてみてください。 この Web ページでは、クリックした製品に合わせて、異なるコンテンツが表示されます。

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]
> ||||||
> |-|-|-|-|-|
> |**_\* SQL Server \*_**|[SQL Database<br />論理サーバー](create-login-transact-sql.md?view=azuresqldb-current)|[SQL Database<br />Managed Instance](create-login-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](create-login-transact-sql.md?view=azure-sqldw-latest)|[SQL Parallel<br />Data Warehouse](create-login-transact-sql.md?view=aps-pdw-2016)

&nbsp;

# <a name="sql-server"></a>SQL Server

## <a name="syntax"></a>構文 
  
```  
-- Syntax for SQL Server  
CREATE LOGIN login_name { WITH <option_list1> | FROM <sources> }  
  
<option_list1> ::=   
    PASSWORD = { 'password' | hashed_password HASHED } [ MUST_CHANGE ]  
    [ , <option_list2> [ ,... ] ]  
  
<option_list2> ::=    
    SID = sid  
    | DEFAULT_DATABASE = database      
    | DEFAULT_LANGUAGE = language  
    | CHECK_EXPIRATION = { ON | OFF}  
    | CHECK_POLICY = { ON | OFF}  
    | CREDENTIAL = credential_name   
  
<sources> ::=  
    WINDOWS [ WITH <windows_options>[ ,... ] ]  
    | CERTIFICATE certname  
    | ASYMMETRIC KEY asym_key_name  
  
<windows_options> ::=        
    DEFAULT_DATABASE = database  
    | DEFAULT_LANGUAGE = language  
```  
  
## <a name="arguments"></a>引数  
*login_name*  
作成するログインの名前を指定します。 ログインには、SQL Server ログイン、Windows ログイン、証明書マッピング ログイン、非対称キー マッピング ログインの 4 種類があります。 Windows ドメイン アカウントからマップされるログインを作成する場合は、Windows 2000 よりも前の Windows で使用されていた [\<domainName>\\<login_name>] 形式のユーザー ログイン名を使用する必要があります。 login_name@DomainName 形式の UPN は使用できません。 例については、この記事の後半の例 D を参照してください。 認証ログインは **sysname** 型であり、[識別子](../../relational-databases/databases/database-identifiers.md) のルールに従っている必要があります。このログインに "**\\**" を含めることはできません。 Windows ログインには "**\\**" を含めることができます。 Active Directory ユーザーに基づくログインは、21 文字未満の名前に制限されます。 

PASSWORD **='***password***'* SQL Server ログインにのみ適用されます。 作成するログインのパスワードを指定します。 強力なパスワードを使用する必要があります。 詳細については、「[強力なパスワード](../../relational-databases/security/strong-passwords.md)」と「[パスワード ポリシー](../../relational-databases/security/password-policy.md)」を参照してください。 SQL Server 2012 (11.x) 以降では、保存されたパスワード情報は salt 化パスワードの SHA-512 を使用して計算されます。 
  
パスワードでは大文字と小文字が区別されます。 パスワードの長さは 8 文字以上 128 文字以下である必要があります。 パスワードには、a ～ z、A ～ Z、0 ～ 9 およびほとんどの英数字以外の文字を含めることができます。 パスワードには、単一引用符、または *login_name* を含めることはできません。 
  
PASSWORD **=***hashed_password*  
HASHED キーワードにのみ適用されます。 作成するログインのパスワードのハッシュ値を指定します。 
  
HASHED SQL Server ログインにのみ適用されます。 PASSWORD 引数の後に入力されたパスワードが、ハッシュ済みであることを示します。 このオプションを選択しなかった場合、パスワードとして入力した文字列は、ハッシュされてからデータベースに格納されます。 このオプションは、あるサーバーから別のサーバーにデータベースを移行する場合にのみ使用してください。 新しいログインを作成する場合は HASHED オプションを使用しないでください。 HASHED オプションは SQL 7 以前で作成されたハッシュでは使用できません。

MUST_CHANGE SQL Server ログインにのみ適用されます。 このオプションが含まれている場合、SQL Server では、新しいログインが最初に使用されたときに、ユーザーに新しいパスワードの入力が求められます。 
  
CREDENTIAL **=***credential_name*  
新しい SQL Server ログインにマップする資格情報の名前。 この資格情報はサーバー内に存在する必要があります。 現在このオプションは、資格情報をログインに関連付けるだけです。 資格情報をシステム管理者 (sa) ログインにマップすることはできません。 
  
SID = *sid*  
ログインを再作成に使用されます。 Windows 認証ログインではなく、SQL Server 認証ログインにのみ適用されます。 新しい SQL Server 認証ログインの SID を指定します。 このオプションが使用されていない場合、SQL Server で自動的に SID が割り当てられます。 SID 構造体は、SQL Server のバージョンに依存します。 SQL Server ログイン SID: GUID に基づく 16 バイト (**binary (16)**) のリテラル値。 たとえば、 `SID = 0x14585E90117152449347750164BA00A7`のようにします。 
  
DEFAULT_DATABASE **=***database*  
ログインに割り当てられる既定のデータベースを指定します。 このオプションを指定しない場合は、既定のデータベースが master に設定されます。 
  
DEFAULT_LANGUAGE **=***language*  
ログインに割り当てられる既定の言語を指定します。 このオプションを指定しない場合は、サーバーの現在の既定の言語が既定の言語になります。 サーバーの既定の言語が将来変更されても、ログインの既定の言語は変更されません。 
  
CHECK_EXPIRATION **=** { ON | **OFF** }  
SQL Server ログインにのみ適用されます。 このログインに、パスワードの有効期限ポリシーを適用するかどうかを指定します。 既定値は OFF です。 
  
CHECK_POLICY **=** { **ON** | OFF }  
SQL Server ログインにのみ適用されます。 SQL Server を実行しているコンピューターの Windows パスワード ポリシーをこのログインに適用するかどうかを指定します。 既定値は ON です。 
  
Windows のポリシーで強力なパスワードが求められる場合は、次の 4 つの特性のうちの少なくとも 3 つをパスワードに含める必要があります。  
  
- 大文字 (A ～ Z)。 
- 小文字 (a ～ z)。 
- 数字 (0 ～ 9)。 
- スペース、_、@、*、^、%、!、$、#、& などの英数字以外の文字。 
  
WINDOWS  
ログインを Windows ログインにマップするよう指定します。 
  
CERTIFICATE *certname*  
ログインに関連付ける証明書の名前を指定します。 この証明書は、master データベース内に既に存在する必要があります。 
  
ASYMMETRIC KEY *asym_key_name*  
ログインに関連付ける非対称キーの名前を指定します。 このキーは、master データベース内に既に存在する必要があります。 
  
## <a name="remarks"></a>Remarks  
- パスワードでは大文字と小文字が区別されます。
- パスワードの事前ハッシュは、SQL Server ログインを作成する場合にのみサポートされます。
- MUST_CHANGE が指定された場合、CHECK_EXPIRATION および CHECK_POLICY は ON に設定されなければなりません。 ON に設定しない場合、ステートメントは失敗します。
- CHECK_POLICY = OFF と CHECK_EXPIRATION = ON の組み合わせはサポートされていません。
- CHECK_POLICY を OFF に設定すると、*lockout_time* はリセットされ、CHECK_EXPIRATION は OFF に設定されます。 
  
> [!IMPORTANT]  
>  CHECK_EXPIRATION および CHECK_POLICY は、Windows Server 2003 以降でのみ適用されます。 詳細については、「 [Password Policy](../../relational-databases/security/password-policy.md)」をご参照ください。 
  
- 証明書または非対称キーから作成されたログインはコード署名用にのみ使用されます。 SQL Server への接続には使用できません。 証明書または非対称キーからログインを作成できるのは、その証明書または非対称キーが master に存在している場合のみです。 
- スクリプトでログインを転送する場合は、「[SQL Server 2005 のインスタンス間でログインおよびパスワードを転送する方法](http://support.microsoft.com/kb/918992)」を参照してください。
- ログインを作成すると、自動的に新しいログインが有効になり、ログインにサーバー レベルの **CONNECT SQL** 権限が与えられます。 
- アクセスを許可するにはサーバーの[認証モード](../../relational-databases/security/choose-an-authentication-mode.md)がログインの種類に一致する必要があります。
- 権限システムの設計の詳細については、「 [データベース エンジンの権限の概要](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)」を参照してください。

## <a name="permissions"></a>アクセス許可  
- ログインを作成できるのは、サーバーに対する **ALTER ANY LOGIN** 権限、または **securityadmin** 固定サーバー ロールのメンバーシップを持つユーザーのみとなります。 詳細については、[サーバー レベルのロール](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles)と [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) (https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles) に関するページを参照してください。
- **CREDENTIAL** オプションを使用する場合は、サーバーに対する **ALTER ANY CREDENTIAL** 権限も必要です。 
  
## <a name="after-creating-a-login"></a>ログインを作成した後  
ログインが作成されたら、ログインは SQL Server に接続できますが、**public** ロールに与えられた権限しか持ちません。 次の操作のいくつかを実行することを検討してください。 
  
 - データベースに接続するには、ログイン用のデータベース ユーザーを作成する必要があります。 詳細については、[CREATE USER](../../t-sql/statements/create-user-transact-sql.md) に関するページを参照してください。 
  
 - [CREATE SERVER ROLE](../../t-sql/statements/create-server-role-transact-sql.md) を使用して、ユーザー定義サーバー ロールを作成します。 使用して **サーバー ロールの ALTER** しています. **メンバーの追加** をユーザー定義サーバー ロールに、新しいログインを追加します。 詳細については、[CREATE SERVER ROLE](../../t-sql/statements/create-server-role-transact-sql.md) と [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) に関するページを参照してください。 
  
 - 固定サーバー ロールにログインを追加するには、**sp_addsrvrolemember** を使用します。 詳細については、「[サーバー レベルのロール](../../relational-databases/security/authentication-access/server-level-roles.md)」と「[sp_addsrvrolemember](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)」を参照してください。 
  
 - 新しいログインまたはログインを含むロールにサーバー レベルの権限を許可するには、**GRANT** ステートメントを使用します。 詳細については、「[GRANT](../../t-sql/statements/grant-transact-sql.md)」を参照してください。 
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-login-with-a-password"></a>A. パスワード付きのログインを作成する  
 次の例では、特定のユーザーのログインを作成し、パスワードを割り当てます。 
  
```sql  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-login-with-a-password-that-must-be-changed"></a>B. 変更する必要のあるパスワード付きのログインを作成する
 次の例では、特定のユーザーのログインを作成し、パスワードを割り当てます。 `MUST_CHANGE` オプションが指定されているため、ユーザーは、最初にサーバーに接続するときにこのパスワードを変更する必要があります。 
  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 
  
```sql  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>' 
    MUST_CHANGE,  CHECK_EXPIRATION = ON;
GO  
``` 

> [!NOTE]
> CHECK_EXPIRATION が OFF のとき、MUST_CHANGE オプションは使用できません。
  
### <a name="c-creating-a-login-mapped-to-a-credential"></a>C. 資格情報にマップされるログインを作成する  
 次の例では、ユーザーを使用して、特定のユーザーのログインを作成します。 このログインは資格情報にマップされます。 
  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 
  
```sql  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>',   
    CREDENTIAL = <credentialName>;  
GO  
```  
  
### <a name="d-creating-a-login-from-a-certificate"></a>D. 証明書からログインを作成する  
 次の例では、master データベースでの証明書から特定のユーザーのログインを作成します。 
  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 
  
```sql
USE MASTER;  
CREATE CERTIFICATE <certificateName>  
    WITH SUBJECT = '<login_name> certificate in master database',  
    EXPIRY_DATE = '12/05/2025';  
GO  
CREATE LOGIN <login_name> FROM CERTIFICATE <certificateName>;  
GO  
```  
  
### <a name="e-creating-a-login-from-a-windows-domain-account"></a>E. Windows ドメイン アカウントからログインを作成する  
 次の例では、Windows ドメイン アカウントからログインを作成します。 
  
**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 
  
```sql  
CREATE LOGIN [<domainName>\<login_name>] FROM WINDOWS;  
GO  
```  
  
### <a name="f-creating-a-login-from-a-sid"></a>F. SID からログインを作成します。  
 次の例では、まず、SQL Server 認証のログインを作成し、ログインの SID を調べています。 
  
```sql  
CREATE LOGIN TestLogin WITH PASSWORD = 'SuperSecret52&&';  
  
SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
 クエリでは、SID として 0x241C11948AEEB749B0D22646DB1A19F2 を返します。 クエリでは、別の値を返します。 次のステートメントは、ログインを削除し、ログインを作成し直します。 前のクエリから SID を使用します。 
  
```sql  
DROP LOGIN TestLogin;  
GO  
  
CREATE LOGIN TestLogin   
WITH PASSWORD = 'SuperSecret52&&', SID = 0x241C11948AEEB749B0D22646DB1A19F2;  
  
SELECT * FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
## <a name="see-also"></a>参照  
- [データベース エンジンの権限の概要](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
- [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
- [パスワード ポリシー](../../relational-databases/security/password-policy.md)   
- [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)   
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)   
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
- [ログインの作成](../../relational-databases/security/authentication-access/create-a-login.md)  
  
::: moniker-end
::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]
> <table>
> <tr>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
> </tr>
> <tr>
>   <th><a href="create-login-transact-sql.md?view=sql-server-2016">SQL Server</a></th>
>   <th><strong><em>* SQL Database<br />論理サーバー *</em></strong></th>
>   <th><a href="create-login-transact-sql.md?view=azuresqldb-mi-current">SQL Database<br />Managed Instance</a></th>
>   <th><a href="create-login-transact-sql.md?view=azure-sqldw-latest">SQL Data<br />Warehouse</a></th>
>   <th><a href="create-login-transact-sql.md?view=aps-pdw-2016">SQL Parallel<br />Data Warehouse</a></th>
> </tr>
> </table>

&nbsp;

# <a name="azure-sql-database-logical-server"></a>Azure SQL Database 論理サーバー
  
## <a name="syntax"></a>構文 
  
```
-- Syntax for Azure SQL Database  
CREATE LOGIN login_name  
 { WITH <option_list> }  
  
<option_list> ::=   
    PASSWORD = { 'password' }  
    [ , SID = sid ]  
```  

## <a name="arguments"></a>引数  
*login_name*  
作成するログインの名前を指定します。 Azure SQL Database 論理サーバーでは SQL ログインのみがサポートされます。 

PASSWORD **='** password**'*  
作成する SQL ログインのパスワードを指定します。 強力なパスワードを使用する必要があります。 詳細については、「[強力なパスワード](../../relational-databases/security/strong-passwords.md)」と「[パスワード ポリシー](../../relational-databases/security/password-policy.md)」を参照してください。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降では、保存されたパスワード情報は salt 化パスワードの SHA-512 を使用して計算されます。 
  
パスワードでは大文字と小文字が区別されます。 パスワードの長さは 8 文字以上 128 文字以下である必要があります。 パスワードには、a ～ z、A ～ Z、0 ～ 9 およびほとんどの英数字以外の文字を含めることができます。 パスワードには、単一引用符、または *login_name* を含めることはできません。 

SID = *sid*  
ログインを再作成に使用されます。 Windows 認証ログインではなく、SQL Server 認証ログインにのみ適用されます。 新しい SQL Server 認証ログインの SID を指定します。 このオプションが使用されていない場合、SQL Server で自動的に SID が割り当てられます。 SID 構造体は、SQL Server のバージョンに依存します。 SQL Database の場合、これは、`0x01060000000000640000000000000000` と、GUID を表す 16 バイトで構成される 32 バイト (**binary(32)**) のリテラルです。 たとえば、 `SID = 0x0106000000000064000000000000000014585E90117152449347750164BA00A7`のようにします。 
  
## <a name="remarks"></a>Remarks  
- パスワードでは大文字と小文字が区別されます。
- スクリプトでログインを転送する場合は、「[SQL Server 2005 のインスタンス間でログインおよびパスワードを転送する方法](http://support.microsoft.com/kb/918992)」を参照してください。
- ログインを作成すると、自動的に新しいログインが有効になり、ログインにサーバー レベルの **CONNECT SQL** 権限が与えられます。 
- アクセスを許可するにはサーバーの[認証モード](../../relational-databases/security/choose-an-authentication-mode.md)がログインの種類に一致する必要があります。
    - 権限システムの設計の詳細については、「 [データベース エンジンの権限の概要](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)」を参照してください。
  
## <a name="login"></a>Login

### <a name="sql-database-logins"></a>SQL データベース ログイン
**CREATE LOGIN** ステートメントはバッチ内の唯一のステートメントである必要があります。 
  
**sqlcmd** などの SQL Database に接続するいくつかのメソッドでは、*\<login>*@*\<server>* の表記法を使用して、接続文字列のログイン名に SQL Database サーバー名を追加する必要があります。 たとえば、ログインが `login1` で、SQL Database サーバーの完全修飾名が `servername.database.windows.net` である場合、接続文字列の *username* パラメーターは `login1@servername` となる必要があります。 の合計の長さ、 *username* パラメーターには、128 文字まで *login_name* サーバー名の長さマイナス 127 文字に制限されます。 この例では、`login_name` が 10 文字であるため、`servername` には 117 文字までしか指定できません。 
  
SQL Database では、ログインを作成する際に master データベースに接続する必要があります。 
  
 SQL Server ルールを使用すると、\<loginname>@\<servername> 形式の SQL Server 認証ログインを作成できます。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] サーバーが **myazureserver** で、ログインが **myemail@live.com** である場合、**myemail@live.com@myazureserver** としてログインを指定する必要があります。 
  
SQL Database では、接続の認証に必要なログイン データおよびサーバー レベルのファイアウォール規則は、各データベースで一時的にキャッシュされます。 このキャッシュは定期的に更新されます。 認証キャッシュを強制的に更新し、データベースに最新バージョンのログイン テーブルがあることを確認するには、[DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md) を実行します。 
  
 SQL Database ログインの詳細については、[Windows Azure SQL Database におけるデータベースとログインの管理](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins)に関する記事を参照してください。 
 
## <a name="permissions"></a>アクセス許可

サーバーレベル プリンシパルのログイン (準備プロセスで作成) または master データベースの `loginmanager` データベース ロールのメンバーだけが新しいログインを作成できます。 詳細については、[サーバー レベルのロール](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles)と [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) (https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles) に関するページを参照してください。

## <a name="logins"></a>Login
- サーバーに対する **ALTER ANY LOGIN** 権限または **securityadmin** 固定サーバー ロールのメンバーシップが必要です。 このコマンドを実行できるのは、サーバーに対する **ALTER ANY LOGIN** 権限または securityadmin 権限のメンバーシップを持つ Azure Active Directory (Azure AD) アカウントのみです。
- Azure SQL 論理サーバーで使用されるのと同じディレクトリ内の Azure AD のメンバーである必要があります。
  
## <a name="after-creating-a-login"></a>ログインを作成した後  
ログインが作成されたら、ログインは SQL Database に接続できますが、**public** ロールに与えられた権限しか持ちません。 次の操作のいくつかを実行することを検討してください。 
  
- データベースに接続するには、そのデータベースにログイン用のデータベース ユーザーを作成する必要があります。 詳細については、[CREATE USER](../../t-sql/statements/create-user-transact-sql.md) に関するページを参照してください。 
- データベースのユーザーに権限を付与するには、**ALTER SERVER ROLE** ...  **ADD MEMBER** ステートメントを使用して組み込みのデータベース ロールのいずれか、またはカスタム ロールにユーザーを追加するか、[GRANT]((../../t-sql/statements/grant-transact-sql.md) ステートメントを使用して直接ユーザーに権限を付与します。 詳細については、[管理者以外のロール](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#non-administrator-users)、[ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) (https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles)、および [GRANT](grant-transact-sql.md) ステートメントに関するページを参照してください。
- サーバー全体の権限を付与するには、master データベースにデータベース ユーザーを作成し、**ALTER SERVER ROLE** ...  **ADD MEMBER** ステートメントを使用して、管理サーバー ロールのいずれかにユーザーを追加します。 詳細については、[サーバー レベルのロール](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles)、[ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md)、および[サーバー ロール](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles)に関するページを参照してください。
- 新しいログインまたはログインを含むロールにサーバー レベルの権限を許可するには、**GRANT** ステートメントを使用します。 詳細については、「[GRANT](../../t-sql/statements/grant-transact-sql.md)」を参照してください。
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-login-with-a-password"></a>A. パスワード付きのログインを作成する  
 次の例では、特定のユーザーのログインを作成し、パスワードを割り当てます。 
  
```sql  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-login-from-a-sid"></a>B. SID からログインを作成します。  
 次の例では、まず、SQL Server 認証のログインを作成し、ログインの SID を調べています。 
  
```sql  
CREATE LOGIN TestLogin WITH PASSWORD = 'SuperSecret52&&';  
  
SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
 クエリでは、SID として 0x241C11948AEEB749B0D22646DB1A19F2 を返します。 クエリでは、別の値を返します。 次のステートメントは、ログインを削除し、ログインを作成し直します。 前のクエリから SID を使用します。 
  
```sql  
DROP LOGIN TestLogin;  
GO  
  
CREATE LOGIN TestLogin   
WITH PASSWORD = 'SuperSecret52&&', SID = 0x241C11948AEEB749B0D22646DB1A19F2;  
  
SELECT * FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [データベース エンジンの権限の概要](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [パスワード ポリシー](../../relational-databases/security/password-policy.md)   
 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)   
 [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)   
 [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
 [ログインの作成](../../relational-databases/security/authentication-access/create-a-login.md)  

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]
> <table>
> <tr>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
> </tr>
> <tr>
>   <th><a href="create-login-transact-sql.md?view=sql-server-2016">SQL Server</a></th>
>   <th><a href="create-login-transact-sql.md?view=azuresqldb-current">SQL Database<br />論理サーバー</a></th>
>   <th><strong><em>* SQL Database<br />Managed Instance *</em></strong></th>
>   <th><a href="create-login-transact-sql.md?view=azure-sqldw-latest">SQL Data<br />Warehouse</a></th>
>   <th><a href="create-login-transact-sql.md?view=aps-pdw-2016">SQL Parallel<br />Data Warehouse</a></th>
> </tr>
> </table>

&nbsp;

# <a name="azure-sql-database-managed-instance"></a>Azure SQL Database Managed Instance

## <a name="overview"></a>概要

## <a name="syntax"></a>構文 
  
```sql
-- Syntax for Azure SQL Database  
CREATE LOGIN login_name  
 { WITH <option_list> }  
  
<option_list> ::=   
    PASSWORD = { 'password' }  
    [ , SID = sid ]  
```  

## <a name="arguments"></a>引数  
*login_name*  
作成するログインの名前を指定します。 Azure SQL Database Managed Instance では SQL ログインのみがサポートされます。 

PASSWORD **='** password**'*  
作成する SQL ログインのパスワードを指定します。 強力なパスワードを使用する必要があります。 詳細については、「[強力なパスワード](../../relational-databases/security/strong-passwords.md)」と「[パスワード ポリシー](../../relational-databases/security/password-policy.md)」を参照してください。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降では、保存されたパスワード情報は salt 化パスワードの SHA-512 を使用して計算されます。 
  
パスワードでは大文字と小文字が区別されます。 パスワードの長さは 8 文字以上 128 文字以下である必要があります。 パスワードには、a ～ z、A ～ Z、0 ～ 9 およびほとんどの英数字以外の文字を含めることができます。 パスワードには、単一引用符、または *login_name* を含めることはできません。 

SID = *sid*  
ログインを再作成に使用されます。 Windows 認証ログインではなく、SQL Server 認証ログインにのみ適用されます。 新しい SQL Server 認証ログインの SID を指定します。 このオプションが使用されていない場合、SQL Server で自動的に SID が割り当てられます。 SID 構造体は、SQL Server のバージョンに依存します。 SQL Database の場合、これは、`0x01060000000000640000000000000000` と、GUID を表す 16 バイトで構成される 32 バイト (**binary(32)**) のリテラルです。 たとえば、 `SID = 0x0106000000000064000000000000000014585E90117152449347750164BA00A7`のようにします。 
  
## <a name="remarks"></a>Remarks  
- パスワードでは大文字と小文字が区別されます。
- スクリプトでログインを転送する場合は、「[SQL Server 2005 のインスタンス間でログインおよびパスワードを転送する方法](http://support.microsoft.com/kb/918992)」を参照してください。
- ログインを作成すると、自動的に新しいログインが有効になり、ログインにサーバー レベルの **CONNECT SQL** 権限が与えられます。 
- アクセスを許可するにはサーバーの[認証モード](../../relational-databases/security/choose-an-authentication-mode.md)がログインの種類に一致する必要があります。
    - 権限システムの設計の詳細については、「 [データベース エンジンの権限の概要](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)」を参照してください。
  
## <a name="login"></a>Login

### <a name="sql-database-logins"></a>SQL データベース ログイン
**CREATE LOGIN** ステートメントはバッチ内の唯一のステートメントである必要があります。 
  
**sqlcmd** などの SQL Database に接続するいくつかのメソッドでは、*\<login>*@*\<server>* の表記法を使用して、接続文字列のログイン名に SQL Database サーバー名を追加する必要があります。 たとえば、ログインが `login1` で、SQL Database サーバーの完全修飾名が `servername.database.windows.net` である場合、接続文字列の *username* パラメーターは `login1@servername` となる必要があります。 の合計の長さ、 *username* パラメーターには、128 文字まで *login_name* サーバー名の長さマイナス 127 文字に制限されます。 この例では、`login_name` が 10 文字であるため、`servername` には 117 文字までしか指定できません。 
  
SQL Database では、ログインを作成する際に master データベースに接続する必要があります。 
  
 SQL Server ルールを使用すると、\<loginname>@\<servername> 形式の SQL Server 認証ログインを作成できます。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] サーバーが **myazureserver** で、ログインが **myemail@live.com** である場合、**myemail@live.com@myazureserver** としてログインを指定する必要があります。 
  
SQL Database では、接続の認証に必要なログイン データおよびサーバー レベルのファイアウォール規則は、各データベースで一時的にキャッシュされます。 このキャッシュは定期的に更新されます。 認証キャッシュを強制的に更新し、データベースに最新バージョンのログイン テーブルがあることを確認するには、[DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md) を実行します。 
  
 SQL Database ログインの詳細については、[Windows Azure SQL Database におけるデータベースとログインの管理](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins)に関する記事を参照してください。 
 
## <a name="permissions"></a>アクセス許可

サーバーレベル プリンシパルのログイン (準備プロセスで作成) または master データベースの `loginmanager` データベース ロールのメンバーだけが新しいログインを作成できます。 詳細については、[サーバー レベルのロール](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles)と [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) (https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles) に関するページを参照してください。

## <a name="logins"></a>Login
- サーバーに対する **ALTER ANY LOGIN** 権限または **securityadmin** 固定サーバー ロールのメンバーシップが必要です。 このコマンドを実行できるのは、サーバーに対する **ALTER ANY LOGIN** 権限または securityadmin 権限のメンバーシップを持つ Azure Active Directory (Azure AD) アカウントのみです。
- Azure SQL 論理サーバーで使用されるのと同じディレクトリ内の Azure AD のメンバーである必要があります。
  
## <a name="after-creating-a-login"></a>ログインを作成した後  
ログインが作成されたら、ログインは SQL Database に接続できますが、**public** ロールに与えられた権限しか持ちません。 次の操作のいくつかを実行することを検討してください。 
  
- データベースに接続するには、そのデータベースにログイン用のデータベース ユーザーを作成する必要があります。 詳細については、[CREATE USER](../../t-sql/statements/create-user-transact-sql.md) に関するページを参照してください。 
- データベースのユーザーに権限を付与するには、**ALTER SERVER ROLE** ...  **ADD MEMBER** ステートメントを使用して組み込みのデータベース ロールのいずれか、またはカスタム ロールにユーザーを追加するか、[GRANT]((../../t-sql/statements/grant-transact-sql.md) ステートメントを使用して直接ユーザーに権限を付与します。 詳細については、[管理者以外のロール](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#non-administrator-users)、[ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) (https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles)、および [GRANT](grant-transact-sql.md) ステートメントに関するページを参照してください。
- サーバー全体の権限を付与するには、master データベースにデータベース ユーザーを作成し、**ALTER SERVER ROLE** ...  **ADD MEMBER** ステートメントを使用して、管理サーバー ロールのいずれかにユーザーを追加します。 詳細については、[サーバー レベルのロール](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles)、[ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md)、および[サーバー ロール](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles)に関するページを参照してください。
- 新しいログインまたはログインを含むロールにサーバー レベルの権限を許可するには、**GRANT** ステートメントを使用します。 詳細については、「[GRANT](../../t-sql/statements/grant-transact-sql.md)」を参照してください。
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-login-with-a-password"></a>A. パスワード付きのログインを作成する  
 次の例では、特定のユーザーのログインを作成し、パスワードを割り当てます。 
  
```sql  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-login-from-a-sid"></a>B. SID からログインを作成します。  
 次の例では、まず、SQL Server 認証のログインを作成し、ログインの SID を調べています。 
  
```sql  
CREATE LOGIN TestLogin WITH PASSWORD = 'SuperSecret52&&';  
  
SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
 クエリでは、SID として 0x241C11948AEEB749B0D22646DB1A19F2 を返します。 クエリでは、別の値を返します。 次のステートメントは、ログインを削除し、ログインを作成し直します。 前のクエリから SID を使用します。 
  
```sql  
DROP LOGIN TestLogin;  
GO  
  
CREATE LOGIN TestLogin   
WITH PASSWORD = 'SuperSecret52&&', SID = 0x241C11948AEEB749B0D22646DB1A19F2;  
  
SELECT * FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [データベース エンジンの権限の概要](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [パスワード ポリシー](../../relational-databases/security/password-policy.md)   
 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)   
 [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)   
 [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
 [ログインの作成](../../relational-databases/security/authentication-access/create-a-login.md)  


  
::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]
> <table>
> <tr>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
> </tr>
> <tr>
>   <th><a href="create-login-transact-sql.md?view=sql-server-2016">SQL Server</a></th>
>   <th><a href="create-login-transact-sql.md?view=azuresqldb-current">SQL Database<br />論理サーバー</a></th>>   <th><strong><em>* SQL Data<br />Warehouse *</em></strong></th>
>   <th><a href="create-login-transact-sql.md?view=aps-pdw-2016">SQL Parallel<br />Data Warehouse</a></th>
> </tr>
> </table>

&nbsp;

# <a name="azure-sql-data-warehouse"></a>Azure SQL データ ウェアハウス
  
## <a name="syntax"></a>構文 
  
```
-- Syntax for Azure SQL Data Warehouse  
CREATE LOGIN login_name  
 { WITH <option_list> }  
  
<option_list> ::=   
    PASSWORD = { 'password' }  
    [ , SID = sid ]  
```  
  
## <a name="arguments"></a>引数  
*login_name*  
作成するログインの名前を指定します。 Azure SQL Database では SQL ログインのみがサポートされます。 

PASSWORD **='** password**'*  
作成する SQL ログインのパスワードを指定します。 強力なパスワードを使用する必要があります。 詳細については、「[強力なパスワード](../../relational-databases/security/strong-passwords.md)」と「[パスワード ポリシー](../../relational-databases/security/password-policy.md)」を参照してください。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降では、保存されたパスワード情報は salt 化パスワードの SHA-512 を使用して計算されます。 
  
パスワードでは大文字と小文字が区別されます。 パスワードの長さは 8 文字以上 128 文字以下である必要があります。 パスワードには、a ～ z、A ～ Z、0 ～ 9 およびほとんどの英数字以外の文字を含めることができます。 パスワードには、単一引用符、または *login_name* を含めることはできません。 

 SID = *sid*  
 ログインを再作成に使用されます。 Windows 認証ログインではなく、SQL Server 認証ログインにのみ適用されます。 新しい SQL Server 認証ログインの SID を指定します。 このオプションが使用されていない場合、SQL Server で自動的に SID が割り当てられます。 SID 構造体は、SQL Server のバージョンに依存します。 SQL Data Warehouse の場合、これは、`0x01060000000000640000000000000000` と、GUID を表す 16 バイトで構成される 32 バイト (**binary(32)**) のリテラルです。 たとえば、 `SID = 0x0106000000000064000000000000000014585E90117152449347750164BA00A7`のようにします。 
  
## <a name="remarks"></a>Remarks  
- パスワードでは大文字と小文字が区別されます。
- スクリプトでログインを転送する場合は、「[SQL Server 2005 のインスタンス間でログインおよびパスワードを転送する方法](http://support.microsoft.com/kb/918992)」を参照してください。
- ログインを作成すると、自動的に新しいログインが有効になり、ログインにサーバー レベルの **CONNECT SQL** 権限が与えられます。 
- アクセスを許可するにはサーバーの[認証モード](../../relational-databases/security/choose-an-authentication-mode.md)がログインの種類に一致する必要があります。
    - 権限システムの設計の詳細については、「 [データベース エンジンの権限の概要](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)」を参照してください。
  
## <a name="logins"></a>Login

**CREATE LOGIN** ステートメントはバッチ内の唯一のステートメントである必要があります。 
  
**sqlcmd** などの SQL Data Warehouse に接続するいくつかのメソッドでは、*\<login>*@*\<server>* の表記法を使用して、接続文字列のログイン名に SQL Data Warehouse サーバー名を追加する必要があります。 たとえば、ログインが `login1` で、SQL Data Warehouse サーバーの完全修飾名が `servername.database.windows.net` である場合、接続文字列の *username* パラメーターは `login1@servername` となる必要があります。 の合計の長さ、 *username* パラメーターには、128 文字まで *login_name* サーバー名の長さマイナス 127 文字に制限されます。 この例では、`login_name` が 10 文字であるため、`servername` には 117 文字までしか指定できません。 
  
SQL Data Warehouse では、ログインを作成する際に master データベースに接続する必要があります。 
  
 SQL Server ルールを使用すると、\<loginname>@\<servername> 形式の SQL Server 認証ログインを作成できます。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] サーバーが **myazureserver** で、ログインが **myemail@live.com** である場合、**myemail@live.com@myazureserver** としてログインを指定する必要があります。 
  
SQL Data Warehouse では、接続の認証に必要なログイン データおよびサーバー レベルのファイアウォール規則は、各データベースで一時的にキャッシュされます。 このキャッシュは定期的に更新されます。 認証キャッシュを強制的に更新し、データベースに最新バージョンのログイン テーブルがあることを確認するには、[DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md) を実行します。 
  
 SQL Data Warehouse ログインの詳細については、[Windows Azure SQL Database におけるデータベースとログインの管理](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins)に関する記事を参照してください。 
 
## <a name="permissions"></a>アクセス許可

サーバーレベル プリンシパルのログイン (準備プロセスで作成) または master データベースの `loginmanager` データベース ロールのメンバーだけが新しいログインを作成できます。 詳細については、[サーバー レベルのロール](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles)と [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) (https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles) に関するページを参照してください。

## <a name="after-creating-a-login"></a>ログインを作成した後  
ログインが作成されたら、ログインは SQL Data Warehouse に接続できますが、**public** ロールに与えられた権限しか持ちません。 次の操作のいくつかを実行することを検討してください。 
  
- データベースに接続するには、ログイン用のデータベース ユーザーを作成する必要があります。 詳細については、[CREATE USER](../../t-sql/statements/create-user-transact-sql.md) に関するページを参照してください。
- データベースのユーザーに権限を付与するには、**ALTER SERVER ROLE** ...  **ADD MEMBER** ステートメントを使用して組み込みデータベース ロールのいずれか、またはカスタム ロールにユーザーを追加するか、[GRANT](grant-transact-sql.md) ステートメントを使用して直接ユーザーに権限を付与します。 詳細については、[管理者以外のロール](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#non-administrator-users)、[ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) (https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles)、および [GRANT](grant-transact-sql.md) ステートメントに関するページを参照してください。
- サーバー全体の権限を付与するには、master データベースにデータベース ユーザーを作成し、**ALTER SERVER ROLE** ...  **ADD MEMBER** ステートメントを使用して、管理サーバー ロールのいずれかにユーザーを追加します。 詳細については、[サーバー レベルのロール](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles)、[ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md)、および[サーバー ロール](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles)に関するページを参照してください。

- 新しいログインまたはログインを含むロールにサーバー レベルの権限を許可するには、**GRANT** ステートメントを使用します。 詳細については、「[GRANT](../../t-sql/statements/grant-transact-sql.md)」を参照してください。 
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-login-with-a-password"></a>A. パスワード付きのログインを作成する  
次の例では、特定のユーザーのログインを作成し、パスワードを割り当てます。 
  
```sql  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';  
GO  
```  

### <a name="b-creating-a-login-from-a-sid"></a>B. SID からログインを作成します。  
 次の例では、まず、SQL Server 認証のログインを作成し、ログインの SID を調べています。 
  
```sql  
CREATE LOGIN TestLogin WITH PASSWORD = 'SuperSecret52&&';  
  
SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
 クエリでは、SID として 0x241C11948AEEB749B0D22646DB1A19F2 を返します。 クエリでは、別の値を返します。 次のステートメントは、ログインを削除し、ログインを作成し直します。 前のクエリから SID を使用します。 
  
```sql  
DROP LOGIN TestLogin;  
GO  
  
CREATE LOGIN TestLogin   
WITH PASSWORD = 'SuperSecret52&&', SID = 0x241C11948AEEB749B0D22646DB1A19F2;  
  
SELECT * FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [データベース エンジンの権限の概要](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [パスワード ポリシー](../../relational-databases/security/password-policy.md)   
 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)   
 [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)   
 [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
 [ログインの作成](../../relational-databases/security/authentication-access/create-a-login.md)  
  
::: moniker-end
::: moniker range="=aps-pdw-2016||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]
> <table>
> <tr>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
>   <th> &nbsp; </th>
> </tr>
> <tr>
>   <th><a href="create-login-transact-sql.md?view=sql-server-2016">SQL Server</a></th>
>   <th><a href="create-login-transact-sql.md?view=azuresqldb-current">SQL Database<br />論理サーバー</a></th>
>   <th><a href="create-login-transact-sql.md?view=azure-sqldw-latest">SQL Data<br />Warehouse</a></th>
>   <th><strong><em>* SQL Parallel<br />Data Warehouse *</em></strong></th>
> </tr>
> </table>

&nbsp;

# <a name="sql-parallel-data-warehouse"></a>SQL Parallel Data Warehouse

  
## <a name="syntax"></a>構文 
  
```
-- Syntax for Parallel Data Warehouse  
CREATE LOGIN loginName { WITH <option_list1> | FROM WINDOWS }  
  
<option_list1> ::=   
    PASSWORD = { 'password' } [ MUST_CHANGE ]  
    [ , <option_list> [ ,... ] ]  
  
<option_list> ::=    
      CHECK_EXPIRATION = { ON | OFF}  
    | CHECK_POLICY = { ON | OFF}  
```  

## <a name="arguments"></a>引数  
*login_name*  
作成するログインの名前を指定します。 ログインには、SQL Server ログイン、Windows ログイン、証明書マッピング ログイン、非対称キー マッピング ログインの 4 種類があります。 Windows ドメイン アカウントからマップされるログインを作成する場合は、Windows 2000 よりも前の Windows で使用されていた [\<domainName>\\<login_name>] 形式のユーザー ログイン名を使用する必要があります。 login_name@DomainName 形式の UPN は使用できません。 例については、この記事の後半の例 D を参照してください。 認証ログインは **sysname** 型であり、[識別子](../../relational-databases/databases/database-identifiers.md) のルールに従っている必要があります。このログインに "**\\**" を含めることはできません。 Windows ログインには "**\\**" を含めることができます。 Active Directory ユーザーに基づくログインは、21 文字未満の名前に制限されます。 

PASSWORD **='***password***'* SQL Server ログインにのみ適用されます。 作成するログインのパスワードを指定します。 強力なパスワードを使用する必要があります。 詳細については、「[強力なパスワード](../../relational-databases/security/strong-passwords.md)」と「[パスワード ポリシー](../../relational-databases/security/password-policy.md)」を参照してください。 SQL Server 2012 (11.x) 以降では、保存されたパスワード情報は salt 化パスワードの SHA-512 を使用して計算されます。 
  
パスワードでは大文字と小文字が区別されます。 パスワードの長さは 8 文字以上 128 文字以下である必要があります。 パスワードには、a ～ z、A ～ Z、0 ～ 9 およびほとんどの英数字以外の文字を含めることができます。 パスワードには、単一引用符、または *login_name* を含めることはできません。 
  
MUST_CHANGE SQL Server ログインにのみ適用されます。 このオプションが含まれている場合、SQL Server では、新しいログインが最初に使用されたときに、ユーザーに新しいパスワードの入力が求められます。 
  
CHECK_EXPIRATION **=** { ON | **OFF** }  
SQL Server ログインにのみ適用されます。 このログインに、パスワードの有効期限ポリシーを適用するかどうかを指定します。 既定値は OFF です。 
  
CHECK_POLICY **=** { **ON** | OFF }  
SQL Server ログインにのみ適用されます。 SQL Server を実行しているコンピューターの Windows パスワード ポリシーをこのログインに適用するかどうかを指定します。 既定値は ON です。 
  
Windows のポリシーで強力なパスワードが求められる場合は、次の 4 つの特性のうちの少なくとも 3 つをパスワードに含める必要があります。  
  
- 大文字 (A ～ Z)。 
- 小文字 (a ～ z)。 
- 数字 (0 ～ 9)。 
- スペース、_、@、*、^、%、!、$、#、& などの英数字以外の文字。 
  
WINDOWS  
ログインを Windows ログインにマップするよう指定します。 
  
## <a name="remarks"></a>Remarks  
- パスワードでは大文字と小文字が区別されます。
- MUST_CHANGE が指定された場合、CHECK_EXPIRATION および CHECK_POLICY は ON に設定されなければなりません。 ON に設定しない場合、ステートメントは失敗します。
- CHECK_POLICY = OFF と CHECK_EXPIRATION = ON の組み合わせはサポートされていません。
- CHECK_POLICY を OFF に設定すると、*lockout_time* はリセットされ、CHECK_EXPIRATION は OFF に設定されます。 
  
> [!IMPORTANT]  
>  CHECK_EXPIRATION および CHECK_POLICY は、Windows Server 2003 以降でのみ適用されます。 詳細については、「 [Password Policy](../../relational-databases/security/password-policy.md)」をご参照ください。 
  
- スクリプトでログインを転送する場合は、「[SQL Server 2005 のインスタンス間でログインおよびパスワードを転送する方法](http://support.microsoft.com/kb/918992)」を参照してください。
- ログインを作成すると、自動的に新しいログインが有効になり、ログインにサーバー レベルの **CONNECT SQL** 権限が与えられます。 
- 権限システムの設計の詳細については、「 [データベース エンジンの権限の概要](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)」を参照してください。

## <a name="permissions"></a>アクセス許可  
ログインを作成できるのは、サーバーに対する **ALTER ANY LOGIN** 権限、または **securityadmin** 固定サーバー ロールのメンバーシップを持つユーザーのみとなります。 詳細については、[サーバー レベルのロール](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles)と [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) (https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles) に関するページを参照してください。
  
## <a name="after-creating-a-login"></a>ログインを作成した後  
ログインが作成されたら、ログインは SQL Data Warehouse に接続できますが、**public** ロールに与えられた権限しか持ちません。 次の操作のいくつかを実行することを検討してください。 
  
 - データベースに接続するには、ログイン用のデータベース ユーザーを作成する必要があります。 詳細については、[CREATE USER](../../t-sql/statements/create-user-transact-sql.md) に関するページを参照してください。 
  
 - [CREATE SERVER ROLE](../../t-sql/statements/create-server-role-transact-sql.md) を使用して、ユーザー定義サーバー ロールを作成します。 使用して **サーバー ロールの ALTER** しています. **メンバーの追加** をユーザー定義サーバー ロールに、新しいログインを追加します。 詳細については、[CREATE SERVER ROLE](../../t-sql/statements/create-server-role-transact-sql.md) と [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) に関するページを参照してください。 
  
 - 固定サーバー ロールにログインを追加するには、**sp_addsrvrolemember** を使用します。 詳細については、「[サーバー レベルのロール](../../relational-databases/security/authentication-access/server-level-roles.md)」と「[sp_addsrvrolemember](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)」を参照してください。 
  
 - 新しいログインまたはログインを含むロールにサーバー レベルの権限を許可するには、**GRANT** ステートメントを使用します。 詳細については、「[GRANT](../../t-sql/statements/grant-transact-sql.md)」を参照してください。 
  
## <a name="examples"></a>使用例  
  
### <a name="g-creating-a-sql-server-authentication-login-with-a-password"></a>G. パスワード付きで SQL Server 認証ログインを作成する  
 次の例では、パスワード `A2c3456` のログイン `Mary7`を作成します。 
  
```sql  
CREATE LOGIN Mary7 WITH PASSWORD = 'A2c3456$#' ;  
```  
  
### <a name="h-using-options"></a>H. オプションを使用する  
 次の例では、ログイン `Mary8` をパスワードおよびいくつかのオプションの引数と共に作成します。 
  
```sql  
CREATE LOGIN Mary8 WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
```  
  
### <a name="i-creating-a-login-from-a-windows-domain-account"></a>I. Windows ドメイン アカウントからログインを作成する  
 次の例では、`Contoso` ドメイン内の `Mary` という名前の Windows ドメイン アカウントからログインを作成します。 
  
```sql  
CREATE LOGIN [Contoso\Mary] FROM WINDOWS;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [データベース エンジンの権限の概要](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [パスワード ポリシー](../../relational-databases/security/password-policy.md)   
 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)   
 [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)   
 [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
 [ログインの作成](../../relational-databases/security/authentication-access/create-a-login.md)  
  
---  

::: moniker-end
