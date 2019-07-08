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

# Supporto SSL (Secure Sockets Layer)
{: #ssl_support}

Il database {{site.data.keyword.dashdbshort_notm}} utilizza un certificato per le connessioni SSL che viene emesso da un'autorità di certificazione (CA) digitale di terze parti. 
{: shortdesc}

Il certificato CA fa parte del pacchetto del driver Db2. Se la tua applicazione si collega a un driver dal pacchetto del driver Db2, non devi scaricare il certificato separatamente. Puoi scaricare il pacchetto del driver Db2 dalla console web.

Tuttavia, se la tua applicazione dispone di un proprio driver, potresti dover scaricare il certificato separatamente. Puoi scaricare il certificato dalla console web.

SSL (Secure Sockets Layer) è un protocollo di sicurezza che fornisce la privacy delle comunicazioni. SSL abilita le applicazioni client e server a comunicare in un modo progettato per evitare intrusioni, manomissioni e contraffazioni dei messaggi. Le applicazioni client abilitate SSL utilizzano tecniche di crittografia standard per garantire la comunicazione protetta.

La configurazione delle tue applicazioni per il collegamento al tuo database {{site.data.keyword.dashdbshort_notm}} con SSL dipende dalla tua politica aziendale. Puoi utilizzare i protocolli SSL e standard per il collegamento al database ed entrambi trasmettono i nomi utente e le password come dati crittografati. Se vuoi garantire la sicurezza end-to-end completa, trasmetti tutte le informazioni del database, inclusi i dati sensibili e i metadati, tramite una connessione SSL. Gli amministratori possono rendere obbligatorie le connessioni SSL modificando un'impostazione sulla console web.


