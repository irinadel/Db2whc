---

copyright:
  years: 2014, 2018
lastupdated: "2018-10-24"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Visualizzazione dati/BI
{: #overview}

Puoi anche
connettere applicazioni e strumenti esterni a {{site.data.keyword.dashdbshort_notm}} e
utilizzarli per un'ulteriore gestione o analisi dei dati. 
{: shortdesc}

## Cognos Analytics
{: #cognos}

Puoi eseguire i report IBM Cognos® sui dati nel cloud piuttosto che sui dati in un database in loco. Dopo aver caricato i tuoi dati in un database {{site.data.keyword.dashdbshort_notm}}, configura il driver JDBC e utilizza gli strumenti di gestione Cognos per creare la connessione al database. <!--These instructions explain how to connect to the database from Cognos version 10.2.1.-->
{: shortdesc}

Guarda questo video per vedere come creare una connessione.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Creating a connection from Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TRUEPVHGi0s?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

Per ulteriori informazioni, consulta [Connecting Cognos Analytics ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/support/knowledgecenter/en/SSEP7J_11.0.0/com.ibm.swg.ba.cognos.ug_cra.doc/c_create_ds.html#create_ds){:new_window}

## Looker
{: #looker}

Puoi collegare Looker a un database {{site.data.keyword.dashdbshort_notm}}. Looker è un'applicazione di business intelligence e una piattaforma di analisi big data con cui puoi esplorare, analizzare e condividere le analisi di business in tempo reale.
{: shortdesc}

[Connecting Looker ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://docs.looker.com/setup-and-management/connecting-to-db){:new_window}

## Tableau
{: #tableau}

Queste istruzioni illustrano come collegare Tableau a un database {{site.data.keyword.dashdbshort_notm}} e applicarlo al Tableau Desktop<!--version 8.x-->, ma puoi utilizzare istruzioni simili per altri strumenti Tableau.
{: shortdesc}

### Prerequisiti

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](connecting.html#prereqs) necessari.

### Procedura

1. In Tableau Desktop, apri la finestra o la pagina nel tuo strumento che utilizzi per definire una connessione al database.
2. Dalla pagina iniziale, fai clic su **Connect to data**.
3. Dall'elenco **Data Sources**, seleziona l'origine dati o il driver da utilizzare per la tua connessione al database. Nella sezione **On a server** dell'elenco, seleziona **IBM Db2**.
4. Dalla finestra **IBM DB2 Connection**, immetti le informazioni di connessione utilizzando la seguente tabella.

| Campo Tableau | Campo informazioni connessione Db2 |
|---------------|-----------------------------------|
| Passo 1: Immetti un nome server | Nome host |
| Passo 2: Porta | Numero porta |
| Passo 3: Immetti un database sul server | Nome database |
| Nome utente | ID utente |
| Password | Password |
{: caption="Tabella 1. Campi in Tableau per le informazioni di connessione" caption-side="top"}

5. Fare clic su **Connect** per stabilire la connessione. Tableau offre diverse opzioni per la connessione ai tuoi dati. Per utilizzare in modo completo il tuo database {{site.data.keyword.dashdbshort_notm}}, scegli l'opzione **Connect Live**.

## Microsoft Excel
{: #excel}

Queste istruzioni spiegano come collegare Microsoft Excel <!--2010-->a un database {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Prerequisiti

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](connecting.html#prereqs) necessari.

Devi disporre del pacchetto del driver Db2 o IBM® Data Server installato sul tuo computer locale. 

**Limitazione**: le connessioni tra Excel e {{site.data.keyword.dashdbshort_notm}} sono supportate solo sul sistema operativo Windows.

### Procedura

1. Nella console web, vai alla pagina **Run SQL**.
    
2. Immetti una o più istruzioni SELECT nella casella di testo dell'editor.

3. Fai clic su una delle opzioni Run.

4. Fai clic su **Excel ODC File**.

5. Scarica a apri il file `BLUExcel.odc` in Excel. Se viene visualizzato un avviso di sicurezza, fai clic su **Enable**.

6. Fa clic su **Open** per il collegamento al database {{site.data.keyword.dashdbshort_notm}}. Viene visualizzata la finestra di dialogo **Connect To DB2 Database**.

7. Immetti l'ID utente e la password che utilizzi per accedere a {{site.data.keyword.dashdbshort_notm}}. Per ottenere l'ID utente e la password, fai clic su **Connect** nella console web o su **Connect > Connection Information**.

8. Assicurati che la modalità di connessione sia `Share` e poi fai clic su **OK**.

### Risultati

I risultati della query vengono visualizzati in un foglio di calcolo Excel. Questi sono gli stessi risultati visualizzati nel visualizzatore dei risultati. Ora puoi generare grafici e report e analizzare i tuoi dati utilizzando Excel. Per ulteriori informazioni su come eseguire questa attività e su come eseguire le query SQL sui tuoi dati dalla console web, consulta: 
- [Tutorial: Generating charts and reports by using Excel ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/explore_excel_reports.html){:new_window}
- [Analyzing with Excel ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/exploreexcel.html){:new_window}

## Esri ArcGIS for Desktop
{: #esri_arcgis}

Puoi collegare Esri ArcGIS per Desktop <!--version 10.3.1 -->a un database {{site.data.keyword.dashdbshort_notm}} e poi utilizzarlo per analizzare e visualizzare i dati geospaziali.
{: shortdesc}

### Prerequisiti

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](connecting.html#prereqs) necessari.

Devi disporre del pacchetto del driver Db2 o IBM® Data Server installato sul tuo computer.

### Procedura

1. Determina il tuo DSN ODBC dalle [informazioni di connessione](credentials.html) che hai annotato in precedenza.

2. Crea una nuova connessione:
      
   a. Nella struttura ad albero ArcCatalog Catalog, apri il nodo Database Connections e fai clic su **Add Database Connection**.
        
   b. Nella procedura guidata Database Connections:
   - Seleziona **DB2** dall'elenco a discesa Database Platform.
   - Immetti la seguente stringa nel campo **Data source**:
     ```
     HostName=<hostname>;Port=<port>;Database=<database>;
     CLIENTBUFFERSUNBOUNDLOBS=1;LOBCACHESIZE=50000000;
     FET_BUF_SIZE=256K  
     ```

     dove `<hostname>`, `<port>` e `<database>` sono segnaposto che rappresentano il nome host, il numero di porta e il nome del database che hai annotato in precedenza.
            
   - Seleziona **Database authentication** come tipo di autenticazione.
            
   - Specifica il nome utente e la password (l'ID utente e la password che hai annotato in precedenza) nei campi corrispondenti.
            
   - Premi **OK**.
        
     ![Procedura guidata Database Connections](images/2_gs_conn.jpg)

### Risultati

Il componente ArcCatalog di Esri ArcGIS for Desktop è ora collegato al tuo database {{site.data.keyword.dashdbshort_notm}}. 


