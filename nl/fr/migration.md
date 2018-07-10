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

# Migration de données vers IBM Cloud
{: #migration}

Vous pouvez charger des données à partir d'un fichier de données dans un format délimité tel que CSV ou TXT situé sur un réseau local ou dans un magasin de données (Amazon S3 ou IBM Cloud Object Storage) vers {{site.data.keyword.dashdblong}}. Vous pouvez même migrer vos données à partir d'un système sur site.
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

Pour charger les données depuis IBM Cloud Object Storage en utilisant directement des tables externes, prenez connaissance de l'instruction SQL exemple suivante :

```
INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net', 
  '<S3-access-key-ID>',
  '<S3-secret-access-key>', 
  '<my_bucket>'
     )
  )      
```

**Remarque :** pour IBM Cloud Object Storage, pour créer des données d'identification HMAC lors de la création de nouvelles données d'identification de service, spécifiez {"HMAC:true"} dans la zone *Ajouter des paramètres de configuration en ligne*.

## Migration de données depuis un système sur site
{: #onprem}

Pour migrer vos données à partir d'un système sur site, choisissez l'une des méthodes suivantes selon la taille de votre jeu de données :
* Moins de 25 To de données : [IBM Lift](#lift)
* 25 To de données et plus : [IBM Cloud Mass Data Migration Service](#mdms)

### Lift
{: #lift}

Lift est une application gratuite que vous pouvez utiliser pour migrer vos données dans {{site.data.keyword.Bluemix_notm}} à partir des différentes sources de données, répertoriées dans le tableau 1. 

| Base de données cible dans IBM Cloud | Source de données |
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

Pour des instructions pas à pas relatives à la migration de vos données dans {{site.data.keyword.Bluemix_notm}} en utilisant Lift, voir : [Migrate data to IBM Db2 Warehouse on Cloud or IBM Db2 on Cloud in 5 minutes](/docs/services/lift-cli/index.html#about-lift){:new_window}.

### Périphérique IBM Cloud MDMS (Mass Data Migration Service)
{: #mdms}

Le périphérique IBM Cloud MDMS (Mass Data Migration Service) peut-être utilisé pour migrer les données provenant de grosses bases de données IBM PureData Systems for Analytics (Netezza) de 25 To et plus vers une base de données {{site.data.keyword.dashdblong}} entièrement gérée sur {{site.data.keyword.Bluemix_notm}}.

MDMS offre un moyen simple, rapide et sécurisé de transférer physiquement d'importants volumes de données (mesurés en téraoctets ou pétaoctets) vers {{site.data.keyword.Bluemix_notm}}. MDMS est un périphérique de stockage mobile proposant 120 To de capacité de stockage utilisable. Il vous permet de relever les défis posés quotidiennement par le transfert de gros volumes d'informations : coûts élevés, temps de transfert longs et problèmes de sécurité – tout ceci, dans un seul et même service.

![Vue du périphérique Mass Data Migration Service](images/mdms.svg)

Pour plus d'informations sur le périphérique MDMS, voir : [Getting started with IBM Cloud Mass Data Migration](/docs/infrastructure/mass-data-migration/index.html#getting-started-with-ibm-cloud-mass-data-migration){:new_window}.

Pour plus d'informations sur la migration de vos données entre une base de données IBM PureData System for Analytics (Netezza) et une base de données {{site.data.keyword.dashdblong}} en utilisant le périphérique MDMS, voir [Migration depuis IBM PureData System for Analytics (Netezza)](/docs/services/Db2whc/pda_db2whc_mdms.html).

