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

# Dettagli database e credenziali di connessione
{: #db_details_cxn_creds}

Per configurare il tuo ambiente di sviluppo locale e per collegare le applicazioni e gli strumenti al tuo database {{site.data.keyword.dashdbshort_notm}}, devi conoscere i dettagli del database e le credenziali di connessione.
{: shortdesc}

## Dettagli del database
{: #db_details}

Esistono dei dettagli del database importanti necessari alla connessione delle applicazioni e degli strumenti al tuo database:

- *Nome host* - Il nome host del server.
- *Numero porta* - Utilizzato dal gestore del database per la comunicazione TCP/IP. (Tieni presente che il tuo servizio viene fornito con un numero di porta per le connessioni che utilizzano SSL (Secure Socket Layer) e una porta diversa per la connessione non SSL).

   Se necessario, puoi ottenere l'indirizzo IP del tuo server utilizzando il comando ping o il comando nslookup, specificando il nome host.
- *Nome database* - Il nome del database Db2, di solito BLUDB.

## Credenziali di connessione
{: #cxn_creds}

Ci sono tre tipi di credenziali:

- *ID IBM* - Se utilizzi {{site.data.keyword.Bluemix_notm}}, questo è l'ID che utilizzi per accedere a {{site.data.keyword.Bluemix_notm}}. Questo non è quello che utilizzi per collegare le applicazioni o gli strumenti al tuo database di Db2 Warehouse on Cloud.
- *Credenziali database Db2* - Il servizio viene fornito con un ID utente e una password del database che possono essere utilizzati per collegare le applicazioni e gli strumenti al tuo database.
- *Utenti creati dall'amministratore* - Alcuni piani {{site.data.keyword.dashdbshort_notm}} consentono agli utenti amministrativi di creare nuovi utenti. Questi ID utente e password creati dall'amministratore possono essere utilizzati per accedere direttamente all'URL della console web e per la connessione al database Db2 dalle applicazioni o dagli strumenti.

## Dove trovare i dettagli del database e le credenziali di connessione
{: #location}

Puoi raccogliere queste informazioni da:

- *Il tuo amministratore* - Se sei il proprietario o l'amministratore della tua istanza Db2, puoi ottenere i dettagli del database e le credenziali di connessione dal tuo amministratore.
- *Console web Db2* - Le credenziali e i dettagli del database sono disponibili nella console web.
- Se stai utilizzando {{site.data.keyword.Bluemix_notm}}: 
   
   - *Dashboard {{site.data.keyword.Bluemix_notm}}* - Quando visualizzi il tuo servizio nel tuo dashboard {{site.data.keyword.Bluemix_notm}}, nell'area "Credenziali del servizio", puoi visualizzare i dettagli del database così come la password e l'ID utente del database.
   - *`VCAP_SERVICES`* - `VCAP_SERVICES` è una variabile di ambiente in {{site.data.keyword.Bluemix_notm}} che contiene le credenziali e i dettagli del database nel formato JSON. Quando visualizzi le credenziali del servizio nel tuo servizio nel tuo dashboard {{site.data.keyword.Bluemix_notm}}, visualizzi i contenuti di `VCAP_SERVICES`. Quando associ altri servizi o applicazioni {{site.data.keyword.Bluemix_notm}} al tuo servizio, tali sevizi e applicazioni possono accedere alle credenziali e ai dettagli del database in modo programmatico leggendo `VCAP_SERVICES`.
