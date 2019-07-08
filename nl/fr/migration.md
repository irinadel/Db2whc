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

# Chargement de données dans {{site.data.keyword.dashdbshort_notm}}
{: #loading_data}

Vous pouvez charger des données depuis un fichier de données dans un format délimité (CSV ou TXT) situé sur un réseau local ou dans un conteneur d'objets (Amazon S3 ou {{site.data.keyword.Bluemix_notm}} Object Storage) vers {{site.data.keyword.dashdblong}}. Vous pouvez même migrer vos données à partir d'un système sur site.
{: shortdesc}

## Chargement de données depuis un conteneur d'objets
{: #cos}

Pour charger des données depuis Amazon S3 ou {{site.data.keyword.Bluemix_notm}} Object Storage dans {{site.data.keyword.dashdblong}}, sélectionnez l'une des méthodes suivantes :
* Depuis la console Web {{site.data.keyword.dashdbshort_notm}} : **Charger > Amazon S3**. 
* Directement depuis des tables externes. Voici un exemple d'instruction SQL :

    ```
    INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
        (CCSID 1208 s3('s3.amazonaws.com',
        '<S3-access-key-ID>',
        '<S3-secret-access-key>',
        '<my_bucket>'
           )
      )      
    ```

  Pour charger les données depuis {{site.data.keyword.Bluemix_notm}} Object Storage en utilisant directement les tables externes, utilisez l'exemple d'instruction SQL ci-dessous :

  ```
  INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net', 
  '<S3-access-key-ID>',
  '<S3-secret-access-key>', 
  '<my_bucket>'
     )
    )      
  ```

  Pour {{site.data.keyword.Bluemix_notm}} Object Storage, pour créer des données d'identification HMAC lors de la création de nouvelles données d'identification de service, spécifiez {"HMAC:true"} dans la zone *Ajouter des paramètres de configuration en ligne*.
  {: note}

* Pour de meilleures performances, vous pouvez également utiliser la commande Db2 **LOAD** pour charger des données depuis Amazon S3 en vous basant sur l'exemple de commande suivant :

  ```
  CALL SYSPROC.ADMIN_CMD('LOAD FROM "S3::<amazon-s3-URL>::<s3-access-key-id>::<s3-secret-access-key>:
  :<s3-bucket-name>::<path-to-data-file>" OF <filetype> <additional-load-options> INTO <table-name>)
  ```

  Exemple d'utilisation de la commande Db2 **LOAD** :

  ```
  CALL SYSPROC.ADMIN_CMD('load from "S3::s3-us-west-2.amazonaws.com::<s3-access-key-id>:
  :<s3-secret-access-key>::ibm-state-store::bdidata2TB/web_site.dat" of DEL modified by codepage=1208 
  coldel0x7c WARNINGCOUNT 1000 MESSAGES ON SERVER INSERT into BDINSIGHTS2.web_site ');
  ```

  Pour les options de commande prises en charge, voir [Commande **LOAD**](https://www.ibm.com/support/knowledgecenter/en/SSEPGG_11.1.0/com.ibm.db2.luw.admin.cmd.doc/doc/r0008305.html){:external}. 

Pour une démonstration de chargement de données depuis {{site.data.keyword.Bluemix_notm}} Object Storage, voir [{{site.data.keyword.dashdblong}} guided demo: Explore data loading](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud){:external}

## Migration de données depuis un système sur site
{: #onprem}

Pour migrer vos données à partir d'un système sur site, choisissez l'une des méthodes suivantes selon la taille de votre jeu de données :
* Moins de 25 To de données : [IBM Lift](#lift)
* 25 To de données et plus : [{{site.data.keyword.Bluemix_notm}} Mass Data Migration Service](#mdms)

### Lift
{: #lift}

Lift est une application gratuite que vous pouvez utiliser pour migrer vos données dans {{site.data.keyword.Bluemix_notm}} à partir des différentes sources de données, répertoriées dans le tableau 1. 

| Base de données cible sur {{site.data.keyword.Bluemix_notm}} | Source de données |
|------------------------------|-------------|
| IBM Db2 Warehouse on Cloud   | IBM Db2 |
|                              | IBM Db2 Warehouse |
|                              | IBM Integrated Analytics System |
|                              | IBM PureData System for Analytics |
|                              | Oracle Database |
|                              | Microsoft SQL Server |
|                              | Format de fichier CSV |
{: caption="Tableau 1. Migration de sources de données" caption-side="top"}

Pour télécharger et installer Lift, voir [Download Lift](https://www.lift-cli.cloud.ibm.com/#download){:external}.

Pour des instructions pas à pas relatives à la migration de vos données dans {{site.data.keyword.Bluemix_notm}} à l'aide de Lift, voir [Migrate data to {{site.data.keyword.dashdblong}}](https://www.lift-cli.cloud.ibm.com/#docs){:external}.

### {{site.data.keyword.Bluemix_notm}} Mass Data Migration Service
{: #mdms}

Le périphérique {{site.data.keyword.Bluemix_notm}} MDMS (Mass Data Migration Service) peut-être utilisé pour migrer les données provenant de grosses bases de données IBM PureData Systems for Analytics (Netezza) de 25 To et plus vers une base de données {{site.data.keyword.dashdblong}} sur {{site.data.keyword.Bluemix_notm}}.

MDMS offre un moyen simple, rapide et sécurisé de transférer physiquement d'importants volumes de données (mesurés en téraoctets ou pétaoctets) vers {{site.data.keyword.Bluemix_notm}}. MDMS est un périphérique de stockage mobile proposant 120 To de capacité de stockage utilisable. Il vous permet de relever les défis posés quotidiennement par le transfert de gros volumes d'informations : coûts élevés, temps de transfert longs et problèmes de sécurité – tout ceci, dans un seul et même service.

![Vue du périphérique Mass Data Migration Service](images/mdms.svg)

Pour plus d'informations sur le périphérique MDMS, voir le [tutoriel d'initiation](/docs/infrastructure/mass-data-migration?topic=mass-data-migration-getting-started-tutorial#getting-started-with-ibm-cloud-mass-data-migration){:external}.

Pour plus d'informations sur la migration de vos données depuis une base de données IBM PureData System for Analytics (Netezza) vers une base de données {{site.data.keyword.dashdblong}} à l'aide du périphérique MDMS, voir [Migration depuis IBM PureData System for Analytics (Netezza)](/docs/services/Db2whc/connecting?topic=Db2whc-pda#pda){:external}.

## Tutoriel : Migration des données depuis des bases de données relationnelles sur site
{: #tutorial}

Ce tutoriel indique comment faire migrer vos données d'une base de données relationnelle sur site vers {{site.data.keyword.dashdbshort_notm}} pour les applications d'analyse commerciale. 

[Création d'entrepôts de données hybrides avec {{site.data.keyword.dashdbshort_notm}}](https://www.ibm.com/cloud/garage/tutorials/ibm-db2-warehouse-on-cloud/hybrid-data-warehousing-with-db-2-warehouse-on-cloud){:external}

