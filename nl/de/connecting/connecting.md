---

copyright:
  years: 2014, 2019
lastupdated: "2019-04-01"

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

# Überblick zum Herstellen von Verbindungen
{: #connect_ov}

Sie können eine Verbindung von Befehlszeilenschnittstellen, IBM® Anwendungen und Tools sowie von Anwendungen oder Tools eines anderen Anbieters oder von Apps, die Sie erstellen, zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank herstellen. 
{: shortdesc}

## Voraussetzungen
{: #prereqs}

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die erforderlichen Voraussetzungen erfüllt werden. 

- Datenbankdetails und Berechtigungsnachweise ermitteln und notieren

   Für Verbindungen zu Ihrer Datenbank benötigen Sie Datenbankdetails wie den Hostnamen und Berechtigungsnachweise wie Benutzer-IDs und Kennwörter. Sie können diese Verbindungsinformationen über die {{site.data.keyword.dashdbshort_notm}}-Webkonsole ermitteln.

- Unterstützung für den installierten Treiber überprüfen

   - Enthält Ihre Anwendung bzw. Ihr Tool bereits das IBM Data Server Driver-Paket von Db2 Version 11.1, kann Ihre Anwendung bzw. Ihr Tool über den betreffenden Treiber mit der {{site.data.keyword.dashdbshort_notm}}-Datenbank verbunden werden.
   - Installieren Sie das Db2-Treiberpaket andernfalls. Das Paket kann über die {{site.data.keyword.dashdbshort_notm}}-Webkonsole heruntergeladen werden.

- Umgebung konfigurieren

  - Fügen Sie Einträge zur Treiberkonfigurationsdatei `db2dsdriver.cfg` für Ihre Datenbank hinzu.
  - Secure Sockets Layer (SSL)

    Sie können Verbindungen mit SSL und Verbindungen ohne SSL herstellen. Die Verbindungsdetails wie der zu verwendende Port und die Verbindungszeichenfolge richten sich danach, ob Sie SSL-Verbindungen oder Verbindungen ohne SSL verwenden.

    Für SSL-Verbindungen wird ein CA-Zertifikat benötigt:
    - Bei Verwendung des neuesten {{site.data.keyword.dashdbshort_notm}}-Treiberpakets ist die Zertifikatsdatei im Paket enthalten und wird nach der Installation für Verbindungen eingesetzt.
    - Bei Verwendung des IBM Data Server Driver-Pakets können Sie das SSL-Zertifikat über die {{site.data.keyword.dashdbshort_notm}}-Webkonsole herunterladen.

- Verfügbarkeit der Ports überprüfen

   Befindet sich Ihr Netz hinter einer Firewall, müssen Sie sicherstellen, dass Verbindungen über den Port `50000` (für Standardprotokolle) bzw. den Port `50001` (für SSL-Verbindungen) zugelassen werden.

<!-- Before you can connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you completed downloading and installing the necessary components on the prerequisites checklist: 

- [Prerequisites checklist](prereqs.html) -->

### Verbindungsinformationen ermitteln und notieren
{: #collect_info}

- [Datenbankdetails und Verbindungsberechtigungsnachweise](/docs/services/Db2whc/connecting?topic=Db2whc-db_details_cxn_creds#db_details_cxn_creds)

### Treiberpakete herunterladen und installieren
{: #dl_install}

- [Treiberpaket herunterladen](/docs/services/Db2whc/connecting?topic=Db2whc-dr_pkg#dr_pkg)
- [Installation unter Linux oder PowerLinux](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_linux#install_dr_pkg_linux)
- [Installation unter Mac OS X](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_mac#install_dr_pkg_mac)
- [Installation unter Windows](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_windows#install_dr_pkg_windows)

### Umgebung konfigurieren
{: #cfg_env}

- [Umgebung konfigurieren](/docs/services/Db2whc/connecting?topic=Db2whc-cfg_loc_env#cfg_loc_env)
- [Unterstützung für Secure Sockets Layer (SSL)](/docs/services/Db2whc/connecting?topic=Db2whc-ssl_support#ssl_support)

## Konnektivitätsoptionen
{: #connect_opts}

{{site.data.keyword.dashdbshort_notm}} bietet abhängig von den Anforderungen Ihrer Anwendungsverbindung mehrere sichere Konnektivitätsoptionen.  
{: shortdesc}

Siehe [Konnektivitätsoptionen](/docs/services/Db2whc/connecting?topic=Db2whc-connect_options#connect_options).

## Programmgestützte Verbindungsherstellung
{: #conx_prgrm}

Für die Erstellung von Anwendungen, die Verbindungen zu einer {{site.data.keyword.dashdbshort_notm}}-Datenbank herstellen, können die gängigen Programmiersprachen verwendet werden.
{: shortdesc}

- [JDBC](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_jdbc#con_prog_jdbc)
- [Microsoft Windows-ODBC oder -Befehlszeilenschnittstelle](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_odbc_cli#con_prog_odbc_cli)
- [.NET](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_net#con_prog_net)
- [ODBC-Datenquellenadministrator](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_odbc_dsa#con_prog_odbc_dsa)
- [PHP](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_php#con_prog_php)
- [REST-API](/docs/services/Db2whc/connecting?topic=Db2whc-con_rest_api#con_rest_api)
<!-- - [C++]() -->
<!-- - [Java]() -->
<!-- - [Node.js]() -->
<!-- - [Perl]() -->
<!-- - [Python]() -->

## Apps und Tools integrieren
{: #conx_apps_tools}

Sie können auch externe Anwendungen und Tools mit {{site.data.keyword.dashdbshort_notm}} verbinden und diese zur weiteren Verwaltung und Analyse der Daten verwenden. Beispiele:

### Datenintegration
{: #di}

- Verbindung Ihrer {{site.data.keyword.Bluemix_short}}-Anwendungen, die eine Analysedatenbank benötigen.
- [DataStage](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#datastage)
- [Informatica](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#informatica)
- [Lift](https://www.lift-cli.cloud.ibm.com/#docs){:external}
- [InfoSphere Data Replication](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#idr)
- [Segment](https://segment.com/docs/destinations/db2/){:external}
- [Data Studio](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#data_studio)
- [Data Server Manager](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#dsm)
- [CLPPLUS](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#clpplus)
- [Aginity Workbench für die Migration von Netezza®-Datenmodellen und -Daten in {{site.data.keyword.dashdbshort_notm}}](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#aginity_wb)
- [InfoSphere Data Architect für den Entwurf und die Bereitstellung des Datenbankschemas](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#ida)

### Datenvisualisierung/Business Intelligence
{: #dvis_bi}

- [Cognos Analytics für Business Intelligence-Berichte zu Ihren Daten](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#cognos)
- [Looker](https://docs.looker.com/setup-and-management/connecting-to-db){:external}
- [Tableau](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#tableau)
- [Microsoft Excel](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#excel)
- [Esri ArcGIS for Desktop für Geodatenanalyse und das Veröffentlichen von Karten mit Ihren Daten](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#esri_arcgis)

### Data Science
{: #dsci}

- [Watson Studio (früher IBM Data Science Experience)](/docs/services/Db2whc/connecting?topic=Db2whc-ds#watson_studio)
- [SPSS Statistics](/docs/services/Db2whc/connecting?topic=Db2whc-ds#spss_stats)
- [SAS](/docs/services/Db2whc/connecting?topic=Db2whc-ds#sas)
- [Lokale Entwicklungsumgebung für R](/docs/services/Db2whc/connecting?topic=Db2whc-ds#r_dev_env)

## Verbindung zu anderer Db2-Datenbank
{: #fed}

Die Db2-Datenvirtualisierung (auch als Föderierung bezeichnet) wird von {{site.data.keyword.dashdbshort_notm}} unterstützt. Mithilfe der Datenvirtualisierung können Sie über eine einzelne Abfrage auf alle Daten zugreifen, die sich auf mehreren verteilten Datenbanken innerhalb Ihrer Organisation befinden. Sie können auf Daten zugreifen, die in beliebigen Ihrer Db2- oder Informix-Datenquellen sowohl lokal als auch in der Cloud gespeichert sind. 

Diese Funktion wird in allen Versionen von {{site.data.keyword.dashdbshort_notm}} unterstützt, mit Ausnahme des Einstiegsplans. Der Einstiegsplan kann jedoch als Ziel genutzt werden, aus dem Daten abgerufen werden können.

- [Datenvirtualisierung (Föderierung)](/docs/services/Db2whc?topic=Db2whc-data_virt_fed#data_virt_fed)


