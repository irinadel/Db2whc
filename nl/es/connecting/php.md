---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# Conexión mediante programas con PHP
{: #con_prog_php}

Defina una conexión entre una aplicación PHP y una base de datos de {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

## Requisitos previos

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](connecting.html#prereqs) necesarios.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedimiento

### Caso de ejemplo 1: Conexión desde fuera de {{site.data.keyword.Bluemix_notm}}:
        
1. Descargue el [paquete de controlador de Db2](driver_pkg.html) desde la consola web y, a continuación, instale el paquete de controlador en la máquina en la que se ejecutará la aplicación PHP.
                
2. Utilice la función [`odbc_connect` ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://php.net/manual/en/function.odbc-connect.php){:new_window} para conectarse a la base de datos BLUDB.
    
   Ejemplo de código de PHP:

   ```
   <?php
   $database = "BLUDB";        # Get these database details from
   $hostname = "<Host-name>";  # the web console
   $user     = "<User-ID >";   #
   $password = "<Password>";   #
   $port     = 50000;          #
   $ssl_port = 50001;          #
   # Build the connection string
   #
   $driver  = "DRIVER={IBM DB2 ODBC DRIVER};";
   $dsn     = "DATABASE=$database; " .
              "HOSTNAME=$hostname;" .
              "PORT=$port;" .
              "PROTOCOL=TCPIP;" .
              "UID=$user;" .
              "PWD=$password;";
   $ssl_dsn = "DATABASE=$database; " .
              "HOSTNAME=$hostname;" .
              "PORT=$ssl_port; " .
              "PROTOCOL=TCPIP;" .
              "UID=$user;" .
              "PWD=$password;" .
              "SECURITY=SSL;";
   $conn_string = $driver . $dsn;     # Non-SSL
   $conn_string = $driver . $ssl_dsn; # SSL
   # Connect
   #
   $conn = odbc_connect( $conn_string, "", "" );
   if( $conn )
   {
       echo "Connection succeeded.";
       # Disconnect
       #
       odbc_close( $conn );
   }
   else
   {
       echo "Connection failed.";
   }
   ?>
   ```

   Guardar este código PHP de ejemplo en un archivo de script llamado `C:\sample.php` y, después, ejecutar el script desde una línea de mandatos genera la salida siguiente:

   ```
   C:\> php –f sample.php

   Connection succeeded.
   ```

### Caso de ejemplo 2: Conexión desde una app web PHP en {{site.data.keyword.Bluemix_notm}}

1. Desde el catálogo {{site.data.keyword.Bluemix_notm}}, cree una nueva app PHP.
        
2. Desde la sección "Iniciación" de la nueva app PHP en el panel de control de {{site.data.keyword.Bluemix_notm}}, descargue el código de inicio de la app en el directorio de trabajo local.
        
3. En el panel de control de {{site.data.keyword.Bluemix_notm}}, cree una nueva conexión desde el servicio Db2 a la nueva app PHP. (La creación de esta conexión en {{site.data.keyword.Bluemix_notm}} hace que la variable de entorno `VCAP_SERVICES` esté disponible para la app PHP. La variable de entorno `VCAP_SERVICES` contiene detalles de base de datos para el servicio Db2. El uso de `VCAP_SERVICES` es más práctico que la grabación en el código fuente de los detalles de base de datos de la app PHP).
        
4. En el directorio de trabajo, actualice el archivo `index.php` para conectarse a la base de datos BLUDB utilizando la función [`db2_connect` ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://php.net/manual/en/function.db2-connect.php){:new_window}.
        
   Ejemplo:

   ```
   <!DOCTYPE html>
   <html>
   <head>
       <title>Aplicación de inicio PHP</title>
       <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
       <link rel="stylesheet" href="style.css" />
   </head>
   <body>
   <?php
   if( getenv( "VCAP_SERVICES" ) )
   {
       # Obtenga detalles de la base de datos a partir de la variable de entorno VCAP_SERVICES
       #
       # *Esto solo funciona si ha utilizado el panel de control de Bluemix para
       # crear una conexión desde el servicio dashDB a la app PHP.
       #
       $details  = json_decode( getenv( "VCAP_SERVICES" ), true );
       $dsn      = $details [ "dashDB" ][0][ "credentials" ][ "dsn" ];
       $ssl_dsn  = $details [ "dashDB" ][0][ "credentials" ][ "ssldsn" ];
       # Build the connection string
       #
       $driver = "DRIVER={IBM DB2 ODBC DRIVER};";
       $conn_string = $driver . $dsn;     # Non-SSL
       $conn_string = $driver . $ssl_dsn; # SSL
       $conn = db2_connect( $conn_string, "", "" );
       if( $conn )
       {
           echo "<p>Connection succeeded.</p>";
           db2_close( $conn );
       }
       else
       {
           echo "<p>Connection failed.</p>";
       }
   } else {
       echo "<p>No credentials.</p>";
   }
   ?>
   </body>
   </html>
   ```

5. Desde el directorio de trabajo local, envíe las actualizaciones a {{site.data.keyword.Bluemix_notm}} siguiendo las instrucciones de la sección "Iniciación" de la app PHP en el panel de control de {{site.data.keyword.Bluemix_notm}}. A continuación, reinicie la app en {{site.data.keyword.Bluemix_notm}} y visualícela en un navegador.


