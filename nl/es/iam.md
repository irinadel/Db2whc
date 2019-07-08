---

copyright:
  years: 2014, 2019
lastupdated: "2019-01-21"

keywords:

subcollection: Db2whc

---

<!-- Attribute definitions --> 
{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}

# Gestión de identidad y acceso (IAM) en {{site.data.keyword.Bluemix_notm}}
{: #iam}

La gestión de identidad y acceso (IAM) le permite autenticar de forma segura usuarios para los servicios de plataforma y controlar el acceso a los recursos de forma coherente en la plataforma de {{site.data.keyword.Bluemix_notm}}. Por ejemplo, con un solo inicio de sesión en {{site.data.keyword.Bluemix_notm}} con IBMid, tiene acceso a cualquiera de las consolas de servicio y a sus aplicaciones sin tener que iniciar sesión en cada una de ellas por separado.
{: shortdesc}

## ¿Está habilitado IAM en su instancia?
{: #enabled}

Durante un período de tiempo, las instancias de base de datos gestionadas de {{site.data.keyword.dashdblong}} en {{site.data.keyword.Bluemix_notm}} estarán habilitadas para utilizar IAM en el control de acceso. Para comprobar que IAM está habilitado en su instancia, ejecute la consulta siguiente:

`SELECT CASE WHEN VALUE = 'IBMIAMauth' THEN 1 ELSE 0 END AS IAM_ENABLED FROM SYSIBMADM.DBMCFG WHERE NAME = 'srvcon_gssplugin_list'`

Si el valor devuelto de **IAM_ENABLED** es 1, IAM estará habilitado en la instancia.

## Características de {{site.data.keyword.Bluemix_notm}} IAM
{: #features}

Las siguientes características de IAM se implementan en el servicio gestionado de {{site.data.keyword.dashdbshort_notm}} con dos tipos de identidades soportadas:

**IBMid**

El administrador de la base de datos debe añadir los usuarios con un IBMid a cada instancia de servicio de base de datos mediante la consola o la API REST antes de que los usuarios puedan conectarse a una instancia de servicio de base de datos determinada. Al igual que para un usuario IBMid no de IBM, es necesario especificar un ID de usuario para la instancia de servicio de base de datos al mismo tiempo que se añade el usuario IBMid. El ID de usuario debe ser exclusivo en la instancia de servicio de base de datos. Este ID de usuario también es el ID de autorización (AUTH) en la base de datos. El administrador de la base de datos puede otorgar y revocar permisos basados en el ID de AUTH.

**ID de servicio**

Un ID de servicio identifica un servicio o una aplicación de forma similar a cómo un ID de usuario identifica un usuario. Los ID de servicio son ID que las aplicaciones pueden utilizar para autenticarse con un servicio de {{site.data.keyword.Bluemix_notm}}. Un ID de servicio representa una entidad individual del IBMid propietario. Por lo tanto, es posible otorgar distintas autorizaciones y permisos específicos para el ID de servicio en la base de datos. Los ID de servicio no tienen contraseñas. Es necesario crear una clave de API para cada ID de servicio para que el este se conecte a la instancia de servicio de la base de datos. Para obtener más información sobre los ID de servicio, consulte: [Presentación de las claves de API y los ID de servicio de {{site.data.keyword.Bluemix_notm}} IAM](https://www.ibm.com/blogs/bluemix/2017/10/introducing-ibm-cloud-iam-service-ids-api-keys/){:external}.

## Conexiones de cliente e inicios de sesión de usuario
{: #connect_login}

**Requisito previo**: Cliente Db2 V11.1 FP3 y posterior.

Es posible utilizar los métodos siguientes para la autenticación de IAM:

**Señal de acceso**

Se puede obtener una señal de acceso del servicio IAM directamente mediante la aplicación a través de la API REST utilizando una clave de API. Para obtener más información, consulte: [Obtención de una señal {{site.data.keyword.Bluemix_notm}} IAM mediante una clave de API](/docs/iam?topic=iam-iamtoken_from_apikey#iamtoken_from_apikey){:external}. El período de validez predeterminado de la señal de acceso antes de que caduque es de 60 minutos. Si la señal de acceso ha caducado, el servidor Db2 no permitirá que se establezca la conexión. No se comprobará la caducidad de la señal hasta que se haya establecido la conexión. Igual que antes de la integración IAM, la conexión permanecerá conectada hasta que se desconecte la aplicación o se termine la conexión debido a otras razones.

```
curl -k -X POST \
  --header "Content-Type: application/x-www-form-urlencoded" \
  --header "Accept: application/json" \
  --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
  --data-urlencode "apikey=<apikey>" \
  "https://iam.bluemix.net/identity/token"
```

Una señal de acceso identifica un usuario de IBMid o un ID de servicio en la base de datos. El servidor de base de datos verifica la validez de la señal de acceso antes de aceptarla. Este es el mejor método si la aplicación debe conectarse a más de una instancia de servicio de base de datos o a otras instancias de servicio de {{site.data.keyword.Bluemix_notm}} porque minimiza la comunicación con el servicio IAM para validar la señal de acceso.

**Clave de API**

Es posible crear varias claves de API para cada usuario IBMid o ID de servicio. Normalmente, cada clase de API se crea para una única aplicación. Esta permite a la aplicación conectarse a la instancia de servicio de la base de datos siempre que el IBMid o ID de servicio del propietario se añada como usuario a la misma instancia de servicio de la base de datos. La clave de API tiene las mismas autorizaciones y permisos dentro de la base de datos que el IBMid o el ID de servicio del propietario. Si una aplicación ya no debería poder conectarse a la base de datos, se puede eliminar la clave de API correspondiente. Este método de autenticación requiere menos cambios en la aplicación que utilizando una señal de acceso ya que no es necesaria ninguna interacción directa con el servicio de IAM. Para obtener más información sobre la creación y la gestión de claves de API, consulte [Gestión de claves de API de usuario](/docs/iam?topic=iam-userapikey#userapikey){:external}.

**IBMid/contraseña**

Se puede utilizar el IBMid/contraseña para iniciar sesión en la consola y en la aplicación de la misma forma que se permite un ID de usuario/contraseña. La excepción se produce cuando el IBMid se federa porque no se puede realizar una redirección a la página de inicio de sesión de la organización. Sin embargo, el método recomendado para que una aplicación establezca una conexión con la instancia de servicio de base de datos es utilizar una señal de acceso.

## Interfaces soportadas
{: #sup-if}

Se ofrece soporte a las interfaces de cliente de base de datos siguientes:

* [ODBC](#odbc-clpplus)
* [CLP](#odbc-clpplus)
* [CLPPLUS](#odbc-clpplus)
* [JDBC](#jdbc)

### ODBC, CLP, y CLPPLUS
{: #odbc-clpplus}

Para que una aplicación ODBC o un cliente de línea de mandatos (CLP, CLPPLUS) se conecte a un servidor de Db2 utilizando la autenticación IAM, primero es necesario configurar un nombre de origen de datos (DSN) en un archivo de configuración `db2dsdriver.cfg` ejecutando el mandato siguiente:

`db2cli writecfg add -dsn <dsn_alias> -database <database_name> -host <host_name_or_IP_address> -port 50001 -parameter "Authentication=GSSPLUGIN;SecurityTransportMode=SSL"`

El archivo de configuración `db2dsdriver.cfg` es un archivo XML que normalmente se encuentra en el directorio `sqllib/cfg` y que contiene una lista de alias de DSN y sus propiedades.

El ejemplo siguiente de un archivo de configuración `db2dsdriver.cfg` muestra las configuraciones que se han utilizado para establecer una conexión a una instancia de servicio de la base de datos. El archivo de configuración proporciona el alias de DSN, el nombre de la base de datos, el nombre de host (o la dirección IP) y el tipo de **autenticación** y los valores del parámetro **SecurityTransportMode**:

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

* La serie de conexión ODBC puede contener una de las siguientes opciones:

    **Señal de acceso**

    `DSN=<dsn>;ACCESSTOKEN=<access_token>`

    **Clave de API**

    `DSN=<dsn>;APIKEY=<api_key>`

    **IBMid/contraseña**
    
    `DSN=<dsn>;UID=<ibmid>;PWD=<password>`

    En ODBC, se puede especificar **AUTHENTICATION=GSSPLUGIN** en el archivo de configuración `db2dsdriver.cfg` o en la serie de conexión de la aplicación.

* El mandato CONNECT de CLP puede contener una de las siguientes opciones:

    **Señal de acceso**

    Conectar con el `<database_server_name>` del servidor de bases de datos y pasar la señal de acceso ejecutando el mandato siguiente en el script o indicador de mandatos de CLP:

    `CONNECT TO <database_server_name> ACCESSTOKEN <access_token_string>`

    **Clave de API**

    Conectar con el `<database_server_name>` del servidor de bases de datos con una clave de API mediante la ejecución del siguiente mandato en el script o indicador de mandatos de CLP:

    `CONNECT TO <database_server_name> APIKEY <api-key-string>`

    **IBMid/contraseña**

    Conectar con el `<database_server_name>` del servidor de bases de datos con IBMid y una contraseña mediante la ejecución del siguiente mandato en el script o indicador de mandatos de CLP:

    `CONNECT TO <database_server_name> USER <IBMid> USING <password>`

    Para obtener información más detallada acerca de cómo conectarse a un servidor de base de datos con CLP, consulte: [Sentencia CONNECT (tipo 2)](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.sql.ref.doc/doc/r0000908.html){:external}. 

* El mandato CONNECT de CLPPLUS puede contener una de las siguientes opciones:

    **Señal de acceso**

    Conectar con el alias de DSN (`@<data_source_name>`) y pasar la señal de acceso mediante la ejecución del siguiente mandato en un script o indicador de mandatos CLPPLUS:

    `connect @<data_source_name> using(accesstoken <access_token_string>)`

    **Clave de API**

    Conectar con el alias de DSN (`@<data_source_name>`) con una clave de API mediante la ejecución del siguiente mandato en un script o indicador de mandatos CLPPLUS:

    `connect @<data_source_name> using(apikey <api-key-string>)`

    **IBMid/contraseña**

    Conectar con el alias de DSN (`@<data_source_name>`) con un IBMid y una contraseña mediante la ejecución del siguiente mandato en un script o indicador de mandatos CLPPLUS:

    `connect <IBMid>/<password>@<data_source_name>`

    Para obtener información más detallada acerca de cómo conectarse a alias de DSN con CLPPLUS, consulte:
[Alias de DSN en CLPPlus](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.clpplus.doc/doc/c0057148.html){:external}.

### JDBC
{: #jdbc}

El controlador JDBC de tipo 4 se admite en la autenticación de IAM.

Los ejemplos siguientes muestran fragmentos de código de la conexión para los tres métodos:

**Señal de acceso**

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

o

```
Connection conn = DriverManager.getConnection( "jdbc:db2://<nombre_host_o_dirección_IP>:50001/BLUDB:accessToken=<señal_acceso>;securityMechanism=15;pluginName=IBMIAMauth;sslConnection=true" );
```

**Clave de API**

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

o

```
Connection conn = DriverManager.getConnection( "jdbc:db2://<host_name_or_IP_address>:50001/BLUDB:apiKey=<api_key>;securityMechanism=15;pluginName=IBMIAMauth;sslConnection=true" );
```

**IBMid/contraseña**

```
DB2SimpleDataSource dataSource;

dataSource.setDriverType( 4 );
dataSource.setDatabaseName( "BLUDB" );
dataSource.setServerName( "<nombre_host_o_dirección_IP>" );
dataSource.setPortNumber( 50001 );
dataSource.setSecurityMechanism( com.ibm.db2.jcc.DB2BaseDataSource.PLUGIN_SECURITY );
dataSource.setPluginName( "IBMIAMauth" );
Connection conn = dataSource.getConnection( "<IBMid>", "<contraseña>" );
```

o

```
Connection conn = DriverManager.getConnection( "jdbc:db2://<nombre_host_o_dirección_IP>:50001/BLUDB:user=<IBMid>;password=<contraseña>;securityMechanism=15;pluginName=IBMIAMauth;sslConnection=true" );
```

## Experiencia del usuario de consola
{: #console-ux}

La página de inicio de sesión de la consola de servicio ofrece la opción de iniciar sesión con el IBMid y la contraseña. Después de pulsar el botón **Iniciar sesión mediante IBMid**, el usuario se dirige a la página de inicio de sesión de IAM en la que especifica la contraseña. Cuando se haya completado la autenticación, el usuario se redirigirá de nuevo a la consola. Para que el inicio de sesión se realice correctamente, el administrador de la base de datos debe añadir al usuario IBMid a cada instancia de servicio de base de datos mediante la consola o la API REST. Al igual que para un usuario IBMid no de IBM, es necesario especificar un ID de usuario para la instancia de servicio de base de datos al mismo tiempo que se añade el usuario IBMid. El ID de usuario debe ser exclusivo en la instancia de servicio de base de datos. Este ID de usuario también es el ID de autorización (AUTH) en la base de datos.

## Experiencia de API REST
{: #api}

La API REST de {{site.data.keyword.dashdbshort_notm}} se ha mejorado para que también acepte una señal de acceso de IAM en las funciones que anteriormente han aceptado una señal de acceso generada por el servicio de base de datos.

* Para añadir un nuevo usuario IBMid, ejecute la siguiente llamada de API de ejemplo:

  `curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid>","ibmid":"<userid>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"`

  El valor `<userid>` para `"id"` e `"ibmid"` no necesariamente tiene que ser el mismo. Los dos ID no están enlazados de ninguna forma.
  {: note}

* Para migrar un usuario de la base de datos IBMid no de IBM (por ejemplo, `abcuser`) y transformarlo en un usuario IBMid, primero suprima el ID del usuario IBMid no de IBM ejecutando la llamada de API del ejemplo siguiente:

  `curl --tlsv1.2 -X DELETE "https://<IPaddress>/dbapi/v3/users/abcuser" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json"`

  A continuación, vuelva a añadir el usuario con un IBMid que sea el mismo que el ID de usuario anterior (`abcuser`) ejecutando la llamada de API del ejemplo siguiente:

  `curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"abcuser","ibmid":"abcuser@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"`

  Puesto que el ID de usuario (`abcuser`) sigue siendo el mismo para el nuevo IBMid del usuario, los permisos de base de datos otorgados al usuario permanecerán sin modificaciones. En caso de que sea necesario migrar una lista de usuarios de base de datos de IBMid no de IBM para transformarlos en usuarios IBMid, deberá ejecutar el par de llamadas API anteriores para cada usuario.

* Para añadir muchos usuarios IBMid nuevos a la vez, cree un archivo de procesamiento por lotes que muestre las llamadas API del ejemplo siguiente, una para cada usuario:

  ```
  curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid1>","ibmid":"<userid1>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"
  curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid2>","ibmid":"<userid2>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"
  .
  .
  .
  ```

Para obtener más detalles sobre la API del servicio, consulte: [API REST de {{site.data.keyword.dashdbshort_notm}}](http://ibm.biz/db2whc_api){:external}.

## Federación de IBMid
{: #ibmid_fed}

Para utilizar su propio proveedor de identidad como, por ejemplo, LDAP, primero debe federar el servidor LDAP con IBMid. Para obtener instrucciones sobre cómo federar el servidor LDAP con IBMid, consulte la [Guía de adopción de federación empresarial de
IBMid](https://ibm.ent.box.com/notes/78040808400?v=IBMid-Federation-Guide){:external}. Una vez que se haya completado la federación de IBMid y que el administrador de base de datos haya añadido los usuarios con permiso a la instancia de servicio de la base de datos, los usuarios podrán iniciar sesión en la consola con el ID de usuario y la contraseña de su empresa. De forma alternativa, los usuarios pueden utilizar una señal de acceso o una clave de API que represente su ID de usuario para conectarse a la instancia de servicio de la base de datos mediante una de las interfaces de cliente de base de datos soportadas.

## Restricciones
{: #restrictions}

A continuación, se muestran las restricciones con respecto a la autenticación de IAM:

* La autenticación de IAM para un cliente Db2 que se está conectando a un servidor Db2 solo se admite a través de una conexión SSL.
* La federación de IBMid está soportada para permitir que el servidor o el portal de gestión de usuarios personalizado se utilicen en la autenticación. Este tipo de soporte no incluye ninguna federación de grupo.
* La autenticación IAM para la federación de base de datos no está soportada.
* La ejecución de mandatos de extensiones definidas por el usuario (UDX) e IDA mediante CLPPlus no está soportada.
* El controlador JDBC de tipo 2 no está soportado.




