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

# Verbindung über ODBC-Datenquellenadministrator herstellen
{: #con_prog_odbc_dsa}

Definieren Sie eine Verbindung zwischen einer ODBC- oder CLI-Anwendung und einer {{site.data.keyword.dashdbshort_notm}}-Datenbank über das Tool 'ODBC-Datenquellenadministrator'.
{: shortdesc}

## Voraussetzungen
{: #prereq91}

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) erfüllt werden.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Vorgehensweise
{: #proc91}

1. Installieren Sie das [Db2-Treiberpaket](/docs/services/Db2whc?topic=Db2whc-dr_pkg#dr_pkg).

2. Öffnen Sie ODBC-Datenquellenadministrator und erstellen Sie einen Benutzer-DSN oder einen System-DSN für das Db2-Treiberpaket.
    
3. Klicken Sie auf **Erweitert**, um die erweiterten Einstellungen aufzurufen. Geben Sie die folgenden CLI-Parameter mit den zugehörigen Werten für den {{site.data.keyword.dashdbshort_notm}}-Server ein: **Hostname**, **Port** und **Database**.
    
4. Geben Sie für eine SSL-Verbindung den CLI-Parameter **Security** mit dem Wert `SSL` ein.
    
5. Klicken Sie auf **Anwenden**.
    
6. Kehren Sie zum Testen der Verbindung zur Hauptseite von ODBC-Datenquellenadministrator zurück. Klicken Sie für den von Ihnen erstellten DSN auf **Konfigurieren**. Geben Sie die Benutzer-ID und das zugehörige Kennwort für den Server ein und klicken Sie auf **Verbinden**.

