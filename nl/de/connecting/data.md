---

copyright:
  years: 2014, 2019
lastupdated: "2019-03-29"

keywords:

subcollection: Db2whc

---

<!-- Attribute definitions --> 
{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}

# Datenintegration
{: #data_int}

Sie können auch externe Anwendungen und Tools mit {{site.data.keyword.dashdbshort_notm}} verbinden und diese zur weiteren Verwaltung und Analyse der Daten verwenden. 
{: shortdesc}

## DataStage
{: #datastage}

Im Folgenden wird beschrieben, wie Sie eine Verbindung ohne SSL zwischen IBM® InfoSphere® DataStage® <!--version 9.1 and later -->und einer {{site.data.keyword.dashdbshort_notm}}-Datenbank definieren können, indem die Datenbank katalogisiert und ein Verbindungsobjekt definiert wird, und wie eine SSL-Verbindung unter Verwendung eines digitalen Zertifikats erstellt wird, das von einem Drittanbieter ausgegeben wurde.
{: shortdesc}

### Voraussetzungen
{: #prereq1}

Es wird dringend empfohlen, DataStage auf die aktuellste Version zu aktualisieren, damit Sie die Vorteile externer Tabellen nutzen können, um Ihre Daten in {{site.data.keyword.dashdbshort_notm}} zu laden.
{: important}

Ist kein IBM Data Server-Client installiert, laden Sie den IBM Data Server-Client <!--Version 10.5 -->herunter, der für das Betriebssystem Ihrer Clientmaschine geeignet ist, und installieren Sie die Software. Nähere Informationen hierzu finden Sie im Abschnitt [IBM Data Server-Client](https://www.ibm.com/marketing/iwm/iwm/web/preLogin.do?source=swg-idsc97){:external}.

Laden Sie die 32-Bit-Variante von Global Security Kit Version 8 herunter und installieren Sie das Programm, damit Verbindungen mit dem SSL-Protokoll eingerichtet werden können. Klicken Sie auf die Betriebssystemregisterkarte für das Betriebssystem Ihrer Clientmaschine. Nähere Informationen hierzu finden Sie im Abschnitt mit den [Installations-, Deinstallations- und Upgradeanweisungen für GSKit V8](http://www.ibm.com/support/docview.wss?uid=swg21631462){:external}. Stellen Sie bei den folgenden Betriebssystemen sicher, dass Sie den Pfad für das GSKit-Installationsverzeichnis in der betriebssystemspezifischen Pfadumgebungsvariable hinzufügen:

- AIX®: **LIBPATH**
   - `/usr/opt/ibm/gsk8/lib`
- Linux: **LD_LIBRARY_PATH**
    - `/usr/local/ibm/gsk8/lib`
- UNIX: **LD_LIBRARY_PATH**
    - `/opt/ibm/gsk8/lib`
- Windows: **PATH**
    - `<installation_directory>\gsk8\bin`
    - `<installation_directory>\gsk8\lib`

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) erfüllt werden.

### Vorgehensweise
{: #proc1}

- Führen Sie die folgenden Schritte aus, um eine Verbindung mit SSL zu erstellen:

  1. Öffnen Sie ein Befehlszeilen- oder Terminalfenster und erstellen Sie im DataStage-System ein neues Verzeichnis für das SSL-Zertifikat und Schlüsseldateien.

     `# /home/db2inst2> mkdir SSL`

     `# /home/db2inst2> cd SSL`

  2. Laden Sie in der {{site.data.keyword.dashdbshort_notm}}-Webkonsole das SSL-Zertifikat von der Seite **Verbindung von den Anwendungen zur Datenbank herstellen** herunter.

     a. Klicken Sie im Hauptmenü auf **Verbinden**.
     
     b. Klicken Sie auf **Verbindung mit SSL** und anschließend auf den Link **SSL-Zertifikat (1 KB)**.
     
     c. Speichern Sie das Zertifikat `DigiCertGlobalRootCA.crt` in dem in Schritt 1 erstellten SSL-Verzeichnis.
        
  3. Erstellen Sie mit dem Dienstprogramm **gsk8capicmd_64** eine Client-Keystore-Datenbank im DataStage-System.

     `# /home/db2inst2/SSL> gsk8capicmd_64 -keydb -create -db <keystore_db.kdb> -pw <ks_db_password> -stash`

     Dabei steht `<keystore_db.kdb>` für die Client-Keystore-Datenbank und `<ks_db_password>` für das Kennwort für die Client-Keystore-Datenbank.
        
  4. Fügen Sie das Zertifikat zu der Client-Keystore-Datenbank hinzu.

     `# /home/db2inst2/SSL> gsk8capicmd_64 -cert -add -db <keystore_db.kdb> -pw <ks_db_password> -label BLUDB_SSL -file DigiCertGlobalRootCA.crt`

     Dabei steht `<keystore_db.kdb>` für die Client-Keystore-Datenbank und `<ks_db_password>` für das Kennwort für die Client-Keystore-Datenbank.
    
  5. Konfigurieren Sie den Db2-Client auf dem DataStage-Server.
            
     a. Aktualisieren Sie die SSL-Konfigurationsparameter im Datenbankmanager.

     `# /home/db2inst2> db2 update dbm cfg using SSL_CLNT_KEYDB /home/db2inst2/SSL/<keystore_db.kdb>`

     Dabei steht `<keystore_db.kdb>` für die Client-Keystore-Datenbank.

     `# /home/db2inst2> db2 update dbm cfg using SSL_CLNT_STASH /home/db2inst2/SSL/<keystore_db.sth>`

     Dabei steht `<keystore_db.sth>` für die Stashdatei mit dem Kennwort für die Client-Keystore-Datenbank.
            
     b. Katalogisieren Sie den Zielknoten mit aktivierter SSL-Sicherheitsoption und anschließend die Datenbank BLUDB auf dem Zielknoten.

     `# /home/db2inst2> db2 catalog tcpip node <node_name> remote <IP_addr_of_BLUDB_database_server> server 50001 security SSL`

     Dabei steht `<node_name>` für Ihren Namen für den Zielknoten und `<IP_addr_of_BLUDB_database_server>` für die IP-Adresse des BLUDB-Datenbankservers.

     `# /home/db2inst2> db2 catalog db BLUDB as <db_alias> at node <node_name>`

     Dabei steht `<db_alias>` für Ihren Namen für die {{site.data.keyword.dashdbshort_notm}}-Datenbank.

  6. Fügen Sie Schreib- und Ausführungsberechtigungen für alle Benutzer für die Dateien im SSL-Verzeichnis hinzu. Der DataStage-Benutzer, der die Jobs ausführt, benötigt einen Zugriff auf diese Dateien, um SSL-Verbindungen zu der Db2-Datenbank herstellen zu können.

     `# /home/db2inst2/SSL> chmod 655 /home/db2inst2/SSL/*`

  7. Testen Sie die SSL-Verbindung auf eine der folgenden Weisen:

     - Testen Sie die Verbindung über den Befehlszeilenprozessor (CLP). Geben Sie den folgenden Befehl ein, um eine Verbindung zur {{site.data.keyword.dashdbshort_notm}}-Datenbank herzustellen:

       `db2 connect to <db_alias> user <user_id>`

       Dabei steht `<db_alias>` für Ihren Namen für die {{site.data.keyword.dashdbshort_notm}}-Datenbank und `<user_id>` ist Ihre {{site.data.keyword.dashdbshort_notm}}-Benutzer-ID. Sie werden zur Kennworteingabe aufgefordert.
    
     - Testen Sie die Verbindung über die Befehlszeilenschnittstelle. Geben Sie den folgenden Befehl ein, um eine Verbindung zur {{site.data.keyword.dashdbshort_notm}}-Datenbank herzustellen:

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

        Dabei steht `<alias>` für einen Alias, den Sie zuvor mit dem Befehl **db2cli writecfg** erstellt haben, und `<user_id>` ist Ihre {{site.data.keyword.dashdbshort_notm}}-Benutzer-ID und `<password>` Ihr {{site.data.keyword.dashdbshort_notm}}-Kennwort.

- Katalogisieren Sie zum Erstellen einer Verbindung ohne SSL die {{site.data.keyword.dashdbshort_notm}}-Zieldatenbank, indem Sie die folgenden Schritte ausführen:

  1. Katalogisieren Sie den {{site.data.keyword.dashdbshort_notm}}-Zielknoten, sodass die Clientanwendungen eine Verbindung zu diesem herstellen können. Führen Sie die folgenden Befehle des Befehlszeilenprozessors aus:

     `<node_name> remote <IP_address_of_BLUDB_database_server> server <port_number_of_BLUDB_database>`

     Dabei steht `<node_name>` für Ihren Namen für den Knoten, `<IP_address_of_BLUDB_database_server>` für die IP-Adresse des BLUDB-Datenbankservers und `<port_number_of_BLUDB_database>` steht für die Portnummer der BLUDB-Datenbank.

  2. Katalogisieren Sie die ferne {{site.data.keyword.dashdbshort_notm}}-Datenbank, damit Clientanwendungen eine Verbindung zu der Datenbank herstellen können. Führen Sie den folgenden Befehl aus:

     `db2 catalog db BLUDB as <db_alias> at node <node_name>`

     Dabei steht `<db_alias>` für Ihren Namen für die {{site.data.keyword.dashdbshort_notm}}-Datenbank und `<node_name>` für Ihren Namen für den Knoten.

  3. Testen Sie die Verbindung ohne SSL auf eine der folgenden Weisen:

      - Testen Sie die Verbindung über den Befehlszeilenprozessor (CLP). Geben Sie den folgenden Befehl ein, um eine Verbindung zur {{site.data.keyword.dashdbshort_notm}}-Datenbank herzustellen:

        `db2 connect to <db_alias> user <user_id>`

        Dabei steht `<db_alias>` für Ihren Namen für die {{site.data.keyword.dashdbshort_notm}}-Datenbank und `<user_id>` ist Ihre {{site.data.keyword.dashdbshort_notm}}-Benutzer-ID. Sie werden zur Kennworteingabe aufgefordert.

        `db2 list tables`

      - Testen Sie die Verbindung über die Befehlszeilenschnittstelle. Geben Sie den folgenden Befehl ein, um eine Verbindung zur {{site.data.keyword.dashdbshort_notm}}-Datenbank herzustellen:

        `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

        Dabei steht `<alias>` für einen Alias, den Sie zuvor mit dem Befehl **db2cli writecfg** erstellt haben, und `<user_id>` ist Ihre {{site.data.keyword.dashdbshort_notm}}-Benutzer-ID und `<password>` Ihr {{site.data.keyword.dashdbshort_notm}}-Kennwort.

  4. Definieren Sie mit den [Verbindungsinformationen](/docs/services/Db2whc/connecting?topic=Db2whc-db_details_cxn_creds#db_details_cxn_creds), die Sie zuvor ermittelt haben, eine Verbindung im DataStage-Client. Wählen Sie auf der Registerkarte **Parameters** die Option **Db2 Connector** für das Feld **Connect using Staging Type** aus.

     Details zur Definition einer Verbindung in DataStage finden Sie in den folgenden Abschnitten der DataStage-Dokumentation: 
     
     - [Datenverbindungsobjekt manuell erstellen](https://www.ibm.com/support/knowledgecenter/SSZJPZ_11.3.0/com.ibm.swg.im.iis.ds.design.doc/topics/t_ddesref_Creating_a_Data_Connection_Object_Manually.html){:external}
     - [Zugriff auf Db2-Datenbanken konfigurieren](https://www.ibm.com/support/knowledgecenter/en/SSZJPZ_11.7.0/com.ibm.swg.im.iis.conn.common.usage.doc/topics/t_configuring_db2conn.html){:external}

## Informatica
{: #informatica}

Sie können Informatica mit der {{site.data.keyword.dashdbshort_notm}} verbinden, um die Verwaltung Ihrer Daten zu vereinfachen.
{: shortdesc}

In dem folgenden Video wird die Integration von {{site.data.keyword.dashdbshort_notm}} mit Informatica Cloud beschrieben.

<iframe class="embed-responsive-item" id="youtubeplayer1" title="Db2 Connections - Lightening Fast How-To with Informatica Cloud" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TUiS_HstLnU?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

<!-- To configure a native Db2 connection to connect to {{site.data.keyword.dashdbshort_notm}}, perform the following steps:

1. Run the `odbcad32.exe` file from your local system.
The ODBC Data Sources Administrator dialog box appears.

2. Create the 32-bit ODBC Data Source Name using the DataDirect Db2 drivers.

3. In the ODBC DB2 Wire Protocol Setup dialog box, click **Security** tab.

4. Set the value of the `Authentication Method` property as `1 -Encrypt Password`. The following image shows the **Security** tab in the ODBC DB2 Wire Protocol Setup dialog box where you can set the `Authentication Method` property:
             
   ![ODBC Db2 Wire Protocol Driver Setup - Security tab](images/odbc_driver.png)
       
5. In the ODBC DB2 Wire Protocol Setup dialog box, click **Modify Bindings** tab.

6. Enter your user name in the Package Collection property. The following image shows the **Modify Bindings** tab in the ODBC DB2 Wire Protocol Setup dialog box where you can set the `Package Collection` property: 

   ![ODBC Db2 Wire Protocol Driver Setup - Modify Bindings tab](images/odbc_driver_2.png)
            
7. In the PowerCenter Designer, use the data source name that you created to import the metadata.

8. In the PowerCenter Workflow Manager, create the required workflow.

9. Ensure that you have the {{site.data.keyword.dashdbshort_notm}} compatible 11.x Db2 clients when you run the workflow.

**Note**: If you want to set the authentication type when you create the Db2 client catalog, you could specify the value of the `AUTHENTICATION TYPE` property as `SERVER_ENCRYPT`. -->

<!-- Watch this video to see how to integrate Db2 and Salesforce with Informatica Cloud.

<iframe class="embed-responsive-item" id="youtubeplayer2" title="Integrate Db2 and Salesforce with Informatica Cloud" type="text/html" width="640" height="390" src="//www.youtube.com/watch?v=RGTLweZvKP8" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe> -->

<!-- [Informatica](https://kb.informatica.com/howto/6/Pages/20/522402.aspx?myk=Connect%20to%20Db2){:external} -->

## Lift
{: #lift}

Mit Lift können Sie Ihre Daten in {{site.data.keyword.dashdbshort_notm}} migrieren.

[Lift](https://www.lift-cli.cloud.ibm.com/#docs){:external}

## InfoSphere Data Replication
{: #idr}

Sie können IBM® InfoSphere® Data Replication <!--version 11.3.3.3-36 or later -->mit einer {{site.data.keyword.dashdbshort_notm}}-Datenbank verbinden. Dies gilt sowohl für SMP- als auch für MPP-Umgebungen. Es gilt jedoch nicht für den Einstiegsplan von {{site.data.keyword.dashdbshort_notm}}. 
{: shortdesc}

### Übersicht
{: #overview2}

Wenn Sie IBM InfoSphere Data Replication mit {{site.data.keyword.dashdbshort_notm}} verbinden, ist IBM InfoSphere Data Replication im Idealfall in demselben {{site.data.keyword.Bluemix_notm}}-Rechenzentrum wie {{site.data.keyword.dashdbshort_notm}} oder auf eigenen Maschinen mit {{site.data.keyword.dashdbshort_notm}} installiert. IBM InfoSphere Data Replication stellt von einem lokalen Server aus eine Verbindung zu der fernen {{site.data.keyword.dashdbshort_notm}}-Instanz her.

Wenn Sie {{site.data.keyword.dashdbshort_notm}} als Verbindungsziel verwenden, ist das Leistungsverhalten von IBM InfoSphere Data Replication zum Teil abhängig von der Bandbreite des Netzes, das die zugehörige Zielengine von der {{site.data.keyword.dashdbshort_notm}}-Instanz trennt. Auch die räumliche Entfernung beeinträchtigt die Leistung. IBM InfoSphere Data Replication sollte sich in möglichst geringer Entfernung zu der {{site.data.keyword.dashdbshort_notm}}-Instanz befinden. Zusätzlich wirkt sich die Netztopologie auf die Leistung aus. Im Idealfall wird die IBM InfoSphere Data Replication-Zielengine beispielsweise auf einer VM in demselben VPN (Sicherheitsdomäne) wie die Zielinstanz ausgeführt. Je weniger Netzknoten (z. B. Firewalls oder Router) zu durchqueren sind, desto vorteilhafter. 

### Voraussetzungen
{: #prereq2}

Laden Sie GSKit V8 herunter und installieren Sie das Programm, wenn das SSL-Protokoll für die Verbindung verwendet werden soll. Siehe dazu den Abschnitt mit [Installations-, Deinstallations- und Upgradeanweisungen für GSKit V8](http://www.ibm.com/support/docview.wss?uid=swg21631462){:external}. Klicken Sie auf die Betriebssystemregisterkarte für das Betriebssystem, das auf Ihrer Clientmaschine verwendet wird. Stellen Sie bei einer GSKit-Installation auf einem Windows-Computer sicher, dass Sie den Verzeichnispfad für die GSKit-Installation (`<installation_directory>\gsk8\bin`) für die Umgebungsvariable **`PATH`** angeben.

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) erfüllt werden.

Soll das SSL-Protokoll für die Verbindung verwendet werden, laden Sie das SSL-Zertifikat `DigiCertGlobalRootCA.crt` über die Webkonsole in ein Verzeichnis auf der Clientmaschine herunter. Klicken Sie zum Herunterladen des Zertifikats auf **Verbindung > Verbindungsinformationen** und anschließend auf die Registerkarte **Verbindung mit SSL**.

### Vorgehensweise
{: #proc2}

1. Entscheiden Sie sich beim Erstellen der Verbindung für eine der folgenden Vorgehensweisen:

   - Führen Sie die folgenden Schritte aus, um eine Verbindung mit SSL zu erstellen:
            
     a. Setzen Sie den folgenden Befehl ab:

     `cd /<ssl_directory_name>/ssl`

     Dabei steht `/<ssl_directory_name>/ssl` für den Pfad zu dem Verzeichnis, in den Sie das SSL-Zertifikat `DigiCertGlobalRootCA.crt` herunterladen.

     b. Erstellen Sie mit dem Tool **GSKCapiCmd** eine Clientschlüsseldatenbank und eine Stashdatei. Der folgende Befehl bewirkt beispielsweise das Erstellen einer Clientschlüsseldatenbank namens `dashclient.kdb` und einer Stashdatei namens `dashclient.sth`:

     `gsk8capicmd_64 -keydb -create -db "dashclient.kdb" -pw "passw0rdpw0" -stash`

     Dabei steht `passw0rdpw0` für ein Kennwort. Über die Option **-stash** wird eine Stashdatei mit der Erweiterung `.sth` in demselben Pfad wie die Clientschlüsseldatenbank erstellt. Zur Verbindungszeit wird die Stashdatei vom Global Security Kit dazu verwendet, das Kennwort für die Clientschlüsseldatenbank abzurufen.
            
     c. Fügen Sie das Zertifikat zu Clientschlüsseldatenbank hinzu. Mit dem Befehl **gsk8capicmd** wird beispielsweise das Zertifikat aus der Datei `/<ssl_directory_name>/ssl/DigiCertGlobalRootCA.crt` in die Clientschlüsseldatenbank mit dem Namen `dashclient.kdb` importiert:

     `gsk8capicmd_64 -cert -add -db "dashclient.kdb" -pw "passw0rdpw0" -label "DigiCert" -file "/<ssl_directory_name>/ssl/DigiCertGlobalRootCA.crt" -format ascii -fips`

     d. Aktualisieren Sie die Werte der Konfigurationsparameter des Datenbankmanagers `SSL_CLNT_KEYDB` und `SSL_CLNT_STASH` auf dem Client mit den Werten für die Clientschlüsseldatenbank und die Stashdatei. Dazu mehrere Beispiele:

     `db2 update dbm cfg using SSL_CLNT_KEYDB /<ssl_directory_name>/ssl/dashclient.kdb`

     `db2 update dbm cfg using SSL_CLNT_STASH /<ssl_directory_name>/ssl/dashclient.sth`

     e. Katalogisieren Sie den {{site.data.keyword.dashdbshort_notm}}-Knoten, damit Clientanwendungen eine Verbindung zu dem Knoten herstellen können. Setzen Sie den folgenden Befehl ab:

     `db2 catalog tcpip node <node_name> remote <Db2_Warehouse_IP_address> server <port_number> security ssl`

     Dabei gilt Folgendes:
                
     `<node_name>` ist Ihr Name für den Knoten.

     `<Db2_Warehouse_IP_address>` ist die IP-Adresse des Db2 Warehouse on Cloud-Servers.

     `<port_number>` ist der Port für die SSL-Verbindung zu Db2 Warehouse. Geben Sie `50001` an, wenn Sie den Standardport verwenden.
            
     f. Katalogisieren Sie die ferne {{site.data.keyword.dashdbshort_notm}}-Datenbank, damit Clientanwendungen eine Verbindung zu der Datenbank herstellen können. Setzen Sie den folgenden Befehl ab:

     `db2 catalog database bludb as <db_alias> at node <node_name>`

     Dabei ist `db_alias` Ihr Name für die {{site.data.keyword.dashdbshort_notm}}-Datenbank.
            
     g. Testen Sie die SSL-Verbindung auf eine der folgenden Weisen:
                
     - Testen Sie die Verbindung über den Befehlszeilenprozessor (CLP), indem Sie mit dem folgenden Befehl eine Verbindung zur {{site.data.keyword.dashdbshort_notm}}-Datenbank herstellen:

       `db2 connect to <db_alias> user <user_id>`

       Dabei steht `<user_id>` für Ihre {{site.data.keyword.dashdbshort_notm}}-Benutzer-ID. Sie werden zur Kennworteingabe aufgefordert.
                
     - Testen Sie die Verbindung über die Befehlszeilenschnittstelle, indem Sie mit dem folgenden Befehl eine Verbindung zur {{site.data.keyword.dashdbshort_notm}}-Datenbank herstellen:

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

       Dabei steht `<alias>` für einen DSN-Alias, den Sie mithilfe des Befehls **db2cli writecfg** erstellt haben, `<user_id>` steht für Ihre {{site.data.keyword.dashdbshort_notm}}-Benutzer-ID und `<password>` für Ihr{{site.data.keyword.dashdbshort_notm}}-Datenbankkennwort.
        
   - Führen Sie die folgenden Schritte aus, um eine Verbindung ohne SSL zu erstellen:

     a. Katalogisieren Sie den {{site.data.keyword.dashdbshort_notm}}-Knoten, damit Clientanwendungen eine Verbindung zu dem Knoten herstellen können. Setzen Sie den folgenden Befehl ab:

     `db2 catalog tcpip node <node_name> remote <Db2_Warehouse_IP_address> server <port_number>`

     Dabei gilt Folgendes:
                
     `<node_name>` ist Ihr Name für den Knoten.

     `<Db2_Warehouse_IP_address>` ist die IP-Adresse des {{site.data.keyword.dashdbshort_notm}}-Servers.

     `<port_number>` ist der Port für eine Verbindung zu {{site.data.keyword.dashdbshort_notm}} ohne SSL. Geben Sie `50000` an, wenn Sie den Standardport verwenden.
            
     b. Katalogisieren Sie die ferne {{site.data.keyword.dashdbshort_notm}}-Datenbank, damit Clientanwendungen eine Verbindung zu der Datenbank herstellen können. Setzen Sie den folgenden Befehl ab:

     `db2 catalog database bludb as <db_alias> at node <node_name>`

     Dabei steht `<db_alias>` für Ihren Namen für die {{site.data.keyword.dashdbshort_notm}}-Datenbank.

     c. Testen Sie die Verbindung ohne SSL auf eine der folgenden Weisen:

     - Testen Sie die Verbindung über den Befehlszeilenprozessor (CLP), indem Sie mit dem folgenden Befehl eine Verbindung zur {{site.data.keyword.dashdbshort_notm}}-Datenbank herstellen:

       `db2 connect to <db_alias> user <user_id>`

       Dabei steht `<user_id>` für Ihre {{site.data.keyword.dashdbshort_notm}}-Benutzer-ID. Sie werden zur Kennworteingabe aufgefordert.
                
     - Testen Sie die Verbindung über die Befehlszeilenschnittstelle, indem Sie mit dem folgenden Befehl eine Verbindung zur {{site.data.keyword.dashdbshort_notm}}-Datenbank herstellen:

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

       Dabei steht `<alias>` für einen DSN-Alias, den Sie zuvor mit dem Befehl **db2cli writecfg** erstellt haben, `<user_id>` steht für Ihre {{site.data.keyword.dashdbshort_notm}}-Benutzer-ID und `<password>` für Ihr Db2 Warehouse on Cloud-Kennwort.
    
2. Starten Sie das Konfigurationstool für InfoSphere Data Replication und führen Sie die folgenden Schritte aus. Bei den in den Screenshots angezeigten Werten handelt es sich um Beispielwerte.
        
   a. Fügen Sie über die Registerkarte **Instanzkonfiguration** eine Quelleninstanz hinzu, um auf Ihre Quellendatenbank zu verweisen:

   ![IIDR-Anzeige für neue Instanz - Quelleninstanz](images/IIDR_source_instance.jpg "Quelleninstanzkonfiguration")

   b. Fügen Sie über die Registerkarte **Instanzkonfiguration** eine Zielinstanz hinzu, um auf Ihre Db2-Zieldatenbank zu verweisen. Wählen Sie das Kontrollkästchen **Pfad für Aktualisierungsladeprogramm angeben** nur aus, wenn Sie IBM InfoSphere Data Replication 11.3.3.3-50 oder eine höhere Version verwenden.

   ![IIDR-Anzeige für neue Instanz - Zielinstanz](images/IIDR_target_instance.jpg "Zielinstanzkonfiguration")

   c. Starten Sie die einzelnen Instanzen:

   ![IIDR-Konfigurationstool](images/IIDR_instances.jpg "IIDR-Konfigurationstool listet Quellen- und Zielinstanzen auf")

3. Starten Sie die InfoSphere Data Replication-Managementkonsole und führen Sie die folgenden Schritte mit Access Manager aus:
        
   a. Erstellen Sie über die Registerkarte **Datenspeicher** einen Datenspeicher, der mit Ihrer Quelleninstanz verbunden werden soll. Da Db2-Datenbanken ursprünglich nicht als Quellendatenbanken unterstützt wurden, müssen Sie Benutzer- und Kennwortinformationen für die Quellendatenbank angeben. Klicken Sie dazu auf **Verbindungsparameter**.

   ![Datenspeichereigenschaften - Quelle](images/IIDR_source_datastore.jpg "Quellendatenspeichereigenschaften")

   b. Erstellen Sie über die Registerkarte **Datenspeicher** einen Datenspeicher, der mit Ihrer Zielinstanz verbunden werden soll. Sie müssen Benutzer- und Kennwortinformationen angeben. Klicken Sie dazu auf **Verbindungsparameter**.

   ![Datenspeichereigenschaften - Ziel](images/IIDR_target_datastore.jpg "Zieldatenspeichereigenschaften")

   c. Ist der Benutzer (z. B. 'admin'), über den die Verbindung zu Access Server hergestellt wird, nicht vorhanden, müssen Sie diesen Benutzer erstellen:

   ![Neuer Benutzer](images/IIDR_management_user.jpg "Erstellungstool für neuen Benutzer")

   d. Klicken Sie auf die Registerkarte **Access Manager**.
        
   e. Ordnen Sie den Benutzer auf der Registerkarte **Datenspeichermanagement** zum Quellen- und zum Zieldatenspeicher zu, indem Sie mit der rechten Maustaste jeweils auf einen der Datenspeicher und anschließend auf **Benutzer zuordnen** klicken. Stellen Sie sicher, dass Sie jeweils die richtigen Berechtigungsnachweise für den Zugriff auf die einzelnen Instanzen angeben.

   ![IIDR-Managementkonsole - Zugriffsmanager](images/IIDR_management_assign_user.jpg "Zugriffsmanagerkonsole")

### Nächster Schritt
{: #what2}

Definieren Sie eine Subskription und führen Sie eine Datenreplikation durch. Weitere Informationen hierzu finden Sie in dem Abschnitt zu dem folgenden Thema:

- [Daten aus InfoSphere Data Replication laden](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/learn_how/loaddata_iidr.html){:external} 

## Segment
{: #segment}

Sie können Segment mit einer {{site.data.keyword.dashdbshort_notm}}-Datenbank integrieren. Bei Segment handelt es sich um eine einzelne Plattform, die Ihre Benutzerdaten erfasst, speichert und an eine Vielzahl von Tools weiterleitet.
{: shortdesc}

[Segment](https://segment.com/docs/destinations/db2/){:external}

## Data Studio
{: #data_studio}

Im Folgenden wird beschrieben, wie Sie eine Verbindung von IBM® Data Studio <!--version 4.1.x -->zu einer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen.
{: shortdesc}

### Voraussetzungen
{: #prereq3}

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) erfüllt werden.

### Vorgehensweise
{: #proc3}

1. Klicken Sie in Data Studio auf **Alle Datenbanken > Neue Verbindung zu einer Datenbank**.

2. Wählen Sie auf der Registerkarte **Lokal** für den Datenbankmanager die Option **Db2 for Linux, UNIX and Windows** aus.
    
3. Geben Sie auf der Registerkarte **Allgemein** die folgenden Werte ein:
   - *Datenbank*: `BLUDB`.
   - *Host*: Der Hostname.
   - *Port*: Geben Sie für eine Verbindung ohne SSL `50000` ein. Geben Sie für eine SSL-Verbindung `50001` ein. 
   - *Benutzername*: Der Benutzername, den Sie für die Anmeldung verwenden.
   - *Kennwort*: Das Kennwort, das Sie für die Anmeldung verwenden.

4. Klicken Sie für eine SSL-Verbindung auf die Registerkarte **Optional** und anschließend auf **Hinzufügen**. Geben Sie für die Eigenschaft `sslConnection` den Wert `true` an.

5. [*Optional*]: ClickAuf  **Verbindung testen** klicken, um zu überprüfen, ob die Verbindung erfolgreich war.

## Data Server Manager (DSM)
{: #dsm}

Eine Verbindung zwischen IBM® Data Server Manager und der {{site.data.keyword.dashdbshort_notm}}-Datenbank ermöglicht es Ihnen, die Datenbank über die Webkonsole von Data Server Manager zu überwachen und zu verwalten. 
{: shortdesc}

### Voraussetzungen
{: #prereq4}

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) erfüllt werden.

### Vorgehensweise
{: #proc4}

<!--The connection procedure was tested on Data Server Manager version 1.1. The same procedure applies to all of the other versions of the Data Server Manager software.
-->
Führen Sie die folgenden Schritte aus, um eine Verbindung zu erstellen:

1. Melden Sie sich bei der Data Server Manager-Webkonsole an.
    
2. Klicken Sie in der Data Server Manager-Webkonsole auf **Einrichten > Datenbankverbindungen**.
    
3. Klicken Sie auf das ![Pluszeichen (+) in einem Kreis](images/icon_R_plus.gif "Hinzufügesymbol"), um eine Datenbankverbindung hinzuzufügen. Geben Sie auf der Seite **Datenbankverbindung hinzufügen** der Registerkarte **Datenbankverbindung** die erforderlichen Informationen in den folgenden Feldern ein:

   - *Name der Datenbankverbindung*: Dieser Name muss in Data Server Manager eindeutig sein.
   - *Datenservertyp*: Wählen Sie im Dropdown-Menü **Db2 for Linux, UNIX and Windows** aus.
   - *Datenbankname*: `BLUDB`
   - *Hostname*: Geben Sie den {{site.data.keyword.dashdbshort_notm}}-Hostnamen ein. 
   - *Portnummer*: Geben Sie für eine Verbindung ohne SSL `50000` ein. Geben Sie für eine SSL-Verbindung `50001` ein. 
   - *JDBC-Sicherheit*: Wählen Sie im Dropdown-Menü die Option **Klartextkennwort** aus.
   - *Benutzer-ID*: Geben Sie Ihre {{site.data.keyword.dashdbshort_notm}}-Benutzer-ID ein. 
   - *Kennwort*: Geben Sie Ihr {{site.data.keyword.dashdbshort_notm}}-Kennwort ein. 

4. Wählen Sie für eine Verbindung mit SSL die Registerkarte **Erweiterte JDBC-Eigenschaften** aus. Geben Sie in den folgenden Feldern die erforderlichen Informationen ein:

   - *Eigenschaft*: `sslConnection`
   - *Wert*: `true`

    Klicken Sie auf die Schaltfläche **Hinzufügen**. Wählen Sie die Registerkarte **Datenbankverbindung** aus.
    
5. Testen Sie die Verbindung, indem Sie auf die Schaltfläche **Verbindung testen** klicken. Klicken Sie auf **OK**, wenn die Verbindung ordnungsgemäß eingerichtet wurde.

## InfoSphere Data Architect
{: #ida}

Im Folgenden wird beschrieben, wie Sie eine Verbindung von InfoSphere® Data Architect <!--version 9.1.x -->zu  einer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen können.
{: shortdesc}

### Voraussetzungen
{: #prereq5}

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) erfüllt werden.

### Vorgehensweise
{: #proc5}

1. Klicken Sie in der Datenquellenexploreransicht von InfoSphere Data Architect mit der rechten Maustaste auf **Datenbankverbindungen** und wählen Sie anschließend **Neu** aus.
    
2. Wählen Sie auf der Registerkarte **Lokal** für den Datenbankmanager die Option **Db2 for Linux, UNIX and Windows** aus.
    
3. Geben Sie auf der Registerkarte **Allgemein** die folgenden Werte ein:

   - *Datenbank*: `BLUDB`.
   - *Host*: Der Hostname, den Sie zuvor ermittelt haben.
   - *Port*: Geben Sie für eine Verbindung ohne SSL `50000` ein. Geben Sie für eine SSL-Verbindung `50001` ein. 
   - *Benutzername*: Die Benutzer-ID, die Sie zuvor ermittelt haben.
   - *Kennwort*: Das Kennwort, das Sie zuvor ermittelt haben.

4. Klicken Sie für eine SSL-Verbindung auf die Registerkarte **Optional**. Geben Sie die Eigenschaft `sslConnection` ein und geben Sie den Wert `true` an. Klicken Sie auf **Hinzufügen**.
    
5. [*Optional*]: ClickAuf  **Verbindung testen** klicken, um zu überprüfen, ob die Verbindung erfolgreich war.

## Aginity Workbench
{: #aginity_wb}

Im Folgenden wird beschrieben, wie Sie Aginity Workbench <!--4.3 --> mit einer {{site.data.keyword.dashdbshort_notm}}-Datenbank verbinden können. Mit Aginity Workbench können Sie IBM PureData for Analytics (Netezza)-Datenmodelle und -Daten in {{site.data.keyword.dashdbshort_notm}} migrieren.
{: shortdesc}

### Voraussetzungen
{: #prereq6}

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) erfüllt werden.

### Vorgehensweise
{: #proc6}

1. Laden Sie Aginity Workbench herunter und installieren Sie das Tool.

2. Ermitteln Sie den ODBC-DSN anhand der Verbindungsinformationen, die Sie zuvor notiert haben.

3. Starten Sie Aginity Workbench. Wird das Dialogfenster für die Datenbankverbindung nicht automatisch geöffnet, öffnen Sie das Dialogfenster, indem Sie in der Symbolleiste auf **Connect** klicken.

4. [Erstellen Sie eine Datenbankverbindung](https://www.aginity.com/documentation/WB/dashDB/Default.htm#Aginity_Topics/Aginity_Workbench/Database_Connection_Dialog_Box.htm){:external}. Verwenden Sie den Hostnamen, die Benutzer-ID und das Kennwort aus den Verbindungsinformationen, die Sie zuvor notiert haben.

## CLPPlus
{: #clpplus}

CLPPLus (Command Line Processor Plus) ist im Db2-Treiberpaket enthalten. Mit CLPPlus verfügen Sie über Befehlszeilenschnittstelle, über die Sie eine Verbindung zur {{site.data.keyword.dashdbshort_notm}}-Datenbank herstellen können. Sie können mit CLPPlus Anweisungen, Scripts und Befehle definieren, bearbeiten und ausführen.
{: shortdesc}

### Voraussetzungen
{: #prereq7}

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) erfüllt werden.

CLPPlus können Sie nur verwenden, wenn ein Software-Development-Kit (SDK) oder eine Java Runtime Environment (JRE) für Java Version 1.5.0 oder eine höhere Version auf Ihrem Computer installiert ist und die jeweiligen Umgebungsvariablen wie folgt festgelegt sind:

- Als Wert für die Umgebungsvariable `JAVA_HOME` ist das Java-Installationsverzeichnis Ihres Computers festgelegt.
- Die Einstellung für die Umgebungsvariable `PATH` beinhaltet das Unterverzeichnis `bin` des Java-Installationsverzeichnisses auf Ihrem Computer.

### Vorgehensweise
{: #proc7}

1. Geben Sie in einer Befehlsshell in einem Linux-Betriebssystem in der Windows-Eingabeaufforderung bzw. unter einem Windows-Betriebssystem im Db2-Befehlsfenster die folgenden Befehle ein:

   Mit diesen Befehlen werden neue Einträge in der Treiberkonfigurationsdatei `db2dsdriver.cfg` auf Ihrem Computer erstellt und die Verbindungsattribute festgelegt. Sie müssen diesen Schritt lediglich ein einziges Mal ausführen.

   - Für SSL-Verbindungen:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`  

     Dabei gilt Folgendes:
     
     - `<hostname>` ist der Hostname des Servers.
     - `<alias>` ist ein von Ihnen gewählter Aliasname.

   - Für Verbindungen ohne SSL:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

2. Führen Sie den folgenden Befehl aus, um CLPPlus mit einer Verbindung zu einer {{site.data.keyword.dashdbshort_notm}}-Datenbank unter Verwendung der Einträge in der Datei `db2dsdriver.cfg` zu starten.

   - Windows-Umgebungen: 

     `clpplus <userid>@<alias>`

   - Linux-Umgebungen:

     `clpplus -nw <userid>@<alias>`

     Dabei gilt Folgendes:
     
     - `<userid>` ist die Benutzer-ID aus den Verbindungsinformationen, die Sie zuvor ermittelt haben.
     - `<alias>` ist der Alias, den Sie mit dem Befehl **db2cli writecfg** erstellt haben.

   Mit diesem Befehl wird ein CLPPlus-Fenster aufgerufen.

3. Geben Sie im CLPPlus-Fenster Ihr Kennwort ein. Im Anschluss an die Datenbankinformationen wird eine SQL-Eingabeaufforderung angezeigt. Dazu eine Beispielausgabe:

```
   Hostname = 192.0.2.0
   Database server = DB2/LINUXX8664  SQL10054
   SQL authorization ID = smith
   Local database alias = BLUDB
   Port = 50001
   
   SQL>
```

### Ergebnisse
{: #results7}

Arbeiten Sie nun mit den Daten in der Datenbank, indem Sie CLPPlus-Befehle oder SELECT-Anweisungen eingeben und Scripts ausführen.

### Beispiele

Bei den folgenden Beispielen werden über ein kurzes Script Zeilen aus der Beispieltabelle `GOSALES.BRANCH` abgerufen. Die zugehörige Scriptdatei mit dem Namen `cities.sql` befindet sich auf dem lokalen Windows-Computer im Verzeichnis `C:\temp`. Die Datei `cities.sql` enthält den folgenden Text:

```
SET ECHO ON
SELECT branch_code, city from GOSALES.BRANCH;
```

#### Beispiel 1 

Interaktive Ausführung des Scripts:

1. Starten Sie CLPPlus mit Ihrer Benutzer-ID und dem Alias, den Sie in der Datei `db2dsdriver.cfg` erstellt haben, indem Sie den folgenden Befehl ausführen:

   `clpplus <user_id>@<alias>`
2. Geben Sie Ihr Kennwort ein.
3. Geben Sie in der SQL-Eingabeaufforderung den folgenden Text ein:

   `start C:\temp\cities.sql`

#### Beispiel 2

Starten Sie CLPPlus mit Ihrer Benutzer-ID und dem Alias, den Sie in der Datei `db2dsdriver.cfg` erstellt haben, und führen Sie das Script in einem einzigen Schritt aus:

`clpplus <user_id>/<password>@<alias> @C:\temp\cities.sql`

Beispielausgabe zum Script `cities.sql`:

```
BRANCH_CODE CITY
----------- --------------------------------------------------
          6 Paris
          7 Milano
          9 Amsterdam
         13 Hamburg
         14 München
         15 Kista
         17 Calgary
         18 Toronto
         19 Boston
         20 Seattle
         21 Los Angeles
         22 Miami
         23 Lyon
         24 Distrito Federal
         25 Tokyo
         26 Osaka City
         28 Melbourne
         29 Bilbao
         30 Sao Paulo
         31 Kuopio
         32 Seoul
         33 Singapore

BRANCH_CODE CITY
----------- --------------------------------------------------
         34 Shanghai
         35 London
         36 Birmingham
         37 Zürich
         38 Heverlee
         39 Wien
         40 Geneve

29 rows were retrieved.
```


