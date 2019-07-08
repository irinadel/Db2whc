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

# Conexión mediante programa con ODBC o CLI
{: #con_prog_odbc_cli}

Defina una conexión entre una ODBC de Microsoft Windows o una aplicación de CLI y una base de datos de {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

## Requisitos previos
{: #prereq81}

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) necesarios.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedimiento
{: #proc81}

1. En un shell de mandatos en sistemas operativos Linux, en el indicador de mandatos Windows o en la ventana de mandatos Db2 en sistemas operativos Windows, especifique los mandatos siguientes:

   **Nota**: Estos mandatos crean nuevas entradas en el archivo de configuración del controlador (`db2dsdriver.cfg`) en el sistema y establecen los atributos de conexión. Solo debe realizar este paso una vez.
   
   - Para una conexión con SSL:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

   - Para una conexión sin SSL:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

   donde:

   `<hostname>` es el nombre de host del servidor

   `<alias>` es el alias de DSN que elija
    
2. [*Opcional*] Para verificar la conexión a la base de datos, ejecute este mandato desde el indicador de mandatos:

   `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

   donde:

   `<alias>` es el alias de DSN que ha creado con el mandatos **db2cli writecfg**

   `<user_id>` es de las credenciales de conexión que ha recopilado antes

   `<password>` es de las credenciales de conexión que ha recopilado antes

3. [*Opcional*] Para registrar el nombre del origen de datos (DSN) con el gestor de controlador ODBC y para trabajar con aplicaciones ODBC de Microsoft, ejecute el mandato siguiente. De forma predeterminada, el DSN se crea como DSN de usuario.

   `db2cli registerdsn -add -dsn <alias>`

   donde:
        
   `<alias>` es el alias de DSN que ha creado con el mandatos **db2cli writecfg**



