---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-15"

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

- [Dettagli database e credenziali di connessione](/docs/services/Db2whc/connecting/credentials.html)

### Scaricamento e installazione del pacchetto del driver
{: #dl_install}

- [Scarica il pacchetto del driver](/docs/services/Db2whc/connecting/driver_pkg.html)
- [Installazione su Linux o PowerLinux](/docs/services/Db2whc/connecting/install_linux.html)
- [Installazione su Mac OS X](/docs/services/Db2whc/connecting/install_mac.html)
- [Installazione su Windows](/docs/services/Db2whc/connecting/install_win.html)

### Configurazione dell'ambiente
{: #cfg_env}

- [Configurazione dell'ambiente](/docs/services/Db2whc/connecting/driver_pkg_cfg.html)
- [Supporto SSL (Secure Sockets Layer)](/docs/services/Db2whc/connecting/ssl.html)

## Collegamento in modo programmatico
{: #conx_prgrm}

Puoi utilizzare linguaggi di programmazione comuni per creare applicazioni che si collegano a un database {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

- [JDBC](/docs/services/Db2whc/connecting/jdbc.html)
- [Microsoft Windows ODBC o CLI](odbc_cli.html)
- [.NET](/docs/services/Db2whc/connecting/net_apps.html)
- [ODBC Data Source Administrator](/docs/services/Db2whc/connecting/odbc_data_source_admin.html)
- [PHP](/docs/services/Db2whc/connecting/php.html)
- [API REST](/docs/services/Db2whc/connecting/rest_api.html)
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
- [DataStage](/docs/services/Db2whc/connecting/data.html#datastage)
- [Informatica](/docs/services/Db2whc/connecting/data.html#informatica)
- [Lift ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://lift.ng.bluemix.net/#docs){:new_window}
- [InfoSphere Data Replication](/docs/services/Db2whc/connecting/data.html#idr)
- [Segment ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://segment.com/docs/destinations/db2/){:new_window}
- [Data Studio](/docs/services/Db2whc/connecting/data.html#data_studio)
- [Data Server Manager](/docs/services/Db2whc/connecting/data.html#dsm)
- [CLPPLUS](/docs/services/Db2whc/connecting/data.html#clpplus)
- [Aginity Workbench per migrare i modelli di dati e i dati Netezza® a {{site.data.keyword.dashdbshort_notm}}](/docs/services/Db2whc/connecting/data.html#aginity_wb)
- [InfoSphere Data Architect per progettare e distribuire lo schema di database](/docs/services/Db2whc/connecting/data.html#ida)

### Visualizzazione dati/BI
{: #dvis_bi}

- [Cognos Analytics per eseguire i report di Business Intelligence per i tuoi dati](/docs/services/Db2whc/connecting/vis_bi.html#cognos)
- [Looker ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://docs.looker.com/setup-and-management/connecting-to-db){:new_window}
- [Tableau](/docs/services/Db2whc/connecting/vis_bi.html#tableau)
- [Microsoft Excel](/docs/services/Db2whc/connecting/vis_bi.html#excel)
- [Esri ArcGIS for Desktop per eseguire analisi geospaziali e associare la pubblicazione ai dati](/docs/services/Db2whc/connecting/vis_bi.html#esri_arcgis)

### Data science
{: #dsci}

- [Watson Studio (in precedenza IBM Data Science Experience)](/docs/services/Db2whc/connecting/data_sci.html#watson_studio)
- [SPSS Statistics](/docs/services/Db2whc/connecting/data_sci.html#spss_stats)
- [SAS](/docs/services/Db2whc/connecting/data_sci.html#sas)
- [Ambiente di sviluppo R locale](/docs/services/Db2whc/connecting/data_sci.html#r_dev_env)

## Collegamento a un altro database Db2
{: #fed}

La virtualizzazione dei dati Db2 (conosciuta anche come federazione) è supportata da {{site.data.keyword.dashdbshort_notm}}. La virtualizzazione dei dati ti fornisce l'accesso con una singola query a tutti i dati presenti su più database distribuiti in qualsiasi punto della tua organizzazione. Puoi accedere ai dati che si trovano su una qualsiasi delle tue origini dati Db2 o Informix, sia nel cloud che in loco. 

Questa funzione è supportata in tutte le versioni di {{site.data.keyword.dashdbshort_notm}}, con l'eccezione del piano d'ingresso. Tuttavia, puoi utilizzare il piano d'ingresso come una destinazione da cui potrai estrarre i dati.

- [Virtualizzazione dei dati (federazione)](/docs/services/Db2whc/federation.html)


