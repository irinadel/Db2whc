---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# Datenbankdetails und Verbindungsberechtigungsnachweise
{: #db_details_cxn_creds}

Beim Konfigurieren Ihrer lokalen Entwicklungsumgebung und Verbinden Ihrer Anwendungen und Tools mit der {{site.data.keyword.dashdbshort_notm}}-Datenbank wird vorausgesetzt, dass Ihnen die Datenbankdetails und Verbindungsberechtigungsnachweise bekannt sind.
{: shortdesc}

## Datenbankdetails
{: #db_details}

Für Verbindungen von Anwendungen und Tools zu Ihrer Datenbank werden wichtige Datenbankdetails benötigt:

- *Hostname* - Der Hostname des Servers.
- *Portnummer* - Vom Datenbankmanager für die TCP/IP-Kommunikation verwendete Portnummer. (Dabei ist zu beachten, dass Ihr Service mit einer bestimmten Portnummer für SSL-Verbindungen und einer anderen Portnummer für Verbindungen ohne SSL bereitgestellt wird.)

   Die IP-Adresse Ihres Servers können Sie, falls erforderlich, mit dem Pingbefehl oder dem Befehl 'nslookup' unter Angabe des Hostnamens abrufen.
- *Datenbankname* - Der Db2-Datenbankname (im Allgemeinen BLUDB).

## Verbindungsberechtigungsnachweise
{: #cxn_creds}

Es gibt drei Typen von Berechtigungsnachweisen:

- *IBMid* - Bei Verwendung von {{site.data.keyword.Bluemix_notm}} ist dies die ID, die für die Anmeldung bei {{site.data.keyword.Bluemix_notm}} vorgesehen ist. Es ist nicht die ID, die Sie verwenden, um Anwendungen und Tools mit der Db2 Warehouse on Cloud-Datenbank zu verbinden.
- *Berechtigungsnachweise für die Db2-Datenbank* - Ihr Service wird mit einer Datenbankbenutzer-ID mit dem zugehörigen Kennwort bereitgestellt, die Sie verwenden können, um Anwendungen und Tools mit Ihrer Datenbank zu verbinden.
- *Von einem Administrator erstellte Benutzer* - Einige {{site.data.keyword.dashdbshort_notm}}-Pläne ermöglichen Benutzern mit Verwaltungsaufgaben das Erstellen neuer Benutzer. Diese von einem Administrator erstellten Benutzer-IDs mit den zugehörigen Kennwörtern können dazu verwendet werden, sich direkt über die Webkonsolen-URL anzumelden und von Anwendungen und Tools aus eine Verbindung zur Db2-Datenbank herzustellen.

## Datenbankdetails und Verbindungsberechtigungsnachweise ermitteln
{: #location}

Sie können die entsprechenden Informationen folgendermaßen ermitteln:

- *Über den Administrator* - Wenn Sie nicht der Eigner oder Administrator Ihrer Db2-Instanz sind, können Sie die Datenbankdetails und Verbindungsberechtigungsnachweise bei Ihrem Administrator erfragen.
- *In der Db2-Webkonsole* - Datenbankdetails und Berechtigungsnachweise werden in der Webkonsole zur Verfügung gestellt.
- Wenn Sie {{site.data.keyword.Bluemix_notm}} verwenden: 
   
   - *Im {{site.data.keyword.Bluemix_notm}}-Dashboard* - Wenn Sie Ihren Service im {{site.data.keyword.Bluemix_notm}}-Dashboard anzeigen, werden die Datenbankdetails sowie die Datenbankbenutzer-ID und das zugehörige Kennwort im Bereich für die Serviceberechtigungsnachweise angezeigt.
   - *`Über VCAP_SERVICES`* - Bei `VCAP_SERVICES` handelt es sich um eine Umgebungsvariable in {{site.data.keyword.Bluemix_notm}}, die Datenbankdetails und Berechtigungsnachweise im JSON-Format enthält. Wenn Sie die Serviceberechtigungsnachweis für Ihren Service im {{site.data.keyword.Bluemix_notm}}-Dashboard anzeigen, handelt es sich bei den angezeigten Angaben um den Inhalt von `VCAP_SERVICES`. Wenn Sie andere {{site.data.keyword.Bluemix_notm}}-Services oder Apps an Ihren Service binden, können diese Services und Apps programmgestützt über einen Lesezugriff auf `VCAP_SERVICES` auf Datenbankdetails und Berechtigungsnachweise zugreifen.
