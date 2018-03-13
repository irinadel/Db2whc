---

copyright:
  years: 2014, 2018
lastupdated: "2017-07-27"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Informazioni su Db2 Warehouse on Cloud
{: #overview}

Nei piani del servizio {{site.data.keyword.dashdblong}}, utilizza il data warehouse per memorizzare i dati relazionali, inclusi i tipi speciali. Analizza i tuoi dati, o i dati caricati da altri servizi cloud,
utilizzando la nostra analisi integrata oppure connettendo delle tue applicazioni. Puoi avvalerti della tecnologia di database in memoria ad elevate
prestazioni con tabelle a colonne per i carichi di lavoro di analisi. La console web {{site.data.keyword.dashdbshort_notm}} gestisce
le comuni attività di gestione dei dati, ad esempio il caricamento di dati, e le attività di analisi come l'esecuzione di query e di script
R.
{: shortdesc}

Puoi anche
connettere applicazioni e strumenti esterni a {{site.data.keyword.dashdbshort_notm}} e
utilizzarli per un'ulteriore gestione o analisi dei dati. Ad esempio:
   * Connetti {{site.data.keyword.IBM_notm}} InfoSphere® Data Architect per progettare e distribuire il tuo schema di database.
<!--   * Connect Esri ArcGIS to perform geospatial analytics and map publishing with your data. -->
   * Connetti un server {{site.data.keyword.IBM_notm}} Cognos® per eseguire i report Cognos sui tuoi dati.
   * Connetti gli strumenti basati su SQL quali Tableau, Microstrategy o Microsoft Excel per manipolare o analizzare i tuoi dati.
   * Connetti le tue applicazioni {{site.data.keyword.Bluemix_short}} che necessitano di
un database di analisi.
   * Connetti Aginity Workbench per migrare i modelli di dati e i dati Netezza® a {{site.data.keyword.dashdbshort_notm}}.

## Servizio gestito Db2 Warehouse on Cloud
{: #managed_service}

Il servizio pienamente gestito di {{site.data.keyword.dashdbshort_notm}} gestisce tutti
gli aggiornamenti software, gli aggiornamenti del sistema operativo e la manutenzione hardware. Il servizio include un monitoraggio dell'integrità sette giorni alla settimana, 24 ore su 24. In caso di malfunzionamento hardware o software, il servizio viene riavviato automaticamente.
{: shortdesc}

Per ulteriori informazioni sugli aspetti del servizio gestito di {{site.data.keyword.dashdbshort_notm}}, vedi: [Servizio gestito da {{site.data.keyword.dashdbshort_notm}} ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/managed_service.html).

## Piani e configurazioni
{: #plans_cfgs}

Puoi scegliere un piano {{site.data.keyword.dashdbshort_notm}} configurato e ottimizzato per il lavoro che devi eseguire:
{: shortdesc}

   * Un piano d'ingresso per provare le funzionalità offerte
   * Piani piccoli, medi e grandi per la produzione
   * Configurazioni MPP per l'elaborazione parallela
   * Piani configurati per l'alta disponibilità o per la compatibilità Oracle
   * E altro ...

Visualizza i piani disponibili nel catalogo {{site.data.keyword.Bluemix}}:
   * Piani configurati per i carichi di lavoro di immagazzinamento (warehouse) e analisi dei dati (OLAP): [{{site.data.keyword.dashdbshort_notm}}](https://console.bluemix.net/catalog/services/db2-warehouse-on-cloud?env_id=ibm:yp:us-south){:new_window}
<!--   * Plans configured for high-speed, transactional processing (OLTP): [{{site.data.keyword.dashdbshort_notm}} for Transactions](https://console.ng.bluemix.net/catalog/services/dashdb-for-transactions-sql-database){:new_window} -->

Se nel catalogo non vedi una configurazione che risponda alle tue esigenze, contatta il settore Vendite di [{{site.data.keyword.IBM_notm}} ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window} per discutere delle altre opzioni.

## Provisioning di Db2 Warehouse on Cloud
{: #whse_provision}

È possibile eseguire il provisioning del database {{site.data.keyword.dashdbshort_notm}} su {{site.data.keyword.BluSoftlayer_full}} e per AWS.
{: shortdesc}

Se vuoi che venga eseguito il provisioning del data warehouse per AWS, seleziona il piano **MPP Small for AWS**.

<!-- If you want to have the data warehouse provisioned for AWS, select the **{{site.data.keyword.IBM_notm}} {{site.data.keyword.dashdbshort_notm}} for Analytics MPP Small for AWS** plan. -->

<!-- ##dashDB for Transactions
{: #dashDB_tr}

In the {{site.data.keyword.dashdbshort_notm}} for Transactions plans, use the {{site.data.keyword.dashdbshort_notm}} relational database for online transaction processing. You can connect new or existing applications, and you can begin processing transactions and storing your data. With DB2® and Oracle compatibility, you can connect small or large applications and benefit from a managed enterprise-class database system. You can leverage the {{site.data.keyword.dashdbshort_notm}} for Transactions web console to manage users, load data, and get connection information.
{: shortdesc} -->

<!-- ##dashDB web console overview
{: #console_overview}

You can manage your {{site.data.keyword.dashdbshort_notm}} database, analyze your data, and monitor sensitive data with the {{site.data.keyword.dashdbshort_notm}} web console accessible from {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Open the web console by clicking the service tile on your application overview page, and then click **Open**.

Single sign-on authentication connects you directly to the web console. You can access connection information from the web console, and the **Downloads** page includes links to client drivers for accessing {{site.data.keyword.dashdbshort_notm}} from remote applications. You can also access sample data and reports.

###Sensitive data reporting

The {{site.data.keyword.dashdbshort_notm}} web console includes a sensitive data reporting feature that detects and monitors sensitive objects in the {{site.data.keyword.dashdbshort_notm}} data warehouse, such as credit card numbers and US Social Security numbers.

To run and view reports that identify columns that contain sensitive data and provide information about connections and activities that access the sensitive data, select **Monitor &gt; Sensitive Data** in the web console. -->


<!-- ##IBM Analytics Services
{: #analytics_services}

For more information about {{site.data.keyword.IBM_notm}} analytics services and finding your local services representative, see: [{{site.data.keyword.IBM_notm}} Analytics Services ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/software/data/services/).
{: shortdesc} -->














