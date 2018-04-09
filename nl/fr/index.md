---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-15"

---

<!-- Attribute definitions --> 
{:javascript: #javascript .ph data-hd-programlang='javascript'}
{:java: #java .ph data-hd-programlang='java'}
{:ruby: #ruby .ph data-hd-programlang='ruby'}
{:php: #php .ph data-hd-programlang='php'}
{:python: #python .ph data-hd-programlang='python'}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}

# Initiation
{: #getting_started}

Le service géré {{site.data.keyword.dashdblong}} est une base de données SQL mise à votre disposition dans le cloud. Vous pouvez utiliser l'entrepôt Db2 de la même manière que vous utilisez n'importe quel logiciel de base de données, sans les frais associés à la configuration de matériel ou à l'installation et la maintenance de logiciels. 
{: shortdesc}

## Essai gratuit
{: #freetrial}

Vous pouvez essayer le plan {{site.data.keyword.dashdbshort_notm}} Entry avec jusqu'à 1 Go de stockage, gratuitement. [Essai gratuit ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.bluemix.net/catalog/services/dashdb){:new_window}

## Interfaces
{: #interfaces}

Vous pouvez utiliser votre base de données d'entrepôt des manières suivantes :
{: shortdesc}

   * A partir de la console Web
   * API REST
   * Connectez des applications ou vos outils préférés depuis votre ordinateur local
   * Utilisez {{site.data.keyword.dashdbshort_notm}} comme source de données pour vos applications ou services {{site.data.keyword.Bluemix_notm}}

### Console Web
{: #web_console}

La console web fournit une interface graphique pour tous les éléments dont vous avez besoin pour utiliser votre base de données : fonctions de chargement, éditeur SQL, téléchargements de pilotes, et plus encore.
{: shortdesc}

![Affichez la page du tableau de bord de la console Web](images/console_v3.png)

<!-- Click the link to take a tour of the {{site.data.keyword.dashdbshort_notm}} for Analytics web console: [General tour ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ibm.biz/dashdb-general-quick-tour){:new_window}. -->

Vous pouvez accéder à la console Web de l'une des manières suivantes :
   * A partir de votre tableau de bord {{site.data.keyword.Bluemix_notm}} : vous pouvez ouvrir la console Web depuis la page Détails du service de votre service {{site.data.keyword.dashdbshort_notm}}.
   * URL directe : vous pouvez ajouter un signet associé à l'URL de la console Web pour votre service {{site.data.keyword.dashdbshort_notm}}.

### API REST
{: #api}

Grâce aux plans de service {{site.data.keyword.dashdbshort_notm}}, vous pouvez effectuer des tâches liées à la gestion de fichiers, au chargement de données et à l'exécution de scripts R à l'aide de l'[API REST {{site.data.keyword.dashdbshort_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://ibm.biz/db2whc_api){:new_window}.
{: shortdesc}

### Connectez des applications ou vos outils préférés depuis votre ordinateur local
{: #connect_apps}

Configurez votre environnement local afin qu'il se connecte à votre base de données d'entrepôt Db2 en procédant comme suit :
{: shortdesc}

1. Téléchargez le [package de pilote ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_driver_package.html){:new_window} à partir de la console Web de Db2 Warehouse on Cloud.
2. [Installez le package de pilote ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_driver_package_install.html){:new_window} sur l'ordinateur sur lequel vos applications ou vos outils sont exécutés.
3. [Configurez les fichiers de pilote ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/en/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_driver_package_config.html){:new_window} pour votre base de données d'entrepôt Db2.

### Utilisez Db2 Warehouse on Cloud comme source de données pour vos applications ou services {{site.data.keyword.Bluemix_notm}}
{: #data_src}

Les applications hébergées sur {{site.data.keyword.Bluemix_notm}} peuvent se connecter à votre base de données {{site.data.keyword.dashdbshort_notm}} exactement de la même manière que vos applications locales se connectent à votre base de données {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

Lorsque vos applications utilisent la plateforme {{site.data.keyword.Bluemix_notm}}, vous pouvez tirer parti de la variable d'environnement `VCAP _SERVICES` pour simplifier la spécification des détails et des données d'identification de la base de données :
1. Dans le tableau de bord {{site.data.keyword.Bluemix_notm}}, dans l'onglet **Connexions** de la page Détails du service de votre service {{site.data.keyword.dashdbshort_notm}}, cliquez sur le bouton **Créer une connexion**.
2. Sélectionnez l'application {{site.data.keyword.Bluemix_notm}} à utiliser avec votre base de données {{site.data.keyword.dashdbshort_notm}} comme source de données, puis cliquez sur le bouton **Connecter**.
3. Mettez à jour le code de votre application pour qu'il extraie les détails et les données d'identification de la base de données à partir de la variable d'environnement `VCAP_SERVICES` :

    **Exemple sans `VCAP_SERVICES`**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    $database    = "BLUDB";         # Get these database details from
    $hostname    = "<Host-name>";   # the Connection info page of the
    $port        = 50000;           # web console.
    $user        = "<User-ID >";    #
    $password    = "<Password>";    #
    $dsn         = "DATABASE=$database;" .
                   "HOSTNAME=$hostname;" .
                   "PORT=$port;" .
                   "PROTOCOL=TCPIP;" .
                   "UID=$user;" .
                   "PWD=$password;";

    $conn_string = $driver . $dsn;

    $conn        = db2_connect( $conn_string, "", "" );
    ?>
    ```

    **Exemple avec `VCAP_SERVICES`**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    $vcap        = json_decode( getenv( "VCAP_SERVICES" ), true );
    $dsn         = $vcap[ "dashDB" ][0][ "credentials" ][ "dsn" ];

    $conn_string = $driver . $dsn;
                                   
    $conn        = db2_connect( $conn_string, "", "" );
    ?>
    ```

## Exemples
{: #samples}

Les liens suivants mènent à des exemples de démonstration indiquant comment se connecter à votre base de données {{site.data.keyword.dashdbshort_notm}} à partir d'applications dans différents langages :
{: shortdesc}

   * [.NET ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting__net_applications.html){:new_window}
<!-- * [JAVA ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_java.html){:new_window} -->
   * [JDBC ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_jdbc_applications.html){:new_window}
<!-- * [Node.js ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_nodejs.html){:new_window} -->
   * [PHP ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_php.html){:new_window}
<!-- * [Python ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_python.html){:new_window} -->
   * [Exemples {{site.data.keyword.dashdbshort_notm}} sur GitHub ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/IBM-Bluemix/dashdb-nodejs-helloworld){:new_window}


