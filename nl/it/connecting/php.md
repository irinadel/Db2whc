---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# Connessione programmatica con PHP
{: #con_prog_php}

Definisci una connessione tra un'applicazione PHP e un database {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

## Prerequisiti
{: #prereq101}

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](/docs/services/Db2whc/connecting/connecting.html#prereqs) necessari.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedura
{: #proc101}

### Scenario 1: Connessione dall'esterno di {{site.data.keyword.Bluemix_notm}}:
{: #scen1}

1. Scarica il [pacchetto del driver Db2](/docs/services/Db2whc/connecting/driver_pkg.html) dalla console web e installalo sulla macchina in cui verrà eseguita la tua applicazione PHP.
                
2. Utilizza la funzione [`odbc_connect` ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://php.net/manual/en/function.odbc-connect.php){:new_window} per il collegamento al database BLUDB.
    
   Esempio di codice PHP:

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

   Salva questo esempio di codice PHP in un file script denominato `C:\sample.php` ed eseguendo lo script da una riga di comando crei il seguente output:

   ```
   C:\> php –f sample.php

   Connection succeeded.
   ```

### Scenario 2: Connessione da una pagina web PHP in {{site.data.keyword.Bluemix_notm}}
{: #scen2}

1. Dal catalogo {{site.data.keyword.Bluemix_notm}}, crea una nuova applicazione PHP.
        
2. Dalla sezione "Getting Started" della nuova applicazione PHP nel tuo dashboard {{site.data.keyword.Bluemix_notm}}, scarica il codice starter dell'applicazione nella tua directory di lavoro locale.
        
3. Nel tuo dashboard {{site.data.keyword.Bluemix_notm}}, crea una nuova connessione dal tuo servizio Db2 alla tua nuova applicazione PHP. (La creazione di questa connessione in {{site.data.keyword.Bluemix_notm}} rende la variabile di ambiente `VCAP_SERVICES` disponibile per la tua applicazione PHP. La variabile di ambiente `VCAP_SERVICES` contiene i dettagli del database per il tuo servizio Db2. L'utilizzo di `VCAP_SERVICES` è più conveniente rispetto a impostare i dettagli del database come hardcoded nella tua applicazione PHP.)
        
4. Nella tua directory di lavoro locale, aggiorna il file `index.php` per collegarsi al database BLUDB utilizzando la funzione [`db2_connect` ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://php.net/manual/en/function.db2-connect.php){:new_window}.
        
   Esempio:

   ```
   <!DOCTYPE html>
   <html>
   <head>
       <title>PHP Starter Application</title>
       <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
       <link rel="stylesheet" href="style.css" />
   </head>
   <body>
   <?php
   if( getenv( "VCAP_SERVICES" ) )
   {
       # Get database details from the VCAP_SERVICES environment variable
       #
       # *This can only work if you have used the Bluemix dashboard to 
       # create a connection from your dashDB service to your PHP App.
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
   }
   else
   {
       echo "<p>No credentials.</p>";
   }
   ?>
   </body>
   </html>
   ```

5. Dalla tua directory i lavoro locale, esegui il push degli aggiornamenti a {{site.data.keyword.Bluemix_notm}} seguendo le istruzioni nella sezione "Getting Started" dell'applicazione PHP nel tuo dashboard {{site.data.keyword.Bluemix_notm}}. Quindi riavvia l'applicazione in {{site.data.keyword.Bluemix_notm}} e visualizzala in un browser.


