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

# Daten in {{site.data.keyword.Bluemix_notm}} migrieren
{: #migration}

Sie können Daten aus einer Datendatei in einem Dateiformat mit Begrenzern (CSV oder TXT), die sich in einem lokalen Netzwerk oder in einem Objektspeicher (Amazon S3 oder {{site.data.keyword.Bluemix_notm}} Object Storage) befinden, in {{site.data.keyword.dashdblong}} laden. Sie können Ihre Daten sogar von einem lokalen System migrieren.
{: shortdesc}

## Daten aus dem Objektspeicher laden
{: #cos}

Um Daten von Amazon S3 zu laden, wählen Sie eine der folgenden Methoden aus:
  * Über die {{site.data.keyword.dashdbshort_notm}}-Webkonsole. **Laden > Amazon S3**. 
  * Direkt über die externen Tabellen. Im Folgenden ist eine SQL-Beispielanweisung dargestellt:

    ```
    INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
        (CCSID 1208 s3('s3.amazonaws.com', 
        '<S3-access-key-ID>',
        '<S3-secret-access-key>', 
        '<my_bucket>'
           )
      )      
    ```

Für das direkte Laden von Daten aus {{site.data.keyword.Bluemix_notm}} Object Storage mithilfe von externen Tabellen finden Sie hier eine SQL-Beispielanweisung:

```
INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net', 
  '<S3-access-key-ID>',
  '<S3-secret-access-key>', 
  '<my_bucket>'
     )
  )      
```

Wenn Sie {{site.data.keyword.Bluemix_notm}} Object Storage zum Erstellen von HMAC-Anmeldeinformationen beim Erstellen neuer Dienstanmeldeinformationen verwenden möchten, geben Sie {"HMAC:true"} im Feld *Inline-Konfigurationsparameter* hinzufügen an.
{: note}

Eine Demo mit einer Anleitung zum Laden von Daten aus {{site.data.keyword.Bluemix_notm}} Object Storage finden Sie in [{{site.data.keyword.dashdblong}} - Demo mit Anleitung zum Laden von Daten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud){:new_window}.

## Daten eines lokalen Systems migrieren
{: #onprem}

Um Ihre Daten von einem lokalen System zu migrieren, wählen Sie abhängig von der Größe Ihres Datasets eine der folgenden Methoden:
* Weniger als 25 TB Daten: [IBM Lift](#lift)
* Mehr als 25 TB Daten: [{{site.data.keyword.Bluemix_notm}} Mass Data Migration Service](#mdms)

### Lift
{: #lift}

Lift ist eine Anwendung, die Sie gebührenfrei nutzen können, um Ihre Daten aus verschiedenen Datenquellen, die in Tabelle 1 aufgelistet werden, zu {{site.data.keyword.Bluemix_notm}} zu migrieren. 

| Zieldatenbank in {{site.data.keyword.Bluemix_notm}} | Datenquelle |
|------------------------------|-------------|
| IBM Db2 Warehouse on Cloud   | IBM Db2 |
|                              | IBM Db2 Warehouse |
|                              | IBM Integrated Analytics System |
|                              | IBM PureData System for Analytics |
|                              | Oracle-Datenbank |
|                              | Microsoft SQL Server |
|                              | CSV-Dateiformat |
{: caption="Tabelle 1. Datenquellen für die Migration" caption-side="top"}

Weitere Informationen zum Herunterladen und Installieren von Lift finden Sie unter: [Lift herunterladen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.lift-cli.cloud.ibm.com/#download){:new_window}.

Schritt-für-Schritt-Anweisungen für die Migration von Daten auf {{site.data.keyword.Bluemix_notm}} mithilfe von Lift finden Sie hier: [Daten auf {{site.data.keyword.dashdblong}} migrieren ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.lift-cli.cloud.ibm.com/#docs){:new_window}.

### {{site.data.keyword.Bluemix_notm}} Mass Data Migration Service
{: #mdms}

Der {{site.data.keyword.Bluemix_notm}} Mass Data Migration Service (MDMS) kann genutzt werden, um die Daten großer IBM PureData Systems for Analytik (Netezza)-Datenbanken mit ca. 25 TB und mehr in eine vollständig verwaltete {{site.data.keyword.dashdblong}}-Datenbank auf {{site.data.keyword.Bluemix_notm}} zu migrieren.

MDMS bietet eine schnelle, einfache und sichere Möglichkeit, Terabytes bis Petabytes an Daten physisch auf {{site.data.keyword.Bluemix_notm}} zu übertragen. MDMS ist eine mobile Speichereinheit mit 120 TB nutzbarer Speicherkapazität. Mit dieser Einheit können Sie allgemeine Übertragungsprobleme wie hohe Kosten, lange Übertragungszeiten und hohe Sicherheitsrisiken mithilfe eines einzigen Services lösen.

![Ansicht der Mass Data Migration Service-Einheit](images/mdms.svg)

Weitere Informationen zur MDMS-Einheit (MDMS, Mass Data Migration Service) finden Sie in [Einführung in IBM Cloud Mass Data Migration](/docs/infrastructure/mass-data-migration?topic=mass-data-migration-getting-started-tutorial#getting-started-with-ibm-cloud-mass-data-migration){:new_window}.

Weitere Informationen zum Migrieren Ihrer Daten aus einer IBM PureData System for Analytics (Netezza)-Datenbank zu einer {{site.data.keyword.dashdblong}}-Datenbank mithilfe einer MDMS-Einheit können Sie über den Link zum folgenden Thema aufrufen: [Von IBM PureData System for Analytics (Netezza) migrieren](/docs/services/Db2whc/connecting?topic=Db2whc-pda#pda){:new_window}.

## Lernprogramm zur Migration von Daten aus lokalen relationalen Datenbanken
{: #tutorial}

In diesem Lernprogramm wird vermittelt, wie Daten aus lokalen relationalen Datenbanken für Business Analytics-Anwendungen in {{site.data.keyword.dashdbshort_notm}} migriert werden können. 

[Lernprogramm zum Hybrid-Data-Warehousing mit {{site.data.keyword.dashdbshort_notm}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/cloud/garage/tutorials/ibm-db2-warehouse-on-cloud/hybrid-data-warehousing-with-db-2-warehouse-on-cloud){:new_window}

