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

# Programmgestützte Verbindungsherstellung - ODBC und Befehlszeilenschnittstelle
{: #con_prog_odbc_cli}

Definieren Sie eine Verbindung zwischen einer ODBC- oder CLI-Anwendung von Microsoft Windows und einer {{site.data.keyword.dashdbshort_notm}}-Datenbank.
{: shortdesc}

## Voraussetzungen
{: #prereq81}

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](/docs/services/Db2whc/connecting/connecting.html#prereqs) erfüllt werden.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Vorgehensweise
{: #proc81}

1. Geben Sie in einer Befehlsshell in einem Linux-Betriebssystem in der Windows-Eingabeaufforderung bzw. unter einem Windows-Betriebssystem im Db2-Befehlsfenster die folgenden Befehle ein:

   **Hinweis**: Mit diesen Befehlen werden neue Einträge in der Treiberkonfigurationsdatei `db2dsdriver.cfg` auf Ihrem Computer erstellt und die Verbindungsattribute festgelegt. Sie müssen diesen Schritt lediglich ein einziges Mal ausführen.
   
   - Für SSL-Verbindungen:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

   - Für Verbindungen ohne SSL:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

   Dabei gilt Folgendes:

   `<hostname>` ist der Hostname des Servers

   `<alias>` ist ein von Ihnen gewählter DSN-Alias
    
2. [*Optional*]: To Zum Testen der Verbindung zur Datenbank geben Sie den folgenden Befehl in der Eingabeaufforderung ein:

   `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

   Dabei gilt Folgendes:

   `<alias>` ist der DSN-Alias, den Sie mit dem Befehl **db2cli writecfg** erstellt haben.

   `<user_id>` stammt aus den Berechtigungsnachweisen für die Verbindung, die Sie zuvor ermittelt haben.

   `<password>` stammt aus den Berechtigungsnachweisen für die Verbindung, die Sie zuvor ermittelt haben.

3. [*Optional*]: To Zum Registrieren des Datenquellennamens bei Microsoft ODBC Driver Manager und zum Arbeiten mit Microsoft-ODBC-Anwendungen den folgenden Befehl ausführen. Standardmäßig wird der DSN als Benutzer-DSN erstellt.

   `db2cli registerdsn -add -dsn <alias>`

   Dabei gilt Folgendes:
        
   `<alias>` ist der DSN-Alias, den Sie mit dem Befehl **db2cli writecfg** erstellt haben.



