---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-15"

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

# Data Science
{: #ds}

Sie können auch externe Anwendungen und Tools mit {{site.data.keyword.dashdbshort_notm}} verbinden und diese zur weiteren Verwaltung und Analyse der Daten verwenden. 
{: shortdesc}

## Watson Studio
{: #watson_studio}

Nach dem Erstellen eines Projekts in IBM Watson Studio (früher Data Science Experience) fügen Sie Datenassets hinzu, um mit den Daten arbeiten zu können. Alle Projektteilnehmer sind automatisch zu einem Zugriff auf die Daten im Projekt berechtigt.
{: shortdesc}

Die Vorgehensweise beim Hinzufügen von Daten und die Positionen für die Daten variieren, je nachdem, ob es sich um ältere Projekte oder IBM Watson-Projekte handelt. Bei IBM Watson-Projekten wird {{site.data.keyword.Bluemix_notm}} Object Storage verwendet. Als ältere Projekte werden Projekte bezeichnet, bei denen Object Storage OpenStack Swift verwendet wird. 

### Gehen Sie wie folgt vor, um eine neue Verbindung in einem IBM Watson-Projekt zu erstellen:

1. Klicken Sie auf **Zu Projekt hinzufügen > Verbindung**.
    
2. Wählen Sie eine Datenquelle aus.
    
3. Geben Sie die Verbindungsinformationen ein, die für Ihre Datenquelle erforderlich sind. In der Regel müssen Sie Informationen wie den Host, die Portnummer, den Benutzernamen und das Kennwort angeben.
    
4. Sie können Assets aus Verbindungen zu {{site.data.keyword.dashdbshort_notm}} aufspüren. Dies ermöglicht es Ihnen, alle über eine Verbindung verfügbaren Tabellen als Datenassets zu einem Projekt hinzuzufügen. Wählen Sie **Datenassets aufspüren** und anschließend ein Projekt aus.
    
5. Klicken Sie auf **Erstellen**. Die Verbindung wird auf der Seite **Assets** angezeigt.

In dem folgenden Video erfahren Sie, wie eine Verbindung erstellt wird und verbundene Daten zu einem Projekt hinzugefügt werden können.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Create a connection and add connected data to a project" type="text/html" width="640" height="390" src="//www.youtube.com/embed/U7-gCbo4QtM?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

### Gehen Sie wie folgt vor, um eine neue Verbindung in einem älteren Projekt zu erstellen:

1. Klicken Sie auf der Seite **Assets** Ihres Projekts auf das Symbol **Daten suchen und hinzufügen**.
    
2. Klicken Sie im Fenster **Verbindungen** auf **Verbindung erstellen**.

3. Geben Sie einen Namen und eine Beschreibung ein und wählen Sie eine Servicekategorie aus:

   **Datenservice** = {{site.data.keyword.Bluemix_notm}}-Datenservice

   Wenn Sie **Datenservice** auswählen, werden Ihre vorhandenen {{site.data.keyword.Bluemix_notm}}-Datenservices in der Liste der **Serviceinstanzen** angezeigt.

4. Wählen Sie den Service oder Datenbankserver in der Liste aus.

5. Geben Sie die Verbindungsinformationen ein:

   Wenn Sie **Datenservice** auswählen, werden Ihre vorhandenen {{site.data.keyword.Bluemix_notm}}-Datenservices in der Liste der **Serviceinstanzen** angezeigt.
    
6. Klicken Sie auf **Erstellen**. Die Verbindung ist für alle älteren Projekte verfügbar.
    
7. Wählen Sie die Verbindung im Fenster **Verbindungen** aus und klicken Sie auf **Anwenden**.

Gehen Sie wie folgt vor, um eine vorhandene Verbindung zu einem älteren Projekt hinzuzufügen:

1. Klicken Sie auf der Seite **Assets** Ihres Projekts auf das Symbol **Daten suchen und hinzufügen**.
    
2. Wählen Sie die Verbindung im Fenster **Verbindungen** aus und klicken Sie auf **Anwenden**.

## SPSS Statistics
{: #spss_stats}

Im Folgenden wird beschrieben, wie Sie eine Verbindung von IBM® SPSS® Statistics zu einer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen.
{: shortdesc}

### Voraussetzungen
{: #prereq11}

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](/docs/services/Db2whc/connecting/connecting.html#prereqs) erfüllt werden.

### Vorgehensweise
{: #proc11}

1. Klicken Sie in SPSS Statistic auf **Datei > Datenbank öffnen > Neue Abfrage**.
    
2. Klicken Sie im Datenbankassistenten auf **ODBC-Datenquelle hinzufügen**.
    
3. Fügen Sie über das Fenster 'ODBC-Datenquellenadministrator' einen ODBC-Datenquellennamen (DSN) für die {{site.data.keyword.dashdbshort_notm}}-Datenbank hinzu:
        
   a. Klicken Sie auf der Registerkarte **Benutzer-DSN** auf **Hinzufügen**.

   b. Wählen Sie im Fenster 'Neue Datenquelle erstellen' den Treiber mit der Bezeichnung **IBM DB2 ODBC DRIVER** aus und klicken Sie auf **Fertigstellen**.

   Achten Sie darauf, dass Sie nicht versehentlich einen Treiber mit einer ähnlichen Bezeichnung, z. B. `IBM DB2® ODBC DRIVER - DB2COPY`, ausgewählen. Ist der Treiber nicht in der Liste enthalten, beenden Sie SPSS Statistics. Laden Sie dann den Treiber herunter und installieren Sie ihn. Weitere Informationen hierzu finden Sie im Abschnitt zum [Db2-Treiberpaket](/docs/services/Db2whc/connecting/driver_pkg.html).
        
   c. Geben Sie im Fenster 'ODBC IBM Driver - Hinzufügen' einen Datenquellennamen (im Allgemeinen der Name der Datenbank, zu der Sie eine Verbindung herstellen) ein und klicken Sie auf **Hinzufügen**.
        
   d. Geben Sie auf der Registerkarte **Datenquelle** im Fenster 'CLI/ODBC-Einstellungen' die Benutzer-ID und das Kennwort aus den [Verbindungsinformationen](/docs/services/Db2whc/connecting/credentials.html) ein, die Sie zuvor ermittelt haben.
        
   e. Klicken Sie auf der Seite 'Erweiterte Einstellungen' für jeden der folgenden Parameter auf **Hinzufügen**, um das Fenster 'CLI-Parameter hinzufügen' zu öffnen und mit dem Hinzufügen zu beginnen. Klicken Sie auf **OK**, um zur Seite 'Erweiterte Einstellungen' zurückzukehren:
            
   - Wählen Sie den Parameter `Database` aus und klicken Sie anschließend auf **OK**, um das Fenster 'CLI/ODBC-Einstellungen' zu öffnen. Geben Sie im Feld **Anstehender Wert** den Datenbanknamen aus den Verbindungsinformationen ein, die Sie zuvor ermittelt haben.

   - Wählen Sie den Parameter `Hostname` aus und klicken Sie anschließend auf **OK**, um das Fenster 'CLI/ODBC-Einstellungen' zu öffnen. Geben Sie im Feld **Anstehender Wert** den Hostnamen aus den Verbindungsinformationen ein, die Sie zuvor ermittelt haben.

   - Wählen Sie den Parameter `Port` aus und klicken Sie anschließend auf **OK**, um das Fenster 'CLI/ODBC-Einstellungen' zu öffnen. Geben Sie im Feld **Anstehender Wert** die Portnummer aus den Verbindungsinformationen ein, die Sie zuvor ermittelt haben.
            
   - Wählen Sie den Parameter `Protocol` aus und klicken Sie anschließend auf **OK**, um das Fenster 'CLI/ODBC-Einstellungen' zu öffnen. Wählen Sie **TCP/IP** aus.
        
   f. Klicken Sie auf **OK**, um zum Fenster 'ODBC-Datenquellenadministrator' zurückzukehren.
        
   g. Wählen Sie auf der Registerkarte **Benutzer-DSN** den Datenquellennamen aus und klicken Sie anschließend auf **Konfigurieren**.
        
   h. Klicken Sie im Fenster 'CLI/ODBC-Einstellungen' auf **Verbinden**, um die Verbindung zu testen.
            
   - Klicken Sie auf **OK**, wenn die Verbindung ordnungsgemäß eingerichtet ist, um zum Fenster 'ODBC-Datenquellenadministrator' zurückzukehren. Klicken Sie anschließend auf **OK**, um das Fenster zu schließen.
            
   - Wurde die Verbindung nicht ordnungsgemäß eingerichtet, notieren Sie sich alle Fehler und beheben Sie sie, bevor Sie die Verbindung erneut testen.

## SAS
{: #sas}

Im Folgenden wird beschrieben, wie Sie eine Verbindung von SAS zu einer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen.
{: shortdesc}

### Voraussetzungen
{: #prereq12}

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](/docs/services/Db2whc/connecting/connecting.html#prereqs) erfüllt werden.

### Vorgehensweise
{: #proc12}

Schrittweise Anleitungen für Verbindungen von SAS zu einer {{site.data.keyword.dashdbshort_notm}}-Datenbank finden Sie in der SAS-Dokumentation:
- [Abschnitt zur SAS/ACCESS-Schnittstelle zu Db2 unter UNIX- und PC-Hosts ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://documentation.sas.com/?docsetId=acreldb&docsetTarget=p1dzq4zjg1iycgn16l4xj9nnvibt.htm&docsetVersion=9.4&locale=en){:new_window}

## R-Entwicklungsumgebung
{: #r_dev_env}

Möglicherweise ziehen Sie der in IBM Watson Studio integrierten RStudio®-Umgebung eine eigene, lokal installierte R-Entwicklungsumgebung vor. Sie verfügen beispielsweise möglicherweise über eine eigene RStudio-Installation oder ziehen ein anderes Entwicklungstool wie Rcmdr oder Rattle vor. Im Folgenden wird beschrieben, wie Sie eine R-Entwicklungsumgebung mit einer {{site.data.keyword.dashdbshort_notm}}-Datenbank verbinden können.
{: shortdesc}

### Voraussetzungen
{: #prereq13}

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](/docs/services/Db2whc/connecting/connecting.html#prereqs) erfüllt werden.

### Vorgehensweise
{: #proc13}

1. Installieren Sie in der lokalen R-Umgebung mit dem folgenden Befehl das Paket `ibmdbR`:

   `install.packages("ibmdbR")`

   Die lokale R-Umgebung greift auf CRAN (Comprehensive R Archive Network) zu und lädt das Paket `ibmdbR` sowie alle vorausgesetzten Pakete, die noch nicht installiert sind, automatisch herunter und installiert sie.
    
2. Erstellen Sie eine ODBC-Treiberverbindung zwischen der R-Entwicklungsumgebung und der {{site.data.keyword.dashdbshort_notm}}-Datenbank:
        
   a. [Richten Sie Ihre Datenbank als ODBC-Datenquelle ein ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_cli_and_odbc_applications.html){:new_window}.
        
   b. Öffnen Sie die lokal installierte R-Entwicklungsumgebung.
        
   c. Geben Sie zum Erstellen der Verbindung in der R-Eingabeaufforderung die im Folgenden aufgeführten Anweisungen ein. Ersetzen Sie dabei die Platzhalter durch die [Verbindungsinformationen](/docs/services/Db2whc/connecting/credentials.html), die Sie zuvor ermittelt haben.

   - Lokal installierte R-Entwicklungsumgebung, die in der {{site.data.keyword.dashdbshort_notm}}-Datenbank ausgeführt wird:

     ```
     library(ibmdbR)
     host.name <- "placeholderForYourHostName"
     port <-"placeholderForPortNumber" # 50000 ohne SSL, 50001 für SSL-Verbindung
     user.name <-"placeholderForYourUserName"
     pwd <- "placeholderForYourPassword"
     con.text <- paste("placeholderForYourDSNName;DRIVER=BLUDB",
                       ";Database=BLUDB",
                       ";Hostname=",host.name,
                       ";Port=",port,
                       ";PROTOCOL=TCPIP",
                       ";UID=", user.name,
                       ";PWD=",pwd,sep="")
     # Über Verbindungszeichenfolge Verbindung zu ferner Datenbank herstellen
     con <- idaConnect(con.text)
     ```

   - Lokal installierte R-Entwicklungsumgebung, die nicht in der {{site.data.keyword.dashdbshort_notm}}-Datenbank ausgeführt wird:

     ```
     library(ibmdbR)
     driver.name <- "{placeholderForYourDriverName}"
     db.name <- "placeholderForYourDatabaseName"
     host.name <- "placeholderForYourHostName"
     port <-"placeholderForYourPort"
     user.name <-"placeholderForYourUserName"
     pwd <- "placeholderForYourPassword"
     con.text <- paste("placeholderForYourDSNName;DRIVER=",driver.name,
                       ";Database=",db.name,
                       ";Hostname=",host.name,
                       ";Port=",port,
                       ";PROTOCOL=TCPIP",
                       ";UID=", user.name,
                       ";PWD=",pwd,sep="")
     # Über Verbindungszeichenfolge Verbindung zu ferner Datenbank herstellen
     con <- idaConnect(con.text)
     ```

     **Hinweis**: Bei der Anweisung zum Erstellen des Verbindungsobjekts wird die Methode `idaConnect()`, nicht die Methode `odbcConnect()` oder `odbcDriverConnect()` verwendet.
        
   d. Initialisieren Sie das Analysepaket, indem Sie den folgenden R-Befehl ausgeben:

   `idaInit(con)`

   e. Testen Sie die Verbindung mit dem folgenden R-Befehl:

   `idaShowTables()`

   In der Konsole wird eine Liste mit allen Tabellen und Ansichten im aktuellen Schema angezeigt.

