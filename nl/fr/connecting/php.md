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

# Connexion à PHP à l'aide d'un programme
{: #con_prog_php}

Définissez une connexion entre une application PHP et une base de données {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

## Prérequis
{: #prereq101}

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) sont remplies.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procédure
{: #proc101}

### Scénario 1 : Connexion depuis l'extérieur de {{site.data.keyword.Bluemix_notm}} :
{: #scen1}

1. Téléchargez le [module de pilote Db2](/docs/services/Db2whc?topic=Db2whc-dr_pkg#dr_pkg) à partir de la console Web, puis installez-le sur l'ordinateur sur lequel votre application PHP s'exécutera.
                
2. Utilisez la fonction [`odbc_connect` ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](http://php.net/manual/en/function.odbc-connect.php){:new_window} pour vous connecter à la base de données BLUDB.
    
   Exemple de code PHP :

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

   Si vous enregistrez cet exemple de code PHP dans un fichier script appelé `C:\sample.php` et que vous exécutez le script depuis une ligne de commande, vous obtenez la sortie suivante :

   ```
   C:\> php –f sample.php

   Connection succeeded.
   ```

### Scénario 2 : Connexion à partir d'une application Web PHP dans {{site.data.keyword.Bluemix_notm}}
{: #scen2}

1. Dans le catalogue {{site.data.keyword.Bluemix_notm}}, créez une nouvelle application PHP.
        
2. Dans la section "Initiation" de la nouvelle application PHP de votre tableau de bord {{site.data.keyword.Bluemix_notm}}, téléchargez le code de démarrage de l'application vers votre répertoire de travail local.
        
3. Dans votre tableau de bord {{site.data.keyword.Bluemix_notm}}, créez une nouvelle connexion entre votre service Db2 et votre nouvelle application PHP. (La création de cette connexion dans {{site.data.keyword.Bluemix_notm}} rend la variable d'environnement `VCAP_SERVICES` disponible pour votre application PHP. La variable d'environnement `VCAP_SERVICES` contient les détails de base de données de votre service Db2. Utiliser `VCAP_SERVICES` est plus pratique que de coder en dur les détails de la base de données dans votre application PHP.)
        
4. Dans votre répertoire de travail local, mettez à jour le fichier `index.php` pour vous connecter à la base de données BLUDB à l'aide de la fonction [`db2_connect` ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](http://php.net/manual/en/function.db2-connect.php){:new_window}.
        
   Exemple :

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
   } else {
       echo "<p>No credentials.</p>";
   }
   ?>
   </body>
   </html>
   ```

5. Dans votre répertoire de travail local, poussez les mises à jour vers {{site.data.keyword.Bluemix_notm}} en suivant les instructions de la section "Initiation" de l'application PHP dans votre tableau de bord {{site.data.keyword.Bluemix_notm}}. Redémarrez ensuite l'application dans {{site.data.keyword.Bluemix_notm}} et affichez l'application dans un navigateur.


