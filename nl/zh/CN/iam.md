---

copyright:
  years: 2014, 2019
lastupdated: "2019-01-21"

keywords:

subcollection: Db2whc

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

# {{site.data.keyword.Bluemix_notm}} 上的 Identity and Access Management (IAM)
{: #iam}

通过 Identity and Access Management (IAM)，您能够安全地对平台服务的用户进行认证，并以一致的方式控制对整个 {{site.data.keyword.Bluemix_notm}} 平台上资源的访问。例如，只需使用您的 IBM 标识登录一次 {{site.data.keyword.Bluemix_notm}}，就可以访问任何服务控制台及其应用程序，而无需单独登录到每个服务控制台和应用程序。
{: shortdesc}

## 实例上是否启用了 IAM？
{: #enabled}

在一段时间内，将在 {{site.data.keyword.Bluemix_notm}} 的 {{site.data.keyword.dashdblong}} 受管数据库实例上启用 IAM 进行访问控制。要检查实例上是否启用了 IAM，请运行以下查询：

`SELECT CASE WHEN VALUE = 'IBMIAMauth' THEN 1 ELSE 0 END AS IAM_ENABLED FROM SYSIBMADM.DBMCFG WHERE NAME = 'srvcon_gssplugin_list'`

如果 **IAM_ENABLED** 的返回值为 1，说明实例上启用了 IAM。

## {{site.data.keyword.Bluemix_notm}} IAM 的功能
{: #features}

针对使用两种类型受支持身份的 {{site.data.keyword.dashdbshort_notm}} 管理的服务，实现了以下 IAM 功能：

**IBM 标识**

数据库管理员必须通过控制台或 REST API 将具有 IBM 标识的用户添加到每个数据库服务实例，然后这些用户才能连接到特定数据库服务实例。与非 IBM 标识用户一样，必须在添加 IBM 标识用户的同时，输入数据库服务实例的用户标识。此用户标识需要在数据库服务实例中唯一。此用户标识也是数据库中的授权 (AUTH) 标识。数据库管理员可以根据 AUTH 标识来授予和撤销许可权。

**服务标识**

服务标识用于标识服务或应用程序，类似于用户标识对用户进行标识的方式。服务标识是可以由应用程序用于向 {{site.data.keyword.Bluemix_notm}} 服务进行认证的标识。服务标识代表持有 IBM 标识中的独立实体。因此，可以授予特定于数据库中服务标识的不同权限和许可权。服务标识没有密码。必须为每个服务标识创建一个 API 密钥，相应的服务标识才能连接到数据库服务实例。有关服务标识的更多信息，请参阅：[{{site.data.keyword.Bluemix_notm}} IAM 服务标识和 API 密钥简介 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/blogs/bluemix/2017/10/introducing-ibm-cloud-iam-service-ids-api-keys/){:new_window}。

## 客户机连接和用户登录
{: #connect_login}

**先决条件**：Db2 Client V11.1 FP3 和更高版本。

以下方法可用于 IAM 认证：

**访问令牌**

访问令牌可以由应用程序使用 API 密钥通过 REST API 直接从 IAM 服务获取。有关更多信息，请参阅：[使用 API 密钥获取 {{site.data.keyword.Bluemix_notm}} IAM 令牌 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/docs/iam/apikey_iamtoken.html#iamtoken_from_apikey){:new_window}。访问令牌的缺省有效期为 60 分钟，在此时间后即到期。如果令牌已到期，那么 Db2 服务器不会允许建立连接。但建立连接后，不会检查令牌是否到期。与集成 IAM 之前一样，连接将保持连接状态，直至应用程序断开连接或由于其他原因而终止连接。

```
curl -k -X POST \
  --header "Content-Type: application/x-www-form-urlencoded" \
  --header "Accept: application/json" \
  --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
  --data-urlencode "apikey=<apikey>" \
  "https://iam.bluemix.net/identity/token"
```

访问令牌用于向数据库表识别 IBM 标识用户或服务标识。数据库服务器在接受访问令牌之前，会验证其有效性。如果应用程序需要连接到多个数据库服务实例或其他 {{site.data.keyword.Bluemix_notm}} 服务实例，那么这是最佳方法，因为它会最大限度减少与 IAM 服务的通信来验证访问令牌。

**API 密钥**

可以为每个 IBM 标识用户或服务标识创建多个 API 密钥。每个 API 密钥通常是为一个应用程序创建的。只要将持有 IBM 标识或服务标识添加为同一数据库服务实例的用户，就能允许应用程序连接到该数据库服务实例。API 密钥在数据库中拥有与持有 IBM 标识或服务标识相同的权限和许可权。如果不应该再允许某个应用程序连接到数据库，那么可以除去相应的 API 密钥。此认证方法无需与 IAM 服务进行直接交互，因此在应用程序中需要的更改比使用访问令牌时需要的更改要少。有关创建和管理 API 密钥的更多信息，请参阅：[管理用户 API 密钥 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://console.bluemix.net/docs/iam/userid_keys.html#userapikey){:new_window}。

**IBM 标识/密码**

IBM 标识/密码可以用于登录到控制台，也可以在应用程序中按照允许使用用户标识/密码的相同方式进行使用。但在联合 IBM 标识时例外，因为无法重定向到您组织的登录页面。但是，要使应用程序与数据库服务实例建立连接，建议的方法是使用访问令牌。

## 支持的接口
{: #sup-if}

支持以下数据库客户机接口：

* [ODBC](#odbc-clpplus)
* [CLP](#odbc-clpplus)
* [CLPPLUS](#odbc-clpplus)
* [JDBC](#jdbc)

### ODBC、CLP、和 CLPPLUS
{: #odbc-clpplus}

要使 ODBC 应用程序或命令行客户机 (CLP, CLPPLUS) 能够使用 IAM 认证连接到 Db2 服务器，需要通过运行以下命令首先在 `db2dsdriver.cfg` 配置文件中配置数据源名称 (DSN)：

`db2cli writecfg add -dsn <dsn_alias> -database <database_name> -host <host_name_or_IP_address> -port 50001 -parameter "Authentication=GSSPLUGIN;SecurityTransportMode=SSL"`

`db2dsdriver.cfg` 配置文件是一个 XML 文件，通常位于 `sqllib/cfg` 目录中，该目录包含 DSN 别名及其属性的列表。

以下 `db2dsdriver.cfg` 配置文件示例显示了用于建立数据库服务实例连接的配置。配置文件提供了 DSN 别名、数据库名称、主机名（或 IP 地址）以及**认证**类型和 **SecurityTransportMode** 参数值：

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

* ODBC 连接字符串可以包含下列其中一项：

    **访问令牌**

    `DSN=<dsn>;ACCESSTOKEN=<access_token>`

    **API 密钥**

    `DSN=<dsn>;APIKEY=<api_key>`

    **IBM 标识/密码**
    
    `DSN=<dsn>;UID=<ibmid>;PWD=<password>`

    对于 ODBC，可以在 `db2dsdriver.cfg` 配置文件或应用程序的连接字符串中指定 **AUTHENTICATION=GSSPLUGIN**。

* CLP CONNECT 语句可以包含下列其中一项：

    **访问令牌**

    连接到数据库服务器 `<database_server_name>` 并传递访问令牌：

    `CONNECT TO <database_server_name> ACCESSTOKEN <access_token_string>`

    **API 密钥**

    连接到数据库服务器 `<database_server_name>`：

    `CONNECT TO <database_server_name> APIKEY <api-key-string>`

    **IBM 标识/密码**

    连接到数据库服务器 `<database_server_name>`：

    `CONNECT TO <database_server_name> USER <IBMid> USING <password>`

    有关使用 CLP 连接数据库服务器的更多详细信息，请参阅 [CONNECT（第 2 类）语句 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.sql.ref.doc/doc/r0000908.html){:new_window}。 

* CLPPLUS CONNECT 语句可以包含下列其中一项：

    **访问令牌**

    连接到 DSN 别名 (`@<data_source_name>`) 并传递访问令牌：

    `connect @<data_source_name> using(accesstoken <access_token_string>)`

    **API 密钥**

    连接到 DSN 别名 (`@<data_source_name>`)：

    `connect @<data_source_name> using(apikey <api-key-string>)`

    **IBM 标识/密码**

    连接到 DSN 别名 (`@<data_source_name>`)：

    `connect <IBMid>/<password>@<data_source_name>`

    有关使用 CLPPLUS 连接到 DSN 别名的更多详细信息，请参阅：[CLPPlus 中的 DSN 别名 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/SSEPGG_11.1.0/com.ibm.swg.im.dbclient.clpplus.doc/doc/c0057148.html){:new_window}。

### JDBC
{: #jdbc}

IAM 认证支持第 4 类 JDBC 驱动程序。

以下示例显示了三种方法的连接片段：

**访问令牌**

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

或者

```
Connection conn = DriverManager.getConnection( "jdbc:db2://<host_name_or_IP_address>:50001/BLUDB:accessToken=<access_token>;securityMechanism=15;pluginName=IBMIAMauth;sslConnection=true" );
```

**API 密钥**

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

或者

```
Connection conn = DriverManager.getConnection( "jdbc:db2://<host_name_or_IP_address>:50001/BLUDB:apikey=<api_key>;securityMechanism=15;pluginName=IBMIAMauth;sslConnection=true" );
```

**IBM 标识/密码**

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

或者

```
Connection conn = DriverManager.getConnection( "jdbc:db2://<host_name_or_IP_address>:50001/BLUDB:user=<IBMid>;password=<password>;securityMechanism=15;pluginName=IBMIAMauth;sslConnection=true" );
```

## 控制台用户体验
{: #console-ux}

服务控制台登录页面提供了使用 IBM 标识和密码登录的选项。单击**通过 IBM 标识登录**按钮后，会将用户定向到 IAM 登录页面，以在其中输入密码。完成认证后，会将用户重定向回控制台。数据库管理员必须通过控制台或 REST API 将 IBM 标识用户添加到每个数据库服务实例后，此类登录才能成功。与非 IBM 标识用户一样，必须在添加 IBM 标识用户的同时，输入数据库服务实例的用户标识。此用户标识需要在数据库服务实例中唯一。此用户标识也是数据库中的授权 (AUTH) 标识。

## REST API 体验
{: #api}

{{site.data.keyword.dashdbshort_notm}} REST API 的功能已增强，先前接受数据库服务生成的访问令牌的功能现在还可接受 IAM 访问令牌。

* 要添加新的 IBM 标识用户，请运行以下示例 API 调用：

  `curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid>","ibmid":"<userid>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"`

  `<userid>` 值不必相同。这两个不同的标识不会以任何方式链接在一起。
  {: note}

* 要迁移现有的非 IBM 标识数据库用户（例如，`abcuser`）并使其成为 IBM 标识用户，请先通过运行以下示例 API 调用来删除非 IBM 标识用户的标识：

  `curl --tlsv1.2 -X DELETE "https://<IPaddress>/dbapi/v3/users/abcuser" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json"`

  接下来，通过运行以下示例 API 调用，重新添加其 IBM 标识与先前的用户标识 (`abcuser`) 相同的用户：

  `curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"abcuser","ibmid":"abcuser@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"`

  因为该用户标识 (`abcuser`) 对于该用户的新 IBM 标识保持不变，所以对该用户授予的数据库许可权也保持不变。如果需要迁移现有非 IBM 标识数据库用户的列表以使其成为 IBM 标识用户，那么您需要对每个用户运行先前的 API 调用对。

* 要一次添加多个新的 IBM 标识用户，请创建一个批处理文件，其中列出以下示例 API 调用，每个用户一个调用：

  ```
  curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid1>","ibmid":"<userid1>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"
  curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid2>","ibmid":"<userid2>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"
  .
  .
  .
  ```

有关服务的 API 的更多详细信息，请参阅：[{{site.data.keyword.dashdbshort_notm}} REST API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://ibm.biz/db2whc_api){:new_window}。

## IBM 标识联合
{: #ibmid_fed}

要使用您自己的身份提供者（例如，LDAP），您必须先使用 IBM 标识联合 LDAP 服务器。有关使用 IBM 标识联合 LDAP 服务器的指示信息，请参阅：[IBMid Enterprise Federation Adoption Guide ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://ibm.ent.box.com/notes/78040808400?s=nhuzrhlsn0ly338zddomx329tlpmfghc){:new_window}。完成 IBM 标识联合，并且数据库管理员将允许的用户添加到数据库服务实例后，这些用户就可以使用其公司用户标识和密码登录到控制台。或者，这些用户可以通过某个支持的数据库客户机接口，使用代表其用户标识的访问令牌或 API 密钥来连接到数据库服务实例。

## 限制
{: #restrictions}

下面是与 IAM 认证相关的限制：

* 对于连接到 Db2 服务器的 Db2 客户机，仅支持通过 SSL 连接进行 IAM 认证。
* 支持 IBM 标识联合，以允许将定制用户管理门户网站或服务器用于认证。此类支持不包括任何集团联合。
* 不支持对数据库联合进行 IAM 认证。
* 不支持通过 CLPPlus 运行 IDA 和用户定义的扩展 (UDX) 命令。
* 不支持第 2 类 JDBC 驱动程序。




