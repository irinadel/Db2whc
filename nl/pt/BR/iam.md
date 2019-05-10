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

# Identidade e gerenciamento de acesso (IAM) em  {{site.data.keyword.Bluemix_notm}}
{: #iam}

O Identity and access management (IAM) permite autenticar com segurança os usuários para serviços de plataforma e controlar o acesso aos recursos de forma consistente na plataforma do {{site.data.keyword.Bluemix_notm}}. Por exemplo, com apenas um único login no {{site.data.keyword.Bluemix_notm}} com seu IBMid, você tem acesso a qualquer um de seus consoles de serviço e aplicativos sem precisar efetuar login em cada um deles separadamente.
{: shortdesc}

## O IAM está ativado em sua instância?
{: #enabled}

Durante um período de tempo, as instâncias de banco de dados gerenciadas do {{site.data.keyword.dashdblong}} no {{site.data.keyword.Bluemix_notm}} serão ativadas para usar o IAM para controle de acesso. Para verificar se o IAM está ativado em sua instância, execute a consulta a seguir:

`SELECT CASE WHEN VALUE = 'IBMIAMauth' THEN 1 ELSE 0 END AS IAM_ENABLED FROM SYSIBMADM.DBMCFG WHERE NAME = 'srvcon_gssplugin_list'`

Se o valor retornado de **IAM_ENABLED** for 1, o IAM será ativado em sua instância.

## Recursos do  {{site.data.keyword.Bluemix_notm}}  IAM
{: #features}

Os recursos do IAM a seguir são implementados para o serviço gerenciado do {{site.data.keyword.dashdbshort_notm}} com dois tipos de identidades suportadas:

**ID IBM**

Os usuários com um IBMid devem ser incluídos em cada instância de serviço de banco de dados pelo administrador de banco de dados por meio do console ou da API de REST antes que possam se conectar à instância de serviço de banco de dados específica. Assim como para um usuário não IBMid, um ID do usuário para a instância de serviço de banco de dados deverá ser inserido ao mesmo tempo em que o usuário IBMid for incluído. Esse ID de usuário precisa ser exclusivo na instância de serviço de banco de dados. Esse ID do usuário também é o ID de autorização (AUTH) dentro do banco de dados. O administrador de banco de dados pode conceder e revogar permissões com base no ID de AUTENTICAÇÃO.

** IDs de Serviço **

Um ID de serviço identifica um serviço ou um aplicativo semelhante a como um ID de usuário identifica um usuário. Os IDs de serviço são IDs que podem ser usados pelos aplicativos para autenticação com um serviço do {{site.data.keyword.Bluemix_notm}}. Um ID de serviço representa uma entidade separada do IBMid proprietário. Portanto, podem ser concedidas diferentes autoridades e permissões específicas ao ID de serviço no banco de dados. Os IDs de serviço não possuem senhas. Uma chave API deve ser criada para cada ID de serviço do ID de serviço para conexão com a instância de serviço de banco de dados. Para obter mais informações sobre IDs de serviço, consulte: [Introduzindo IDs de serviço e chaves API do IAM do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2017/10/introducing-ibm-cloud-iam-service-ids-api-keys/){:new_window}.

## Conexões do Cliente e Logins do Usuário
{: #connect_login}

**Pré-requisito**: Db2 Client V11.1 FP3 e mais recente.

Os métodos a seguir podem ser usados para autenticação do IAM:

** Token de acesso **

Um token de acesso pode ser obtido do serviço do IAM diretamente pelo aplicativo por meio da API de REST usando uma chave API. Para obter mais informações, consulte: [Obtendo um token do IAM do {{site.data.keyword.Bluemix_notm}} usando uma chave API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](/docs/iam?topic=iam-iamtoken_from_apikey#iamtoken_from_apikey){:new_window}. O token de acesso tem um período de validade padrão de 60 minutos antes de expirar. Se o token tiver expirado, o servidor Db2 não permitirá que a conexão seja estabelecida. Depois que a conexão é estabelecida, o token não é verificado quanto à expiração. Assim como era antes da integração do IAM, a conexão permanecerá conectada até que o aplicativo seja desconectado ou a conexão seja finalizada devido a outros motivos.

```
curl -k -X POST \
  --header "Content-Type: application/x-www-form-urlencoded" \
  --header "Accept: application/json" \
  --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
  --data-urlencode "apikey=<apikey>" \
  "https://iam.bluemix.net/identity/token "
```

Um token de acesso identifica um usuário IBMid ou um ID de serviço para o banco de dados. O servidor de banco de dados verifica a validade do token de acesso antes de aceitá-lo. Esse será o melhor método se o aplicativo precisar se conectar a mais de uma instância de serviço de banco de dados ou a outras instâncias de serviço do {{site.data.keyword.Bluemix_notm}} porque minimiza a comunicação com o serviço do IAM para validar o token de acesso.

** Chave de API **

Várias chaves API podem ser criadas para cada usuário IBMid ou ID de serviço. Em geral, cada chave API é criada para um único aplicativo. Ela permite que o aplicativo se conecte à instância de serviço de banco de dados contanto que o IBMid proprietário ou o ID de serviço sejam incluídos como um usuário na mesma instância de serviço de banco de dados. A chave API possui as mesmas autoridades e permissões no banco de dados como o IBMid ou o ID de serviço proprietário. Se um aplicativo deve não ter mais permissão para se conectar ao banco de dados, a chave API correspondente pode ser removida. Esse método de autenticação requer menos mudanças no aplicativo do que o uso de um token de acesso, pois não requer nenhuma interação direta com o serviço do IAM. Para obter mais informações sobre a criação e o gerenciamento de chaves API, consulte: [Gerenciando chaves API do usuário ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](/docs/iam?topic=iam-userapikey#userapikey){:new_window}.

** IBMid/password **

O IBMid/senha pode ser usado para efetuar login no console e também pode ser usado no aplicativo das mesmas maneiras que um ID de usuário/senha tem permissão. A exceção ocorre quando o IBMid é federado porque um redirecionamento para a página de login de sua organização não pode ser feito. No entanto, o método recomendado para um aplicativo estabelecer uma conexão com a instância de serviço de banco de dados é usar um token de acesso.

## Interfaces Suportadas
{: #sup-if}

As interfaces do cliente de banco de dados a seguir são suportadas:

* [ ODBC ](#odbc-clpplus)
* [CLP](#odbc-clpplus)
* [ CLPPLUS ](#odbc-clpplus)
* [ JDBC ](#jdbc)

### ODBC, CLP e CLPPLUS
{: #odbc-clpplus}

Para que um aplicativo ODBC ou um cliente da linha de comando (CLP, CLPPLUS) se conecte a um servidor Db2 usando a autenticação do IAM, um nome de origem de dados (DSN) precisa ser configurado primeiro em um arquivo de configuração `db2dsdriver.cfg` executando o comando a seguir:

`db2cli writecfg add -dsn <dsn_alias> -database <database_name> -host <host_name_or_IP_address> -port 50001 -parameter "Authentication=GSSPLUGIN;SecurityTransportMode=SSL"`

O arquivo de configuração `db2dsdriver.cfg` é um arquivo XML, geralmente localizado no diretório `sqllib/cfg`, que contém uma lista de aliases DSN e suas propriedades.

O exemplo a seguir de um arquivo de configuração `db2dsdriver.cfg` mostra as configurações usadas para estabelecer uma conexão com uma instância de serviço de banco de dados. O arquivo de configuração fornece o alias do DSN, o nome do banco de dados, o nome do host (ou endereço IP) e os valores de parâmetro de tipo **Authentication** e **SecurityTransportMode**:

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

* A sequência de conexões ODBC pode conter um dos seguintes:

    ** Token de acesso **

    `DSN=<dsn>;ACCESSTOKEN=<access_token>`

    ** Chave de API **

    `DSN=<dsn>;APIKEY=<api_key>`

    ** IBMid/password **
    
    `DSN=<dsn>;UID=<ibmid>;PWD=<password>`

    Para ODBC, o **AUTHENTICATION=GSSPLUGIN** pode ser especificado no arquivo de configuração `db2dsdriver.cfg` ou na sequência de conexões do aplicativo.

* A instrução CLP CONNECT pode conter um dos seguintes:

    ** Token de acesso **

    Conecte-se ao servidor de banco de dados `<database_server_name>` e passe o token de acesso executando o comando a seguir no prompt de comandos ou script do CLP:

    `CONNECT TO <database_server_name> ACCESSTOKEN <access_token_string>`

    ** Chave de API **

    Conecte-se ao servidor de banco de dados `<database_server_name>` com uma chave de API, executando o comando a seguir no prompt de comandos ou script do CLP:

    `CONNECT TO <database_server_name> APIKEY <api-key-string>`

    ** IBMid/password **

    Conecte-se ao servidor de banco de dados `<database_server_name>` com um IBMid/senha, executando o comando a seguir no prompt de comandos ou script do CLP:

    `CONNECT TO <database_server_name> USER <IBMid> USING <password>`

    Para obter mais detalhes sobre como conectar-se a um servidor de banco de dados com o CLP, consulte: [Instrução CONNECT (tipo 2) ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.sql.ref.doc/doc/r0000908.html){:new_window}. 

* A instrução CLPPLUS CONNECT pode conter um dos seguintes:

    ** Token de acesso **

    Conecte-se ao alias do DSN (`@<data_source_name>`) e passe o token de acesso, executando o comando a seguir no prompt de comandos ou script do CLPPLUS:

    `connect @<data_source_name> using(accesstoken <access_token_string>)`

    ** Chave de API **

    Conecte-se ao alias do DSN (`@<data_source_name>`) com uma chave de API executando o comando a seguir no prompt de comandos ou script do CLPPLUS:

    `connect @<data_source_name> using(apikey <api-key-string>)`

    ** IBMid/password **

    Conecte-se ao alias do DSN (`@<data_source_name>`) com um IBMid/senha, executando o comando a seguir no prompt de comandos ou script do CLPPLUS:

    `connect <IBMid>/<password>@<data_source_name>`

    Para obter mais detalhes sobre como se conectar aos aliases do DSN com o CLPPLUS, consulte: [Aliases do DSN no CLPPlus ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.clpplus.doc/doc/c0057148.html){:new_window}.

### JDBC
{: #jdbc}

O Driver JDBC Tipo 4 é suportado para autenticação do IAM.

Os exemplos a seguir mostram fragmentos de conexão para os três métodos:

** Token de acesso **

```
DataSource; DB2SimpleDataSource;

dataSource.setDriverType( 4 );
dataSource.setDatabaseName( "BLUDB" );
dataSource.setServerName( "<host_name_or_IP_address>" );
dataSource.setPortNumber( 50001 );
dataSource.setSecurityMechanism( com.ibm.db2.jcc.DB2BaseDataSource.PLUGIN_SECURITY );
dataSource.setPluginName( "IBMIAMauth" );
dataSource.setAccessToken( "<access_token>" );
Connection conn = dataSource.getConnection( );
```

ou o

```
Connection conn = DriverManager.getConnection( "jdbc:db2://<host_name_or_IP_address>:50001/BLUDB:accessToken=<access_token>;securityMechanism=15;pluginName=IBMIAMauth;sslConnection=true" );
```

** Chave de API **

```
DataSource; DB2SimpleDataSource;

dataSource.setDriverType( 4 );
dataSource.setDatabaseName( "BLUDB" );
dataSource.setServerName( "<host_name_or_IP_address>" );
dataSource.setPortNumber( 50001 );
dataSource.setSecurityMechanism( com.ibm.db2.jcc.DB2BaseDataSource.PLUGIN_SECURITY );
dataSource.setPluginName( "IBMIAMauth" );
dataSource.setApiKey( "<api_key>" );
Connection conn = dataSource.getConnection( );
```

ou o

```
Connection conn = DriverManager.getConnection( "jdbc:db2://<host_name_or_IP_address>:50001/BLUDB:apiKey=<api_key>;securityMechanism=15;pluginName=IBMIAMauth;sslConnection=true" );
```

** IBMid/password **

```
DataSource; DB2SimpleDataSource;

dataSource.setDriverType( 4 );
dataSource.setDatabaseName( "BLUDB" );
dataSource.setServerName( "<host_name_or_IP_address>" );
dataSource.setPortNumber( 50001 );
dataSource.setSecurityMechanism( com.ibm.db2.jcc.DB2BaseDataSource.PLUGIN_SECURITY );
dataSource.setPluginName( "IBMIAMauth" );
Connection conn = dataSource.getConnection( "<IBMid>", "<password>" );
```

ou o

```
Connection conn = DriverManager.getConnection( "jdbc:db2://<host_name_or_IP_address>:50001/BLUDB:user=<IBMid>;password=<password>;securityMechanism=15;pluginName=IBMIAMauth;sslConnection=true" );
```

## Experiência do Usuário do
{: #console-ux}

A página de login do console de serviço tem a opção de efetuar login com seu IBMid e senha. Depois que o botão **Conectar-se via IBMid** é clicado, o usuário é direcionado para a página de login do IAM, na qual a senha é inserida. Quando a autenticação é concluída, o usuário é redirecionado de volta para o console. Para que esse login possa ser bem-sucedido, o usuário IBMid deve ser incluído em cada instância de serviço de banco de dados pelo administrador de banco de dados por meio do console ou da API de REST. Assim como para um usuário não IBMid, um ID do usuário para a instância de serviço de banco de dados deverá ser inserido ao mesmo tempo em que o usuário IBMid for incluído. O ID do usuário precisa ser exclusivo na instância de serviço de banco de dados. Esse ID do usuário também é o ID de autorização (AUTH) dentro do banco de dados.

## Experiência da API de REST
{: #api}

A API de REST do {{site.data.keyword.dashdbshort_notm}} foi aprimorada para também aceitar um token de acesso do IAM para as funções que anteriormente aceitavam um token de acesso gerado pelo serviço de banco de dados.

* Para incluir um novo usuário IBMid, execute a chamada API de exemplo a seguir:

  `curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid>","ibmid":"<userid>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"`

  O valor `<userid>` para `"id"` e `"ibmid"` não precisa ser o mesmo. Os dois IDs diferentes não são vinculados de nenhuma maneira.
  {: note}

* Para migrar um usuário de banco de dados não IBMid existente (por exemplo, `abcuser`) e torná-lo um usuário IBMid, exclua primeiramente o ID de usuário não IBMid executando a chamada API de exemplo a seguir:

  `curl --tlsv1.2 -X DELETE "https://<IPaddress>/dbapi/v3/users/abcuser" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json"`

  Em seguida, inclua novamente o usuário com um IBMid que seja o mesmo que o ID de usuário anterior (`abcuser`) executando a chamada API de exemplo a seguir:

  `curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"abcuser","ibmid":"abcuser@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"`

  Como o ID de usuário (`abcuser`) permanece o mesmo para o novo IBMid desse usuário, as permissões de banco de dados concedidas para o usuário permanecem inalteradas. Se uma lista de usuários de banco de dados não IBMid existentes precisar ser migrada para torná-los usuários IBMid, será necessário executar o par anterior de chamadas API de cada usuário.

* Para incluir vários novos usuários IBMid ao mesmo tempo, crie um arquivo de lote que liste as chamadas API de exemplo a seguir, uma para cada usuário:

  ```
  curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid1>","ibmid":"<userid1>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"
  curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid2>","ibmid":"<userid2>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"
  .
  .
  .
  ```

Para obter mais detalhes sobre a API de seu serviço, consulte: [API de REST do {{site.data.keyword.dashdbshort_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://ibm.biz/db2whc_api){:new_window}.

## Federação do IBMid
{: #ibmid_fed}

Para usar seu próprio provedor de identidade, como o LDAP, deve-se primeiro federar seu servidor LDAP com o IBMid. Para obter instruções sobre como federar seu servidor LDAP com o IBMid, consulte: [IBMid Enterprise Federation Adoption Guide ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://ibm.ent.box.com/notes/78040808400?v=IBMid-Federation-Guide){:new_window}. Depois que a federação de IBMid for concluída e os usuários permitidos forem incluídos na instância de serviço de banco de dados pelo administrador de banco de dados, eles poderão efetuar login no console com seu ID de usuário e senha da empresa. Como alternativa, esses usuários poderão usar um token de acesso ou uma chave API que representem seu ID de usuário para se conectar à instância de serviço de banco de dados por meio de uma das interfaces do cliente de banco de dados suportadas.

## Restrições
{: #restrictions}

A seguir estão as restrições no que se refere à autenticação do IAM:

* A autenticação do IAM para um cliente Db2 que está se conectando a um servidor Db2 é suportada apenas em uma conexão SSL.
* A federação do IBMid é suportada para permitir que o portal ou o servidor de gerenciamento de usuários customizado sejam usados para autenticação. Esse suporte não inclui nenhuma federação de grupo.
* A autenticação do IAM para federação de banco de dados não é suportada.
* A execução de comandos IDA e de extensão definida pelo usuário (UDX) por meio do CLPPlus não é suportada.
* O Driver JDBC tipo 2 não é suportado.




