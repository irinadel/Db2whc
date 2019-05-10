---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-24"

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

# Datenvisualisierung/Business Intelligence
{: #data_vis_bi}

Sie können auch externe Anwendungen und Tools mit {{site.data.keyword.dashdbshort_notm}} verbinden und diese zur weiteren Verwaltung und Analyse der Daten verwenden. 
{: shortdesc}

## Cognos Analytics
{: #cognos}

IBM Cognos®-Berichte lassen sich eher für Daten in der Cloud als für die Daten in einer lokalen Datenbank erstellen. Richten Sie nach dem Laden Ihrer Daten in eine {{site.data.keyword.dashdbshort_notm}}-Datenbank den JDBC-Treiber ein und erstellen Sie die Datenbankverbindung anschließend mit den Cognos Administration-Tools. <!--These instructions explain how to connect to the database from Cognos version 10.2.1.-->
{: shortdesc}

In dem folgenden Video erfahren Sie, wie eine Verbindung erstellt wird.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Creating a connection from Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TRUEPVHGi0s?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

Weitere Informationen hierzu finden Sie in dem Abschnitt zum Thema [Cognos Analytics verbinden![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/support/knowledgecenter/en/SSEP7J_11.0.0/com.ibm.swg.ba.cognos.ug_cra.doc/c_create_ds.html#create_ds){:new_window}.

## Looker
{: #looker}

Sie können Looker mit einer {{site.data.keyword.dashdbshort_notm}}-Datenbank verbinden. Bei Looker handelt es sich um eine Business-Intelligence-App und Plattform für Big-Data-Analyse für das Erkunden, Analysieren und gemeinsame Nutzen von echtzeitorientierten Geschäftsanalysen.
{: shortdesc}

Abschnitt zu [Looker-Verbindungen ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.looker.com/setup-and-management/connecting-to-db){:new_window}

## Tableau
{: #tableau}

Im Folgenden wird beschrieben, wie Sie Tableau mit einer {{site.data.keyword.dashdbshort_notm}}-Datenbank verbinden und die Verbindung in Tableau Desktop übernehmen können<!--version 8.x-->, die Vorgehensweise kann jedoch auch auf andere Tableau-Tools übertragen werden.
{: shortdesc}

### Voraussetzungen
{: #prereq8}

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) erfüllt werden.

### Vorgehensweise
{: #proc8}

1. Öffnen Sie in Tableau Desktop das Fenster bzw. die Seite in Ihrem Tool, über die Datenbankverbindungen definiert werden.
2. Klicken Sie auf der Startseite auf **Connect to data**.
3. Wählen Sie in der Liste der **Data Sources** die Datenquelle bzw. den Treiber aus, der für Ihre Datenbankverbindung verwendet werden soll. Wählen Sie im Bereich **On a server** der Liste **IBM Db2** aus.
4. Geben Sie im Fenster **IBM Db2 Connection** die Verbindungsinformationen (siehe nachfolgende Tabelle) ein.

| Tableau-Feld | Feld für Db2-Verbindungsinformationen |
|---------------|-----------------------------------|
| Schritt 1: Servernamen eingeben | Hostname |
| Schritt 2: Port | Portnummer |
| Schritt 3: Datenbank auf einem Server eingeben | Datenbankname |
| Benutzername | Benutzer-ID |
| Kennwort | Kennwort |
{: caption="Tabelle 1. Felder für Verbindungsinformationen in Tableau" caption-side="top"}

5. Klicken Sie auf **Connect**, um die Verbindung herzustellen. In Tableau stehen verschiedene Optionen für die Verbindung zu Ihren Daten zur Auswahl. Wählen Sie die Option **Live-Verbindung** aus, um einen umfassenden Zugriff auf die {{site.data.keyword.dashdbshort_notm}}-Datenbank zu erhalten.

## Microsoft Excel
{: #excel}

Im Folgenden wird beschrieben, wie Sie Microsoft Excel <!--2010--> mit einer {{site.data.keyword.dashdbshort_notm}}-Datenbank verbinden können.
{: shortdesc}

### Voraussetzungen
{: #prereq9}

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) erfüllt werden.

Auf Ihrem lokalen Computer muss das Db2-Treiberpaket oder das IBM Data Server Driver-Paket installiert sein. 

**Einschränkung**: Verbindungen zwischen Excel und {{site.data.keyword.dashdbshort_notm}} werden nur unter Windows-Betriebssystemen unterstützt.

### Vorgehensweise
{: #proc9}

1. Rufen Sie in der Webkonsole die Seite **SQL ausführen** auf.
    
2. Geben Sie Editortextfeld die gewünschten SELECT-Anweisungen ein.

3. Klicken Sie auf eine der Ausführungsoptionen.

4. Klicken Sie auf **Excel-ODC-Datei**.

5. Laden Sie die Datei `BLUExcel.odc` herunter und öffnen Sie sie in Excel. Wenn ein Sicherheitshinweis angezeigt wird, klicken Sie auf **Aktivieren**.

6. Klicken Sie auf **Öffnen**, um eine Verbindung zu der {{site.data.keyword.dashdbshort_notm}}-Datenbank herzustellen. Das Dialogfeld **Mit Db2-Datenbank verbinden** wird geöffnet.

7. Geben Sie die Kombination aus Benutzer-ID und Kennwort ein, die Sie für die Anmeldung bei {{site.data.keyword.dashdbshort_notm}} verwenden. Benutzer-ID und Kennwort können Sie abrufen, indem Sie in der Webkonsole auf **Verbinden** oder **Verbinden > Verbindungsinformationen** klicken.

8. Stellen Sie sicher, dass der Verbindungsmodus mit `Gemeinsam nutzen` definiert ist und klicken Sie dann auf **OK**.

### Ergebnisse
{: #results2}

Die Abfrageergebnisse werden in einem Excel-Arbeitsblatt angezeigt. Dabei handelt es sich um dieselben Ergebnisse, die auch in der Anzeigefunktion für Ergebnisse angezeigt werden. Sie können jetzt Diagramme und Berichte generieren und Ihre Daten in Excel analysieren. Weitere Informationen zur Vorgehensweise und zum Ausführen von SQL-Abfragen für Ihre Daten über die Webkonsole können Sie über die folgenden Links aufrufen: 
- [Lernprogramm zum Generieren von Diagrammen und Berichten in Excel ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/explore_excel_reports.html){:new_window}
- [Datenanalyse in Excel ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/exploreexcel.html){:new_window}

## Esri ArcGIS for Desktop
{: #esri_arcgis}

Sie können Esri ArcGIS for Desktop <!--version 10.3.1 --> mit einer {{site.data.keyword.dashdbshort_notm}}-Datenbank verbinden und anschließend über diese Verbindung Geodaten analysieren und darstellen.
{: shortdesc}

### Voraussetzungen
{: #prereq10}

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) erfüllt werden.

Auf Ihrem Computer muss das Db2-Treiberpaket oder das IBM Data Server Driver-Paket installiert sein.

### Vorgehensweise
{: #proc10}

1. Ermitteln Sie Ihre ODBC-DSN-Daten anhand der [Verbindungsinformationen](/docs/services/Db2whc/connecting?topic=Db2whc-db_details_cxn_creds#db_details_cxn_creds), die Sie zuvor notiert haben.

2. Erstellen Sie eine neue Verbindung:
      
   a. Öffnen Sie den Datenbankverbindungsknoten in der Baumstruktur des ArcCatalog-Katalogs und klicken Sie auf die Option zum Hinzufügen einer Datenbankverbindung****.
        
   b. Gehen Sie im Assistenten für Datenbankverbindungen wie folgt vor:
   - Wählen Sie in der Dropdown-Liste der Datenbankplattformen die Option **Db2** aus.
   - Geben Sie im Feld für die Datenquelle**** die folgende Zeichenfolge ein:
     ```
     HostName=<hostname>;Port=<port>;Database=<database>;
     CLIENTBUFFERSUNBOUNDLOBS=1;LOBCACHESIZE=50000000;
     FET_BUF_SIZE=256K  
     ```

     Dabei sind `<hostname>`, `<port>` und `<database>` Platzhalter für die Werte für Hostnamen, Portnummer und Datenbankname, die Sie zuvor notiert haben.
            
   - Wählen Sie als Authentifizierungstyp die **** Datenbankauthentifizierung aus.
            
   - Geben Sie in den entsprechenden Feldern Ihre Benutzer-ID und Ihr Kennwort ein, d. h. die zuvor notierte Kombination aus Benutzername und Kennwort.
            
   - Klicken Sie auf **OK**.
        
     ![Assistent für Datenbankverbindungen](images/2_gs_conn.jpg)

### Ergebnisse
{: #results3}

Die Esri ArcGIS for Desktop-Komponente 'ArcCatalog' ist nun mit Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank verbunden. 


