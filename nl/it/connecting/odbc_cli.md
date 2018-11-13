---

copyright:
  years: 2014, 2018
lastupdated: "2018-09-25"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Connessione programmatica con ODBC o la CLI

Definisci una connessione tra un Microsoft Windows ODBC o l'applicazione CLI e un database {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

## Prerequisiti

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](connecting.html#prereqs) necessari.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedura

1. In una shell di comandi sui sistemi operativi Linux, sul prompt dei comandi di Windows o nella finestra di comando Db2 sui sistemi operativi Windows, immetti i seguenti comandi:

   **Nota**: questi comandi creano nuove voci nel file di configurazione del driver (`db2dsdriver.cfg`) sul tuo computer e impostano gli attributi di connessione. Hai bisogno di eseguire questo passo solo una volta.
   
   - Per una connessione con SSL:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

   - Per una connessione senza SSL:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

   dove:

   `<hostname>` è il nome host del server

   `<alias>` è un alias DSN di tua scelta
    
2. [*Optional*]: To verifica la connessione al database, esegui questo comando dal prompt dei comandi:

   `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

   dove:

   `<alias>` è l'alias DNS che hai creato con il comando **db2cli writecfg**

   `<user_id>` è dalle credenziali di connessione che hai raccolto in precedenza

   `<password>` è dalle credenziali di connessione che hai raccolto in precedenza

3. [*Optional*]: To per registrare il nome dell'origine dati (DSN) con Microsoft ODBC Driver Manger e per utilizzare le applicazioni Microsoft ODBC, immetti il seguente comando.  Per impostazione predefinita, il DSN viene creato come un utente DSN.

   `db2cli registerdsn -add -dsn <alias>`

   dove:
        
   `<alias>` è l'alias DNS che hai creato con il comando **db2cli writecfg**



