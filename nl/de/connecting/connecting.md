---

copyright:
  years: 2014, 2018
lastupdated: "2018-10-15"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Überblick zum Herstellen von Verbindungen
{: #overview}

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

- [Datenbankdetails und Verbindungsberechtigungsnachweise](credentials.html)

### Treiberpakete herunterladen und installieren
{: #dl_install}

- [Treiberpaket herunterladen](driver_pkg.html)
- [Installation unter Linux oder PowerLinux](install_linux.html)
- [Installation unter Mac OS X](install_mac.html)
- [Installation unter Windows](install_win.html)

### Umgebung konfigurieren
{: #cfg_env}

- [Umgebung konfigurieren](driver_pkg_cfg.html)
- [Unterstützung für Secure Sockets Layer (SSL)](ssl.html)

## Programmgestützte Verbindungsherstellung
{: #conx_prgrm}

Für die Erstellung von Anwendungen, die Verbindungen zu einer {{site.data.keyword.dashdbshort_notm}}-Datenbank herstellen, können die gängigen Programmiersprachen verwendet werden.
{: shortdesc}

- [JDBC](jdbc.html)
- [Microsoft Windows-ODBC oder -Befehlszeilenschnittstelle](odbc_cli.html)
- [.NET](net_apps.html)
- [ODBC-Datenquellenadministrator](odbc_data_source_admin.html)
- [PHP](php.html)
- [REST-API](rest_api.html)
<!-- - [C++]() -->
<!-- - [Java]() -->
<!-- - [Node.js]() -->
<!-- - [Perl]() -->
<!-- - [Python]() -->

## Apps und Tools integrieren
{: #conx_apps_tools}

Sie können auch externe Anwendungen und Tools mit {{site.data.keyword.dashdbshort_notm}} verbinden und diese zur weiteren Verwaltung und Analyse der Daten verwenden. Beispiele:

### Datenintegration
- Verbindung Ihrer {{site.data.keyword.Bluemix_short}}-Anwendungen, die eine Analysedatenbank benötigen.
- [DataStage](data.html#datastage)
- [Informatica](data.html#informatica)
- [Lift ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://lift.ng.bluemix.net/#docs){:new_window}
- [InfoSphere Data Replication](data.html#idr)
- [Segment ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://segment.com/docs/destinations/db2/){:new_window}
- [Data Studio](data.html#data_studio)
- [Data Server Manager](data.html#dsm)
- [CLPPLUS](data.html#clpplus)
- [Aginity Workbench für die Migration von Netezza®-Datenmodellen und -Daten in {{site.data.keyword.dashdbshort_notm}}](data.html#aginity_wb)
- [InfoSphere Data Architect für den Entwurf und die Bereitstellung des Datenbankschemas](data.html#ida)

### Datenvisualisierung/Business Intelligence
- [Cognos Analytics für Business Intelligence-Berichte zu Ihren Daten](vis_bi.html#cognos)
- [Looker ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.looker.com/setup-and-management/connecting-to-db){:new_window}
- [Tableau](vis_bi.html#tableau)
- [Microsoft Excel](vis_bi.html#excel)
- [Esri ArcGIS for Desktop für Geodatenanalyse und das Veröffentlichen von Karten mit Ihren Daten](vis_bi.html#esri_arcgis)

### Data Science
- [Watson Studio (früher IBM Data Science Experience)](data_sci.html#watson_studio)
- [SPSS Statistics](data_sci.html#spss_stats)
- [SAS](data_sci.html#sas)
- [Lokale Entwicklungsumgebung für R](data_sci.html#r_dev_env)

## Verbindung zu anderer Db2-Datenbank
{: #fed}

Die Db2-Datenvirtualisierung (auch als Föderierung bezeichnet) wird von {{site.data.keyword.dashdbshort_notm}} unterstützt. Mithilfe der Datenvirtualisierung können Sie über eine einzelne Abfrage auf alle Daten zugreifen, die sich auf mehreren verteilten Datenbanken innerhalb Ihrer Organisation befinden. Sie können auf Daten zugreifen, die in beliebigen Ihrer Db2- oder Informix-Datenquellen sowohl lokal als auch in der Cloud gespeichert sind. 

Diese Funktion wird in allen Versionen von {{site.data.keyword.dashdbshort_notm}} unterstützt, mit Ausnahme des Einstiegsplans. Der Einstiegsplan kann jedoch als Ziel genutzt werden, aus dem Daten abgerufen werden können.

- [Datenvirtualisierung (Föderierung)](../federation.html)


