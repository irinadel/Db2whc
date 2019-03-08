---

copyright:
  years: 2014, 2019
lastupdated: "2018-11-08"

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

# Integración de datos
{: #data_int}

También puede conectar aplicaciones externas a {{site.data.keyword.dashdbshort_notm}} y utilizarlas para gestionar o analizar todavía más sus datos. 
{: shortdesc}

## DataStage
{: #datastage}

En estas instrucciones se explica cómo definir una conexión sin SSL entre IBM® InfoSphere® DataStage® <!--version 9.1 and later -->y una base de datos de {{site.data.keyword.dashdbshort_notm}} catalogando la base de datos y definiendo un objeto de conexión, o cómo crear una conexión con SSL mediante un certificado digital emitido por un tercero.
{: shortdesc}

### Requisitos previos
{: #prereq1}

Si todavía no ha instalado ningún cliente de servidor de datos, descargue e instale el cliente de servidor de datos de IBM <!--Version 10.5 -->que sea adecuado para el sistema operativo de la máquina del cliente: [Cliente de servidor de datos de IBM ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/marketing/iwm/iwm/web/preLogin.do?source=swg-idsc97){:new_window}.

Para realizar conexiones con el protocolo SSL, descargue e instale el GSKit V8 de 32-bits. Pulse el separador OS que sea adecuado para el sistema operativo de la máquina del cliente: [GSKit V8 - Instrucciones de instalación, desinstalación y actualización ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/support/docview.wss?uid=swg21631462){:new_window}. Para los sistemas operativos siguientes, asegúrese de que añade la vía de acceso del directorio de instalación de GSKit a la variable de entorno de la vía de acceso específica del sistema operativo:

- AIX®: **LIBPATH**
   - `/usr/opt/ibm/gsk8/lib`
- Linux: **LD_LIBRARY_PATH**
    - `/usr/local/ibm/gsk8/lib`
- UNIX: **LD_LIBRARY_PATH**
    - `/opt/ibm/gsk8/lib`
- Windows: **PATH**
    - `<installation_directory>\gsk8\bin`
    - `<installation_directory>\gsk8\lib`

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](/docs/services/Db2whc/connecting/connecting.html#prereqs) necesarios.

### Procedimiento
{: #proc1}

- Para crear una conexión con SSL, complete los pasos siguientes:

  1. Abra una línea de mandatos o un terminal y cree un nuevo directorio en el sistema DataStage para almacenar el certificado SSL y los archivos de claves.

     `# /home/db2inst2> mkdir SSL`

     `# /home/db2inst2> cd SSL`

  2. En la consola web de {{site.data.keyword.dashdbshort_notm}}, descargue el certificado SSL desde la página **Conexión de aplicaciones a la base de datos**.

     a. Desde el menú principal, pulse **Conectar**.
     
     b. Pulse **Conexión con SSL** y, después, pulse el enlace **Certificado SSL (1 KB)**.
     
     c. Guarde el certificado `DigiCertGlobalRootCA.crt` en el directorio SSL que ha creado en el paso 1.
        
  3. Cree una base de datos del almacén de claves del cliente en el sistema DataStage utilizando el programa de utilidad **gsk8capicmd_64**.

     `# /home/db2inst2/SSL> gsk8capicmd_64 -keydb -create -db <keystore_db.kdb> -pw <ks_db_password> -stash`

     donde `<keystore_db.kdb>` representa la base de datos del almacén de claves del cliente y `<ks_db_password>` representa la contraseña de la base de datos del almacén de claves del cliente.
        
  4. Añada el certificado a la base de datos del almacén de claves del cliente.

     `# /home/db2inst2/SSL> gsk8capicmd_64 -cert -add -db <keystore_db.kdb> -pw <ks_db_password> -label BLUDB_SSL -file DigiCertGlobalRootCA.crt`

     donde `<keystore_db.kdb>` representa la base de datos del almacén de claves del cliente y `<ks_db_password>` representa la contraseña de la base de datos del almacén de claves del cliente.
    
  5. Configure el cliente Db2 en el servidor de DataStage.
            
     a. Actualice los parámetros de configuración de SSL en el gestor de base de datos.

     `# /home/db2inst2> db2 update dbm cfg using SSL_CLNT_KEYDB /home/db2inst2/SSL/<keystore_db.kdb>`

     donde `<keystore_db.kdb>` representa la base de datos del almacén de claves del cliente.

     `# /home/db2inst2> db2 update dbm cfg using SSL_CLNT_STASH /home/db2inst2/SSL/<keystore_db.sth>`

     donde `<keystore_db.sth>`representa la ocultación de contraseña de la base de datos del almacén de claves del cliente.
            
     b. Catalogue el nodo de destino con la opción de seguridad SSL y, después, la base de datos BLUDB en el nodo de destino.

     `# /home/db2inst2> db2 catalog tcpip node <node_name> remote <IP_addr_of_BLUDB_database_server> server 50001 security SSL`

     donde `<node_name>` representa el nombre para el nodo de destino y `<IP_addr_of_BLUDB_database_server>` representa la dirección IP del servidor de base de datos BLUDB,

     `# /home/db2inst2> db2 catalog db BLUDB as <db_alias> at node <node_name>`

     donde `<db_alias>` es el nombre de la base de datos de {{site.data.keyword.dashdbshort_notm}}.

  6. Añada permisos de lectura y ejecución sobre los archivos del directorio SSL para todos. El usuario de DataStage que ejecuta los trabajos debe acceder a los archivos para realizar conexiones SSL a la base de datos Db2.

     `# /home/db2inst2/SSL> chmod 655 /home/db2inst2/SSL/*`

  7. Pruebe la conexión SSL de una de las formas siguientes:

     - Pruebe la conexión mediante CLP. Emita el mandato siguiente para conectarse a la base de datos de {{site.data.keyword.dashdbshort_notm}}:

       `db2 connect to <db_alias> user <user_id>`

       donde `<db_alias>` es su nombre para la base de datos de {{site.data.keyword.dashdbshort_notm}} y `<user_id>` es su ID de usuario de {{site.data.keyword.dashdbshort_notm}}. Se le pedirá que especifique la contraseña.
    
     - Pruebe la conexión mediante CLI. Emita el mandato siguiente para conectarse a la base de datos de {{site.data.keyword.dashdbshort_notm}}:

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

        donde `<alias>` es un alias que ha creado utilizando el mandato **db2cli writecfg**, `<user_id>` es el ID de usuario de {{site.data.keyword.dashdbshort_notm}}, y `<password>` is la contraseña de {{site.data.keyword.dashdbshort_notm}}.

- Para crear una conexión sin SSL, catalogue la base de datos {{site.data.keyword.dashdbshort_notm}} de destino completando los pasos siguientes:

  1. Catalogue el nodo de {{site.data.keyword.dashdbshort_notm}} de destino, de forma que las aplicaciones cliente se puedan conectar. Ejecute los siguientes mandatos de CLP:

     `db2 catalog tcpip node <node_name> remote <IP_address_of_BLUDB_database_server> server <port_number_of_BLUDB_database>`

     donde `<node_name>` representa el nombre para el nodo, `<IP_address_of_BLUDB_database_server>` representa la dirección IP del servidor de base de datos BLUDB, y `<port_number_of_BLUDB_database>` representa el número de puerto de la base de datos BLUDB.

  2. Catalogue la base de datos remota {{site.data.keyword.dashdbshort_notm}} de forma que las aplicaciones cliente puedan conectarse. Ejecute el mandato siguiente:

     `db2 catalog db BLUDB as <db_alias> at node <node_name>`

     donde `<db_alias>` representa su nombre para la base de datos de {{site.data.keyword.dashdbshort_notm}} y `<node_name>` representa el nombre del nodo.

  3. Pruebe la conexión no SSL de una de las formas siguientes:

      - Pruebe la conexión mediante CLP. Emita el mandato siguiente para conectarse a la base de datos de {{site.data.keyword.dashdbshort_notm}}:

        `db2 connect to <db_alias> user <user_id>`

        donde `<db_alias>` es su nombre para la base de datos de {{site.data.keyword.dashdbshort_notm}} y `<user_id>` es su ID de usuario de {{site.data.keyword.dashdbshort_notm}}. Se le pedirá que especifique la contraseña.

        `db2 list tables`

      - Pruebe la conexión mediante CLI. Emita el mandato siguiente para conectarse a la base de datos de {{site.data.keyword.dashdbshort_notm}}:

        `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

        donde `<alias>` es un alias que ha creado utilizando el mandato **db2cli writecfg**, `<user_id>` es el ID de usuario de {{site.data.keyword.dashdbshort_notm}}, y `<password>` is la contraseña de {{site.data.keyword.dashdbshort_notm}}.

  4. Utilice la [información de conexión](/docs/services/Db2whc/connecting/credentials.html) que ha recopilado antes para definir una conexión en el cliente DataStage. En el separador **Parámetros**, debe seleccionar el **DB2 Connector** para el campo **Conectar utilizando tipo de transferencia**.

     Para obtener detalles sobre cómo definir una conexión en DataStage, consulte los siguientes temas de la documentación de DataStage: 
     
     - [Creación de un objeto de conexión de datos de forma manual ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/SSZJPZ_11.3.0/com.ibm.swg.im.iis.ds.design.doc/topics/t_ddesref_Creating_a_Data_Connection_Object_Manually.html){:new_window}
     - [Configuración del acceso a bases de datos de DB2 ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/en/SSZJPZ_11.7.0/com.ibm.swg.im.iis.conn.common.usage.doc/topics/t_configuring_db2conn.html){:new_window}

## Informatica
{: #informatica}

Puede conectar Informatica a {{site.data.keyword.dashdbshort_notm}} para que le ayude a gestionar los datos.
{: shortdesc}

Vea este vídeo para aprender a integrar {{site.data.keyword.dashdbshort_notm}} con Informatica Cloud.

<iframe class="embed-responsive-item" id="youtubeplayer1" title="Conexiones DB2 - Guía rápida sobre cómo utilizar Informatica Cloud" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TUiS_HstLnU?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

<!-- To configure a native Db2 connection to connect to {{site.data.keyword.dashdbshort_notm}}, perform the following steps:

1. Run the `odbcad32.exe` file from your local system.
The ODBC Data Sources Administrator dialog box appears.

2. Create the 32-bit ODBC Data Source Name using the DataDirect Db2 drivers.

3. In the ODBC DB2 Wire Protocol Setup dialog box, click **Security** tab.

4. Set the value of the `Authentication Method` property as `1 -Encrypt Password`. The following image shows the **Security** tab in the ODBC DB2 Wire Protocol Setup dialog box where you can set the `Authentication Method` property:
             
   ![ODBC Db2 Wire Protocol Driver Setup - Security tab](images/odbc_driver.png)
       
5. In the ODBC DB2 Wire Protocol Setup dialog box, click **Modify Bindings** tab.

6. Enter your user name in the Package Collection property. The following image shows the **Modify Bindings** tab in the ODBC DB2 Wire Protocol Setup dialog box where you can set the `Package Collection` property: 

   ![ODBC Db2 Wire Protocol Driver Setup - Modify Bindings tab](images/odbc_driver_2.png)
            
7. In the PowerCenter Designer, use the data source name that you created to import the metadata.

8. In the PowerCenter Workflow Manager, create the required workflow.

9. Ensure that you have the {{site.data.keyword.dashdbshort_notm}} compatible 11.x Db2 clients when you run the workflow.

**Note**: If you want to set the authentication type when you create the Db2 client catalog, you could specify the value of the `AUTHENTICATION TYPE` property as `SERVER_ENCRYPT`. -->

<!-- Watch this video to see how to integrate Db2 and Salesforce with Informatica Cloud.

<iframe class="embed-responsive-item" id="youtubeplayer2" title="Integrate Db2 and Salesforce with Informatica Cloud" type="text/html" width="640" height="390" src="//www.youtube.com/watch?v=RGTLweZvKP8" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe> -->

<!-- [Informatica ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://kb.informatica.com/howto/6/Pages/20/522402.aspx?myk=Connect%20to%20Db2){:new_window} -->

## Lift
{: #lift}

Utilice Lift para migrar los datos a {{site.data.keyword.dashdbshort_notm}}.

[Lift ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://lift.ng.bluemix.net/#docs){:new_window}

## InfoSphere Data Replication
{: #idr}

Puede conectar IBM® InfoSphere® Data Replication <!--version 11.3.3.3-36 or later -->a una base de datos de {{site.data.keyword.dashdbshort_notm}}. Esta prestación se aplica a ambos entornos, SMP y MPP. No se aplica al plan de entrada de {{site.data.keyword.dashdbshort_notm}}. 
{: shortdesc}

### Visión general
{: #overview2}

Idealmente, cuando conecta IBM InfoSphere Data Replication a {{site.data.keyword.dashdbshort_notm}}, este se encuentra en el mismo centro de datos de {{site.data.keyword.Bluemix_notm}} que {{site.data.keyword.dashdbshort_notm}} o lo comparte con {{site.data.keyword.dashdbshort_notm}}. IBM InfoSphere Data Replication se conecta desde un servidor local a la instancia remota de {{site.data.keyword.dashdbshort_notm}}.

Al utilizar {{site.data.keyword.dashdbshort_notm}} como destino de conexión, el rendimiento de IBM InfoSphere Data Replication depende en parte del ancho de banda de la red que separa el motor de destino de la instancia de {{site.data.keyword.dashdbshort_notm}}. La distancia física también afecta al rendimiento: lo ideal es que IBM InfoSphere Data Replication esté tan cerca como sea posible de la instancia de {{site.data.keyword.dashdbshort_notm}}. La topología de red también afecta al rendimiento. Por ejemplo, lo ideal es que el motor de destino de IBM InfoSphere Data Replication se ejecute en una VM en la misma VPN (dominio de seguridad) que la instancia de destino. Cuantos menos nodos de red hay que recorrer (por ejemplo, cortafuegos o direccionadores), mejor. 

### Requisitos previos
{: #prereq2}

Si tiene previsto conectarse utilizando el protocolo SSL, descargue e instale GSKit V8. Consulte [GSKit V8 - Instrucciones de instalación, desinstalación y actualización ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/support/docview.wss?uid=swg21631462){:new_window}. Pulse el separador del sistema operativo que se aplica al sistema operativo de la máquina cliente. Si está instalando GSKit en un sistema Windows, asegúrese de especificar la vía de acceso del directorio de instalación de GSKit (`<installation_directory>\gsk8\bin`) para la variable de entorno **`PATH`**.

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](/docs/services/Db2whc/connecting/connecting.html#prereqs) necesarios.

Si tiene previsto conectarse utilizando el protocolo SSL, descargue el certificado SSL `DigiCertGlobalRootCA.crt` desde la consola web en un directorio de la máquina cliente. Para descargar el certificado, pulse **Conexión > Información de conexión** y seleccione el separador **Conexión con SSL**.

### Procedimiento
{: #proc2}

1. Elija uno de los siguientes métodos para realizar la conexión:

   - Para crear una conexión con SSL, complete los pasos siguientes:
            
     a. Emita el mandato siguiente:

     `cd /<ssl_directory_name>/ssl`

     donde `/<ssl_directory_name>/ssl` es la vía de acceso al directorio en el que ha descargado el certificado SSL `DigiCertGlobalRootCA.crt`.

     b. Cree una base de datos de claves de cliente y un archivo de ocultación utilizando la herramienta **GSKCapiCmd**. Por ejemplo, el mandato siguiente crea una base de datos de claves de cliente llamada `dashclient.kdb` y un archivo de ocultación llamado `dashclient.sth`:

     `gsk8capicmd_64 -keydb -create -db "dashclient.kdb" -pw "passw0rdpw0" -stash`

     donde `passw0rdpw0` es una contraseña. La opción **-stash** crea un archivo de ocultación en la misma vía de acceso que la de la base de datos de claves de cliente, con una extensión de archivo `.sth`. Durante el tiempo de conexión, GSKit utiliza el archivo de ocultación para obtener la contraseña para la base de datos de claves de cliente.
            
     c. Añada el certificado a la base de datos de claves de cliente. Por ejemplo, el mandato **gsk8capicmd** siguiente importa el certificado del archivo `/<ssl_directory_name>/ssl/DigiCertGlobalRootCA.crt` a la base de datos de claves de cliente `dashclient.kdb`:

     `gsk8capicmd_64 -cert -add -db "dashclient.kdb" -pw "passw0rdpw0" -label "DigiCert" -file "/<ssl_directory_name>/ssl/DigiCertGlobalRootCA.crt" -format ascii -fips`

     d. Actualice los valores de los parámetros de configuración del gestor de bases de datos `SSL_CLNT_KEYDB` y `SSL_CLNT_STASH` en el cliente para especificar la base de datos de claves de cliente y el archivo de ocultación. A continuación, se muestran algunos ejemplos:

     `db2 update dbm cfg using SSL_CLNT_KEYDB /<ssl_directory_name>/ssl/dashclient.kdb`

     `db2 update dbm cfg using SSL_CLNT_STASH /<ssl_directory_name>/ssl/dashclient.sth`

     e. Catalogue el nodo de {{site.data.keyword.dashdbshort_notm}}, de forma que las aplicaciones cliente se puedan conectar. Emita el mandato siguiente:

     `db2 catalog tcpip node <node_name> remote <Db2_Warehouse_IP_address> server <port_number> security ssl`

     donde:
                
     `<node_name>` es el nombre del nodo.

     `<Db2_Warehouse_IP_address>` es la dirección IP del servidor de Db2 Warehouse on Cloud.

     `<port_number>` es el puerto que se utiliza para conectarse a Db2 Warehouse mediante una conexión SSL. Si está utilizando el puerto predeterminado, especifique `50001`.
            
     f. Catalogue la base de datos remota {{site.data.keyword.dashdbshort_notm}} de forma que las aplicaciones cliente puedan conectarse. Emita el mandato siguiente:

     `db2 catalog database bludb as <db_alias> at node <node_name>`

     donde `alias_bd` es el nombre de la base de datos {{site.data.keyword.dashdbshort_notm}}.
            
     g. Pruebe la conexión SSL de una de las formas siguientes:
                
     - Pruebe la conexión utilizando el CLP emitiendo el mandato siguiente para conectarse a la base de datos {{site.data.keyword.dashdbshort_notm}}:

       `db2 connect to <db_alias> user <user_id>`

       donde `<user_id>` es su ID de usuario de {{site.data.keyword.dashdbshort_notm}}. Se le pedirá que especifique la contraseña.
                
     - Pruebe la conexión utilizando la CLI emitiendo el mandato siguiente para conectarse a la base de datos {{site.data.keyword.dashdbshort_notm}}:

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

       donde `<alias>` es un alias DSN que ha creado utilizando el mandato **db2cli writecfg**, `<user_id>` es el ID de usuario de {{site.data.keyword.dashdbshort_notm}}, y `<password>` es la contraseña de la base de datos de {{site.data.keyword.dashdbshort_notm}}.
        
   - Para crear una conexión sin SSL, complete los pasos siguientes:

     a. Catalogue el nodo de {{site.data.keyword.dashdbshort_notm}}, de forma que las aplicaciones cliente se puedan conectar. Emita el mandato siguiente:

     `db2 catalog tcpip node <node_name> remote <Db2_Warehouse_IP_address> server <port_number>`

     donde:
                
     `<node_name>` es el nombre del nodo.

     `<Db2_Warehouse_IP_address>` es la dirección IP del servidor de {{site.data.keyword.dashdbshort_notm}}.

     `<port_number>` es el puerto que se utiliza para conectarse a {{site.data.keyword.dashdbshort_notm}} sin utilizar una conexión SSL. Si está utilizando el puerto predeterminado, especifique `50000`.
            
     b. Catalogue la base de datos remota {{site.data.keyword.dashdbshort_notm}} de forma que las aplicaciones cliente puedan conectarse. Emita el mandato siguiente:

     `db2 catalog database bludb as <db_alias> at node <node_name>`

     donde `<db_alias>` es el nombre de la base de datos de {{site.data.keyword.dashdbshort_notm}}.

     c. Pruebe la conexión no SSL de una de las formas siguientes:

     - Pruebe la conexión utilizando el CLP emitiendo el mandato siguiente para conectarse a la base de datos {{site.data.keyword.dashdbshort_notm}}:

       `db2 connect to <db_alias> user <user_id>`

       donde `<user_id>` es su ID de usuario de {{site.data.keyword.dashdbshort_notm}}. Se le pedirá que especifique la contraseña.
                
     - Pruebe la conexión utilizando la CLI emitiendo el mandato siguiente para conectarse a la base de datos {{site.data.keyword.dashdbshort_notm}}:

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

       donde `<alias>` es un alias DSN que ha creado utilizando el mandato **db2cli writecfg**, `<user_id>` es el ID de usuario de {{site.data.keyword.dashdbshort_notm}}, y `<password>` es su contraseña de Db2 Warehouse on Cloud.
    
2. Inicie la herramienta de configuración de InfoSphere Data Replication y realice los pasos siguientes. Los valores que se muestran en las capturas de pantalla son ejemplos.
        
   a. Añada una instancia para que apunte a la base de datos de origen utilizando el separador **Configuración de instancia**:

   ![Nueva instancia de IIDR - Instancia de origen](images/IIDR_source_instance.jpg)

   b. Añada una instancia de destino para que apunte a la base de datos Db2 de destino mediante el separador **Configuración de instancia**. Si no está utilizando IBM InfoSphere Data Replication 11.3.3.3-50 o posterior, no elija el recuadro de selección **Especificar vía de acceso del cargador de actualización**.

   ![Nueva instancia de IIDR - Instancia de destino](images/IIDR_target_instance.jpg)

   c. Inicie cada instancia:

   ![Herramienta de configuración IIDR](images/IIDR_instances.jpg)

3. Inicie la consola de gestión de InfoSphere Data Replication y utilice el gestor de acceso para completar los pasos siguientes:
        
   a. Cree un almacén de datos para conectarse a la instancia de origen utilizando el separador **Almacén de datos**. Puesto que originalmente no se admitía ninguna base de datos Db2 como base de datos de origen, debe proporcionar información de usuario y contraseña para la base de datos de origen pulsando **Parámetros de conexión**.

   ![Propiedades de almacén de datos - Origen](images/IIDR_source_datastore.jpg)

   b. Cree un almacén de datos para conectarse a la instancia de destino utilizando el separador **Almacén de datos**. Debe proporcionar información de usuario y contraseña pulsando **Parámetros de conexión**.

   ![Propiedades de almacén de datos - Destino](images/IIDR_target_datastore.jpg)

   c. Si el usuario (por ejemplo, admin) que se conectará a Access Server no existe, créelo:

   ![Nuevo usuario](images/IIDR_management_user.jpg)

   d. Pulse el separador **Access Manager**.
        
   e. En el separador **Gestión de almacén de datos**, asigne el usuario a ambos almacenes de datos, de origen y de destino, pulsando con el botón derecho del ratón en **Asignar usuario**. Asegúrese de que las credenciales para acceder a cada instancia son correctas.

   ![Consola de gestión IIDR - Gestor de acceso](images/IIDR_management_assign_user.jpg)

### Qué hacer a continuación
{: #what2}

Defina una suscripción y realice la réplica de datos. Para obtener más información, consulte:

- [Carga de datos desde InfoSphere Data Replication ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/learn_how/loaddata_iidr.html){:new_window} 

## Segment
{: #segment}

Puede integrar Segment con una base de datos de {{site.data.keyword.dashdbshort_notm}}. Segment es una plataforma única que recopila, almacena y direcciona los datos de usuario a cientos de herramientas.
{: shortdesc}

[Segment ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://segment.com/docs/destinations/db2/){:new_window}

## Data Studio
{: #data_studio}

En las instrucciones se explica cómo crear una conexión desde IBM® Data Studio <!--version 4.1.x -->a una base de datos de {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Requisitos previos
{: #prereq3}

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](/docs/services/Db2whc/connecting/connecting.html#prereqs) necesarios.

### Procedimiento
{: #proc3}

1. En Data Studio, pulse **Todas las bases de datos > Nueva conexión a una base de datos**.

2. En el separador **Local**,
seleccione **DB2 para Linux, UNIX y Windows** como
gestor de base de datos.
    
3. En el separador **General**, especifique los valores siguientes:
   - *Base de datos*: `BLUDB`
   - *Host*: El nombre de host.
   - *Puerto*: Para una conexión sin SSL, especifique `50000`. Para una conexión con SSL, especifique `50001`. 
   - *Nombre de usuario*: El nombre de usuario que utiliza para iniciar sesión.
   - *Contraseña*: La contraseña que utiliza para iniciar sesión.

4. Para una conexión SSL, pulse el separador **Opcional** y, después, pulse **Añadir**. Para la propiedad `sslConnection`, especifique `true`.

5. [*Opcional*] Pulse **Pruebe la conexión** para verificar que la conexión se ha realizado correctamente.

## Data Server Manager (DSM)
{: #dsm}

Una conexión entre IBM® Data Server Manager y su base de datos de {{site.data.keyword.dashdbshort_notm}} le permite supervisar y gestionar la base de datos desde la consola web de Data Server Manager. 
{: shortdesc}

### Requisitos previos
{: #prereq4}

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](/docs/services/Db2whc/connecting/connecting.html#prereqs) necesarios.

### Procedimiento
{: #proc4}

<!--The connection procedure was tested on Data Server Manager version 1.1. The same procedure applies to all of the other versions of the Data Server Manager software.
-->
Para crear una conexión, complete los pasos siguientes:

1. Inicie sesión en la consola web de Data Server Manager.
    
2. En la consola web de Data Server Manager, vaya a **Configurar > Conexiones de base de datos**.
    
3. Pulse el ![signo + dentro de un círculo](images/icon_R_plus.gif) icono para añadir una conexión de base de datos. En la página **Añadir conexión de base de datos** bajo el separador **Conexión de base de datos**, especifique la información necesaria en los campos siguientes:

   - *Nombre de conexión de base de datos*: El nombre debe ser exclusivo de Data Server Manager
   - *Tipo de servidor de datos*: En el menú desplegable, seleccione **DB2 for Linux, UNIX, and Windows**
   - *Nombre de base de datos*: `BLUDB`
   - *Nombre de host*: Especifique el nombre de host de {{site.data.keyword.dashdbshort_notm}} 
   - *Número de puerto*: Para una conexión sin SSL, especifique `50000`. Para una conexión con SSL, especifique `50001`. 
   - *Seguridad JDBC*: En el menú desplegable, seleccione **Contraseña de texto simple**
   - *ID de usuario*: Su ID de usuario de {{site.data.keyword.dashdbshort_notm}} 
   - *Contraseña*: Su contraseña de {{site.data.keyword.dashdbshort_notm}} 

4. Para una conexión con SSL, seleccione el separador **Propiedades JDBC avanzadas**. Escriba la información necesaria en los campos siguientes:

   - *Propiedad*: `sslConnection`
   - *Valor*: `true`

    Pulse el botón **Añadir**. Seleccione el separador **Conexión de base de datos**.
    
5. Pruebe la conexión pulsando el botón **Probar conexión**. Si la conexión se ha realizado satisfactoriamente, pulse **Aceptar**.

## InfoSphere Data Architect
{: #ida}

En las instrucciones se explica cómo crear una conexión desde InfoSphere® Data Architect <!--version 9.1.x -->a una base de datos de {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Requisitos previos
{: #prereq5}

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](/docs/services/Db2whc/connecting/connecting.html#prereqs) necesarios.

### Procedimiento
{: #proc5}

1. En la vista Explorador de orígenes de datos de InfoSphere Data Architect, pulse con el botón derecho en **Conexiones de base de datos**, seleccione **Nuevo**.
    
2. En el separador **Local**,
seleccione **DB2 para Linux, UNIX y Windows** como
gestor de base de datos.
    
3. En el separador **General**, especifique los valores siguientes:

   - *Base de datos*: `BLUDB`
   - *Host*: El nombre de host que ha recopilado antes.
   - *Puerto*: Para una conexión sin SSL, especifique `50000`. Para una conexión con SSL, especifique `50001`. 
   - *Nombre de usuario*: El ID de usuario que ha recopilado antes.
   - *Contraseña*: La contraseña que ha recopilado antes.

4. Para una conexión SSL, pulse el separador **Opcional**. Entre una propiedad `sslConnection` y especifique un valor de `true`. Pulse
**Añadir**.
    
5. [*Opcional*] Pulse **Pruebe la conexión** para verificar que la conexión se ha realizado correctamente.

## Aginity Workbench
{: #aginity_wb}

En estas instrucciones se explica cómo conectar Aginity Workbench <!--4.3 -->a una base de datos de {{site.data.keyword.dashdbshort_notm}}. Puede utilizar Aginity Workbench para migrar datos y modelos de datos de IBM PureData for Analytics (Netezza) a {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Requisitos previos
{: #prereq6}

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](/docs/services/Db2whc/connecting/connecting.html#prereqs) necesarios.

### Procedimiento
{: #proc6}

1. Descargue e instale Aginity Workbench.

2. Determine el DSN ODBC de la información de conexión que ha anotado anteriormente.

3. Inicie Aginity Workbench. Si el recuadro de diálogo de conexión a base de datos no se abre automáticamente, ábralo pulsando **Conectar** en la barra de herramientas.

4. [Establecer una conexión de base de datos ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.aginity.com/documentation/WB/dashDB/Default.htm#Aginity_Topics/Aginity_Workbench/Database_Connection_Dialog_Box.htm){:new_window}. Utilice el nombre de host, el ID de usuario y la contraseña de la información de conexión que ha anotado antes.

## CLPPlus
{: #clpplus}

El procesador de línea de mandatos plus (CLPPlus) se incluye en el paquete de controlador de Db2. CLPPlus proporciona una interfaz de línea de mandatos que puede utilizar para conectarse a una base de datos de {{site.data.keyword.dashdbshort_notm}}. Puede utilizar CLPPlus para definir, editar y ejecutar sentencias, scripts y mandatos.
{: shortdesc}

### Requisitos previos
{: #prereq7}

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](/docs/services/Db2whc/connecting/connecting.html#prereqs) necesarios.

Para utilizar CLPPlus, asegúrese de que está instalado en el sistema un kit de desarrollo de software (SDK) o un Java Runtime Environment (JRE) para Java versión 1.5.0 o posterior y que las variables de entorno están establecidas del modo siguiente:

- La variable de entorno `JAVA_HOME` está establecida en el directorio de instalación de Java en el sistema.
- La definición de la variable de entorno `PATH` incluye el subdirectorio `bin` del directorio de instalación de Java en el sistema.

### Procedimiento
{: #proc7}

1. En un shell de mandatos en sistemas operativos Linux, en el indicador de mandatos Windows o en la ventana de mandatos DB2 en sistemas operativos Windows, ejecute los mandatos siguientes:

   Estos mandatos crean nuevas entradas en el archivo de configuración del controlador (`db2dsdriver.cfg`) en el sistema y establecen los atributos de conexión. Solo debe realizar este paso una vez.

   - Para una conexión con SSL:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`  

     donde:
     
     - `<hostname>` es el nombre de host del servidor.
     - `<alias>` es el alias que elija.

   - Para una conexión sin SSL:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

2. Para iniciar CLPPlus con una conexión a una base de datos de {{site.data.keyword.dashdbshort_notm}} que utiliza entradas en el archivo `db2dsdriver.cfg`, ejecute el mandato siguiente:

   - Entornos Windows: 

     `clpplus <userid>@<alias>`

   - Entornos Linux:

     `clpplus -nw <userid>@<alias>`

     donde:
     
     - `<userid>` es el ID de usuario de las credenciales de conexión que ha recopilado antes.
     - `<alias>` es el alias que ha creado con el mandato **db2cli writecfg**.

   La ejecución de este mandato abre una ventana de CLPPlus.

3. En la ventana de CLPPLus, especifique la contraseña. Se muestra la información de base de datos, seguida de una solicitud SQL. A continuación, se muestra la salida de ejemplo:

```
   Hostname = 192.0.2.0
   Database server = DB2/LINUXX8664  SQL10054
   SQL authorization ID = smith
   Local database alias = BLUDB
   Port = 50001
   
   SQL>
```

### Resultados
{: #results7}

Ahora puede entrar mandatos CLPPlus o sentencias SELECT y ejecutar scripts para trabajar con los datos en la base de datos.

### Ejemplos

Los ejemplos siguientes utilizan un script corto que recupera filas de la tabla de ejemplo `GOSALES.BRANCH`. El archivo de script se denomina `cities.sql` y se encuentra en el sistema Windows local en `C:\temp directory`. El archivo `cities.sql` contiene el texto siguiente:

```
SET ECHO ON
SELECT branch_code, city from GOSALES.BRANCH;
```

#### Ejemplo 1 

Para ejecutar el script de forma interactiva:

1. Inicie CLPPlus con el ID de usuario y el alias que ha creado en el archivo `db2dsdriver.cfg` ejecutando el mandato siguiente:

   `clpplus <user_id>@<alias>`
2. Escriba la contraseña.
3. En el indicador SQL, entre el texto siguiente:

   `start C:\temp\cities.sql`

#### Ejemplo 2

Inicie CLPPlus con el ID de usuario y el alias que ha creado en el archivo `db2dsdriver.cfg` y ejecute el script en un paso:

`clpplus <user_id>/<password>@<alias> @C:\temp\cities.sql`

A continuación, se muestra la salida de ejemplo del script `cities.sql`:

```
BRANCH_CODE CITY
----------- --------------------------------------------------
          6 Paris
          7 Milano
          9 Amsterdam
         13 Hamburg
         14 München
         15 Kista
         17 Calgary
         18 Toronto
         19 Boston
         20 Seattle
         21 Los Angeles
         22 Miami
         23 Lyon
         24 Distrito Federal
         25 Tokyo
         26 Osaka City
         28 Melbourne
         29 Bilbao
         30 Sao Paulo
         31 Kuopio
         32 Seoul
         33 Singapore

BRANCH_CODE CITY
----------- --------------------------------------------------
         34 Shanghai
         35 London
         36 Birmingham
         37 Zürich
         38 Heverlee
         39 Wien
         40 Geneve

29 rows were retrieved.
```


