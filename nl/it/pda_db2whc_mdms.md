---

copyright:
  years: 2014, 2018
lastupdated: "2018-06-15"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Migrazione da IBM PureData System for Analytics (Netezza)
{: #pda}

{{site.data.keyword.Bluemix_notm}} MDMS (Mass Data Migration Service) può essere utilizzato per migrare i dati da grandi database IBM PureData Systems for Analytics (Netezza) di circa 25 TB e più a un database {{site.data.keyword.dashdblong}} completamente gestito su {{site.data.keyword.Bluemix_notm}}.

MDMS offre un modo sicuro, veloce e semplice per trasferire fisicamente terabyte, o anche petabyte, di dati a {{site.data.keyword.Bluemix_notm}}. MDMS è un dispositivo di archiviazione mobile con 120 TB di capacità di archiviazione utilizzabile. Questo dispositivo ti consente di superare le comuni sfide presentate dai trasferimenti quali i costi elevati, i lunghi tempi di trasferimento e le preoccupazioni inerenti alla sicurezza, e tutto questo in un singolo servizio.
{: shortdesc}

![Vista del dispositivo Mass Data Migration Service](images/mdms.svg)

## Cosa ti servirà quando richiedi un dispositivo
{: #prereq}

1. Impostazioni di rete per il dispositivo di archiviazione
   - Indirizzo IP statico
   - Maschera di rete per abilitare il trasferimento dati
2. Impostazioni di rete per il computer remoto
   - Indirizzo IP statico
   - Maschera di rete 
   - Gateway predefinito per accedere all'interfaccia utente (IU)
3. Destinazione di download di Cloud Object Storage <br/>
   **Importante**: per completare il modulo di richiesta, devi disporre di almeno un account {{site.data.keyword.cos_full}} e di un bucket in una sede degli Stati Uniti in più regioni o degli Stati Uniti Sud. Se non hai ancora un account {{site.data.keyword.cos_full_notm}}}, creane uno prima di richiedere il dispositivo MDMS. Per ulteriori informazioni, consulta: [Informazioni su {{site.data.keyword.cos_full}}](/docs/services/cloud-object-storage/about-cos.html){:new_window}.

## Passo 1: Creazione di una richiesta
{: #create-req}

1. Esegui l'accesso al [{{site.data.keyword.slportal}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://control.softlayer.com/){:new_window} utilizzando le tue credenziali univoche.
2. Seleziona **Storage > Data Migration > Mass Data Migration** dalla barra di navigazione per accedere alla pagina di destinazione MDMS.
3. Fai clic su **Request Device** per aprire il modulo d'ordine.
4. Completa ogni campo nel modulo d'ordine di **Mass Data Migration**.
   - **Shipping Address**: questo modulo non è precompilato e ogni campo è modificabile. Fornisci il nome della persona che accetterà la consegna del dispositivo nel campo Attention. Quando scegli il luogo di consegna, considera il peso del dispositivo (30 chili, ossia 66 libbre, con la sua custodia) e l'accessibilità. <br/> (**Nota**: il dispositivo è dotato di ruote e maniglia a scomparsa per manovrarlo).
   - **Key Migration Contacts**: questo modulo non è precompilato. Ogni campo è modificabile. Può essere aggiunta più di una persona.
   - **Data Center Network Configuration**: fornisci i dettagli di configurazione di rete per il pre-provisioning della porta Eth3 sul dispositivo MDMS prima della spedizione.
   - **Data Offload Destination**: seleziona il tuo account di destinazione esistente dall'elenco.
   - **Request Name**: immetti un nome per aiutarti a tracciare il tuo ordine.
5. Seleziona la casella di spunta **I have read and agree to the full terms of the Mass Data Migration Agreement** dopo aver letto ogni accordo di servizio che viene fornito.
6. Fai clic su **Place Request** per inoltrare la richiesta. Fai clic su **Cancel** per abbandonare completamente il modulo e tornare alla pagina di destinazione di MDMS.

## Passo 2: Preparazione e spedizione
{: #prep-ship}

Dopo l'inoltro della richiesta, lo stato del ticket di richiesta si presenta come *Processing Request*. Dopo che la tua richiesta è stata elaborata, {{site.data.keyword.IBM}} inizia a preconfigurare il successivo dispositivo disponibile e lo stato nella griglia [Requests ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://control.softlayer.com/storage/mdms){:new_window} mostrerà *Prepping Device* seguito da *Awaiting Shipment*. Dopo essere passata allo stato *Awaiting Shipment*, la tua richiesta non può essere più annullata. 

Il dispositivo viene prelevato dal corriere per essere inviato alla tua ubicazione. A questo punto, lo stato della richiesta viene aggiornato e diventa *Device Shipped*. Il numero di traccia viene condiviso con te nella sezione **Order Details** della griglia [Requests ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://control.softlayer.com/storage/mdms){:new_window}.

## Passo 3: Ricezione e connessione
{: #rec-con}

<!-- **[Editor's note: What to keep from this section immediately below?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
1. The device arrives pre-configured for you. Basic [powering/connectivity instructions](docs/infrastructure/mass-data-migration/user-instructions.html) are included.  **[Editor's note: Are the instructions included in the MDMS package? If so, are they different from the instructions found with the "powering/connectivity" link?]**<br/>
  **Note**: User name and storage pool password is provided separately. Check the **Request Details** in your [Requests ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/storage/mdms){:new_window} grid for the credentials.
2. Point your browser to the static IP address that you provided in the order form. **[Editor's note: Is this done on PDA? What system is the static IP address for?]**
3. Log in. Enter password to unlock the empty storage pool. **[Editor's note: How is this done?]**<br/>
   **Note**: See the **Request Details** of your [Requests ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/storage/mdms){:new_window} grid for the password.
4. Mount the NFS share on your server. **[Editor's note: How is this done?]**
5. Rerun your DataShuttle inventory to ensure any new files are captured. **[Editor's note: Is "DataShuttle inventory" a command that is run on PDA?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& -->

### Panoramica

Il dispositivo {{site.data.keyword.cloud}} Mass Data Migration è un dispositivo di archiviazione portatile in grado di presentare condivisioni NFS (Network File system) o FileNet CFS (Content Federation Services) e viene gestito tramite un'interfaccia del browser web. Il dispositivo viene spedito al tuo data center, caricato con i dati in sito, restituito a un data center {{site.data.keyword.BluSoftlayer_full}} e i tuoi dati vengono caricati nel tuo account {{site.data.keyword.cos_full}}.

### Alimentazione

Il dispositivo include un cavo di alimentazione C13-US ([IEC 60320 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://en.wikipedia.org/wiki/IEC_60320){:new_window}). Se il dispositivo viene utilizzato fuori dagli Stati Uniti, potrebbe essere necessario un adattatore di alimentazione.

Il dispositivo MDMS accetta tutte le gamme di potenza standard.
![Gamma di potenza](/images/PowerRating.png)

### Connettività Ethernet

Ci sono due connessioni Ethernet da realizzare. Una per la gestione dei dispositivi tramite un browser e una per lo spostamento dei dati sulla stessa sottorete in cui risiedono i dati di origine.

Entrambe le porte hanno origine dal dispositivo come RJ45 e sono forniti dei cavi CAT6A, Sono forniti degli adattatori SFP+ di rame per la conversione da RJ45. Gli adattatori funzionano con tutti i produttori di interruttori. Questi adattatori si trovano in una tasca sul lato inferiore del coperchio di spedizione.

- Eth1 (1GbE-B) viene utilizzato per la gestione del dispositivo e, pertanto, deve avere un gateway specificato nella configurazione dell'indirizzo IP. Ciò può essere visualizzato nella schermata LCD dopo l'accensione del dispositivo (consulta la sezione [Configurazione dell'indirizzo IP](#ip_cfg)).

- Eth3 (10GbE-B) viene utilizzato per il trasferimento dei dati. Questa connessione deve essere sulla stessa sottorete dei dati di origine o, se necessario, può essere connessa direttamente al server.

Se è richiesto un fattore di forma differente della connessione Ethernet, devi fornire il convertitore.

### Istruzioni dettagliate per l'utente

1. Il dispositivo MDMS arriva preconfigurato con i tuoi indirizzo IP e nome utente, pool di archiviazione bloccato e condivisione NFS. La password utente e la password del pool di archiviazione vengono comunicate tramite una e-mail separata.

2. Determina la posizione più appropriata in cui collocare il dispositivo, dove raggiungerà sia l'alimentazione che le tue connessioni Ethernet (1GbE e 10GbE) e con un calpestio minimo nelle sue prossimità.

3. Posiziona il dispositivo da connettere. Durante l'uso può rimanere nella custodia di trasporto. Assicurati che il dispositivo sia a temperatura ambiente e che non vi sia condensa su di esso. Connetti all'alimentazione utilizzando il cavo di alimentazione fornito sotto il coperchio della custodia. Accendi il dispositivo.<br/>
    **Nota**: ci sono due interruttori di alimentazione.
    ![Interruttori di alimentazione](/images/MDMSPowerSwitch.png)
    **Nota**: non è necessario rimuovere il dispositivo dalla custodia portatile.

4. Rimuovi il cavo CAT6A dal coperchio della custodia e connettilo alla porta Eth3 (10GbE-B) mostrata nella figura.
    ![Ubicazione delle porte Eth1 e Eth3](/images/MDMSNewEth1and3.png)

5. Connetti l'adattatore CAT6A/SFP+ fornito ed esegui la connessione al tuo interruttore da 10Gb.

6. Se l'indirizzo IP configurato per Eth3 può essere raggiunto tramite un `https://<your_Eth3_IP_Address>` del browser, continua al passo successivo. 

   Altrimenti, stabilisci una connessione alla porta Eth1 (1GbE-B). Apri il tuo browser e immetti `https://<your_Eth1_IP_Address>`. Immetti l'indirizzo IP Eth1 appropriato per la tua configurazione di rete. Accetta l'eccezione del certificato.<br/>
   **Nota**: se hai bisogno di modificare le impostazioni IP per Eth3 o Eth1, consulta la sezione [Configurazione dell'indirizzo IP](#ip_cfg).

7. Utilizza il nome utente e la password forniti per eseguire l'accesso.<br/>
    ![Pagina di accesso](/images/Login.png)

8. La procedura guidata del flusso di lavoro presenta l'accesso agli specifici elementi generalmente utilizzati nell'ordine da sinistra a destra.<br/>
    ![Icone del flusso di lavoro](/images/workflow.png) <br/>
    **NOTA**: il flusso di lavoro può essere riaperto utilizzando **Workflow Manager** nell'angolo superiore sinistro della GUI.

9. Attiva il pool di archiviazione preconfigurato:
    - Fai clic su **Unlock and Start Storage Pool**.
    - Immetti la tua passphrase del pool di archiviazione e fai clic su **OK**.
![Attiva pool di archiviazione](/images/UnlockPool.png)

10. Per impostazione predefinita, la condivisione ha entrambi i protocolli NFS e SMB abilitati senza limitazioni di accesso sulla condivisione. Per limitare l'accesso a questa condivisione (per NFS o SMB), fai clic con il tasto destro del mouse sul nome della condivisione e seleziona la voce di menu appropriata.<br/>
    ![Limita l'accesso alla condivisione](/images/ShareControls.png)

11. Quando il pool di archiviazione è abilitato, la condivisione NFS è disponibile per il montaggio. Nel flusso di lavoro, fai clic su **View Network Shares** per visualizzare la vista delle condivisioni di rete. Chiudi il flusso di lavoro, fai clic con il tasto destro del mouse sulla condivisione e seleziona **View Mount Command** per visualizzare il nome della condivisione e le informazioni di montaggio. Monta la condivisione sul tuo server di origine. Assicurati di specificare l'indirizzo IP del link da 10 GB quando monti la condivisione.
    ![Montaggio della condivisione](/images/MountCommand.png)

## Passo 4: Copia dei dati e spedizione
{: #copy-ship}

<!-- &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&

1. Run the DataShuttle copy to move the data. **[Editor's note: What is "DataShuttle"? Is "DataShuttle copy" a command that is run on PDA?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& -->

1. Copia i tuoi dati nella condivisione NFS. Scegli uno dei seguenti metodi per estrarre i tuoi dati dal tuo database Netezza.
    1. Esegui questo esempio del programma di utilità **nz_backup**:

       `/nz/support/contrib/bin/nz_backup –db <db_name> –d <target_directory>  ascii threads 4`

       **Nota**: la directory di destinazione (`<target_directory>`) è la condivisione NFS sul dispositivo MDMS che è montata sul server Netezza.
   
    2. Esegui il seguente esempio di un'istruzione CREATE EXTERNAL TABLE:

       `CREATE EXTERNAL TABLE '<path_to_mdms_device>/<file_name>' SELECT * FROM <table name>`

       **Nota:** se hai utilizzato le opzioni di clausola `USING` per l'esportazione dei dati, ricorda o salva le opzioni di clausola. La clausola viene riutilizzata successivamente durante il processo di caricamento della tabella esterna da IBM Cloud Object Storage.

       Per ulteriori informazioni sull'istruzione SQL, consulta: [CREATE EXTERNAL TABLE statement ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.sql.ref.doc/doc/r_create_ext_table.html){:new_window}. 

<!--       - Provide the {{site.data.keyword.Bluemix_notm}} team with the "USING" clause that was used for data export. The clause is reused during the load process on {{site.data.keyword.Bluemix_notm}}.
       - Select FORMAT = "Text"
-->

2. Nel flusso di lavoro, fai clic su **View Network Activity** per visualizzare il caricamento Ethernet in entrata nella GUI mentre i dati vengono trasferiti al dispositivo sul collegamento da 10Gb/sec.
    ![Visualizza l'attività](/images/UserGuide13.png)

3. Nel flusso di lavoro, fai clic su **View Storage Pools** per monitorare l'utilizzo dell'archiviazione e l'IOPS sul dispositivo.
    ![Visualizza i pool di archiviazione](/images/UserGuide14.png)

4. Una volta eseguita la copia, spegni normalmente il sistema. Lo spegnimento del dispositivo blocca anche il pool di archiviazione. Nel flusso di lavoro, fai clic su **Shutdown Appliance...**.  
    ![Ubicazione del pulsante dell'interfaccia utente di spegnimento dell'applicazione](/images/Shutdown.png)

5. Disconnetti il dispositivo. Restituisci il cavo di alimentazione, il cavo Ethernet e l'adattatore SFP+ nelle loro rispettive ubicazioni di conservazione sotto il coperchio.

6. Attacca l'etichetta di spedizione fornita al dispositivo. Informa lo spedizioniere e restituisci il dispositivo al data center {{site.data.keyword.BluSoftlayer_full}}. Dopo che il dispositivo è arrivato al data center, i tuoi dati vengono caricati nel tuo bucket {{site.data.keyword.cos_full_notm}}.

Dopo che il dispositivo viene restituito al team {{site.data.keyword.BluSoftlayer}}, lo stato della richiesta cambia e diventa *Device Received*.

## Passo 5: Offload e accesso
{: #offload}

Durante il processo di trasferimento dei dati, lo stato della richiesta viene visualizzato come *Offloading Data*. Lo stato cambia nuovamente quando la migrazione al bucket {{site.data.keyword.objectstorageshort}} viene completata (*Offload Complete*). I tuoi dati sono immediatamente accessibili quanto l'offload ad alta velocità nel tuo bucket Cloud Object Storage è completato. 

Dopo che la migrazione dei tuoi dati nel bucket Cloud Object Storage sarà stata completata, puoi procedere a [importare i tuoi dati nel tuo database {{site.data.keyword.dashdbshort_notm}}](#import).

## Passo 6: Importazione di dati da IBM Cloud Object Storage
{: #import}

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

**Note:** 
* Assicurati di utilizzare le stesse opzioni di clausola `USING` che hai utilizzato per estrarre i dati dal tuo database PureData System for Analytics (Netezza) utilizzando l'istruzione CREATE EXTERNAL TABLE.
* Per IBM Cloud Object Storage, per creare le credenziali HMAC quando si creano nuove credenziali di servizio, specifica, {"HMAC:true"} nel campo *Aggiungi parametri di configurazione inline*.

Per un'esercitazione guidata sull'importazione dei dati da IBM Cloud Object Storage, consulta: [IBM Db2 Warehouse on Cloud guided demo: Explore data loading ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud/){:new_window}.

## Passo 7: Eliminazione dei dati sul dispositivo MDMS
{: #erase}

{{site.data.keyword.IBM}} implementa l'eliminazione dei dati al livello dei requisiti del Dipartimento della Difesa degli Stati Uniti per eliminare in modo permanente i tuoi dati dal dispositivo MDMS. Al termine di tale operazione, lo stato della tua richiesta viene visualizzato come *Erase Complete*.

## Note aggiuntive
{: #notes}

### Univocità nel bucket

Per garantire che i nomi oggetto siano univoci quando vengono copiati nel bucket, il percorso file viene incluso come un prefisso nel nome oggetto. Ad esempio, il file config.ini nella cartella `/root/user/` viene ridenominato come "root/user/config.ini" quando viene copiato nel bucket.

### Bucket

Se non esiste, il bucket di destinazione viene creato. Se esiste deve essere vuoto, altrimenti la copia non può procedere.

### File system

I collegamenti simbolici e i collegamenti reali vengono ignorati durante il processo di scansione.

### Configurazione dell'indirizzo IP
{: #ip_cfg}

Il display LCD sul dispositivo può essere utilizzato per configurare gli indirizzi IP per le porte Ethernet. Ti sposti nel display LCD utilizzando i pulsanti **freccia su**, **freccia giù**, **esc** e **enter** (invio). Il pulsante **enter** (invio) ti porta a un menu e **esc** ti fa uscire dal menu.

![Display LCD](/images/MDMSLCD.png)

Quando modifichi un indirizzo IP o una maschera di sottorete, il tasto **enter** (invio) ti fa muovere di un carattere in avanti per volta; il tasto **esc** ti fa muovere di un carattere all'indietro per volta. I tasti **freccia su** e **freccia giù** fanno scorrere i numeri per l'ubicazione selezionata.

Utilizza **esc** per tornare al menu precedente.  

Vai alla voce di menu **Update...** e premi il tasto **enter** (invio) per salvare le impostazioni.
