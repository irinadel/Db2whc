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

# Programmgestützte Verbindungsherstellung - PHP
{: #con_prog_php}

Definieren Sie eine Verbindung zwischen einer PHP-Anwendung und einer {{site.data.keyword.dashdbshort_notm}}-Datenbank.
{: shortdesc}

## Voraussetzungen
{: #prereq101}

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](/docs/services/Db2whc/connecting/connecting.html#prereqs) erfüllt werden.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Vorgehensweise
{: #proc101}

### Szenario 1: Außerhalb von {{site.data.keyword.Bluemix_notm}} eine Verbindung herstellen:
{: #scen1}

1. Laden Sie das [Db2-Treiberpaket](/docs/services/Db2whc/connecting/driver_pkg.html) über die Webkonsole herunter und installieren Sie das Paket auf der Maschine, auf dem Ihre PHP-Anwendung ausgeführt werden soll.
                
2. Stellen Sie über die Funktion [`odbc_connect` ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://php.net/manual/en/function.odbc-connect.php){:new_window} eine Verbindung zu der Datenbank BLUDB her.
    
   PHP-Beispielcode:

   ```
   <?php
   $database = "BLUDB";        # Rufen Sie diese Datenbankdetails über
   $hostname = "<Host-name>";  # die Webkonsole ab.
   $user     = "<User-ID >";   #
   $password = "<Password>";   #
   $port     = 50000;          #
   $ssl_port = 50001;          #
   # Verbindungszeichenfolge erstellen
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
   $conn_string = $driver . $dsn;     # Verbindung ohne SSL
   $conn_string = $driver . $ssl_dsn; # SSL-Verbindung
   # Verbinden
   #
   $conn = odbc_connect( $conn_string, "", "" );
   if( $conn )
   {
       echo "Connection succeeded.";
       # Verbindung trennen
       #
       odbc_close( $conn );
   }
   else
   {
       echo "Connection failed.";
   }
   ?>
   ```

   Das Speichern dieses PHP-Beispielcodes in einer Scriptdatei namens `C:\sample.php` und anschließende Ausführen des Scripts über eine Befehlszeile führt zu der folgenden Ausgabe:

   ```
   C:\> php –f sample.php

   Connection succeeded.
   ```

### Szenario 2: Verbindung von PHP-Web-App aus in {{site.data.keyword.Bluemix_notm}} herstellen
{: #scen2}

1. Erstellen Sie über den {{site.data.keyword.Bluemix_notm}}-Katalog eine neue PHP-App.
        
2. Laden Sie wie im Bereich 'Einführung' der neuen PHP-App in Ihrem {{site.data.keyword.Bluemix_notm}}-Dashboard den Startercode für die App in Ihr lokales Arbeitsverzeichnis herunter.
        
3. Erstellen Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard eine neue Verbindung zwischen dem Db2-Service und der neuen PHP-App. (Das Erstellen dieser Verbindung in {{site.data.keyword.Bluemix_notm}} führt dazu, dass die Umgebungsvariable `VCAP_SERVICES` in der PHP-App verfügbar ist. Die Umgebungsvariable `VCAP_SERVICES` enthält die Datenbankdetails für den Db2-Service. Die Verwendung von `VCAP_SERVICES` hat Vorteile gegenüber einer festen Codierung der Datenbankdetails in der PHP-App.)
        
4. Aktualisieren Sie im lokalen Arbeitsverzeichnis die Datei `index.php`, um die Verbindung zur Datenbank BLUDB über die Funktion [`db2_connect` ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://php.net/manual/en/function.db2-connect.php){:new_window} herzustellen.
        
   Beispiel:

   ```
   <!DOCTYPE html>
   <html>
   <head>
       <title>PHP-Starteranwendung</title>
       <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
       <link rel="stylesheet" href="style.css" />
   </head>
   <body>
   <?php
   if( getenv( "VCAP_SERVICES" ) )
   {
       # Datenbankdetails über die Umgebungsvariable VCAP_SERVICES abrufen
       #
       # *Dies ist nur möglich, wenn Sie das Bluemix-Dashboard zum Erstellen einer
       # Verbindung zwischen dem Service 'dashDB' und der PHP-App verwendet haben.
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

5. Übertragen Sie die Aktualisierungen für {{site.data.keyword.Bluemix_notm}} vom lokalen Arbeitsverzeichnis aus mit einer Push-Operation. Orientieren Sie sich dabei an den Anweisungen im Bereich 'Einführung' der PHP-App in Ihrem {{site.data.keyword.Bluemix_notm}}-Dashboard. Starten Sie die App anschließend in {{site.data.keyword.Bluemix_notm}} und zeigen Sie die App in einem Browser an.


