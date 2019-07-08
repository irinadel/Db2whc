---

copyright:
  years: 2014, 2019
lastupdated: "2019-05-08"

keywords: Db2 Warehouse on Cloud, loading data, object store, IBM Cloud Object Storage, Amazon S3, LOAD command, Mass Data Migration Service (MDMS), migration, Lift

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

# Caricamento di dati a {{site.data.keyword.dashdbshort_notm}}
{: #loading_data}

Puoi caricare i dati da un file di dati in un formato delimitato (CSV o TXT) ubicato su una rete locale o in un archivio oggetti (Amazon S3 o {{site.data.keyword.Bluemix_notm}} Object Storage) su {{site.data.keyword.dashdblong}}. Puoi anche migrare i tuoi dati da un sistema in loco.
{: shortdesc}

## Caricamento di dati da un archivio oggetti
{: #cos}

Per caricare i dati da Amazon S3 o {{site.data.keyword.Bluemix_notm}} Object Storage a {{site.data.keyword.dashdblong}}, seleziona uno dei seguenti metodi:
* Console web {{site.data.keyword.dashdbshort_notm}} . **Load > Amazon S3**. 
* Direttamente dalle tabelle esterne. Il seguente è un esempio di istruzione SQL:

    ```
    INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
        (CCSID 1208 s3('s3.amazonaws.com', 
        '<S3-access-key-ID>',
        '<S3-secret-access-key>', 
        '<my_bucket>'
           )
      )      
    ```

  Per caricare dati da {{site.data.keyword.Bluemix_notm}} Object Storage utilizzando direttamente le tabelle esterne, viene qui di seguito riportata un'istruzione SQL di esempio:

  ```
  INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net',
  '<S3-access-key-ID>',
  '<S3-secret-access-key>',
  '<my_bucket>'
     )
    )      
  ```

  Per {{site.data.keyword.Bluemix_notm}} Object Storage, per creare le credenziali HMAC quando si creano nuove credenziali di servizio, specifica, {"HMAC:true"} nel campo *Aggiungi parametri di configurazione inline*.
  {: note}

* Per prestazioni migliorate, è anche possibile utilizzare il comando **LOAD** Db2 per caricare i dati da Amazon S3 utilizzando il seguente comando di esempio:

  ```
  CALL SYSPROC.ADMIN_CMD('LOAD FROM "S3::<amazon-s3-URL>::<s3-access-key-id>::<s3-secret-access-key>:
  :<s3-bucket-name>::<path-to-data-file>" OF <filetype> <additional-load-options> INTO <table-name>)
  ```

  Il seguente è un utilizzo di esempio di un comando **LOAD** Dn2:

  ```
  CALL SYSPROC.ADMIN_CMD('load from "S3::s3-us-west-2.amazonaws.com::<s3-access-key-id>:
  :<s3-secret-access-key>::ibm-state-store::bdidata2TB/web_site.dat" of DEL modified by codepage=1208
  coldel0x7c WARNINGCOUNT 1000 MESSAGES ON SERVER INSERT into BDINSIGHTS2.web_site ');
  ```

  Per le opzioni di comando supportate, vedi [**LOAD** command](https://www.ibm.com/support/knowledgecenter/en/SSEPGG_11.1.0/com.ibm.db2.luw.admin.cmd.doc/doc/r0008305.html){:external}. 

Per una demo guidata sul caricamento dei dati da {{site.data.keyword.Bluemix_notm}} Object Storage, consulta: [{{site.data.keyword.dashdblong}} guided demo: Explore data loading](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud){:external}

## Migrazione di dati da un sistema in loco
{: #onprem}

Per migrare i tuoi dati da un sistema in loco, scegli uno dei seguenti metodi, a seconda della dimensione del tuo dataset:
* Meno di 25 TB di dati: [IBM Lift](#lift)
* 25 TB di dati o più: [{{site.data.keyword.Bluemix_notm}} Mass Data Migration Service](#mdms)

### Lift
{: #lift}

Lift è un'applicazione che puoi utilizzare gratuitamente per migrare i tuoi dati a {{site.data.keyword.Bluemix_notm}} dalle diverse origini dati elencate nella Tabella 1. 

| Database di destinazione su {{site.data.keyword.Bluemix_notm}} | Origine dati |
|------------------------------|-------------|
| IBM Db2 Warehouse on Cloud   | IBM Db2 |
|                              | IBM Db2 Warehouse |
|                              | IBM Integrated Analytics System |
|                              | IBM PureData System for Analytics |
|                              | Database Oracle |
|                              | Microsoft SQL Server |
|                              | Formato file CSV |
{: caption="Tabella 1. Origini dati di migrazione" caption-side="top"}

Per scaricare e installare Lift, vedi [Download Lift](https://www.lift-cli.cloud.ibm.com/#download){:external}.

Per istruzioni dettagliate sulla migrazione dei tuoi dati a {{site.data.keyword.Bluemix_notm}} utilizzando Lift, vedi: [Migrate data to {{site.data.keyword.dashdblong}}](https://www.lift-cli.cloud.ibm.com/#docs){:external}.

### {{site.data.keyword.Bluemix_notm}} Mass Data Migration Service
{: #mdms}

{{site.data.keyword.Bluemix_notm}} MDMS (Mass Data Migration Service) può essere utilizzato per migrare i dati da grandi database IBM PureData Systems for Analytics (Netezza) di circa 25 TB e più a un database {{site.data.keyword.dashdblong}} completamente gestito su {{site.data.keyword.Bluemix_notm}}.

MDMS offre un modo sicuro, veloce e semplice per trasferire fisicamente terabyte, o anche petabyte, di dati a {{site.data.keyword.Bluemix_notm}}. MDMS è un dispositivo di archiviazione mobile con 120 TB di capacità di archiviazione utilizzabile. Questo dispositivo ti consente di superare le comuni sfide presentate dai trasferimenti quali i costi elevati, i lunghi tempi di trasferimento e le preoccupazioni inerenti alla sicurezza, e tutto questo in un singolo servizio.

![Vista del dispositivo Mass Data Migration Service](images/mdms.svg)

Per informazioni sul dispositivo MDMS, consulta: [Esercitazione introduttiva](/docs/infrastructure/mass-data-migration?topic=mass-data-migration-getting-started-tutorial#getting-started-with-ibm-cloud-mass-data-migration){:external}.

Per informazioni sulla migrazione dei tuoi dati da un database IBM PureData System for Analytics (Netezza) a un database {{site.data.keyword.dashdblong}} utilizzando il dispositivo MDMS, consulta: [Migrazione da IBM PureData System for Analytics (Netezza)](/docs/services/Db2whc/connecting?topic=Db2whc-pda#pda){:external}.

## Esercitazione: Migrazione dei dati dai database relazionali in loco
{: #tutorial}

Questa esercitazione illustra come migrare i dati dai database relazionali in loco in {{site.data.keyword.dashdbshort_notm}} per le applicazioni di analisi di business. 

[Immagazzinamento di dati ibridi con {{site.data.keyword.dashdbshort_notm}}](https://www.ibm.com/cloud/garage/tutorials/ibm-db2-warehouse-on-cloud/hybrid-data-warehousing-with-db-2-warehouse-on-cloud){:external}

