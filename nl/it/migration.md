---

copyright:
  years: 2014, 2018
lastupdated: "2018-05-08"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Migrazione di dati a IBM Cloud
{: #migration}

Puoi caricare i dati da un file di dati in un formato delimitato (CSV o TXT) ubicato su una rete locale o in un archivio oggetti (Amazon S3 o IBM Cloud Object Storage) su {{site.data.keyword.dashdblong}}. Puoi anche migrare i tuoi dati da un sistema in loco.
{: shortdesc}

## Caricamento di dati dall'archivio oggetti
{: #cos}

Per caricare dati da Amazon S3, seleziona uno dei seguenti metodi:
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

Per caricare dati da IBM Cloud Object Storage utilizzando direttamente le tabelle esterne, viene qui di seguito riportata un'istruzione SQL di esempio:

```
INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net',
  '<S3-access-key-ID>',
  '<S3-secret-access-key>',
  '<my_bucket>'
     )
  )      
```

**Nota:** per IBM Cloud Object Storage, per creare le credenziali HMAC quando si creano nuove credenziali di servizio, specifica, {"HMAC:true"} nel campo *Aggiungi parametri di configurazione inline*.

## Migrazione di dati da un sistema in loco
{: #onprem}

Per migrare i tuoi dati da un sistema in loco, scegli uno dei seguenti metodi, a seconda della dimensione del tuo dataset:
* Meno di 25 TB di dati: [IBM Lift](#lift)
* 25 TB di dati o più: [IBM Cloud Mass Data Migration Service](#mdms)

### Lift
{: #lift}

Lift è un'applicazione che puoi utilizzare gratuitamente per migrare i tuoi dati a {{site.data.keyword.Bluemix_notm}} dalle diverse origini dati elencate nella Tabella 1. 

| Database di destinazione su IBM Cloud | Origine dati |
|------------------------------|-------------|
| IBM Db2 Warehouse on Cloud   | IBM Db2 |
|                              | IBM Db2 Warehouse |
|                              | IBM Integrated Analytics System |
|                              | IBM PureData System for Analytics |
|                              | Database Oracle |
|                              | Microsoft SQL Server |
|                              | Formato file CSV |
{: caption="Tabella 1. Origini dati di migrazione" caption-side="top"}

Per scaricare e installare Lift, consulta [Download Lift ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://lift.ng.bluemix.net/#download){:new_window}.

Per istruzioni dettagliate sulla migrazione dei tuoi dati a {{site.data.keyword.Bluemix_notm}} utilizzando Lift, consulta: [Migrate data to {{site.data.keyword.dashdblong}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://lift.ng.bluemix.net/#docs){:new_window}.

### IBM Cloud Mass Data Migration Service
{: #mdms}

IBM Cloud MDMS (Mass Data Migration Service) può essere utilizzato per migrare i dati da grandi database IBM PureData Systems for Analytics (Netezza) di circa 25 TB e più a un database {{site.data.keyword.dashdblong}} completamente gestito su {{site.data.keyword.Bluemix_notm}}.

MDMS offre un modo sicuro, veloce e semplice per trasferire fisicamente terabyte, o anche petabyte, di dati a {{site.data.keyword.Bluemix_notm}}. MDMS è un dispositivo di archiviazione mobile con 120 TB di capacità di archiviazione utilizzabile. Questo dispositivo ti consente di superare le comuni sfide presentate dai trasferimenti quali i costi elevati, i lunghi tempi di trasferimento e le preoccupazioni inerenti alla sicurezza, e tutto questo in un singolo servizio.

![Vista del dispositivo Mass Data Migration Service](images/mdms.svg)

Per ulteriori informazioni sul dispositivo MDMS, consulta: [Introduzione a IBM Cloud Mass Data Migration](/docs/infrastructure/mass-data-migration/index.html#getting-started-with-ibm-cloud-mass-data-migration){:new_window}.

Per informazioni sulla migrazione dei tuoi dati da un database IBM PureData System for Analytics (Netezza) a un database {{site.data.keyword.dashdblong}} utilizzando il dispositivo MDMS, consulta: [Migrazione da IBM PureData System for Analytics (Netezza)](/docs/services/Db2whc/pda_db2whc_mdms.html).

