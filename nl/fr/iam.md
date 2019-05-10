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

# IAM (Identity and access management) sur {{site.data.keyword.Bluemix_notm}}
{: #iam}

Le système de gestion des identités et des accès IAM vous permet de d'authentifier les utilisateurs en toute sécurité pour les services de plateforme et de contrôler l'accès aux ressources de manière cohérente dans l'ensemble de la plateforme {{site.data.keyword.Bluemix_notm}}. Par exemple, avec une seule connexion à {{site.data.keyword.Bluemix_notm}} avec votre IBMid, vous avez accès à toutes vos consoles de service et leurs applications sans avoir à vous connecter à chacune d'entre elles séparément.
{: shortdesc}

## IAM est-elle activée sur votre instance ?
{: #enabled}

Au fil du temps, les instances de bases de données gérées {{site.data.keyword.dashdblong}} sur {{site.data.keyword.Bluemix_notm}} seront autorisées à utiliser IAM pour le contrôle d'accès. Pour vérifier si IAM est activé sur votre instance, exécutez la requête suivante :

`SELECT CASE WHEN VALUE = 'IBMIAMauth' THEN 1 ELSE 0 END AS IAM_ENABLED FROM SYSIBMADM.DBMCFG WHERE NAME = 'srvcon_gssplugin_list'`

Si la valeur renvoyée de **IAM_ENABLED** est 1, IAM est activé sur votre instance.

## Fonctions de {{site.data.keyword.Bluemix_notm}} IAM
{: #features}

Les fonctions IAM suivantes sont implémentées pour le service géré {{site.data.keyword.dashdbshort_notm}} avec deux types d'identités prises en charge :

**IBMid**

Les utilisateurs possédant un IBMid doivent être ajoutés à chaque instance de service de base de données par l'administrateur de base de données via la console ou l'API REST avant que les utilisateurs puissent se connecter à l'instance de service de base de données particulière. Tout comme pour un utilisateur qui n'est pas un utilisateur IBMid, un ID d'utilisateur doit être saisi pour l'instance de service de base de données en même temps que l'utilisateur IBMid est ajouté. Cet ID d'utilisateur doit être unique dans l'instance de service de base de données. Cet ID d'utilisateur est également l'ID d'autorisation (AUTH) dans la base de données. L'administrateur de base de données peut accorder et révoquer des droits en fonction de l'ID AUTH.

**ID de service**

Un ID de service identifie un service ou une application de la même façon qu'un ID d'utilisateur identifie un utilisateur. Les ID de service sont des identifiants qui peuvent être utilisés par les applications pour s'authentifier auprès d'un service {{site.data.keyword.Bluemix_notm}}. Un ID de service représente une entité séparée du IBMid propriétaire. Par conséquent, différentes autorités et permissions peuvent être accordées en fonction de l'ID de service dans la base de données. Les ID de service n'ont pas de mot de passe. Une clé d'API doit être créée pour chaque ID de service pour que l'ID de service se connecte à l'instance de service de base de données. Pour en savoir plus sur les ID de service, voir : [Introducing {{site.data.keyword.Bluemix_notm}} IAM Service IDs and API Keys ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/blogs/bluemix/2017/10/introducing-ibm-cloud-iam-service-ids-api-keys/){:new_window}.

## Connexions client et logins utilisateur
{: #connect_login}

**Prérequis** : Db2 Client V11.1 FP3 et versions ultérieures.

Les méthodes suivantes peuvent être utilisées pour l'authentification IAM :

**Jeton d'accès**

Un jeton d'accès peut être obtenu directement du service IAM par l'application via l'API REST à l'aide d'une clé d'API. Pour toute information supplémentaire, voir : [Getting an {{site.data.keyword.Bluemix_notm}} IAM token by using an API key ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](/docs/iam?topic=iam-iamtoken_from_apikey#iamtoken_from_apikey){:new_window}. Le jeton d'accès a une période de validité par défaut de 60 minutes avant d'expirer. Si le jeton a expiré, le serveur Db2 n'autorisera pas l'établissement de la connexion. La date d'expiration du jeton n'est pas vérifiée une fois que la connexion est établie. Comme c'était le cas avant l'intégration d'IAM, la connexion est maintenue jusqu'à ce que l'application se déconnecte ou que la connexion soit interrompue pour d'autres raisons.

```
curl -k -X POST \
  --header "Content-Type: application/x-www-form-urlencoded" \
  --header "Accept: application/json" \
  --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
  --data-urlencode "apikey=<apikey>" \
  "https://iam.bluemix.net/identity/token"
```

Un jeton d'accès identifie un utilisateur IBMid ou un ID de service dans la base de données. Le serveur de base de données vérifie la validité du jeton d'accès avant de l'accepter. C'est la meilleure méthode si l'application doit se connecter à plus d'une instance de service de base de données ou à d'autres instances de service {{site.data.keyword.Bluemix_notm}} car elle minimise la communication au service IAM pour valider le jeton d'accès.

**Clé d'API**

Plusieurs clés d'API peuvent être créées pour chaque utilisateur IBMid ou ID de service. Chaque clé d'API est généralement créée pour une seule application. Elle permet à l'application de se connecter à l'instance de service de base de données tant que l'IBMid propriétaire ou l'ID de service est ajouté en tant qu'utilisateur à la même instance de service de base de données. La clé d'API possède les mêmes autorisations et permissions dans la base de données que l'IBMid ou l'ID de service propriétaire. Si une application n'est plus autorisée à se connecter à la base de données, la clé d'API correspondante peut être supprimée. Cette méthode d'authentification nécessite moins de changements dans l'application que l'utilisation d'un jeton d'accès car elle ne nécessite aucune interaction directe avec le service IAM. Pour en savoir plus sur la création et la gestion des clés d'API, voir : [Gestion des clés d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](/docs/iam?topic=iam-userapikey#userapikey){:new_window}.

**IBMid/mot de passe**

L'IBMid et le mot de passe peuvent être utilisés pour la connexion à la console ainsi qu'au sein de l'application de la même manière qu'un ID d'utilisateur/mot de passe est autorisé. Une exception se produit lorsque l'IBMid est fédéré parce qu'une redirection vers la page de connexion de votre organisation ne peut être effectuée. Cependant, la méthode recommandée pour qu'une application établisse une connexion à l'instance de service de base de données est d'utiliser un jeton d'accès.

## Interfaces prises en charge
{: #sup-if}

Les interfaces de client de base de données suivantes sont prises en charge :

* [ODBC
](#odbc-clpplus)
* [CLP](#odbc-clpplus)
* [CLPPLUS](#odbc-clpplus)
* [JDBC](#jdbc)

### ODBC, CLP et CLPPLUS
{: #odbc-clpplus}

Pour qu'une application ODBC ou un client de ligne de commande (CLP, CLPPLUS) puisse se connecter à un serveur Db2 en utilisant l'authentification IAM, un nom de source de données (DSN) doit d'abord être défini dans un fichier de configuration `db2dsdriver.cfg` à l'aide de la commande suivante :

`db2cli writecfg add -dsn <dsn_alias> -database <database_name> -host <host_name_or_IP_address> -port 50001 -parameter "Authentication=GSSPLUGIN;SecurityTransportMode=SSL"`

Le fichier de configuration `db2dsdriver.cfg` est un fichier XML généralement situé dans le répertoire `sqllib/cfg` qui contient une liste des alias DSN et leurs propriétés.

L'exemple suivant d'un fichier de configuration `db2dsdriver.cfg` montre les configurations qui sont utilisées pour établir une connexion vers une instance de service de base de données. Le fichier de configuration fournit l'alias DSN, le nom de base de données, le nom d'hôte (ou l'adresse IP), ainsi que le type d'**authentification** et les valeurs de paramètre **SecurityTransportMode** :

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

* La chaîne de connexion ODBC peut contenir l'un des éléments suivants :

    **Jeton d'accès**

    `DSN=<dsn>;ACCESSTOKEN=<access_token>`

    **Clé d'API**

    `DSN=<dsn>;APIKEY=<api_key>`

    **IBMid/mot de passe**
    
    `DSN=<dsn>;UID=<ibmid>;PWD=<password>`

    Pour ODBC, **AUTHENTICATION=GSSPLUGIN** peut être spécifié dans le fichier de configuration `db2dsdriver.cfg` ou bien dans la chaîne de connexion de l'application.

* L'instruction CLP CONNECT peut inclure l'un des éléments suivants :

    **Jeton d'accès**

    Connectez-vous au serveur de base de données `<database_server_name>` et transmettez le jeton d'accès en exécutant la commande suivante sur le script ou l'invite de commande CLP :

    `CONNECT TO <database_server_name> ACCESSTOKEN <access_token_string>`

    **Clé d'API**

    Connectez-vous au serveur de base de données `<database_server_name>` avec une clé d'API en exécutant la commande suivante sur le script ou l'invite de commande CLP :

    `CONNECT TO <database_server_name> APIKEY <api-key-string>`

    **IBMid/mot de passe**

    Connectez-vous au serveur de base de données `<database_server_name>` avec un IBMid/mot de passe en exécutant la commande suivante sur le script ou l'invite de commande CLP :

    `CONNECT TO <database_server_name> USER <IBMid> USING <password>`

    Pour en savoir plus sur la connexion à un serveur de base de données avec CLP, voir [CONNECT (type 2) statement ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.sql.ref.doc/doc/r0000908.html){:new_window}. 

* L'instruction CLPPLUS CONNECT peut inclure l'un des éléments suivants :

    **Jeton d'accès**

    Connectez-vous à l'alias DSN (`@<data_source_name>`) et transmettez le jeton d'accès en exécutant la commande suivante sur l'invite de commande CLPPLUS ou le script :

    `connect @<data_source_name> using(accesstoken <access_token_string>)`

    **Clé d'API**

    Connectez-vous à l'alias DSN (`@<data_source_name>`) avec une clé d'API en exécutant la commande suivante sur l'invite de commande CLPPLUS ou le script :

    `connect @<data_source_name> using(apikey <api-key-string>)`

    **IBMid/mot de passe**

    Connectez-vous à l'alias DSN (`@<data_source_name>`) avec un IBMid/mot de passe en exécutant la commande suivante sur l'invite de commande CLPPLUS ou le script :

    `connect <IBMid>/<password>@<data_source_name>`

    Pour en savoir plus sur la connexion aux alias DSN avec CLPPLUS, voir : [DSN aliases in CLPPlus ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.clpplus.doc/doc/c0057148.html){:new_window}.

### JDBC
{: #jdbc}

Le pilote JDBC de type 4 est pris en charge pour l'authentification IAM.

Les exemples suivants montre les fragments de connexion pour les trois méthodes :

**Jeton d'accès**

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

ou

```
Connection conn = DriverManager.getConnection( "jdbc:db2://<host_name_or_IP_address>:50001/BLUDB:accessToken=<access_token>;securityMechanism=15;pluginName=IBMIAMauth;sslConnection=true" );
```

**Clé d'API**

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

ou

```
Connection conn = DriverManager.getConnection( "jdbc:db2://<host_name_or_IP_address>:50001/BLUDB:apiKey=<api_key>;securityMechanism=15;pluginName=IBMIAMauth;sslConnection=true" );
```

**IBMid/mot de passe**

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

ou

```
Connection conn = DriverManager.getConnection( "jdbc:db2://<host_name_or_IP_address>:50001/BLUDB:user=<IBMid>;password=<password>;securityMechanism=15;pluginName=IBMIAMauth;sslConnection=true" );
```

## Expérience utilisateur de la console
{: #console-ux}

La page de connexion de la console de service a la possibilité de se connecter avec votre IBMid et votre mot de passe. Après avoir cliqué sur le bouton **Sign In via IBMid**, l'utilisateur est dirigé vers la page de connexion IAM, sur laquelle le mot de passe est entré. Une fois l'authentification terminée, l'utilisateur est redirigé vers la console. Avant qu'une telle connexion puisse être réussie, l'utilisateur IBMid doit être ajouté à chaque instance de service de base de données par l'administrateur de base de données via la console ou l'API REST. Tout comme pour un utilisateur qui n'est pas un utilisateur IBMid, un ID d'utilisateur doit être saisi pour l'instance de service de base de données en même temps que l'utilisateur IBMid est ajouté. L'ID d'utilisateur doit être unique dans l'instance du service de base de données. Cet ID d'utilisateur est également l'ID d'autorisation (AUTH) dans la base de données.

## Expérience de l'API REST
{: #api}

L'API REST {{site.data.keyword.dashdbshort_notm}} a été améliorée afin d'accepter également un jeton d'accès IAM pour les fonctions qui acceptaient auparavant un jeton d'accès généré par le service de base de données.

* Pour ajouter un nouvel utilisateur IBMid, exécutez l'exemple d'appel API suivant :

  `curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid>","ibmid":"<userid>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"`

  Les valeurs `<userid>` des éléments `"id"` et `"ibmid"` n'ont pas besoin d'être identiques. Les deux ID différents ne sont pas liés entre eux.
  {: note}

* Pour faire migrer un utilisateur de base de données non-IBMid existant (par exemple `abcuser`) et le convertir en utilisateur IBMid, supprimez d'abord l'ID de l'utilisateur non-IBMid en exécutant l'exemple d'appel API suivant :

  `curl --tlsv1.2 -X DELETE "https://<IPaddress>/dbapi/v3/users/abcuser" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json"`

  Ensuite, ajoutez à nouveau l'utilisateur avec un IBMid identique à l'ID d'utilisateur précédent (`abcuser`) en exécutant l'exemple suivant d'appel API :

  `curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"abcuser","ibmid":"abcuser@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"`

  Comme l'ID d'utilisateur (`abcuser`) reste le même pour le nouvel IBMid de cet utilisateur, les permissions accordées à l'utilisateur pour la base de données restent les mêmes. Si une liste d'utilisateurs de base de données non IBMid existants doit être migrée pour en faire des utilisateurs IBMid, vous devez exécuter les deux appels API précédents pour chaque utilisateur.

* Pour ajouter un grand nombre de nouveaux utilisateurs IBMid à la fois, créez un fichier de traitement par lots répertoriant les exemples d'appels API suivants, à raison d'un par utilisateur :

  ```
  curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid1>","ibmid":"<userid1>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"
  curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid2>","ibmid":"<userid2>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"
  .
  .
  .
  ```

Pour en savoir plus sur votre API de service, voir : [{{site.data.keyword.dashdbshort_notm}} REST API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://ibm.biz/db2whc_api){:new_window}.

## Fédération IBMid
{: #ibmid_fed}

Pour utiliser votre propre fournisseur d'identité tel que LDAP, vous devez d'abord fédérer votre serveur LDAP avec IBMid. Pour recevoir des instructions sur la fédération de votre serveur LDAP avec IBMid, voir : [IBMid Enterprise Federation Adoption Guide ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://ibm.ent.box.com/notes/78040808400?v=IBMid-Federation-Guide){:new_window}. Une fois que la fédération IBMid est terminée et que les utilisateurs autorisés ont été ajoutés à l'instance du service de base de données par l'administrateur de la base de données, ces utilisateurs peuvent se connecter à la console avec le nom utilisateur de leur entreprise et le mot de passe. Ces utilisateurs peuvent également utiliser un jeton d'accès ou une clé d'API qui représente leur ID d'utilisateur pour se connecter à l'instance du service de base de données via l'une des interfaces de client de base de données prises en charge.

## Restrictions
{: #restrictions}

Les restrictions suivantes s'appliquent à l'authentification IAM :

* L'authentification IAM pour un client Db2 qui se connecte à un serveur Db2 n'est prise en charge que par le biais d'une connexion SSL.
* La fédération IBMid est prise en charge pour permettre l'utilisation d'un portail ou d'un serveur de gestion des utilisateurs personnalisé pour l'authentification. Ce type de prise en charge n'inclut aucune fédération de groupe.
* L'authentification IAM n'est pas prise en charge pour la fédération des bases de données.
* L'exécution de commandes IDA et d'extensions définies par l'utilisateur (UDX) via CLPPlus n'est pas prise en charge.
* Le pilote JDBC de type 2 n'est pas pris en charge.




