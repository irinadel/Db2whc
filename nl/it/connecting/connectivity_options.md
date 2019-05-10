---

copyright:
  years: 2014, 2019
lastupdated: "2019-04-01"

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

# Opzioni di connettività
{: #connect_options}

{{site.data.keyword.dashdblong}} offre più opzioni di connettività sicura a seconda dei requisiti di connessione della tua applicazione.  
{: shortdesc}

## Connessione a un endpoint pubblico (opzione predefinita)
{: #pub_endpt}

Come per qualsiasi servizio cloud pubblico, puoi collegare la tua applicazione tramite un nome host pubblico che viene fornito al momento del provisioning del tuo servizio. L'accesso ai tuoi dati è protetto tramite l'autenticazione avanzata, numerosi controlli di accesso e opzioni di autorizzazioni Db2, la crittografia dei dati trasmessi e memorizzati e le procedure consigliate di conformità e di sicurezza IBM per lo sviluppo e le operazioni. Viene offerta anche un'opzione facoltativa di inserimento in whitelist degli IP. Crea un caso di supporto IBM se vuoi abilitare l'inserimento in whitelist degli IP. 

### Come collegarsi a un endpoint pubblico:
{: #pub_endpt_steps}

Il modo più semplice per collegare il tuo data warehouse è tramite il nome host pubblico fornito nella tua lettera di benvenuto. Puoi anche ottenere il tuo nome host e le credenziali nel seguente modo: 

1. Accedi a {{site.data.keyword.cloud_notm}} e fai clic sulla tua istanza del servizio. 
2. Fai clic su **Credenziali del servizio**.
3. Fai clic su **Nuova credenziale**, quindi fai clic su **Aggiungi**.
4. Una volta create le credenziali, nella colonna `Azioni`, fai clic su **Visualizza credenziali**.
5. Nel seguente esempio di documento JSON, prendi nota del contenuto dei campi hostname, password e username. Questi tre componenti vengono utilizzati per stabilire la connessione all'endpoint pubblico: 

   ```
   {
     "hostname": "db2whoc-flex-xxxxxxx.services.dal.bluemix.net",
     "password": "DTPY7KXxhp_pKtjLSt",
     "https_url": "https://db2whoc-flex-xxxxxxx.services.dal.bluemix.net",
     "port": 50000,
     "ssldsn": "DATABASE=BLUDB;HOSTNAME=db2whoc-flex-xxxxxx.services.dal.bluemix.net;PORT=50001;PROTOCOL=TCPIP;UID=bluadmin;PWD=DTPY7KXWxhp_pKtjLSt;Security=SSL;",
     "host": "db2whoc-flex-xxxxx.services.dal.bluemix.net",
     "jdbcurl": "jdbc:db2://db2whoc-flex-xxxx.services.dal.bluemix.net:50000/BLUDB",
     "uri": "db2://bluadmin:DTPY7KXx1p_pKtjLSt@db2whoc-flex-hyftpsb.services.dal.bluemix.net:50000/BLUDB",
     "db": "BLUDB",
     "dsn": "DATABASE=BLUDB;HOSTNAME=db2whoc-flex-xxxxx.services.dal.bluemix.net;PORT=50000;PROTOCOL=TCPIP;UID=bluadmin;PWD=DTPYZunlWxhp_pKtjLSt;",
     "username": "bluadmin",
     "ssljdbcurl": "jdbc:db2://db2whoc-flex-xxxx.services.dal.bluemix.net:50001/BLUDB:sslConnection=true;"
   }

   ```

   ![Accesso di rete pubblico a {{site.data.keyword.cloud_notm}}](images/public_connection.png)

## Connessione a un endpoint privato: endpoint del servizio IBM Cloud
{: #priv_endpt}

Se hai un'applicazione distribuita nel tuo account {{site.data.keyword.cloud_notm}} e vuoi collegarla al tuo database senza che il traffico del database fluisca nelle reti pubbliche, puoi utilizzare l'opzione dell'**endpoint del servizio {{site.data.keyword.cloud_notm}}** quando ordini il tuo database. Ti verrà fornito un nome host privato al momento del provisioning del servizio e potrai collegarti ad esso solo dal tuo account {{site.data.keyword.cloud_notm}}.  

Per ulteriori informazioni sull'opzione dell'endpoint del servizio {{site.data.keyword.cloud_notm}}, vedi [Endpoint servizio: informazioni](/docs/services/service-endpoint?topic=service-endpoint-about#about).


### Come collegarsi a un endpoint privato con l'endpoint del servizio IBM Cloud 
{: #priv_endpt_steps}

La comunicazione tra la rete pubblica e l'endpoint avviene tramite il servizio dell'endpoint del servizio {{site.data.keyword.cloud_notm}}. Il servizio dell'endpoint del servizio rende semplice instradare in modo sicuro e veloce il traffico di rete tra i diversi servizi {{site.data.keyword.cloud_notm}} e il tuo database warehouse tramite il backplane di rete privato {{site.data.keyword.cloud_notm}}. Questo instradamento di rete garantisce che i tuoi dati non verranno mai trasmessi su internet pubblico.  

Per iniziare con l'endpoint del servizio, il tuo account {{site.data.keyword.cloud_notm}} deve essere abilitato per VRF (Virtual Routing and Forwarding). Per abilitare il tuo account, vedi [Abilitazione del tuo account per l'utilizzo dell'endpoint del servizio utilizzando la CLI IBM Cloud](/docs/services/service-endpoint?topic=service-endpoint-getting-started#cs_cli_install_steps).

Una volta che il tuo account è abilitato per VRF e che l'endpoint del servizio è abilitato, segui le istruzioni fornite nella tua lettera di benvenuto. 

Ora è il momento di collegare la tua istanza {{site.data.keyword.dashdbshort_notm}} dal tuo account {{site.data.keyword.cloud_notm}} tramite l'indirizzo di rete privato fornito nella tua lettera di benvenuto. 

## Connessione a un endpoint privato: VPN (virtual private network)
{: #vpn}

Se hai un'applicazione distribuita in una rete privata che si trova all'esterno di {{site.data.keyword.cloud_notm}} senza l'accesso a internet pubblico e vuoi collegarti al tuo database tramite una connessione VPN (virtual private network), puoi effettuare la richiesta al momento dell'ordine del servizio o aprendo un caso di supporto IBM. Gli ingegneri di rete IBM assisteranno i tuoi ingegneri di rete nella configurazione del tunnel VPN tra la tua rete privata e {{site.data.keyword.cloud_notm}}.

### Come collegarsi a un endpoint privato con una VPN
{: #priv_endpt_vpn_steps}

Per stabilire una connessione VPN al tuo data warehouse cloud dietro un endpoint pubblico, [crea un caso di supporto {{site.data.keyword.cloud_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/unifiedsupport/cases/add){:new_window} che include i seguenti dettagli: 

* **Type of support**: tecnico 
* **Category**: database 
* **Offering**: seleziona la tua istanza {{site.data.keyword.dashdbshort_notm}} 
* **Subject**: richiesta di connessione VPN 
* **Description**: fornisci le seguenti informazioni obbligatorie
  * **Customer-side VPN Peer Address** (il tuo endpoint VPN): `<IP Address>`
  * **Customer-side Encryption Domain** (sii specifico su ciò che è necessario – 10.0.0.0/8 è inattuabile perché l'indirizzamento 10 viene utilizzato anche all'interno di {{site.data.keyword.cloud_notm}} per i servizi di backend): `<Domain>`
  * **Customer-side VPN Hardware & Version**: `<Hardware and Version number>`
  * **Customer-side VPN Contact** (nome e indirizzo email del contatto tecnico): 
    * `<Name>` 
    * `<Title>` 
    * `<Email Address>`

  **Facoltativo** (apporta modifiche solo se i seguenti valori predefiniti non sono adatti):

  *Parametri IKE/ISAKMP (Fase I)*

  * **Encryption Method**: IKEv1
  * **IKE Encryption / Encryption Algorithm**: AES-256
  * **Authentication Algorithm**: SHA1
  * **DH-Group**: Gruppo 5
  * **Security Association Lifetime (seconds)**: 1d (86400 secondi)

  *Parametri IPSEC (Fase II)*

  * **IPsec Encryption / Encryption Algorithm**: AES-256
  * **Authentication Algorithm**: SHA1
  * **DH-Group** (if using PF-Secrecy): Gruppo 5
  * **Security Association Lifetime (seconds)**: 3600 secondi

Dopo aver ricevuto la tua richiesta, i tecnici {{site.data.keyword.cloud_notm}} apriranno le porte appropriate del firewall ed inseriranno in whitelist l'indirizzo IP fornito. La comunicazione e la risoluzione alla richiesta verranno effettuate tramite il ticket del caso di supporto {{site.data.keyword.cloud_notm}}.

![Accesso di rete pubblico a {{site.data.keyword.cloud_notm}}](images/public_connection_vpn.png)
