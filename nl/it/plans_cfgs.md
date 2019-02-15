---

copyright:
  years: 2014, 2019
lastupdated: "2018-12-07"

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

# Piani e configurazioni
{: #plans_cfgs}

Puoi scegliere un piano {{site.data.keyword.dashdbshort_notm}} configurato e ottimizzato per il lavoro che devi eseguire:
{: shortdesc}

   * Un piano d'ingresso per provare le funzionalità offerte. È una prova gratuita con un massimo di 1 GB di archiviazione. Consulta: [Limitazioni piano d'ingresso](#ep_restrictions)
   * I piani Flex in cui puoi indipendentemente ridimensionare le risorse di archiviazione e di calcolo
   * I piani SMP di diverse dimensioni per la produzione, piccolo, medio e grande, consistono in un singolo nodo e una singola istanza
   * Configurazioni cluster a più nodi MPP per l'elaborazione parallela e prestazioni elevate
   * Piani configurati per l'alta disponibilità
   * Compatibilità Oracle

Visualizza tutti i piani disponibili {{site.data.keyword.dashdbshort_notm}} nel catalogo [{{site.data.keyword.Bluemix}}](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window}.
<!--   * Plans configured for data warehouse and online analytical processing (OLAP) workloads: [{{site.data.keyword.dashdbshort_notm}}](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window} -->
<!--   * Plans configured for high-speed, transactional processing (OLTP): [{{site.data.keyword.dashdbshort_notm}} for Transactions](https://console.ng.bluemix.net/catalog/services/dashdb-for-transactions-sql-database){:new_window} -->

Guarda questo video per vedere un'introduzione al piano {{site.data.keyword.dashdbshort_notm}} Flex Performance.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Creating a connection from Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

Puoi richiedere che venga distribuito il tuo servizio {{site.data.keyword.dashdbshort_notm}} in un ambiente isolato dalla rete in {{site.data.keyword.Bluemix}}. Contatta [il settore Vendite di {{site.data.keyword.IBM_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window}.

Se nel catalogo non vedi una configurazione che risponda alle tue esigenze, contatta il settore Vendite di [{{site.data.keyword.IBM_notm}} ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window} per discutere delle altre opzioni.

## Disponibilità dei piani nei data center
{: #availability}

La seguente tabella fornisce le informazioni sulla disponibilità dei vari piani {{site.data.keyword.dashdbshort_notm}} per i data center ubicati in regioni geografiche:


| Piani {{site.data.keyword.dashdbshort_notm}} | Asia/Pacific | Europe    | North/Central America     | South America |
|------------------------------|--------------|-----------|-----------------------    |---------------|
| Flex                         | *NA          | Frankfurt | Washington D.C. (us-east) | *NA           |
|                              |              |           | Dallas (us-south)         |               |  
|      |||||
| SMP                          | Hong Kong    | Amsterdam | Washington D.C. (us-east) | Sao Paulo     |
|                              | Seoul        | Frankfurt | Dallas (us-south)         |               | 
|                              | Singapore    | London    | Montréal                  |               | 
|                              | Sydney       | Milan     | Querétaro                 |               | 
|                              | Tokyo        | Oslo      | Toronto                   |               | 
|                              |              | Paris     |                           |               |
|      |||||
| MPP                          | Hong Kong    | Amsterdam | Washington D.C. (us-east) | Sao Paulo     |
|                              | Seoul        | Frankfurt | Dallas (us-south)         |               | 
|                              | Singapore    | London    | Montréal                  |               | 
|                              | Sydney       | Milan     | Querétaro                 |               | 
|                              | Tokyo        | Oslo      | Toronto                   |               | 
|                              |              | Paris     |                           |               |
{: caption="Tabella 1. Data center che supportano i piani di servizio Db2 Warehouse on Cloud" caption-side="top"}

*NA = Non disponibile in questo momento

## Limitazioni piano d'ingresso 
{: #ep_restrictions}

Ti consigliamo fortemente di utilizzare un piano di servizio a livello aziendale invece di un piano di servizio d'ingresso per i carichi di lavoro di importanza critica o sensibili alle prestazioni.
{: important}

La seguente è una tabella delle limitazioni del piano d'ingresso {{site.data.keyword.dashdbshort_notm}}:

| Categoria | Voce | Limitazione | 
|----------|------|-------------|
| Risorse | Archiviazione | 20 GB di archiviazione per utente. Il piano è gratuito solo se viene utilizzato meno di 1 GB di archiviazione. |
|  | Connessioni | 50 connessioni per utente. Questo limite può venire modificato dinamicamente per conservare l'integrità di sistema dell'istanza. |
|  | Prestazioni | Le prestazioni potrebbero fluttuare a causa di carichi di lavoro eseguiti da altri utenti sul sistema a più tenant |
|  |  |
| Funzioni e funzionalità | Federazione | Non supportato |
|  | Compatibilità Oracle | Non supportato |
|  | Estensioni definite dall'utente (UDF) | Non supportato |
|  | Gestione degli utenti | Autorità di gestione non fornita all'utente |
|  | RCAC (Row and column access control) | Non supportato |
|  | IBM InfoSphere Data Replication da utilizzare nel caricamento dei dati | Non supportato |
|  |  |
| Ambiente di rete | IBM Cloud Integrated Analytics | Non supportato |
|  | IBM Cloud dedicato | Non supportato |
|  |  |
| Conformità di sicurezza | HIPAA (Health Information Portability and Accountability Act) del 1996 | Non supportato. Fai riferimento alla tua descrizione del servizio. |
|  | Regolamento generale sulla protezione dei dati EU (GDPR) | Nessuna limitazione specifica applicata |
|  |  |
| Gestione account | Riattivazione | Nessun requisito di riattivazione |
{: caption="Tabella 1. Limitazioni del piano d'ingresso {{site.data.keyword.dashdbshort_notm}} " caption-side="top"}
