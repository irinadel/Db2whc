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

# Daten zu IBM Cloud migrieren
{: #migration}

Sie können Daten aus einer Datendatei in einem begrenzten Format (CSV oder TXT), die sich in einem lokalen Netzwerk oder in einem Objektspeicher (Amazon S3 oder IBM Cloud Object Storage) in {{site.data.keyword.dashdblong}} laden. Sie können Ihre Daten sogar von einem lokalen System migrieren.
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

Um Daten aus IBM Cloud Object Storage mithilfe von externen Tabellen direkt zu laden, finden Sie hier eine Beispiel-SQL-Anweisung:

```
INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net', 
  '<S3-access-key-ID>',
  '<S3-secret-access-key>', 
  '<my_bucket>'
     )
  )      
```

**Hinweis:** Wenn Sie IBM Cloud Object Storage zum Erstellen von HMAC-Anmeldeinformationen beim Erstellen neuer Dienstanmeldeinformationen verwenden möchten, geben Sie {"HMAC:true"} im Feld *Inline-Konfigurationsparameter* hinzufügen an.

## Daten von einem lokalen System migrieren
{: #onprem}

Um Ihre Daten von einem lokalen System zu migrieren, wählen Sie abhängig von der Größe Ihres Datasets eine der folgenden Methoden:
* Weniger als 25 TB Daten: [IBM Lift](#lift)
* Mehr als 25 TB Daten: [IBM Cloud Mass Data Migration Service](#mdms)

### Lift
{: #lift}

Lift ist eine Anwendung, die Sie gebührenfrei nutzen können, um Ihre Daten aus verschiedenen Datenquellen, die in Tabelle 1 aufgelistet werden, zu {{site.data.keyword.Bluemix_notm}} zu migrieren. 

| Zieldatenbank auf IBM Cloud | Datenquelle |
|------------------------------|-------------|
| IBM Db2 Warehouse on Cloud   | IBM Db2 |
|                              | IBM Db2 Warehouse |
|                              | IBM Integrated Analytics System |
|                              | IBM PureData System for Analytics |
|                              | Oracle-Datenbank |
|                              | Microsoft SQL Server |
|                              | CSV-Dateiformat |
{: caption="Tabelle 1. Datenquellen für die Migration" caption-side="top"}

Weitere Informationen zum Herunterladen und Installieren von Lift finden Sie unter: [Lift herunterladen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://lift.ng.bluemix.net/#download){:new_window}.

Schritt-für-Schritt-Anweisungen für die Migration von Daten auf {{site.data.keyword.Bluemix_notm}} mithilfe von Lift finden Sie hier: [Daten auf {{site.data.keyword.dashdblong}} migrieren ![für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://lift.ng.bluemix.net/#docs){:new_window}.

### IBM Cloud Mass Data Migration Service
{: #mdms}

Der IBM Mass Data Migration Service (MDMS) kann genutzt werden, um die Daten großer IBM PureData Systems for Analytik (Netezza)-Datenbanken mit ca. 25 TB und mehr in eine vollständig verwaltete {{site.data.keyword.dashdblong}}-Datenbank auf {{site.data.keyword.Bluemix_notm}} zu migrieren.

MDMS bietet eine schnelle, einfache und sichere Möglichkeit, Terabytes bis Petabytes an Daten physisch auf {{site.data.keyword.Bluemix_notm}} zu übertragen. MDMS ist eine mobile Speichereinheit mit 120 TB nutzbarer Speicherkapazität. Mit dieser Einheit können Sie allgemeine Übertragungsprobleme wie hohe Kosten, lange Übertragungszeiten und hohe Sicherheitsrisiken mithilfe eines einzigen Services lösen.

![Ansicht der Mass Data Migration Service-Einheit](images/mdms.svg)

Weitere Informationen zur MDMS-Einheit finden Sie unter: [Einführung in IBM Cloud Mass Data Migration](/docs/infrastructure/mass-data-migration/index.html#getting-started-with-ibm-cloud-mass-data-migration){:new_window}.

Weitere Informationen zum Migrieren Ihrer Daten aus einer IBM PureData System for Analytics (Netezza)-Datenbank zu einer {{site.data.keyword.dashdblong}}-Datenbank mithilfe einer MDMS-Einheit finden Sie unter: [Von IBM PureData System for Analytics (Netezza) migrieren](/docs/services/Db2whc/pda_db2whc_mdms.html).

