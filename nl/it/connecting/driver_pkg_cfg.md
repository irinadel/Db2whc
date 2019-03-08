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

# Configurazione del tuo ambiente locale
{: #cfg_loc_env}

Per collegare gli strumenti e le applicazioni locali al tuo database {{site.data.keyword.dashdbshort_notm}}, devi configurare il tuo ambiente.  
{: shortdesc}

## Prerequisiti
{: #prereq21}

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](/docs/services/Db2whc/connecting/connecting.html#prereqs) necessari.

<!-- 1. Install the Db2 driver package for your operating system.

   - [Installing on Windows](install_win.html)
   - [Installing on Linux or PowerLinux](install_linux.html)
   - [Installing on Mac OS X](install_mac.html)
2. Decide whether or not you will be using Secure Sockets Layer (SSL) to connect to your database.
3. Collect database details and connect credentials, including the host name of your server, and your database user ID and password. -->

## Procedura
{: #proc21}

1. Aggiungi le voci al file di configurazione del driver, `db2dsdriver.cfg`, per il tuo database.

   La procedura di configurazione è diversa a seconda che desideri o meno collegarti al tuo database utilizzando SSL:

   **Con SSL**

   Per collegare le tue applicazioni e i tuoi strumenti al tuo database utilizzando SSL, immetti i seguenti comandi in una shell di comandi sui sistemi operativi Linux, al prompt dei comandi di Windows o in una finestra di comando DB2: 

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50001`

   `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

    dove:

   - `<hostname>` è il nome host del tuo server.
   - `<alias>` è un alias di tua scelta. L'alias non può essere uguale al nome del database, `BLUDB`. Se desideri avere degli spazi nell'alias, racchiudi l'alias tra doppi apici.

   **Senza SSL**

   Per collegare le tue applicazioni e i tuoi strumenti al tuo database non utilizzando SSL, immetti i seguenti comandi in una shell di comandi sui sistemi operativi Linux, al prompt dei comandi di Windows o in una finestra di comando DB2: 

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

   `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

    dove:

   - `<hostname>` è il nome host del tuo server.
   - `<alias>` è un alias di tua scelta. L'alias non può essere uguale al nome del database, `BLUDB`. Se desideri avere degli spazi nell'alias, racchiudi l'alias tra doppi apici.

2. Verifica la connessione immettendo il comando **db2cli validate** dal prompt dei comandi:

   `db2cli validate -dsn <alias> -connect -user <userid> -passwd <password>`

   dove: 
   
   - `<alias>` è un alias che hai creato con il comando **db2cli writecfg**.
   - `<userid>` è il tuo ID utente Db2.
   - `<password>` è la tua password Db2.

3. [*Facoltativo*] Per poter collegare le applicazioni e gli strumenti ODBC locali al tuo database, registra il DSN con il gestore driver ODBC:
 
   Immetti il seguente comando su una riga di comando: 

   `db2cli registerdsn -add -dsn <alias>`

   dove: 

   - `<alias>` è un alias che hai creato con il comando **db2cli writecfg**.

   Per impostazione predefinita, il DSN viene creato come un utente DSN.

