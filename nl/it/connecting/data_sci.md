---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-15"

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

# Data science
{: #ds}

Puoi anche
connettere applicazioni e strumenti esterni a {{site.data.keyword.dashdbshort_notm}} e
utilizzarli per un'ulteriore gestione o analisi dei dati. 
{: shortdesc}

## Watson Studio
{: #watson_studio}

Dopo aver creato un progetto in IBM Watson Studio (precedentemente noto come Data Science Experience), aggiungi gli asset dei dati ad esso in modo da poter utilizzare i dati. Tutti i collaboratori del progetto sono automaticamente autorizzati ad accedere ai dati del progetto.
{: shortdesc}

Il modo in cui aggiungi i dati e da dove puoi aggiungerli differisce tra i progetti legacy e IBM Watson. I progetti IBM Watson utilizzano {{site.data.keyword.Bluemix_notm}} Object Storage. Il progetto è un progetto legacy se utilizza Object Storage OpenStack Swift. 

### Per creare una nuova connessione in un progetto IBM Watson:

1. Fai clic su **Add to project > Connection**.
    
2. Scegli un'origine dati.
    
3. Immetti le informazioni di connessione richieste per l'origine dati. Normalmente, devi fornire informazioni come l'host, il numero di porta, il nome utente e la password.
    
4. Puoi rilevare gli asset dalle connessioni a {{site.data.keyword.dashdbshort_notm}}, che ti dà la possibilità di aggiungere tutte le tabelle dalla connessione come asset di dati ad un progetto. Seleziona **Discover data assets** e scegli un progetto.
    
5. Fai clic su **Create**. La connessione viene visualizzata nella pagina **Assets**.

Guarda questo video per vedere come creare una connessione e aggiungere i dati collegati a un progetto.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Crea una connessione e aggiungi i dati collegati a un progetto" type="text/html" width="640" height="390" src="//www.youtube.com/embed/U7-gCbo4QtM?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

### Per creare una nuova connessione in un progetto legacy:

1. Dalla pagina **Assets** del tuo progetto, fai clic sull'icona **Find and add data**.
    
2. Nel pannello **Connections**, fai clic su **Create Connection**.

3. Immetti un nome e una descrizione e scegli una categoria del servizio:

   **Data Service** = Servizio dati {{site.data.keyword.Bluemix_notm}}

   Quando scegli **Data Service**, i servizi dati {{site.data.keyword.Bluemix_notm}} esistenti vengono visualizzati nell'elenco **Service Instance**.

4. Scegli il servizio o il server di database dall'elenco.

5. Immetti le informazioni di connessione:

   Quando scegli **Data Service**, i servizi dati {{site.data.keyword.Bluemix_notm}} esistenti vengono visualizzati nell'elenco **Service Instance**.
    
6. Fai clic su **Create**. La connessione è disponibile per tutti i progetti legacy.
    
7. Nel pannello **Connections**, seleziona la connessione e fai clic su **Apply**.

Per aggiungere una connessione esistente ad un progetto legacy:

1. Dalla pagina **Assets** del tuo progetto, fai clic sull'icona **Find and add data**.
    
2. Nel pannello **Connections**, seleziona la connessione e fai clic su **Apply**.

## SPSS Statistics
{: #spss_stats}

Queste istruzioni spiegano come creare una connessione da IBM® SPSS® Statistics a un database {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Prerequisiti
{: #prereq1}

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](connecting.html#prereqs) necessari.

### Procedura
{: #proc1}

1. In SPSS Statistics, fai clic su **File > Open Database > New Query**.
    
2. Nella procedura guidata Database, fai clic su **Add ODBC data source**.
    
3. Utilizza la finestra ODBC Data Source Administrator per aggiungere un nome dell'origine dati (DSN) ODBC per il database {{site.data.keyword.dashdbshort_notm}}:
        
   a. Nella scheda **User DSN**, fai clic su **Add**.

   b. Nella finestra Create New Data Source, seleziona il driver denominato **IBM DB2 ODBC DRIVER** e fai clic su **Finish**.

   Assicurati che il driver selezionato non sia un driver con un nome simile come ad esempio `IBM DB2® ODBC DRIVER - DB2COPY`. Se il driver non compare nell'elenco, esci da SPSS Statistics, quindi scarica e installa il driver. Consulta [Pacchetto del driver Db2](driver_pkg.html).
        
   c. Nella finestra ODBC IBM Driver - Add, immetti un nome dell'origine dati (normalmente il nome del database a cui ti stai collegando) e fai clic su **Add**.
        
   d. Dalla finestra CLI/ODBC Settings, nella scheda **Data Source**, immetti l'ID utente e la password dalle [informazioni di connessione](credentials.html) che hai raccolto in precedenza.
        
   e. Nella pagina Advanced Settings, per ognuno dei seguenti parametri, fai clic su **Add** per aprire la finestra Add CLI Parameter ed iniziare la procedura e fai clic su **OK** per tornare alla pagina Advanced Settings:
            
   - Seleziona il parametro `Database` e fai clic su **OK** per aprire la finestra CLI/ODBC Settings. Nel campo **Pending Value**, immetti il nome del database dalle informazioni di connessione che hai raccolto in precedenza.

   - Seleziona il parametro `Hostname` e fai clic su **OK** per aprire la finestra CLI/ODBC Settings. Nel campo **Pending Value**, immetti il nome host dalle informazioni di connessione che hai raccolto in precedenza.

   - Seleziona il parametro `Port` e fai clic su **OK** per aprire la finestra CLI/ODBC Settings. Nel campo **Pending Value**, immetti il numero di porta dalle informazioni di connessione che hai raccolto in precedenza.
            
   - Seleziona il parametro `Protocol` e fai clic su **OK** per aprire la finestra CLI/ODBC Settings. Seleziona **TCP/IP**.
        
   f. Fai clic su **OK** per tornare alla finestra ODBC Data Source Administrator.
        
   g. Nella scheda **User DSN**, seleziona il nome dell'origine dati e fai clic su **Configure**.
        
   h. Nella finestra CLI/ODBC Settings, fai clic su **Connect** per verificare la connessione.
            
   - Se la connessione ha esito positivo, fai clic su **OK** per ritornare alla finestra ODBC Data Source Administrator e fai poi clic su **OK** per uscire dalla finestra.
            
   - Se la connessione non ha esito positivo, trova e correggi tutti gli errori prima di verificare nuovamente la connessione.

## SAS
{: #sas}

Queste istruzioni spiegano come creare una connessione da SAS a un database {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Prerequisiti
{: #prereq2}

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](connecting.html#prereqs) necessari.

### Procedura
{: #proc2}

Per i passi su come eseguire la connessione da SAS a un database {{site.data.keyword.dashdbshort_notm}}, consulta la documentazione SAS:
- [SAS/ACCESS Interface to DB2 under UNIX and PC Hosts ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://documentation.sas.com/?docsetId=acreldb&docsetTarget=p1dzq4zjg1iycgn16l4xj9nnvibt.htm&docsetVersion=9.4&locale=en){:new_window}

## Ambiente di sviluppo R
{: #r_dev_env}

Invece di utilizzare l'ambiente RStudio® integrato in IBM Watson Studio, potresti preferire utilizzare il tuo ambiente di sviluppo R installato localmente. Ad esempio, potresti avere la tua installazione di RStudio o preferire di utilizzare qualche altro strumento di sviluppo come Rcmdr o Rattle. Queste istruzioni spiegano come collegare un ambiente di sviluppo R a un database {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Prerequisiti
{: #prereq3}

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](connecting.html#prereqs) necessari.

### Procedura
{: #proc3}

1. Nel tuo ambiente R locale, installa il pacchetto `ibmdbR` immettendo il seguente comando:

   `install.packages("ibmdbR")`

   Il tuo ambiente R locale accede al Comprehensive R Archive Network (CRAN) e scarica automaticamente e installa il pacchetto `ibmdbR` e tutti i pacchetti prerequisiti che non sono già installati.
    
2. Crea una connessione driver ODBC tra il tuo ambiente di sviluppo R e il tuo database {{site.data.keyword.dashdbshort_notm}}:
        
   a. [Set up your database as an ODBC data source ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_cli_and_odbc_applications.html){:new_window}.
        
   b. Apri il tuo ambiente di sviluppo R installato localmente.
        
   c. Al prompt di R, immetti le seguenti istruzioni per creare la connessione. Sostituisci i segnaposti con le [informazioni di connessione](credentials.html) che hai raccolto in precedenza.

   - Se il tuo ambiente di sviluppo R installato localmente è in esecuzione nel database {{site.data.keyword.dashdbshort_notm}}:

     ```
     library(ibmdbR)
     host.name <- "placeholderForYourHostName"
     port <-"placeholderForPortNumber" # 50000 if not using SSL or 50001 if using SSL
     user.name <-"placeholderForYourUserName"
     pwd <- "placeholderForYourPassword"
     con.text <- paste("placeholderForYourDSNName;DRIVER=BLUDB",
                       ";Database=BLUDB",
                       ";Hostname=",host.name,
                       ";Port=",port,
                       ";PROTOCOL=TCPIP",
                       ";UID=", user.name,
                       ";PWD=",pwd,sep="")
     # Connect to using a odbc Driver Connection string to a remote database
     con <- idaConnect(con.text)
     ```

   - Se il tuo ambiente di sviluppo R installato localmente non è in esecuzione nel database {{site.data.keyword.dashdbshort_notm}}:

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
     # Connect to using a odbc Driver Connection string to a remote database
     con <- idaConnect(con.text)
     ```

     **Nota**: l'istruzione che viene utilizzata per creare l'oggetto di connessione utilizza il metodo `idaConnect()`, non i metodi `odbcConnect()` o `odbcDriverConnect()`.
        
   d. Inizializza il pacchetto di analisi immettendo il seguente comando R:

   `idaInit(con)`

   e. Per verificare se la connessione è in esecuzione, immetti il seguente comando R:

   `idaShowTables()`

   La console visualizza un elenco di tutte le tabelle e viste nello schema corrente.

