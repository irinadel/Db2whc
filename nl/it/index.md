---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-24"

keywords:

subcollection: Db2whc

---

<!-- Attribute definitions --> 
{:javascript: #javascript .ph data-hd-programlang='javascript'}
{:java: #java .ph data-hd-programlang='java'}
{:ruby: #ruby .ph data-hd-programlang='ruby'}
{:php: #php .ph data-hd-programlang='php'}
{:python: #python .ph data-hd-programlang='python'}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}

# Introduzione
{: #getting_started}

Il servizio gestito da {{site.data.keyword.dashdblong}} è un database SQL di cui viene eseguito il provisioning nel cloud per te. Puoi utilizzare il warehouse Db2 come useresti qualsiasi software database ma senza dover sostenere il carico di lavoro e i costi necessari per la configurazione dell'hardware o l'installazione e la manutenzione del software. 
{: shortdesc}

## Versione di prova gratuita
{: #freetrial}

Puoi provare il piano d'ingresso {{site.data.keyword.dashdbshort_notm}} con un massimo di 1 GB di archiviazione senza addebiti. [Versione di prova gratuita ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window}

## Interfacce
{: #interfaces}

Puoi lavorare con il tuo database warehouse nei seguenti modi:
{: shortdesc}

   * Dalla console web
   * API REST
   * Connetti le applicazioni o i tuoi strumenti preferiti dal tuo computer locale
   * Usa {{site.data.keyword.dashdbshort_notm}} come origine dati per le tue applicazioni o i tuoi servizi {{site.data.keyword.Bluemix_notm}}

### Console web
{: #web_console}

La console web fornisce un'interfaccia grafica per tutto quello che ti serve per utilizzare il tuo database, tra cui: funzionalità di carico, un editor SQL, dei download di driver e altro ancora.
{: shortdesc}

![Vista della pagina del dashboard della console web](images/console_v3.png)

<!-- Click the link to take a tour of the {{site.data.keyword.dashdbshort_notm}} for Analytics web console: [General tour ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ibm.biz/dashdb-general-quick-tour){:new_window}. -->

Puoi accedere alla tua console web nei seguenti modi:
   * Dal tuo dashboard {{site.data.keyword.Bluemix_notm}} - puoi aprire la console web dalla pagina Dettagli del servizio per il tuo servizio {{site.data.keyword.dashdbshort_notm}}.
   * URL diretto - puoi mettere tra i preferiti l'URL della console web per il tuo servizio {{site.data.keyword.dashdbshort_notm}}.

### API REST
{: #api}

Con i piani del servizio {{site.data.keyword.dashdbshort_notm}}, puoi eseguire le attività correlate alla gestione dei file e al caricamento dei dati utilizzando l'[API REST {{site.data.keyword.dashdbshort_notm}} ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](http://ibm.biz/db2whc_api){:new_window}.
{: shortdesc}

### Connetti le applicazioni o i tuoi strumenti preferiti dal tuo computer locale
{: #connect_apps}

Configura il tuo ambiente locale per stabilire una connessione al tuo database {{site.data.keyword.dashdbshort_notm}} completando la seguente procedura:
{: shortdesc}

1. Scarica il [pacchetto del driver](/docs/services/Db2whc/connecting/driver_pkg.html) dalla console web {{site.data.keyword.dashdbshort_notm}}.
2. Installa il pacchetto del driver sul computer in cui sono in esecuzione le tue applicazioni e i tuoi strumenti:
   - [Installazione su Linux o PowerLinux](/docs/services/Db2whc/connecting/install_linux.html)
   - [Installazione su Mac OS X](/docs/services/Db2whc/connecting/install_mac.html)
   - [Installazione su Windows](/docs/services/Db2whc/connecting/install_win.html)
3. [Configura i file del driver](/docs/services/Db2whc/connecting/driver_pkg_cfg.html) per il tuo database {site.data.keyword.dashdbshort_notm}}.

### Usa Db2 Warehouse on Cloud come origine dati per le tue applicazioni o i tuoi servizi {{site.data.keyword.Bluemix_notm}}
{: #data_src}

Le applicazioni ospitate su {{site.data.keyword.Bluemix_notm}} possono connettersi al tuo database {{site.data.keyword.dashdbshort_notm}} nello stesso identico modo in cui le tue applicazioni locali si connettono al tuo database {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

Quando le tue applicazioni utilizzano la piattaforma {{site.data.keyword.Bluemix_notm}}, puoi usare la variabile di ambiente `VCAP _SERVICES` per semplificare l'attività di specifica dei dettagli e delle credenziali del database:
1. Sul tuo dashboard {{site.data.keyword.Bluemix_notm}}, nella scheda **Connessioni** della pagina Dettagli del servizio per il tuo servizio {{site.data.keyword.dashdbshort_notm}}, fai clic sul pulsante **Crea connessione**.
2. Seleziona l'applicazione {{site.data.keyword.Bluemix_notm}} da utilizzare con il tuo database {{site.data.keyword.dashdbshort_notm}} come un'origine dati e fai quindi clic sul pulsante **Connetti**.
3. Aggiorna il tuo codice applicativo per richiamare i dettagli e le credenziali del database dalla variabile di ambiente `VCAP_SERVICES`:

    **Esempio senza `VCAP_SERVICES`**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    $database    = "BLUDB";         # Ottieni questi dettagli del database dalla
    $hostname    = "<Host-name>";   # pagina di informazioni sulla connessione della
    $port        = 50000;           # console web.
    $user        = "<User-ID >";    #
    $password    = "<Password>";    #
    $dsn         = "DATABASE=$database;" .
                   "HOSTNAME=$hostname;" .
                   "PORT=$port;" .
                   "PROTOCOL=TCPIP;" .
                   "UID=$user;" .
                   "PWD=$password;";

    $conn_string = $driver . $dsn;

    $conn        = db2_connect( $conn_string, "", "" );
    ?>
    ```

    **Esempio con `VCAP_SERVICES`**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    $vcap        = json_decode( getenv( "VCAP_SERVICES" ), true );
    $dsn         = $vcap[ "dashDB" ][0][ "credentials" ][ "dsn" ];

    $conn_string = $driver . $dsn;
                                   
    $conn        = db2_connect( $conn_string, "", "" );
    ?>
    ```

## Esempi
{: #samples}

Sono qui riportati dei link ad esempi che illustrano come stabilire una connessione in modo programmatico al tuo database {{site.data.keyword.dashdbshort_notm}} da applicazioni in linguaggi differenti:
{: shortdesc}

- [JDBC](/docs/services/Db2whc/connecting/jdbc.html)
- [Microsoft Windows ODBC o CLI](/docs/services/Db2whc/connecting/odbc_cli.html)
- [.NET](/docs/services/Db2whc/connecting/net_apps.html)
- [ODBC Data Source Administrator](/docs/services/Db2whc/connecting/odbc_data_source_admin.html)
- [PHP](/docs/services/Db2whc/connecting/php.html)
- [API REST](/docs/services/Db2whc/connecting/rest_api.html)

## Video: Introduzione a Db2 Warehouse on Cloud
{: #intro_vid}

Guarda questo video per vedere un'introduzione a {{site.data.keyword.dashdbshort_notm}}.

<iframe class="embed-responsive-item" id="youtubeplayer1" title="Introduction to {{site.data.keyword.dashdbshort_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/0NO9OTFWzKs?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

## Video: Introduzione al piano Flex Performance
{: #intro_vid_flex}

Guarda questo video per vedere un'introduzione al piano {{site.data.keyword.dashdbshort_notm}} Flex Performance.

<iframe class="embed-responsive-item" id="youtubeplayer2" title="Creating a connection from Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

## Video: Connessione di un'applicazione di analisi
{: #cognos_vid}

Guarda questo video per vedere come creare una connessione da Cognos Analytics.

<iframe class="embed-responsive-item" id="youtubeplayer3" title="Creating a connection from Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TRUEPVHGi0s?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

