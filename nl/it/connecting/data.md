---

copyright:
  years: 2014, 2019
lastupdated: "2018-11-08"

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

# Integrazione dei dati
{: #data_int}

Puoi anche
connettere applicazioni e strumenti esterni a {{site.data.keyword.dashdbshort_notm}} e
utilizzarli per un'ulteriore gestione o analisi dei dati. 
{: shortdesc}

## DataStage
{: #datastage}

Queste istruzioni illustrano come definire una connessione senza SSL tra IBM® InfoSphere® DataStage® <!--version 9.1 and later --> e un database {{site.data.keyword.dashdbshort_notm}} catalogando il database e definendo un oggetto di connessione, o come creare una connessione con SSL utilizzando un certificato digitale emesso da terze parti.
{: shortdesc}

### Prerequisiti
{: #prereq1}

Se non disponi già di un client del server di dati installato, scarica e installa l'IBM Data Server Client <!--Version 10.5 -->appropriato per il tuo sistema operativo della macchina client: [IBM Data Server Client ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/marketing/iwm/iwm/web/preLogin.do?source=swg-idsc97){:new_window}.

Per effettuare le connessioni con il protocollo SSL, scarica e installa il GSKit V8 a 32 bit. Fai clic sulla scheda del sistema operativo appropriata per il sistema operativo della tua macchina client: [GSKit V8 - Install, Uninstall and Upgrade instructions ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/support/docview.wss?uid=swg21631462){:new_window}. Per i seguenti sistemi operativi, assicurarti di aggiungere il percorso di directory di installazione di GSKit alla variabile di ambiente del percorso specifico del sistema operativo:

- AIX®: **LIBPATH**
   - `/usr/opt/ibm/gsk8/lib`
- Linux: **LD_LIBRARY_PATH**
    - `/usr/local/ibm/gsk8/lib`
- UNIX: **LD_LIBRARY_PATH**
    - `/opt/ibm/gsk8/lib`
- Windows: **PATH**
    - `<installation_directory>\gsk8\bin`
    - `<installation_directory>\gsk8\lib`

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](/docs/services/Db2whc/connecting/connecting.html#prereqs) necessari.

### Procedura
{: #proc1}

- Per creare una connessione con SSL, completa la seguente procedura:

  1. Apri una riga di comando o un terminale e crea una nuova directory nel sistema DataStage per memorizzare il certificato SSL e i file chiave.

     `# /home/db2inst2> mkdir SSL`

     `# /home/db2inst2> cd SSL`

  2. Nella console web {{site.data.keyword.dashdbshort_notm}}, scarica il certificato SSL dalla pagina **Connect your applications to the database**.

     a. Dal menu principale, fai clic su **Connect**.
     
     b. Fai clic su **Connection with SSL** e poi sul link **SSL certificate (1 KB)**.
     
     c. Salva il certificato `DigiCertGlobalRootCA.crt` nella directory SSL che hai creato nel passo 1.
        
  3. Crea un database keystore client nel sistema DataStage utilizzando il programma di utilità **gsk8capicmd_64**.

     `# /home/db2inst2/SSL> gsk8capicmd_64 -keydb -create -db <keystore_db.kdb> -pw <ks_db_password> -stash`

     dove `<keystore_db.kdb>` rappresenta il database keystore client e `<ks_db_password>` rappresenta la password del database keystore client.
        
  4. Aggiungi il certificato al database keystore client.

     `# /home/db2inst2/SSL> gsk8capicmd_64 -cert -add -db <keystore_db.kdb> -pw <ks_db_password> -label BLUDB_SSL -file DigiCertGlobalRootCA.crt`

     dove `<keystore_db.kdb>` rappresenta il database keystore client e `<ks_db_password>` rappresenta la password del database keystore client.
    
  5. Configura il client Db2 sul server DataStage.
            
     a. Aggiorna i parametri di configurazione SSL nel gestore database.

     `# /home/db2inst2> db2 update dbm cfg using SSL_CLNT_KEYDB /home/db2inst2/SSL/<keystore_db.kdb>`

     dove `<keystore_db.kdb>` rappresenta il database keystore client.

     `# /home/db2inst2> db2 update dbm cfg using SSL_CLNT_STASH /home/db2inst2/SSL/<keystore_db.sth>`

     dove `<keystore_db.sth>` rappresenta lo stash password del database keystore client.
            
     b. Cataloga il nodo di destinazione con l'opzione di sicurezza SSL e poi il database BLUDB per tale nodo di destinazione.

     `# /home/db2inst2> db2 catalog tcpip node <node_name> remote <IP_addr_of_BLUDB_database_server> server 50001 security SSL`

     dove `<node_name>` rappresenta il tuo nome per il nodo di destinazione e `<IP_addr_of_BLUDB_database_server>` rappresenta l'indirizzo IP del server database BLUDB,

     `# /home/db2inst2> db2 catalog db BLUDB as <db_alias> at node <node_name>`

     dove `<db_alias>` è il tuo nome del database {{site.data.keyword.dashdbshort_notm}}.

  6. Aggiungi le autorizzazioni di lettura e di esecuzione sui file nella directory SSL per tutti. L'utente DataStage che esegue i lavori ha bisogno di accedere a questi file per effettuare le connessioni SSL al database Db2.

     `# /home/db2inst2/SSL> chmod 655 /home/db2inst2/SSL/*`

  7. Verifica la connessione SSL in uno dei seguenti modi:

     - Verifica la connessione utilizzando CLP. Immetti il seguente comando per la connessione al database {{site.data.keyword.dashdbshort_notm}}:

       `db2 connect to <db_alias> user <user_id>`

       dove `<db_alias>` è il tuo nome per il database {{site.data.keyword.dashdbshort_notm}} e `<user_id>` è il tuo ID utente {{site.data.keyword.dashdbshort_notm}}. Ti viene richiesto di immettere la password.
    
     - Verifica la connessione utilizzando la CLI. Immetti il seguente comando per la connessione al database {{site.data.keyword.dashdbshort_notm}}:

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

        dove `<alias>` è un alias che hai creato utilizzando il comando **db2cli writecfg**, `<user_id>` è il tuo ID utente {{site.data.keyword.dashdbshort_notm}} e `<password>` è la tua password {{site.data.keyword.dashdbshort_notm}}.

- Per creare una connessione senza SSL, cataloga il database {{site.data.keyword.dashdbshort_notm}} di destinazione completando la seguente procedura:

  1. Cataloga il nodo {{site.data.keyword.dashdbshort_notm}} di destinazione in modo che le applicazioni client possano collegarsi a esso. Immetti i seguenti comandi CLP:

     `db2 catalog tcpip node <node_name> remote <IP_address_of_BLUDB_database_server> server <port_number_of_BLUDB_database>`

     dove `<node_name>` rappresenta il tuo nome per il nodo, `<IP_address_of_BLUDB_database_server>` rappresenta l'indirizzo IP del server database BLUDB e `<port_number_of_BLUDB_database>` rappresenta il numero di porta del database BLUDB.

  2. Cataloga il database {{site.data.keyword.dashdbshort_notm}} remoto in modo che le applicazioni client possano collegarsi a esso. Immetti il seguente comando:

     `db2 catalog db BLUDB as <db_alias> at node <node_name>`

     dove `<db_alias>` rappresenta il tuo nome per il database {{site.data.keyword.dashdbshort_notm}} e `<node_name>` rappresenta il tuo nome per il nodo.

  3. Verifica la connessione non SSL in uno dei seguenti modi:

      - Verifica la connessione utilizzando CLP. Immetti il seguente comando per la connessione al database {{site.data.keyword.dashdbshort_notm}}:

        `db2 connect to <db_alias> user <user_id>`

        dove `<db_alias>` è il tuo nome per il database {{site.data.keyword.dashdbshort_notm}} e `<user_id>` è il tuo ID utente {{site.data.keyword.dashdbshort_notm}}. Ti viene richiesto di immettere la password.

        `db2 list tables`

      - Verifica la connessione utilizzando la CLI. Immetti il seguente comando per la connessione al database {{site.data.keyword.dashdbshort_notm}}:

        `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

        dove `<alias>` è un alias che hai creato utilizzando il comando **db2cli writecfg**, `<user_id>` è il tuo ID utente {{site.data.keyword.dashdbshort_notm}} e `<password>` è la tua password {{site.data.keyword.dashdbshort_notm}}.

  4. Utilizza le [informazioni di connessione](/docs/services/Db2whc/connecting/credentials.html) raccolte precedentemente per definire una connessione nel client DataStage. Nella scheda **Parameters**, devi selezionare il **DB2 Connector** per il campo **Connect using Staging Type**.

     Per i dettagli sulla definizione di una connessione in DataStage, consulta i seguenti argomenti della documentazione di DataStage: 
     
     - [Creating a data connection object manually ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/support/knowledgecenter/SSZJPZ_11.3.0/com.ibm.swg.im.iis.ds.design.doc/topics/t_ddesref_Creating_a_Data_Connection_Object_Manually.html){:new_window}
     - [Configuring access to Db2 databases ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/support/knowledgecenter/en/SSZJPZ_11.7.0/com.ibm.swg.im.iis.conn.common.usage.doc/topics/t_configuring_db2conn.html){:new_window}

## Informatica
{: #informatica}

Puoi collegare Informatica a {{site.data.keyword.dashdbshort_notm}} per facilitare la gestione dei dati.
{: shortdesc}

Guarda questo video per vedere come integrare {{site.data.keyword.dashdbshort_notm}} con Informatica Cloud.

<iframe class="embed-responsive-item" id="youtubeplayer1" title="DB2 Connections - Lightening Fast How-To with Informatica Cloud" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TUiS_HstLnU?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

<!-- To configure a native Db2 connection to connect to {{site.data.keyword.dashdbshort_notm}}, perform the following steps:

1. Run the `odbcad32.exe` file from your local system.
The ODBC Data Sources Administrator dialog box appears.

2. Create the 32-bit ODBC Data Source Name using the DataDirect Db2 drivers.

3. In the ODBC DB2 Wire Protocol Setup dialog box, click **Security** tab.

4. Set the value of the `Authentication Method` property as `1 -Encrypt Password`. The following image shows the **Security** tab in the ODBC DB2 Wire Protocol Setup dialog box where you can set the `Authentication Method` property:
             
   ![ODBC Db2 Wire Protocol Driver Setup - Security tab](images/odbc_driver.png)
       
5. In the ODBC DB2 Wire Protocol Setup dialog box, click **Modify Bindings** tab.

6. Enter your user name in the Package Collection property. The following image shows the **Modify Bindings** tab in the ODBC DB2 Wire Protocol Setup dialog box where you can set the `Package Collection` property: 

   ![ODBC Db2 Wire Protocol Driver Setup - Modify Bindings tab](images/odbc_driver_2.png)
            
7. In the PowerCenter Designer, use the data source name that you created to import the metadata.

8. In the PowerCenter Workflow Manager, create the required workflow.

9. Ensure that you have the {{site.data.keyword.dashdbshort_notm}} compatible 11.x Db2 clients when you run the workflow.

**Note**: If you want to set the authentication type when you create the Db2 client catalog, you could specify the value of the `AUTHENTICATION TYPE` property as `SERVER_ENCRYPT`. -->

<!-- Watch this video to see how to integrate Db2 and Salesforce with Informatica Cloud.

<iframe class="embed-responsive-item" id="youtubeplayer2" title="Integrate Db2 and Salesforce with Informatica Cloud" type="text/html" width="640" height="390" src="//www.youtube.com/watch?v=RGTLweZvKP8" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe> -->

<!-- [Informatica ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://kb.informatica.com/howto/6/Pages/20/522402.aspx?myk=Connect%20to%20Db2){:new_window} -->

## Lift
{: #lift}

Utilizza Lift per migrare i dati in {{site.data.keyword.dashdbshort_notm}}.

[Lift ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://lift.ng.bluemix.net/#docs){:new_window}

## InfoSphere Data Replication
{: #idr}

Puoi collegare IBM® InfoSphere® Data Replication <!--version 11.3.3.3-36 or later -->a un database {{site.data.keyword.dashdbshort_notm}}. Questa funzionalità si applica sia agli ambienti SMP che MPP. Non si applica al piano d'ingresso di {{site.data.keyword.dashdbshort_notm}}. 
{: shortdesc}

### Panoramica
{: #overview2}

Idealmente, quando colleghi IBM InfoSphere Data Replication a {{site.data.keyword.dashdbshort_notm}}, IBM InfoSphere Data Replication si trova nello stesso data center {{site.data.keyword.Bluemix_notm}} di {{site.data.keyword.dashdbshort_notm}} o è collocato con {{site.data.keyword.dashdbshort_notm}}. IBM InfoSphere Data Replication si collega da un server locale all'istanza {{site.data.keyword.dashdbshort_notm}} remota.

Quando utilizzi {{site.data.keyword.dashdbshort_notm}} come una destinazione di connessione, le prestazioni di IBM InfoSphere Data Replication dipendono in parte dalla larghezza di banda della rete che separa il proprio motore di destinazione dall'istanza {{site.data.keyword.dashdbshort_notm}}. Anche la distanza fisica influisce sulle prestazioni: idealmente, IBM InfoSphere Data Replication deve essere il più vicino possibile all'istanza {{site.data.keyword.dashdbshort_notm}}. Anche la topologia di rete influenza le prestazioni. Ad esempio, idealmente, il motore di destinazione di IBM InfoSphere Data Replication viene eseguito su una VM nella stessa VPN (dominio di sicurezza) dell'istanza di destinazione. Meno sono i nodi di rete (ad esempio, i firewall o i router) da attraversare e meglio è. 

### Prerequisiti
{: #prereq2}

Se intendi effettuare la connessione utilizzando il protocollo SSL, scarica e installa GSKit V8. Consulta [GSKit V8 - Install, Uninstall and Upgrade instructions ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/support/docview.wss?uid=swg21631462){:new_window}. Fai clic sulla scheda del sistema operativo che si applica al sistema operativo della macchina client. Se stai installando il GSKit su un computer Windows, assicurati di specificare il percorso della directory di installazione di GSKit (`<installation_directory>\gsk8\bin`) per la variabile di ambiente **`PATH`**.

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](/docs/services/Db2whc/connecting/connecting.html#prereqs) necessari.

Se intendi effettuare la connessione utilizzando il protocollo SSL, scarica il certificato SSL `DigiCertGlobalRootCA.crt` dalla console web in una directory sulla macchina client. Per scaricare il certificato, fai clic su **Connection > Connection Information** e poi sulla scheda **Connection with SSL**.

### Procedura
{: #proc2}

1. Scegli uno dei seguenti approcci per effettuare la tua connessione:

   - Per creare una connessione con SSL, completa la seguente procedura:
            
     a. Immetti il seguente comando:

     `cd /<ssl_directory_name>/ssl`

     dove `/<ssl_directory_name>/ssl` è il percorso alla directory in cui hai scaricato il certificato SSL `DigiCertGlobalRootCA.crt`.

     b. Crea un database di chiavi client e un file stash utilizzando lo strumento **GSKCapiCmd**. Ad esempio, il seguente comando crea un database di chiavi client denominato `dashclient.kdb` e un file stash denominato `dashclient.sth`:

     `gsk8capicmd_64 -keydb -create -db "dashclient.kdb" -pw "passw0rdpw0" -stash`

     dove `passw0rdpw0` è una password. L'opzione **-stash** crea un file stash nello stesso percorso di quello del database delle chiavi client, con un'estensione file di `.sth`. Nel momento della connessione, GSKit utilizza il file stash per ottenere la password del database delle chiavi client.
            
     c. Aggiungi il certificato al database delle chiavi client. Ad esempio, il seguente comando **gsk8capicmd** importa il certificato dal file `/<ssl_directory_name>/ssl/DigiCertGlobalRootCA.crt` nel database delle chiavi client denominato `dashclient.kdb`:

     `gsk8capicmd_64 -cert -add -db "dashclient.kdb" -pw "passw0rdpw0" -label "DigiCert" -file "/<ssl_directory_name>/ssl/DigiCertGlobalRootCA.crt" -format ascii -fips`

     d. Aggiorna i valori dei parametri di configurazione del gestore del database `SSL_CLNT_KEYDB` e `SSL_CLNT_STASH` sul client per specificare il database delle chiavi client e il file stash. Seguono degli esempi:

     `db2 update dbm cfg using SSL_CLNT_KEYDB /<ssl_directory_name>/ssl/dashclient.kdb`

     `db2 update dbm cfg using SSL_CLNT_STASH /<ssl_directory_name>/ssl/dashclient.sth`

     e. Cataloga il nodo {{site.data.keyword.dashdbshort_notm}} in modo che le applicazioni client possano collegarsi a esso. Immetti il seguente comando:

     `db2 catalog tcpip node <node_name> remote <Db2_Warehouse_IP_address> server <port_number> security ssl`

     dove:
                
     `<node_name>` è il tuo nome del nodo.

     `<Db2_Warehouse_IP_address>` è l'indirizzo IP del server Db2 Warehouse on Cloud.

     `<port_number>` è la porta che viene utilizzata per il collegamento a Db2 Warehouse utilizzando una connessione SSL. Se stai utilizzando la porta predefinita, specifica `50001`.
            
     f. Cataloga il database {{site.data.keyword.dashdbshort_notm}} remoto in modo che le applicazioni client possano collegarsi a esso. Immetti il seguente comando:

     `db2 catalog database bludb as <db_alias> at node <node_name>`

     dove `db_alias` è il tuo nome per il database {{site.data.keyword.dashdbshort_notm}}.
            
     g. Verifica la connessione SSL in uno dei seguenti modi:
                
     - Verifica la connessione utilizzando CLP immettendo il seguente comando per il collegamento al database {{site.data.keyword.dashdbshort_notm}}:

       `db2 connect to <db_alias> user <user_id>`

       dove `<user_id>` è il tuo ID utente {{site.data.keyword.dashdbshort_notm}}. Ti viene richiesto di immettere la password.
                
     - Verifica la connessione utilizzando la CLI immettendo il seguente comando per il collegamento al database {{site.data.keyword.dashdbshort_notm}}:

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

       dove `<alias>` è un alias DSN che hai creato utilizzando il comando **db2cli writecfg**, `<user_id>` è il tuo ID utente {{site.data.keyword.dashdbshort_notm}} e `<password>` è la tua password del database {{site.data.keyword.dashdbshort_notm}}.
        
   - Per creare una connessione senza SSL, completa la seguente procedura:

     a. Cataloga il nodo {{site.data.keyword.dashdbshort_notm}} in modo che le applicazioni client possano collegarsi a esso. Immetti il seguente comando:

     `db2 catalog tcpip node <node_name> remote <Db2_Warehouse_IP_address> server <port_number>`

     dove:
                
     `<node_name>` è il tuo nome del nodo.

     `<Db2_Warehouse_IP_address>` è l'indirizzo IP del server {{site.data.keyword.dashdbshort_notm}} .

     `<port_number>` è la porta che viene utilizzata per il collegamento a {{site.data.keyword.dashdbshort_notm}} senza l'utilizzo di una connessione SSL. Se stai utilizzando la porta predefinita, specifica `50000`.
            
     b. Cataloga il database {{site.data.keyword.dashdbshort_notm}} remoto in modo che le applicazioni client possano collegarsi a esso. Immetti il seguente comando:

     `db2 catalog database bludb as <db_alias> at node <node_name>`

     dove `<db_alias>` è il tuo nome del database {{site.data.keyword.dashdbshort_notm}}.

     c. Verifica la connessione non SSL in uno dei seguenti modi:

     - Verifica la connessione utilizzando CLP immettendo il seguente comando per il collegamento al database {{site.data.keyword.dashdbshort_notm}}:

       `db2 connect to <db_alias> user <user_id>`

       dove `<user_id>` è il tuo ID utente {{site.data.keyword.dashdbshort_notm}}. Ti viene richiesto di immettere la password.
                
     - Verifica la connessione utilizzando la CLI immettendo il seguente comando per il collegamento al database {{site.data.keyword.dashdbshort_notm}}:

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

       dove `<alias>` è un alias DSN che hai creato utilizzando il comando **db2cli writecfg**, `<user_id>` è il tuo ID utente {{site.data.keyword.dashdbshort_notm}} e `<password>` è la tua password di Db2 Data Warehouse on Cloud.
    
2. Avvia lo strumento di configurazione InfoSphere Data Replication ed esegui la seguente procedura. I valori mostrati nelle schermate sono degli esempi.
        
   a. Aggiungi un'istanza di origine che punta al tuo database di origine utilizzando la scheda **Instance Configuration**:

   ![IIDR New Instance - Source instance](images/IIDR_source_instance.jpg)

   b. Aggiungi un'istanza di destinazione che punta al tuo database Db2 di destinazione utilizzando la scheda **Instance Configuration**. Se non stai utilizzando IBM InfoSphere Data Replication 11.3.3.3-50 o successive, non selezionare la casella di spunta **Specify refresh loader path**.

   ![IIDR New Instance - Target instance](images/IIDR_target_instance.jpg)

   c. Avvia tutte le istanze:

   ![IIDR Configuration Tool](images/IIDR_instances.jpg)

3. Avvia la console di gestione di InfoSphere Data Replication e utilizza Access Manager per completare i seguenti passi:
        
   a. Crea un datastore per collegarti alla tua istanza di origine utilizzando la scheda **Datastore**. Poiché un database Db2 non è stato originariamente supportato come database di origine, devi fornire le informazioni sull'utente e sulla password per il database di origine facendo clic su **Connection Parameters**.

   ![Datastore Properties - Source](images/IIDR_source_datastore.jpg)

   b. Crea un datastore per collegarti alla tua istanza di destinazione utilizzando la scheda **Datastore**. Devi fornire le informazioni sull'utente e sulla parola d'ordine facendo clic su **Connection Parameters**.

   ![Datastore Properties - Target](images/IIDR_target_datastore.jpg)

   c. Se l'utente (ad esempio, admin) che si collegherà a Access Server non esiste, crea quell'utente:

   ![New User](images/IIDR_management_user.jpg)

   d. Fai clic sulla scheda **Access Manager**.
        
   e. Nella scheda **Datastore Management**, assegna l'utente ai datastore di origine e di destinazione facendo clic con il tasto destro del mouse su ciascun datastore e facendo clic su **Assign User**. Assicurati che le credenziali per l'accesso a ciascuna istanza siano corrette.

   ![IIDR Management Console - Access Manager](images/IIDR_management_assign_user.jpg)

### Operazioni successive
{: #what2}

Definisci una sottoscrizione ed esegui la replica dei dati. Per informazioni, consulta:

- [Loading data from InfoSphere Data Replication ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/learn_how/loaddata_iidr.html){:new_window} 

## Segment
{: #segment}

Puoi integrare Segment con un database {{site.data.keyword.dashdbshort_notm}}. Segment è una piattaforma unica che raccoglie, archivia e instrada i tuoi dati utente a centinaia di strumenti.
{: shortdesc}

[Segment ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://segment.com/docs/destinations/db2/){:new_window}

## Data Studio
{: #data_studio}

Queste istruzioni spiegano come creare una connessione da IBM® Data Studio <!--version 4.1.x -->a un database {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Prerequisiti
{: #prereq3}

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](/docs/services/Db2whc/connecting/connecting.html#prereqs) necessari.

### Procedura
{: #proc3}

1. In Data Studio, fai clic su **All Databases > New Connection to a database**.

2. Sulla scheda **Locale**, seleziona **DB2 for Linux, UNIX, and Windows** come gestore database.
    
3. Nella scheda **General**, immetti i seguenti valori:
   - *Database*: `BLUDB`
   - *Host*: il nome host.
   - *Port*: per una connessione senza SSL, immetti `50000`. Per una connessione con SSL, immetti `50001`. 
   - *User name*: il nome utente che hai utilizzato per accedere.
   - *Password*: la password che hai utilizzato per accedere.

4. Per una connessione SSL, fai clic sulla scheda **Optional** e poi su **Add**. Per la proprietà `sslConnection`, specifica `true`.

5. [*Optional*]: Click **Test Connection** per verificare che la connessione funzioni.

## Data Server Manager (DSM)
{: #dsm}

Una connessione tra il tuo IBM® Data Server Manager e il tuo database {{site.data.keyword.dashdbshort_notm}} ti consente di monitorare e gestire il database dalla console web di Data Server Manager. 
{: shortdesc}

### Prerequisiti
{: #prereq4}

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](/docs/services/Db2whc/connecting/connecting.html#prereqs) necessari.

### Procedura
{: #proc4}

<!--The connection procedure was tested on Data Server Manager version 1.1. The same procedure applies to all of the other versions of the Data Server Manager software.
-->
Per creare una connessione, completa la seguente procedura:

1. Accedi alla console web di Data Server Manager.
    
2. Nella console web di Data Server Manager, vai a **Set Up > Database Connections**.
    
3. Fai clic sull'icona ![segno + all'interno di un cerchio](images/icon_R_plus.gif) per aggiungere una connessione al database. Nella pagina **Add Database Connection** nella scheda **Database Connection**, immetti le informazioni richieste nei seguenti campi:

   - *Database connection name*: il nome deve essere univoco per Data Server Manager
   - *Data server type*: dal menu a discesa, seleziona **DB2 for Linux, UNIX, and Windows**
   - *Database name*: `BLUDB`
   - *Host name*: immetti il nome host {{site.data.keyword.dashdbshort_notm}} 
   - *Port number*: per una connessione senza SSL, immetti `50000`. Per una connessione con SSL, immetti `50001`. 
   - *JDBC security*: dal menu a discesa, seleziona **Clear text password**
   - *User ID*: il tuo ID utente {{site.data.keyword.dashdbshort_notm}} 
   - *Password*: la tua password {{site.data.keyword.dashdbshort_notm}} 

4. Per una connessione con SSL, seleziona la scheda **Advanced JDBC Properties**. Immetti le informazioni richieste nei seguenti campi:

   - *Property*: `sslConnection`
   - *Value*: `true`

    Fai clic sul pulsante **Add**. Seleziona la scheda **Database Connection**.
    
5. Verifica la connessione facendo clic sul pulsante **Test Connection**. Se la connessione ha esito positivo, fai clic su **OK**.

## InfoSphere Data Architect
{: #ida}

Queste istruzioni spiegano come creare una connessione da InfoSphere® Data Architect <!--version 9.1.x -->a un database {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Prerequisiti
{: #prereq5}

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](/docs/services/Db2whc/connecting/connecting.html#prereqs) necessari.

### Procedura
{: #proc5}

1. Nella vista Data Source Explorer di InfoSphere Data Architect, fai clic con il tasto destro del mouse su **Database Connections**, quindi seleziona **New**.
    
2. Sulla scheda **Locale**, seleziona **DB2 for Linux, UNIX, and Windows** come gestore database.
    
3. Nella scheda **General**, immetti i seguenti valori:

   - *Database*: `BLUDB`
   - *Host*: il nome host che hai raccolto in precedenza.
   - *Port*: per una connessione senza SSL, immetti `50000`. Per una connessione con SSL, immetti `50001`. 
   - *User name*: l'ID utente che hai raccolto in precedenza.
   - *Password*: la password che hai raccolto in precedenza.

4. Per una connessione SSL, fai clic sulla scheda **Optional**. Immetti una proprietà `sslConnection` e specifica un valore di `true`. Fai clic su **Add**.
    
5. [*Optional*]: Click **Test Connection** per verificare che la connessione funzioni.

## Aginity Workbench
{: #aginity_wb}

Queste istruzioni spiegano come collegare Aginity Workbench <!--4.3 -->a un database {{site.data.keyword.dashdbshort_notm}}. Puoi utilizzare Aginity Workbench per migrare i modelli di dati IBM PureData for Analytics (Netezza) e i dati a {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Prerequisiti
{: #prereq6}

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](/docs/services/Db2whc/connecting/connecting.html#prereqs) necessari.

### Procedura
{: #proc6}

1. Scarica e installa Aginity Workbench.

2. Determina il tuo DSN ODBC dalle informazioni di connessione che hai annotato in precedenza.

3. Avvia Aginity Workbench. Se la finestra di dialogo di connessione al database non si apre automaticamente, aprila facendo clic su **Connect** nella barra degli strumenti.

4. [Establish a database connection ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.aginity.com/documentation/WB/dashDB/Default.htm#Aginity_Topics/Aginity_Workbench/Database_Connection_Dialog_Box.htm){:new_window}. Utilizza il nome host, l'ID utente e la password dalle informazioni di connessione che hai annotato in precedenza.

## CLPPlus
{: #clpplus}

Command line processor plus (CLPPlus) è incluso nel pacchetto del driver Db2. CLPPlus fornisce un'interfaccia della riga di comando che puoi utilizzare per collegarti a un database {{site.data.keyword.dashdbshort_notm}}. Puoi utilizzare CLPPlus per definire, modificare ed eseguire istruzioni, script e comandi.
{: shortdesc}

### Prerequisiti
{: #prereq7}

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](/docs/services/Db2whc/connecting/connecting.html#prereqs) necessari.

Per utilizzare CLPPlus, assicurati che sia installata una SDK (Software Development Kit) o una JRE (Java Runtime environment) per Java versione 1.5.0 o successiva sul tuo computer e che le variabili di ambiente siano impostate come segue:

- La variabile di ambiente `JAVA_HOME` sia impostata sulla directory di installazione Java sul tuo computer.
- L'impostazione della variabile di ambiente `PATH` include la directory secondaria `bin` della directory di installazione Java sul tuo computer.

### Procedura
{: #proc7}

1. In una shell di comandi sui sistemi operativi Linux, sul prompt dei comandi di Windows o nella finestra di comando DB2 sui sistemi operativi Windows, immetti i seguenti comandi:

   Questi comandi creano nuove voci nel file di configurazione del driver (`db2dsdriver.cfg`) sul tuo computer e impostano gli attributi di connessione. Hai bisogno di eseguire questo passo solo una volta.

   - Per una connessione con SSL:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`  

     dove:
     
     - `<hostname>` è il nome host del server.
     - `<alias>` è un alias di tua scelta.

   - Per una connessione senza SSL:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

2. Per avviare CLPPlus con una connessione a un database {{site.data.keyword.dashdbshort_notm}} che utilizza le voci nel file `db2dsdriver.cfg`, immetti il seguente comando:

   - Ambienti Windows: 

     `clpplus <userid>@<alias>`

   - Ambienti Linux:

     `clpplus -nw <userid>@<alias>`

     dove:
     
     - `<userid>` è l'ID utente dalle credenziali di connessione che hai raccolto in precedenza.
     - `<alias>` è l'alias che hai creato con il comando **db2cli writecfg**.

   L'esecuzione di questo comando apre una finestra CLPPlus.

3. Nella finestra CLPPlus, immetti la tua password. Le informazioni del database vengono visualizzate, seguite da una richiesta SQL. Il seguente è un output di esempio:

```
   Hostname = 192.0.2.0
   Database server = DB2/LINUXX8664  SQL10054
   SQL authorization ID = smith
   Local database alias = BLUDB
   Port = 50001
   
   SQL>
```

### Risultati
{: #results7}

Puoi ora immettere i comandi CLPPlus o le istruzioni SELECT ed eseguire gli script per gestire i dati nel database.

### Esempi

I seguenti esempi utilizzano uno script breve che richiama le righe dalla tabella di esempio `GOSALES.BRANCH`. Il file script è denominato `cities.sql` e si trova sul computer Windows locale in `C:\temp directory`. Il file `cities.sql` contiene il seguente testo:

```
SET ECHO ON
SELECT branch_code, city from GOSALES.BRANCH;
```

#### Esempio 1 

Per eseguire lo script in modalità interattiva:

1. Avvia CLPPlus con il tuo ID utente e l'alias creato nel file `db2dsdriver.cfg` immettendo il seguente comando:

   `clpplus <user_id>@<alias>`
2. Immetti la tua password.
3. Nel prompt SQL, immetti il seguente testo:

   `start C:\temp\cities.sql`

#### Esempio 2

Avvia CLPPlus con il tuo ID utente e l'alias creato nel file `db2dsdriver.cfg` ed esegui lo script in una fase:

`clpplus <user_id>/<password>@<alias> @C:\temp\cities.sql`

Il seguente è l'output di esempio dallo script `cities.sql`:

```
BRANCH_CODE CITY
----------- --------------------------------------------------
          6 Paris
          7 Milano
          9 Amsterdam
         13 Hamburg
         14 München
         15 Kista
         17 Calgary
         18 Toronto
         19 Boston
         20 Seattle
         21 Los Angeles
         22 Miami
         23 Lyon
         24 Distrito Federal
         25 Tokyo
         26 Osaka City
         28 Melbourne
         29 Bilbao
         30 Sao Paulo
         31 Kuopio
         32 Seoul
         33 Singapore

BRANCH_CODE CITY
----------- --------------------------------------------------
         34 Shanghai
         35 London
         36 Birmingham
         37 Zürich
         38 Heverlee
         39 Wien
         40 Geneve

29 rows were retrieved.
```


