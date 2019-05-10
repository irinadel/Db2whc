---

copyright:
  years: 2014, 2019
lastupdated: "2019-03-15"

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

# Pläne und Konfigurationen
{: #plans_cfgs}

Sie können einen {{site.data.keyword.dashdbshort_notm}}-Plan auswählen, der für die jeweiligen Aufgaben konfiguriert und optimiert ist:
{: shortdesc}

   * Einstiegsplan zum Testen der Funktionen. Dies ist eine kostenlose Testversion mit bis zu 1 GB Speicher. Weitere Informationen finden Sie in [Einschränkungen des Einstiegsplans](#ep_restrictions).
   * Flex-Pläne für unabhängige Skalierung von Speicher- und Prozessorressourcen
   * SMP-Pläne in verschiedenen Größen für die Produktion: Small, Medium und Large bestehen aus einem einzigen Knoten und einer einzigen Instanz
   * MPP-Clusterkonfigurationen mit mehreren Knoten für eine parallele Verarbeitung und hohe Leistung
   * Für die Hochverfügbarkeit konfigurierte Pläne
   * Oracle-Kompatibilität

Alle verfügbaren {{site.data.keyword.dashdbshort_notm}}-Pläne können im [{{site.data.keyword.Bluemix}}-Katalog](https://cloud.ibm.com/catalog/services/db2-warehouse){:new_window} angezeigt werden.
<!--   * Plans configured for data warehouse and online analytical processing (OLAP) workloads: [{{site.data.keyword.dashdbshort_notm}}](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window} -->
<!--   * Plans configured for high-speed, transactional processing (OLTP): [{{site.data.keyword.dashdbshort_notm}} for Transactions](https://console.ng.bluemix.net/catalog/services/dashdb-for-transactions-sql-database){:new_window} -->

Das folgende Video enthält eine Einführung in den Flex Performance-Plan von {{site.data.keyword.dashdbshort_notm}}.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Creating a connection from Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

Sie können anfordern, dass Ihr {{site.data.keyword.dashdbshort_notm}}-Service in einer Umgebung mit Netzisolierung in {{site.data.keyword.Bluemix}} bereitgestellt wird. Wenden Sie sich an den [{{site.data.keyword.IBM_notm}} Vertrieb ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window}.

Wenn die benötigte Konfiguration im Katalog nicht angezeigt wird, wenden Sie sich an [{{site.data.keyword.IBM_notm}} Sales ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window}, um sich über weitere Optionen zu informieren.

## Verfügbarkeit von Plänen in Rechenzentren
{: #availability}

Die folgende Tabelle enthält nach Rechenzentren in verschiedenen Regionen geordnete Informationen zur Verfügbarkeit der verschiedenen {{site.data.keyword.dashdbshort_notm}}-Pläne:

| {{site.data.keyword.dashdbshort_notm}}-Pläne | Asien/Pazifik | Europa    | Nord-/Mittelamerika     | Südamerika |
|------------------------------|--------------|-----------|---------------------------|---------------|
| Flex                         | Tokio        | Frankfurt | Washington D.C. (Vereinigte Staaten (Osten)) | *NV           |
|                              |              |           | Dallas (Vereinigte Staaten (Süden))         |               |  
|      |||||
| SMP                          | Hongkong    | Amsterdam | Washington D.C. (Vereinigte Staaten (Osten)) | Sao Paulo     |
|                              | Seoul        | Frankfurt | Dallas (Vereinigte Staaten (Süden))         |               | 
|                              | Singapur    | London    | Montreal                  |               | 
|                              | Sydney       | Mailand     | Querétaro                 |               | 
|                              | Tokio        | Oslo      | Toronto                   |               | 
|                              |              | Paris     |                           |               |
|      |||||
| MPP                          | Hongkong    | Amsterdam | Washington D.C. (Vereinigte Staaten (Osten)) | Sao Paulo     |
|                              | Seoul        | Frankfurt | Dallas (Vereinigte Staaten (Süden))         |               | 
|                              | Singapur    | London    | Montreal                  |               | 
|                              | Sydney       | Mailand     | Querétaro                 |               | 
|                              | Tokio        | Oslo      | Toronto                   |               | 
|                              |              | Paris     |                           |               |
{: caption="Tabelle 1. Rechenzentren, in denen Db2 Warehouse on Cloud-Servicepläne unterstützt werden" caption-side="top"}

*NV = derzeit nicht verfügbar

## Einschränkungen des Einstiegsplans
{: #ep_restrictions}

Für geschäftskritische oder leistungskritische Workloads wird die Verwendung eines auf das Unternehmen abgestimmten Serviceplans anstelle eines Einstiegsserviceplans unbedingt empfohlen. 
{: important}

In der folgenden Tabelle sind die Einschränkungen des {{site.data.keyword.dashdbshort_notm}}-Einstiegsplans aufgeführt:

| Kategorie | Element | Einschränkung | 
|----------|------|-------------|
| Ressourcen | Speicher | 20 GB Speicher pro Benutzer. Der Plan ist nur bei einer Nutzung von weniger als 1 GB Speicher kostenfrei. |
|  | Verbindungen | 50 Verbindungen pro Benutzer. Dieser Grenzwert kann dynamisch angepasst werden, um die Systemintegrität der Instanz aufrecht zu erhalten. |
|  | Leistung | Die Leistung kann aufgrund von Workloads, die von anderen Benutzern im Multi-Tenant-System ausgeführt werden, fluktuieren. |
|  |  |
| Features & Funktionen | Föderierung | Nicht unterstützt |
|  | Oracle-Kompatibilität | Nicht unterstützt |
|  | Benutzerdefinierte Erweiterungen (UDFs) | Nicht unterstützt |
|  | Benutzerverwaltung | Benutzer erhält keine Administratorberechtigung |
|  | Zugriffssteuerung für Zeilen und Spalten (RCAC) | Nicht unterstützt |
|  | IBM InfoSphere Data Replication zur Verwendung beim Laden von Daten | Nicht unterstützt |
|  |  |
| Netzumgebung | IBM Cloud Integrated Analytics | Nicht unterstützt |
|  | IBM Cloud Dedicated | Nicht unterstützt |
|  |  |
| Einhaltung von Sicherheitsvorgaben | Health Information Portability and Accountability Act von 1996 (HIPAA) | Nicht unterstützt. Siehe Servicebeschreibung. |
|  | Datenschutz-Grundverordnung der EU (DSGVO) | Es gelten keine spezifischen Einschränkungen. |
|  |  |
| Kontoverwaltung | Reaktivierung | Keine Reaktivierungsanforderung |
{: caption="Tabelle 1. Einschränkungen des {{site.data.keyword.dashdbshort_notm}}-Einstiegsplans" caption-side="top"}
