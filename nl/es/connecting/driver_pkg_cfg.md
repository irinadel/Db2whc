---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# Configuración del entorno local
{: #cfg_loc_env}

Para conectar aplicaciones y herramientas locales a la base de datos {{site.data.keyword.dashdbshort_notm}}, tendrá que configurar el entorno.  
{: shortdesc}

## Requisitos previos
{: #prereq21}

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) necesarios.

<!-- 1. Install the Db2 driver package for your operating system.

   - [Installing on Windows](install_win.html)
   - [Installing on Linux or PowerLinux](install_linux.html)
   - [Installing on Mac OS X](install_mac.html)
2. Decide whether or not you will be using Secure Sockets Layer (SSL) to connect to your database.
3. Collect database details and connect credentials, including the host name of your server, and your database user ID and password. -->

## Procedimiento
{: #proc21}

1. Añada entradas al archivo de configuración del controlador, `db2dsdriver.cfg`, para la base de datos.

   Los pasos de configuración son diferentes en función de si desea conectarse a la base de datos utilizando SSL:

   **Con SSL**

   Para conectar las aplicaciones y herramientas a la base de datos utilizando SSL, especifique los mandatos siguientes en un shell de mandatos en sistemas operativos Linux, en el indicador de mandatos Windows o en una ventana de mandatos DB2: 

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50001`

   `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

    donde:

   - `<hostname>` es el nombre de host del servidor.
   - `<alias>` es el alias que elija. El alias no puede ser el mismo que el nombre de la base de datos, `BLUDB`. Si desea que haya espacios en el alias, escriba el alias con comillas dobles.

   **Sin SSL**

   Para conectar las aplicaciones y herramientas a la base de datos sin utilizar SSL, especifique los mandatos siguientes en un shell de mandatos en sistemas operativos Linux, en el indicador de mandatos Windows o en una ventana de mandatos DB2: 

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

   `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

    donde:

   - `<hostname>` es el nombre de host del servidor.
   - `<alias>` es el alias que elija. El alias no puede ser el mismo que el nombre de la base de datos, `BLUDB`. Si desea que haya espacios en el alias, escriba el alias con comillas dobles.

2. Pruebe la conexión emitiendo el mandato **db2cli validate** desde el indicador de mandatos:

   `db2cli validate -dsn <alias> -connect -user <userid> -passwd <password>`

   donde: 
   
   - `<alias>` es un alias que ha creado con el mandato **db2cli writecfg**.
   - `<userid>` es el ID de usuario de Db2.
   - `<password>` es la contraseña de Db2.

3. [*Opcional*] Para poder conectar aplicaciones y herramientas ODBC locales a la base de datos, registre el DSN con el gestor de controladores ODBC:
 
   Ejecute el mandato siguiente desde una línea de mandatos: 

   `db2cli registerdsn -add -dsn <alias>`

   donde: 

   - `<alias>` es un alias que ha creado con el mandato **db2cli writecfg**.

   De forma predeterminada, el DSN se crea como un DSN de usuario.

