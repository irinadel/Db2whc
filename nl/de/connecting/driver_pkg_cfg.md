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

# Lokale Umgebung konfigurieren
{: #cfg_loc_env}

Wenn lokale Anwendungen und Tools mit der {{site.data.keyword.dashdbshort_notm}}-Datenbank verbunden werden sollen, müssen Sie Ihre Umgebung entsprechend konfigurieren.  
{: shortdesc}

## Voraussetzungen
{: #prereq21}

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) erfüllt werden.

<!-- 1. Install the Db2 driver package for your operating system.

   - [Installing on Windows](install_win.html)
   - [Installing on Linux or PowerLinux](install_linux.html)
   - [Installing on Mac OS X](install_mac.html)
2. Decide whether or not you will be using Secure Sockets Layer (SSL) to connect to your database.
3. Collect database details and connect credentials, including the host name of your server, and your database user ID and password. -->

## Vorgehensweise
{: #proc21}

1. Fügen Sie Einträge zur Treiberkonfigurationsdatei `db2dsdriver.cfg` für Ihre Datenbank hinzu.

   Die Konfigurationsschritte variieren, je nachdem, ob eine SSL-Verbindung oder eine Verbindung ohne SSL-Verschlüsselung zu der Datenbank eingerichtet werden soll:

   **Mit SSL**

   Geben Sie die folgenden Befehl in einer Befehlsshell unter einem Linux-Betriebssystem, in einer Windows-Eingabeaufforderung oder in einem Db2-Befehlsfenster ein, wenn SSL-Verbindungen zwischen Ihren Anwendungen und Tools und der Datenbank eingerichtet werden sollen: 

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50001`

   `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

    Dabei gilt Folgendes:

   - `<hostname>` ist der Hostname des Servers.
   - `<alias>` ist ein von Ihnen gewählter Aliasname. Der Aliasname darf nicht mit dem Datenbanknamen `BLUDB` übereinstimmen. Enthält der gewählte Aliasname Leerzeichen, setzen Sie den Aliasnamen in Anführungszeichen.

   **Ohne SSL**

   Geben Sie die folgenden Befehl in einer Befehlsshell unter einem Linux-Betriebssystem, in einer Windows-Eingabeaufforderung oder in einem Db2-Befehlsfenster ein, wenn Verbindungen ohne SSL-Verschlüsselung zwischen Ihren Anwendungen und Tools und der Datenbank eingerichtet werden sollen: 

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

   `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

    Dabei gilt Folgendes:

   - `<hostname>` ist der Hostname des Servers.
   - `<alias>` ist ein von Ihnen gewählter Aliasname. Der Aliasname darf nicht mit dem Datenbanknamen `BLUDB` übereinstimmen. Enthält der gewählte Aliasname Leerzeichen, setzen Sie den Aliasnamen in Anführungszeichen.

2. Testen Sie die Verbindung, indem Sie den Befehl **db2cli validate** in der Eingabeaufforderung absetzen:

   `db2cli validate -dsn <alias> -connect -user <userid> -passwd <password>`

   Dabei gilt Folgendes: 
   
   - `<alias>` ist ein Aliasname, den Sie mit dem Befehl **db2cli writecfg** erstellt haben.
   - `<userid>` ist Ihre Db2-Benutzer-ID.
   - `<password>` ist Ihr Db2-Kennwort.

3. [*Optional*] Sollen lokale ODBC-Anwendungen und -Tools mit Ihrer Datenbank verbunden werden können, registrieren Sie den DSN beim ODBC-Treibermanager.
 
   Führen Sie den folgenden Befehl in einer Befehlszeile aus: 

   `db2cli registerdsn -add -dsn <alias>`

   Dabei gilt Folgendes: 

   - `<alias>` ist ein Aliasname, den Sie mit dem Befehl **db2cli writecfg** erstellt haben.

   Standardmäßig wird der DSN als Benutzer-DSN erstellt.

