---

copyright:
  years: 2014, 2018
lastupdated: "2017-07-17"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Informationen zu Db2 Warehouse on Cloud
{: #overview}

In den Db2 Warehouse on Cloud-Serviceplänen können Sie das Data-Warehouse zum Speichern relationaler Daten, einschließlich spezieller Datentypen, verwenden. Analysieren Sie eigene oder von anderen Cloud-Services geladene Daten unter Verwendung der integrierten Analysefunktionen oder durch Verbinden Ihrer eigenen Apps. Sie können die leistungsfähige, speicherinterne Datenbanktechnologie mit Spaltentabellen für analytische Workloads nutzen. Die Db2 Warehouse on Cloud-Webkonsole verarbeitet allgemeine Datenverwaltungstasks wie das Laden von Daten und Analysetasks wie das Ausführen von Abfragen und R-Scripts.
{: shortdesc}

Sie können auch externe Anwendungen und Tools mit Db2 Warehouse on Cloud verbinden und diese zur weiteren Verwaltung und Analyse der Daten verwenden. Beispiele:
   * Verbindung mit {{site.data.keyword.IBM_notm}} InfoSphere® Data Architect für den Entwurf und die Bereitstellung des Datenbankschemas.
<!--   * Connect Esri ArcGIS to perform geospatial analytics and map publishing with your data. -->
   * Verbindung mit einem {{site.data.keyword.IBM_notm}} Cognos®-Server zur Ausführung von Cognos-Berichten für Ihre Daten.
   * Verbindung mit SQL-basierten Tools wie Tableau, Microstrategy oder Microsoft Excel für die Datenbearbeitung oder -analyse.
   * Verbindung Ihrer {{site.data.keyword.Bluemix_short}}-Anwendungen, die eine Analysedatenbank benötigen.
   * Verbindung mit Aginity Workbench für die Migration von Netezza®-Datenmodellen und -Daten in Db2 Warehouse on Cloud.

## Verwalteter Db2 Warehouse on Cloud-Service
{: #managed_service}

Der vollständig verwaltete Service von Db2 Warehouse on Cloud verarbeitet alle Software-Upgrades, Betriebssystemaktualisierungen und Hardwarewartungstasks. Der Service umfasst die 24x7-Statusüberwachung der Datenbank und der Infrastruktur. Beim Auftreten eines Hardware- oder Softwarefehlers wird der Service automatisch neu gestartet.
{: shortdesc}

Weitere Informationen zu den Aspekten eines verwalteten Service von Db2 Warehouse on Cloud finden Sie in [Verwalteter Db2 Warehouse on Cloud-Service![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/managed_service.html "Symbol für externen Link").

## Pläne und Konfigurationen
{: #plans_cfgs}

Sie können einen Db2 Warehouse on Cloud-Plan auswählen, der für die jeweiligen Aufgaben konfiguriert und optimiert ist:
{: shortdesc}

   * Einstiegsplan zum Testen der Funktionen
   * Kleine, mittlere und große Pläne für die Produktion
   * MPP-Konfigurationen für die parallele Verarbeitung
   * Für die Hochverfügbarkeit oder für die Oracle-Kompatibilität konfigurierte Pläne
   * Und mehr...

Sie können die verfügbaren Pläne im {{site.data.keyword.Bluemix}}-Katalog anzeigen:
   * Für Data-Warehouse- und Analyse-Workloads (OLAP) konfigurierte Pläne: [Db2 Warehouse on Cloud](https://console.ng.bluemix.net/catalog/services/dashdb-for-analytics){:new_window}
<!--   * Plans configured for high-speed, transactional processing (OLTP): [{{site.data.keyword.dashdbshort_notm}} for Transactions](https://console.ng.bluemix.net/catalog/services/dashdb-for-transactions-sql-database){:new_window} -->

Wenn die benötigte Konfiguration im Katalog nicht angezeigt wird, [wenden Sie sich an {{site.data.keyword.IBM_notm}} Sales ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw "Symbol für externen Link"){:new_window}, um sich über weitere Optionen zu informieren.

## Db2 Warehouse on Cloud bereitstellen
{: #whse_provision}

Das {{site.data.keyword.IBM_notm}} Db2 Warehouse on Cloud-Data-Warehouse kann in {{site.data.keyword.BluSoftlayer_full}} und für AWS bereitgestellt werden.
{: shortdesc}

Wenn das Data-Warehouse für AWS bereitgestellt werden soll, wählen Sie den Plan **Db2 Warehouse on Cloud MPP Small for AWS** aus. 

<!-- If you want to have the data warehouse provisioned for AWS, select the **{{site.data.keyword.IBM_notm}} {{site.data.keyword.dashdbshort_notm}} for Analytics MPP Small for AWS** plan. -->

<!-- ##dashDB for Transactions
{: #dashDB_tr}

In the {{site.data.keyword.dashdbshort_notm}} for Transactions plans, use the {{site.data.keyword.dashdbshort_notm}} relational database for online transaction processing. You can connect new or existing applications, and you can begin processing transactions and storing your data. With DB2® and Oracle compatibility, you can connect small or large applications and benefit from a managed enterprise-class database system. You can leverage the {{site.data.keyword.dashdbshort_notm}} for Transactions web console to manage users, load data, and get connection information.
{: shortdesc} -->

<!-- ##dashDB web console overview
{: #console_overview}

You can manage your {{site.data.keyword.dashdbshort_notm}} database, analyze your data, and monitor sensitive data with the {{site.data.keyword.dashdbshort_notm}} web console accessible from {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Open the web console by clicking the service tile on your application overview page, and then click **Open**.

Single sign-on authentication connects you directly to the web console. You can access connection information from the web console, and the **Downloads** page includes links to client drivers for accessing {{site.data.keyword.dashdbshort_notm}} from remote applications. You can also access sample data and reports.

###Sensitive data reporting

The {{site.data.keyword.dashdbshort_notm}} web console includes a sensitive data reporting feature that detects and monitors sensitive objects in the {{site.data.keyword.dashdbshort_notm}} data warehouse, such as credit card numbers and US Social Security numbers.

To run and view reports that identify columns that contain sensitive data and provide information about connections and activities that access the sensitive data, select **Monitor &gt; Sensitive Data** in the web console. -->


<!-- ##IBM Analytics Services
{: #analytics_services}

For more information about {{site.data.keyword.IBM_notm}} analytics services and finding your local services representative, see: [{{site.data.keyword.IBM_notm}} Analytics Services ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/software/data/services/).
{: shortdesc} -->














