---

copyright:
  years: 2014, 2019
lastupdated: "2019-04-01"

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

# Panoramica di collegamento
{: #connect_ov}

Puoi collegare le interfacce della riga di comando, strumenti e applicazioni di terze parti o di IBM® o applicazioni che hai creato nel tuo database {{site.data.keyword.dashdbshort_notm}}. 
{: shortdesc}

## Prerequisiti
{: #prereqs}

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i prerequisiti necessari. 

- Raccogli i dettagli e le credenziali del database

   Per collegarti al database, hai bisogno dei dettagli del database (come il nome host), così come delle credenziali (ad esempio un ID utente e una password). Puoi raccogliere queste informazioni di connessione dalla console web {{site.data.keyword.dashdbshort_notm}}.

- Verifica che sia installato un driver supportato

   - Se la tua applicazione o il tuo strumento già contiene il pacchetto del driver Db2 v11.1 IBM Data Server, allora l'applicazione o lo strumento è in grado di collegarsi al tuo database {{site.data.keyword.dashdbshort_notm}} utilizzando quel driver.
   - Altrimenti, installa il pacchetto del driver Db2, che puoi scaricare dalla console web {{site.data.keyword.dashdbshort_notm}}.

- Configura il tuo ambiente

  - Aggiungi le voci al file di configurazione del driver, `db2dsdriver.cfg`, per il tuo database.
  - SSL (Secure Sockets Layer)

    Puoi scegliere di collegarti con o senza SSL. I dettagli di connessione, come ad esempio la porta da utilizzare e la stringa di connessione, dipendono dal fatto se utilizzi o meno connessioni SSL.

    Per utilizzare le connessioni SSL, hai bisogno di un certificato CA:
    - Se utilizzi l'ultimo pacchetto del driver {{site.data.keyword.dashdbshort_notm}}, il file del certificato è integrato con il pacchetto e verrà utilizzato per le connessioni.
    - Se utilizzi il pacchetto del driver IBM Data Server, puoi scaricare il certificato SSL dalla console web {{site.data.keyword.dashdbshort_notm}}.

- Conferma che le porte sono disponibili

   Se la tua rete è dietro un firewall, conferma che le comunicazioni sono consentite sul numero di porta `50000` per i protocolli standard o il numero di porta `50001` per le connessioni SSL.

<!-- Before you can connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you completed downloading and installing the necessary components on the prerequisites checklist: 

- [Prerequisites checklist](prereqs.html) -->

### Raccolta delle informazioni di connessione
{: #collect_info}

- [Dettagli database e credenziali di connessione](/docs/services/Db2whc/connecting?topic=Db2whc-db_details_cxn_creds#db_details_cxn_creds)

### Scaricamento e installazione del pacchetto del driver
{: #dl_install}

- [Scarica il pacchetto del driver](/docs/services/Db2whc/connecting?topic=Db2whc-dr_pkg#dr_pkg)
- [Installazione su Linux o PowerLinux](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_linux#install_dr_pkg_linux)
- [Installazione su Mac OS X](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_mac#install_dr_pkg_mac)
- [Installazione su Windows](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_windows#install_dr_pkg_windows)

### Configurazione dell'ambiente
{: #cfg_env}

- [Configurazione dell'ambiente](/docs/services/Db2whc/connecting?topic=Db2whc-cfg_loc_env#cfg_loc_env)
- [Supporto SSL (Secure Sockets Layer)](/docs/services/Db2whc/connecting?topic=Db2whc-ssl_support#ssl_support)

## Opzioni di connettività
{: #connect_opts}

{{site.data.keyword.dashdbshort_notm}} offre più opzioni di connettività sicura a seconda dei requisiti di connessione della tua applicazione.  
{: shortdesc}

Vedi [Opzioni di connettività](/docs/services/Db2whc/connecting?topic=Db2whc-connect_options#connect_options).

## Collegamento in modo programmatico
{: #conx_prgrm}

Puoi utilizzare linguaggi di programmazione comuni per creare applicazioni che si collegano a un database {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

- [JDBC](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_jdbc#con_prog_jdbc)
- [Microsoft Windows ODBC o CLI](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_odbc_cli#con_prog_odbc_cli)
- [.NET](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_net#con_prog_net)
- [ODBC Data Source Administrator](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_odbc_dsa#con_prog_odbc_dsa)
- [PHP](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_php#con_prog_php)
- [API REST](/docs/services/Db2whc/connecting?topic=Db2whc-con_rest_api#con_rest_api)
<!-- - [C++]() -->
<!-- - [Java]() -->
<!-- - [Node.js]() -->
<!-- - [Perl]() -->
<!-- - [Python]() -->

## Integrazione di applicazioni e strumenti
{: #conx_apps_tools}

Puoi anche
connettere applicazioni e strumenti esterni a {{site.data.keyword.dashdbshort_notm}} e
utilizzarli per un'ulteriore gestione o analisi dei dati. Ad esempio:

### Integrazione dei dati
{: #di}

- Connetti le tue applicazioni {{site.data.keyword.Bluemix_short}} che necessitano di
un database di analisi.
- [DataStage](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#datastage)
- [Informatica](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#informatica)
- [Lift](https://www.lift-cli.cloud.ibm.com/#docs){:external}
- [InfoSphere Data Replication](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#idr)
- [Segment](https://segment.com/docs/destinations/db2/){:external}
- [Data Studio](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#data_studio)
- [Data Server Manager](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#dsm)
- [CLPPLUS](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#clpplus)
- [Aginity Workbench per migrare i modelli di dati e i dati Netezza® a {{site.data.keyword.dashdbshort_notm}}](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#aginity_wb)
- [InfoSphere Data Architect per progettare e distribuire lo schema di database](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#ida)

### Visualizzazione dati/BI
{: #dvis_bi}

- [Cognos Analytics per eseguire i report di Business Intelligence per i tuoi dati](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#cognos)
- [Looker](https://docs.looker.com/setup-and-management/connecting-to-db){:external}
- [Tableau](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#tableau)
- [Microsoft Excel](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#excel)
- [Esri ArcGIS for Desktop per eseguire analisi geospaziali e associare la pubblicazione ai dati](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#esri_arcgis)

### Data science
{: #dsci}

- [Watson Studio (in precedenza IBM Data Science Experience)](/docs/services/Db2whc/connecting?topic=Db2whc-ds#watson_studio)
- [SPSS Statistics](/docs/services/Db2whc/connecting?topic=Db2whc-ds#spss_stats)
- [SAS](/docs/services/Db2whc/connecting?topic=Db2whc-ds#sas)
- [Ambiente di sviluppo R locale](/docs/services/Db2whc/connecting?topic=Db2whc-ds#r_dev_env)

## Collegamento a un altro database Db2
{: #fed}

La virtualizzazione dei dati Db2 (conosciuta anche come federazione) è supportata da {{site.data.keyword.dashdbshort_notm}}. La virtualizzazione dei dati ti fornisce l'accesso con una singola query a tutti i dati presenti su più database distribuiti in qualsiasi punto della tua organizzazione. Puoi accedere ai dati che si trovano su una qualsiasi delle tue origini dati Db2 o Informix, sia nel cloud che in loco. 

Questa funzione è supportata in tutte le versioni di {{site.data.keyword.dashdbshort_notm}}, con l'eccezione del piano d'ingresso. Tuttavia, puoi utilizzare il piano d'ingresso come una destinazione da cui potrai estrarre i dati.

- [Virtualizzazione dei dati (federazione)](/docs/services/Db2whc?topic=Db2whc-data_virt_fed#data_virt_fed)


