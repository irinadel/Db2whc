---

copyright:
  years: 2014, 2019
lastupdated: "2019-05-21"

keywords:

subcollection: Db2whc

---

<!-- Attribute definitions --> 
{:javascript: #javascript .ph data-hd-programlang='javascript'}
{:java: #java .ph data-hd-programlang='java'}
{:ruby: #ruby .ph data-hd-programlang='ruby'}
{:php: #php .ph data-hd-programlang='php'}
{:python: #python .ph data-hd-programlang='python'}
{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}

# Lernprogramm 'Einführung'
{: #getting-started}

Beim verwalteten {{site.data.keyword.dashdblong}}-Service handelt es sich um eine SQL-Datenbank, die für Sie in der Cloud bereitgestellt wird. Sie können Db2 Warehouse wie jede andere Datenbanksoftware verwenden, der Aufwand und die Kosten für die Hardwareeinrichtung sowie die Softwareinstallation und -verwaltung fallen jedoch weg. 
{: shortdesc}

<!-- New tutorial submitted by Olaf Depper of DTE on 5-May-2019. Working on edits of Word doc. -->
<!--To get started on accessing and working with {{site.data.keyword.dashdbshort_notm}}, go through the [Getting started tutorial](https://cloudcontent.mybluemix.net/cloud/garage/dte/tutorial/test-db2-warehouse-cloud-post-sales){:external}. -->

## Kostenfreier Test
{: #freetrial}

Sie können den Einstiegsplan für {{site.data.keyword.dashdbshort_notm}} mit bis zu 1 GB Speicher kostenfrei testen. [Kostenfreier Test](https://cloud.ibm.com/catalog/services/db2-warehouse){:external}

## Schnittstellen
{: #interfaces}

Für die Arbeit mit der Warehousedatenbank stehen Ihnen die folgenden Möglichkeiten zur Verfügung:
{: shortdesc}

   * Webkonsole
   * REST-API
   * Herstellen einer Verbindung für Anwendungen oder bevorzugte Tools vom lokalen Computer
   * Verwenden von {{site.data.keyword.dashdbshort_notm}} als Datenquelle für {{site.data.keyword.Bluemix_notm}}-Apps oder -Services

### Webkonsole
{: #web_console}

Die Webkonsole bietet eine grafische Schnittstelle für alle Funktionen, die Sie für die Verwendung der Datenbank benötigen. Hierzu gehören z. B. Ladefunktionen, ein SQL-Editor, Treiberdownloads usw.
{: shortdesc}

![Ansicht der Dashboardseite mit der Webkonsole](images/uc.png "Webkonsole wird auf der Dashboardseite geöffnet")

<!-- Click the link to take a tour of the {{site.data.keyword.dashdbshort_notm}} for Analytics web console: [General tour](http://ibm.biz/dashdb-general-quick-tour){:external}. -->

Für den Zugriff auf die Webkonsole stehen Ihnen die folgenden Möglichkeiten zur Verfügung:
   * Über das {{site.data.keyword.Bluemix_notm}}-Dashboard - Sie können die Webkonsole über die Servicedetailseite für Ihren {{site.data.keyword.dashdbshort_notm}}-Service öffnen.
   * Direkt über die URL - Sie können die URL der Webkonsole für Ihren {{site.data.keyword.dashdbshort_notm}}-Service mit einem Lesezeichen markieren.

### REST-API
{: #api}

Mit {{site.data.keyword.dashdbshort_notm}}-Serviceplänen können Sie Tasks im Zusammenhang mit dem Verwalten von Dateien und dem Laden von Daten ausführen, wobei Sie die [{{site.data.keyword.dashdbshort_notm}}-REST-API](http://ibm.biz/db2whc_api){:external} verwenden.
{: shortdesc}

### Herstellen einer Verbindung für Anwendungen oder bevorzugte Tools vom lokalen Computer
{: #connect_apps}

Führen Sie die folgenden Schritte aus, um die lokale Umgebung für die Verbindung zur {{site.data.keyword.dashdbshort_notm}}-Datenbank zu konfigurieren:
{: shortdesc}

1. Laden Sie das [Treiberpaket](/docs/services/Db2whc/connecting?topic=Db2whc-dr_pkg#dr_pkg) über die {{site.data.keyword.dashdbshort_notm}}-Webkonsole herunter.
2. Installieren Sie das Treiberpaket auf dem Computer, auf dem Ihre Apps bzw. Tools ausgeführt werden:
   - [Installation unter Linux oder PowerLinux](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_linux#install_dr_pkg_linux)
   - [Installation unter Mac OS X](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_mac#install_dr_pkg_mac)
   - [Installation unter Windows](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_windows#install_dr_pkg_windows)
3. [Konfigurieren Sie die Treiberdateien](/docs/services/Db2whc/connecting?topic=Db2whc-cfg_loc_env#cfg_loc_env) für Ihre {{site.data.keyword.dashdbshort_notm}}-Datenbank.

### Verwenden von Db2 Warehouse on Cloud als Datenquelle für {{site.data.keyword.Bluemix_notm}}-Apps oder -Services
{: #data_src}

Für Apps, die per Hosting in {{site.data.keyword.Bluemix_notm}} bereitgestellt werden, können Verbindungen zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank auf dieselbe Weise hergestellt werden wie bei Verbindungen für lokalen Anwendungen zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank.
{: shortdesc}

Wenn Ihre Apps die {{site.data.keyword.Bluemix_notm}}-Plattform verwenden, können Sie die Umgebungsvariable `VCAP _SERVICES` nutzen, um das Angeben von Datenbankdetails und -berechtigungsnachweisen zu vereinfachen:
1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf der Registerkarte **Verbindungen** der Servicedetailseite für Ihren {{site.data.keyword.dashdbshort_notm}}-Service auf die Schaltfläche **Verbindung erstellen**.
2. Wählen Sie die {{site.data.keyword.cloud_notm}}-App aus, die mit der {{site.data.keyword.dashdbshort_notm}}-Datenbank als Datenquelle verwendet werden soll, und klicken Sie dann auf die Schaltfläche **Verbinden**.
3. Aktualisieren Sie den Anwendungscode, um Datenbankdetails- und -berechtigungsnachweise aus der Umgebungsvariablen `VCAP_SERVICES` abzurufen:

    **Beispiel ohne `VCAP_SERVICES`**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    $database    = "BLUDB";         # Diese Datenbankdetails von
    $hostname    = "<Host-name>";   # der Seite mit Verbindungsinformationen
    $port        = 50000;           # der Webkonsole abrufen.
    $user        = "<Benutzer-ID >";    #
    $password    = "<Kennwort>";    #
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

    **Beispiel mit `VCAP_SERVICES`**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    $vcap        = json_decode( getenv( "VCAP_SERVICES" ), true );
    $dsn         = $vcap[ "dashDB" ][0][ "credentials" ][ "dsn" ];

    $conn_string = $driver . $dsn;
                                   
    $conn        = db2_connect( $conn_string, "", "" );
    ?>
    ```

## Beispiele
{: #samples}

Über die folgenden Links können Sie Beispiele aufrufen, die veranschaulichen, wie Sie von Anwendungen in verschiedenen Sprachen aus eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank programmgestützt herstellen:
{: shortdesc}

- [JDBC](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_jdbc#con_prog_jdbc)
- [Microsoft Windows-ODBC oder -Befehlszeilenschnittstelle](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_odbc_cli#con_prog_odbc_cli)
- [.NET](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_net#con_prog_net)
- [ODBC-Datenquellenadministrator](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_odbc_dsa#con_prog_odbc_dsa)
- [PHP](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_php#con_prog_php)
- [REST-API](/docs/services/Db2whc/connecting?topic=Db2whc-con_rest_api#con_rest_api)

## Video mit Einführung zu Db2 Warehouse on Cloud
{: #intro_vid}

Sehen Sie sich das folgende Video an, um eine Einführung in {{site.data.keyword.dashdbshort_notm}} zu erhalten.

<iframe class="embed-responsive-item" id="youtubeplayer1" title="Introduction to {{site.data.keyword.dashdbshort_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/0NO9OTFWzKs?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

## Video mit Einführung zum Flex Performance-Plan
{: #intro_vid_flex}

Das folgende Video enthält eine Einführung in den Flex Performance-Plan von {{site.data.keyword.dashdbshort_notm}}.

<iframe class="embed-responsive-item" id="youtubeplayer2" title="Creating a connection from Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

## Video zum Herstellen einer Verbindung mit einer Analyseanwendung
{: #cognos_vid}

In dem folgenden Video erfahren Sie, wie Sie eine Verbindung von Cognos Analytics aus erstellen können.

<iframe class="embed-responsive-item" id="youtubeplayer3" title="Creating a connection from Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TRUEPVHGi0s?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

