---

copyright:
  years: 2014, 2019
lastupdated: "2019-01-21"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}

# {{site.data.keyword.Bluemix_notm}} での Identity and access management (IAM)
{: #iam}

Identity and access management (IAM) を使用すると、プラットフォーム・サービスのユーザーをセキュアに認証でき、また {{site.data.keyword.Bluemix_notm}} プラットフォーム全体で一貫してリソースへのアクセスを制御できます。 例えば、IBMid を使用した {{site.data.keyword.Bluemix_notm}} への単一ログインのみで、どのサービス・コンソールおよびアプリケーションにも、それぞれ別々にログインせずにアクセスすることができます。
{: shortdesc}

## インスタンスで IAM は有効になっていますか?
{: #enabled}

一定期間にわたり、{{site.data.keyword.Bluemix_notm}} 上の {{site.data.keyword.dashdblong}} 管理対象データベース・インスタンスは、IAM をアクセス制御に使用できるようになります。 インスタンスで IAM が有効になっているかどうかを確認するには、以下の照会を実行してください。

`SELECT CASE WHEN VALUE = 'IBMIAMauth' THEN 1 ELSE 0 END AS IAM_ENABLED FROM SYSIBMADM.DBMCFG WHERE NAME = 'srvcon_gssplugin_list'`

**IAM_ENABLED** の戻り値が 1 の場合は、インスタンスで IAM が有効になっています。

## {{site.data.keyword.Bluemix_notm}} IAM のフィーチャー
{: #features}

2 つのタイプのサポートされる ID を使用して、{{site.data.keyword.dashdbshort_notm}} 管理対象サービスで以下の IAM フィーチャーが実装されています。

**IBMid**

IBMid を持つユーザーが特定のデータベース・サービス・インスタンスに接続する前に、データベース管理者はコンソールまたは REST API を介してそれらのユーザーを各データベース・サービス・インスタンスに追加する必要があります。 非 IBMid ユーザーの場合と同様に、データベース・サービス・インスタンスのユーザー ID は、IBMid ユーザーを追加するのと同時に入力する必要があります。 このユーザー ID は、データベース・サービス・インスタンス内で固有でなければなりません。 このユーザー ID はまた、データベース内の許可 (AUTH) ID でもあります。 データベース管理者は、その AUTH ID に基づいて許可を付与したり取り消したりすることができます。

**サービス ID**

ユーザー ID がユーザーを識別するのと同様の方法で、サービス ID はサービスまたはアプリケーションを識別します。 サービス ID は、アプリケーションが {{site.data.keyword.Bluemix_notm}} サービスでの認証を行うために使用できる ID です。 サービス ID は、所有する IBMid とは別個のエンティティーを表します。 したがって、データベース内のサービス ID に固有で、さまざまな権限と許可を付与できます。 サービス ID にはパスワードはありません。 サービス ID がデータベース・サービス・インスタンスに接続するためには、サービス ID ごとに API キーを作成する必要があります。 サービス ID について詳しくは、[Introducing {{site.data.keyword.Bluemix_notm}} IAM Service IDs and API Keys ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2017/10/introducing-ibm-cloud-iam-service-ids-api-keys/){:new_window} を参照してください。

## クライアント接続およびユーザー・ログイン
{: #connect}

**前提条件**: Db2 Client V11.1 FP3 以降。

IAM 認証には、以下の方式を使用できます。

**アクセス・トークン**

アクセス・トークンは、API キーを使用して REST API を介し、アプリケーションにより IAM サービスから直接入手できます。 詳しくは、[API キーを使用した {{site.data.keyword.Bluemix_notm}} IAM トークンの取得 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net/docs/iam/apikey_iamtoken.html#iamtoken_from_apikey){:new_window} を参照してください。 アクセス・トークンには、期限切れまでに 60 分間のデフォルト有効期間があります。 トークンの有効期限が切れると、Db2 サーバーは、接続の確立を許可しません。 接続が確立された後は、トークンの有効期限のチェックは行われません。 IAM 統合以前のように、アプリケーションが切断するか、他の理由によって接続が終了されるまで、接続されたままになります。

```
curl -k -X POST \
  --header "Content-Type: application/x-www-form-urlencoded" \
  --header "Accept: application/json" \
  --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
  --data-urlencode "apikey=<apikey>" \
  "https://iam.bluemix.net/identity/token"
```

アクセス・トークンは、IBMid ユーザー、またはデータベースへのサービス ID を識別します。 データベース・サーバーは、アクセス・トークンを受け入れる前に有効期間を確認します。 この方式を使用すると、アクセス・トークンを検証するための IAM サービスへの通信が最小限になるため、アプリケーションが複数のデータベース・サービス・インスタンスや他の {{site.data.keyword.Bluemix_notm}} サービス・インスタンスに接続する必要がある場合は、これが最良の方式になります。

**API キー**

IBMid ユーザーまたはサービス ID ごとに複数の API キーを作成できます。 通常、各 API キーは、単一アプリケーションに対して作成されます。 API キーは、所有する IBMid またはサービス ID がデータベース・サービス・インスタンスにユーザーとして追加されている限り、アプリケーションが同じデータベース・サービス・インスタンスに接続することを許可します。 API キーは、所有する IBMid またはサービス ID と同じ権限および許可をデータベース内で持っています。 アプリケーションのデータベースへの接続の許可を取りやめる場合は、対応する API キーを削除できます。 この認証方式は、IAM サービスとの直接対話が必要ないため、アクセス・トークンを使用した場合よりも、アプリケーションで行う変更が少なくなります。 API キーの作成および管理について詳しくは、[ユーザーの API キーの管理![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.bluemix.net/docs/iam/userid_keys.html#userapikey){:new_window} を参照してください。

**IBMid/パスワード**

IBMid/パスワードはコンソールへのログインに使用できます。また、ユーザー ID/パスワードが許可されているのと同じ方法でアプリケーション内で使用することもできます。 IBMid が統合されている場合は、ユーザーの組織のログイン・ページへのリダイレクトを実行できないため、例外が発生します。 ただし、アプリケーションがデータベース・サービス・インスタンスへの接続を確立するための推奨方式は、アクセス・トークンを使用することです。

## サポートされるインターフェース
{: #sup-if}

以下のデータベース・クライアント・インターフェースがサポートされています。

* [ODBC](#odbc-clpplus)
* [CLP](#odbc-clpplus)
* [CLPPLUS](#odbc-clpplus)
* [JDBC 
](#jdbc)

### ODBC、CLP、および CLPPLUS
{: #odbc-clpplus}

ODBC アプリケーションまたはコマンド・ライン・クライアント (CLP、CLPPLUS) が IAM 認証を使用して DB2 サーバーに接続するには、まず、以下のコマンドを実行して `db2dsdriver.cfg` 構成ファイル内にデータ・ソース名 (DSN) を構成する必要があります。

`db2cli writecfg add -dsn <dsn_alias> -database <database_name> -host <host_name_or_IP_address> -port 50001 -parameter "Authentication=GSSPLUGIN;SecurityTransportMode=SSL"`

`db2dsdriver.cfg` 構成ファイルは、DSN 別名とそれらのプロパティーのリストを含む XML ファイルで、通常、`sqllib/cfg` ディレクトリーにあります。

以下の `db2dsdriver.cfg` 構成ファイルの例は、データベース・サービス・インスタンスへの接続を確立するために使用される構成を示しています。 この構成ファイルは、DSN 別名、データベース名、ホスト名 (または IP アドレス)、および**認証**タイプと **SecurityTransportMode** パラメーター値を提供します。

```
<?xml version="1.0" encoding="UTF-8" standalone="no" ?>
<configuration>
        <dsncollection>
        <dsn alias="<data_source_name>" name="bludb" host="<host_name_or_IP_address>" port="50001">
            <parameter name="Authentication" value="GSSPLUGIN"/>
            <parameter name="SecurityTransportMode" value="SSL"/>
        </dsn>
        </dsncollection>
        <databases>
            <database name="bludb" host="<host_name_or_IP_address>" port="50001"/>
        </databases>
</configuration>
```

* ODBC 接続ストリングには、次のいずれかを含めることができます。

    **アクセス・トークン**

    `DSN=<dsn>;ACCESSTOKEN=<access_token>`

    **API キー**

    `DSN=<dsn>;APIKEY=<api_key>`

    **IBMid/パスワード**
    
    `DSN=<dsn>;UID=<ibmid>;PWD=<password>`

    ODBC の場合、`db2dsdriver.cfg` 構成ファイルまたはアプリケーションの接続ストリングのいずれかに **AUTHENTICATION=GSSPLUGIN** を指定できます。

* CLP CONNECT ステートメントには、次のいずれかを含めることができます。

    **アクセス・トークン**

    CLP コマンド・プロンプトまたはスクリプトで以下のコマンドを実行して、データベース・サーバー `<database_server_name>` に接続して、アクセス・トークンを渡します。

    `CONNECT TO <database_server_name> ACCESSTOKEN <access_token_string>`

    **API キー**

    CLP コマンド・プロンプトまたはスクリプトで以下のコマンドを実行して、API キーを使用してデータベース・サーバー `<database_server_name>` に接続します。

    `CONNECT TO <database_server_name> APIKEY <api-key-string>`

    **IBMid/パスワード**

    CLP コマンド・プロンプトまたはスクリプトで以下のコマンドを実行して、IBMid/パスワードを使用してデータベース・サーバー `<database_server_name>` に接続します。

    `CONNECT TO <database_server_name> USER <IBMid> USING <password>`

    CLP を使用したデータベース・サーバーへの接続について詳しくは、[CONNECT (type 2) ステートメント![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.sql.ref.doc/doc/r0000908.html){:new_window}を参照してください。 

* CLPPLUS CONNECT ステートメントには、次のいずれかを含めることができます。

    **アクセス・トークン**

    CLPPLUS コマンド・プロンプトまたはスクリプトで以下のコマンドを実行して、DSN 別名 (`@<data_source_name>`) に接続して、アクセス・トークンを渡します。

    `connect @<data_source_name> using(accesstoken <access_token_string>)`

    **API キー**

    CLPPLUS コマンド・プロンプトまたはスクリプトで以下のコマンドを実行して、API キーを使用して DSN 別名 (`@<data_source_name>`) に接続します。

    `connect @<data_source_name> using(apikey <api-key-string>)`

    **IBMid/パスワード**

    CLPPLUS コマンド・プロンプトまたはスクリプトで以下のコマンドを実行して、IBMid/パスワードを使用して DSN 別名 (`@<data_source_name>`) に接続します。

    `connect <IBMid>/<password>@<data_source_name>`

    CLPPLUS を使用した DSN 別名への接続について詳しくは、[CLPPlus での DSN 別名 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/SSEPGG_11.1.0/com.ibm.swg.im.dbclient.clpplus.doc/doc/c0057148.html){:new_window} を参照してください。

### JDBC
{: #jdbc}

IAM 認証では、タイプ 4 JDBC ドライバーがサポートされています。

以下の例は、3 つの方式の接続スニペットを示しています。

**アクセス・トークン**

```
DB2SimpleDataSource dataSource;

dataSource.setDriverType( 4 );
dataSource.setDatabaseName( "BLUDB" );
dataSource.setServerName( "<host_name_or_IP_address>" );
dataSource.setPortNumber( 50001 );
dataSource.setSecurityMechanism( com.ibm.db2.jcc.DB2BaseDataSource.PLUGIN_SECURITY );
dataSource.setPluginName( "IBMIAMauth" );
dataSource.setAccessToken( "<access_token>" );
Connection conn = dataSource.getConnection( );
```

または

```
Connection conn = DriverManager.getConnection( "jdbc:db2://<host_name_or_IP_address>:50001/BLUDB:accessToken=<access_token>;securityMechanism=15;pluginName=IBMIAMauth;sslConnection=true" );
```

**API キー**

```
DB2SimpleDataSource dataSource;

dataSource.setDriverType( 4 );
dataSource.setDatabaseName( "BLUDB" );
dataSource.setServerName( "<host_name_or_IP_address>" );
dataSource.setPortNumber( 50001 );
dataSource.setSecurityMechanism( com.ibm.db2.jcc.DB2BaseDataSource.PLUGIN_SECURITY );
dataSource.setPluginName( "IBMIAMauth" );
dataSource.setApiKey( "<api_key>" );
Connection conn = dataSource.getConnection( );
```

または

```
Connection conn = DriverManager.getConnection( "jdbc:db2://<host_name_or_IP_address>:50001/BLUDB:apikey=<api_key>;securityMechanism=15;pluginName=IBMIAMauth;sslConnection=true" );
```

**IBMid/パスワード**

```
DB2SimpleDataSource dataSource;

dataSource.setDriverType( 4 );
dataSource.setDatabaseName( "BLUDB" );
dataSource.setServerName( "<host_name_or_IP_address>" );
dataSource.setPortNumber( 50001 );
dataSource.setSecurityMechanism( com.ibm.db2.jcc.DB2BaseDataSource.PLUGIN_SECURITY );
dataSource.setPluginName( "IBMIAMauth" );
Connection conn = dataSource.getConnection( "<IBMid>", "<password>" );
```

または

```
Connection conn = DriverManager.getConnection( "jdbc:db2://<host_name_or_IP_address>:50001/BLUDB:user=<IBMid>;password=<password>;securityMechanism=15;pluginName=IBMIAMauth;sslConnection=true" );
```

## コンソール・ユーザー・エクスペリエンス
{: #console-ux}

サービス・コンソールのログイン・ページには、IBMid とパスワードを使用してログインするオプションがあります。 **「IBMid でサインイン (Sign In via IBMid)」**ボタンをクリックすると、ユーザーは IAM ログイン・ページに誘導され、そこでパスワードを入力します。 認証が完了すると、ユーザーはコンソールにリダイレクトされます。 そのようなログインを成功させるには、データベース管理者がコンソールまたは REST API を介して IBMid ユーザーを各データベース・サービス・インスタンスに追加する必要があります。 非 IBMid ユーザーの場合と同様に、データベース・サービス・インスタンスのユーザー ID は、IBMid ユーザーを追加するのと同時に入力する必要があります。 ユーザー ID は、データベース・サービス・インスタンス内で固有である必要があります。 このユーザー ID はまた、データベース内の許可 (AUTH) ID でもあります。

## REST API エクスペリエンス
{: #api}

{{site.data.keyword.dashdbshort_notm}} REST API は、以前データベース・サービスの生成したアクセス・トークンを受け入れていた機能で IAM アクセス・トークンも受け入れるように拡張されました。

* 新規 IBMid ユーザーを追加するには、以下のサンプル API 呼び出しを実行します。

  `curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid>","ibmid":"<userid>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"`

  `"id"` および `"ibmid"` の `<userid>` 値は同じである必要はありません。これらの 2 つの異なる ID が一緒にリンクされることはありません。
  {: note}

* 既存の非 IBMid データベース・ユーザー (例えば、`abcuser`) をマイグレーションして IBMid ユーザーにするには、まず、以下のサンプル API 呼び出しを実行して非 IBMid ユーザー ID を削除します。

  `curl --tlsv1.2 -X DELETE "https://<IPaddress>/dbapi/v3/users/abcuser" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json"`

  次に、以下のサンプル API 呼び出しを実行して、前のユーザー ID (`abcuser`) と同じ IBMid でユーザーを再び追加します。

  `curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"abcuser","ibmid":"abcuser@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"`

  そのユーザーのユーザー ID (`abcuser`) は、新しい IBMid でも同じままなので、そのユーザーに付与されるデータベース許可も変更されません。 既存の非 IBMid データベース・ユーザーのリストをマイグレーションしてそれらのユーザーを IBMid ユーザーにする必要がある場合は、ユーザーごとに、前述の API 呼び出しのペアを実行する必要があります。

* 多くの新規 IBMid ユーザーを同時に追加するには、以下のサンプル API 呼び出し (ユーザーごとに 1 つ) をリストするバッチ・ファイルを作成します。

  ```
  curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid1>","ibmid":"<userid1>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"
  curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid2>","ibmid":"<userid2>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"
  .
  .
  .
  ```

サービスの API について詳しくは、[{{site.data.keyword.dashdbshort_notm}} REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://ibm.biz/db2whc_api){:new_window} を参照してください。

## IBMid の統合
{: #fed}

LDAP などの独自の ID プロバイダーを使用するには、まず LDAP サーバーを IBMid に統合する必要があります。 LDAP サーバーと IBMid との統合に関する説明については、[IBMid Enterprise Federation Adoption Guide ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://ibm.ent.box.com/notes/78040808400?s=nhuzrhlsn0ly338zddomx329tlpmfghc){:new_window} を参照してください。 IBMid の統合が完了して、許可されたユーザーがデータベース管理者によってデータベース・サービス・インスタンスに追加されると、それらのユーザーは、自分の企業のユーザー ID とパスワードを使用してコンソールにログインできるようになります。 代わりに、それらのユーザーは、自分のユーザー ID を表すアクセス・トークンまたは API キーを使用して、サポートされるデータベース・クライアント・インターフェースのいずれかを介してデータベース・サービス・インスタンスに接続することもできます。

## 制約事項
{: #restrictions}

IAM 認証に関連する制約事項を以下に示します。

* Db2 サーバーに接続している Db2 クライアントの IAM 認証は、SSL 接続でのみサポートされます。
* IBMid 統合では、カスタム・ユーザー管理ポータルまたはサーバーを認証に使用することを許可することがサポートされています。 そのようなサポートには、グループ統合は含まれません。
* データベース統合のための IAM 認証はサポートされていません。
* CLPPlus からの IDA およびユーザー定義拡張機能 (UDX) コマンドの実行はサポートされていません。
* タイプ 2 JDBC ドライバーはサポートされていません。




