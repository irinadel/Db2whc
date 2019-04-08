---

copyright:
  years: 2014, 2019
lastupdated: "2018-11-20"

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

# Migration des données vers {{site.data.keyword.Bluemix_notm}}
{: #migration}

Vous pouvez charger des données depuis un fichier de données dans un format délimité (CSV ou TXT) situé sur un réseau local ou dans un conteneur d'objets (Amazon S3 ou {{site.data.keyword.Bluemix_notm}} Object Storage) vers {{site.data.keyword.dashdblong}}. Vous pouvez même migrer vos données à partir d'un système sur site.
{: shortdesc}

## Chargement de données depuis un conteneur d'objets
{: #cos}

Pour charger des données depuis Amazon S3, sélectionnez l'une des méthodes suivantes :
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

Pour accéder à une démonstration présentant comment charger des données depuis {{site.data.keyword.Bluemix_notm}} Object Storage, consultez la page [{{site.data.keyword.dashdblong}} guided demo: Explore data loading ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud){:new_window}.

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

Pour télécharger et installer, voir : [Download Lift CLI![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://lift.ng.bluemix.net/#download){:new_window}.

Pour des instructions pas à pas relatives à la migration de vos données dans {{site.data.keyword.Bluemix_notm}} en utilisant Lift, voir : [Migrate data to {{site.data.keyword.dashdblong}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://lift.ng.bluemix.net/#docs){:new_window}.

### {{site.data.keyword.Bluemix_notm}} Mass Data Migration Service
{: #mdms}

Le périphérique {{site.data.keyword.Bluemix_notm}} MDMS (Mass Data Migration Service) peut-être utilisé pour migrer les données provenant de grosses bases de données IBM PureData Systems for Analytics (Netezza) de 25 To et plus vers une base de données {{site.data.keyword.dashdblong}} sur {{site.data.keyword.Bluemix_notm}}.

MDMS offre un moyen simple, rapide et sécurisé de transférer physiquement d'importants volumes de données (mesurés en téraoctets ou pétaoctets) vers {{site.data.keyword.Bluemix_notm}}. MDMS est un périphérique de stockage mobile proposant 120 To de capacité de stockage utilisable. Il vous permet de relever les défis posés quotidiennement par le transfert de gros volumes d'informations : coûts élevés, temps de transfert longs et problèmes de sécurité – tout ceci, dans un seul et même service.

![Vue du périphérique Mass Data Migration Service](images/mdms.svg)

Pour en savoir plus sur le périphérique MDMS, voir : 
- [Initiation à {{site.data.keyword.Bluemix_notm}} Mass Data Migration](/docs/infrastructure/mass-data-migration/getting-started.html#getting-started-with-ibm-cloud-mass-data-migration){:new_window}.

Pour savoir comment faire migrer vos données d'une base de données IBM PureData System for Analytics (Netezza) vers une base de données {{site.data.keyword.dashdblong}} à l'aide du périphérique MDMS, voir : 
- [Migration depuis IBM PureData System for Analytics (Netezza)](/docs/services/Db2whc/pda_db2whc_mdms.html){:new_window}.

## Tutoriel : Migration des données depuis des bases de données relationnelles sur site
{: #tutorial}

Ce tutoriel indique comment faire migrer vos données d'une base de données relationnelle sur site vers {{site.data.keyword.dashdbshort_notm}} pour les applications d'analyse commerciale. 

[Création d'entrepôts de données hybrides avec {{site.data.keyword.dashdbshort_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud/garage/tutorials/ibm-db2-warehouse-on-cloud/hybrid-data-warehousing-with-db-2-warehouse-on-cloud){:new_window}

