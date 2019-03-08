---

copyright:
  years: 2014, 2019
lastupdated: "2018-06-15"

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

# Von IBM PureData System for Analytics (Netezza) migrieren
{: #pda}

Der {{site.data.keyword.Bluemix_notm}} Mass Data Migration Service (MDMS) kann genutzt werden, um die Daten großer IBM PureData Systems for Analytik (Netezza)-Datenbanken mit ca. 25 TB und mehr in eine vollständig verwaltete {{site.data.keyword.dashdblong}}-Datenbank auf {{site.data.keyword.Bluemix_notm}} zu migrieren.

MDMS bietet eine schnelle, einfache und sichere Möglichkeit, Terabytes bis Petabytes an Daten physisch auf {{site.data.keyword.Bluemix_notm}} zu übertragen. MDMS ist eine mobile Speichereinheit mit 120 TB nutzbarer Speicherkapazität. Mit dieser Einheit können Sie allgemeine Übertragungsprobleme wie hohe Kosten, lange Übertragungszeiten und hohe Sicherheitsrisiken mithilfe eines einzigen Services lösen.
{: shortdesc}

![Ansicht der Mass Data Migration Service-Einheit](images/mdms.svg)

## Voraussetzungen für die Anforderung einer Einheit
{: #prereq}

1. Netzeinstellungen für die Speichereinheit
   - Statische IP-Adresse
   - Netzmaske für das Aktivieren der Datenübertragung
2. Netzeinstellungen für den fernen Computer
   - Statische IP-Adresse
   - Netzmaske 
   - Standardgateway zum Zugreifen auf die Benutzerschnittstelle
3. Download-Zieladresse für die Cloud Object Storage-Instanz <br/>
   Sie benötigen mindestens ein {{site.data.keyword.cos_full}}-Konto und mindestens ein Bucket in einer US-Cross-Region oder im Süden der USA, um das Anfrageformular auszufüllen. Wenn Sie noch kein {{site.data.keyword.cos_full_notm}}-Konto haben, erstellen Sie ein Konto, bevor Sie die MDMS-Einheit anfordern. Weitere Informationen finden Sie unter [Informationen zu {{site.data.keyword.cos_full}}](/docs/services/cloud-object-storage/about-cos.html){:new_window}.
   {: important}

## Schritt 1: Anfrageerstellung
{: #create-req}

1. Melden Sie sich mit Ihren eindeutigen Berechtigungsnachweisen beim [{{site.data.keyword.slportal}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://control.softlayer.com/){:new_window} an.
2. Wählen Sie in der Navigationsleiste **Speicher > Datenmigration > Mass Data Migration** aus, um die MDMS-Landing-Page aufzurufen.
3. Klicken Sie auf die Option zum **Anfordern der Einheit**, um das Bestellformular zu öffnen.
4. Füllen Sie jedes Feld im Bestellformular für die **Mass Data Migration** aus.
   - **Versandadresse**: Dieses Formular ist nicht vorab ausgefüllt und jedes Feld ist bearbeitbar. Geben Sie im Hinweisfeld den Namen der Person an, die die Zustellung der Einheit annehmen soll. Berücksichtigen Sie bei der Auswahl des Lieferorts das Gewicht der Einheit (30 kg mit Verpackung) und die Zugangsmöglichkeiten. <br/> (**Hinweis**: Die Einheit ist mit Rädern und einem Kipphebel für eine leichtere Handhabung ausgestattet.)
   - **Wichtige Kontakte für die Migration**: Dieses Formular ist nicht vorab ausgefüllt. Jedes Feld ist bearbeitbar. Es können mehrere Personen hinzugefügt werden.
   - **Rechenzentrum-Netzkonfiguration**: Stellen Sie Netzkonfigurationsdetails für die vorherige Bereitstellung des Eth3-Ports auf der MDMS-Einheit vor dem Versand zur Verfügung.
   - **Daten-Offload-Zieladresse**: Wählen Sie aus der Liste Ihr vorhandenes Zielkonto aus.
   - **Anfragename**: Geben Sie einen Namen ein, damit Sie Ihre Bestellung verfolgen können.
5. Wählen Sie aus, dass Sie den **Bedingungen der Mass Data Migration-Vereinbarung zustimmen**, nachdem Sie jede Servicevereinbarung gelesen haben.
6. Klicken Sie auf **Anfrage platzieren**, um die Anfrage einzureichen. Klicken Sie auf **Abbrechen**, um das Formular zu verlassen und zur MDMS-Landing-Page zurückzukehren.

## Schritt 2: Vorbereitung und Versand
{: #prep-ship}

Nachdem die Anfrage eingereicht wurde, ändert sich der Status für das Anfrageticket zu *Anfrage wird verarbeitet*. Wenn Ihre Anfrage verarbeitet wurde, beginnt {{site.data.keyword.IBM}} mit der Vorkonfiguration der nächsten verfügbaren Einheit und der Rasterstatus [Anfrage ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://control.softlayer.com/storage/mdms){:new_window} zeigt die *Vorbereitung der Einheit* und dann *Warten auf Versand* an. Wenn Ihre Anfrage den Status *Warten auf Versand* erhält, kann sie nicht mehr abgebrochen werden. 

Die Einheit wird vom Netzbetreiber abgeholt und an Ihren Standort gesendet. Daraufhin wird der Status zu *Einheit geliefert* aktualisiert. Die Tracking-Nummer finden Sie im Abschnitt **Auftragsdetails** im Raster [Anfragen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://control.softlayer.com/storage/mdms){:new_window}.

## Schritt 3: Empfangnahme und Verbindung
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

### Übersicht

Die {{site.data.keyword.cloud}} Mass Data Migration-Einheit ist eine tragbare Speichereinheit, die montierbare Network File System (NFS) oder FileNet Content Federation Services (CF) S-Freigaben darstellen kann und über eine Webbrowser-Schnittstelle verwaltet wird. Die Einheit wird an Ihr Rechenzentrum geliefert und vor Ort mit Daten geladen. Sie wird an ein {{site.data.keyword.BluSoftlayer_full}}-Rechenzentrum zurückgegeben und Ihre Daten werden in Ihr {{site.data.keyword.cos_full}}-Konto geladen.

### Stromversorgung

Die Einheit besitzt ein C13-US-Netzkabel ([IEC 60320 ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://en.wikipedia.org/wiki/IEC_60320){:new_window}). Wenn die Einheit außerhalb der USA verwendet wird, ist möglicherweise ein Netzteil erforderlich.

Die MDMS-Einheit ist für alle Standard-Spannungsbereiche geeignet.
![Spannungsbereiche](/images/PowerRating.png)

### Ethernet-Verbindung

Es gibt zwei Ethernet-Verbindungen: Eine für das Einheitenmanagement über einen Browser und eine für die Datenübertragung im selben Teilnetz, in dem sich die Quellendaten befinden.

Für beide Ports der Einheit werden RJ45- und CAT6A-Kabel mitgeliefert. SFP+-Kupferadapter werden für die Konvertierung von RJ45 bereitgestellt. Die Adapter funktionieren mit allen Switch-Herstellern. Diese Adapter befinden sich in einer Tasche an der Unterseite der Versandabdeckung.

- Eth1 (1GbE-B) wird für das Einheitenmanagement verwendet und muss daher in der IP-Adresskonfiguration ein Gateway haben. Dies kann nach dem Einschalten der Einheit auf dem LCD-Bildschirm angezeigt werden (siehe Abschnitt [IP-Adresskonfiguration](#ip_cfg)).

- Eth3 (10GbE-B) wird für die Datenübertragung verwendet. Diese Verbindung muss sich entweder im selben Teilnetz wie die Quellendaten befinden oder kann bei Bedarf direkt mit dem Server verbunden sein.

Wenn ein anderer Formfaktor der Ethernet-Verbindung erforderlich ist, müssen Sie den Konverter selbst bereitstellen.

### Schritt-für-Schritt-Benutzeranweisungen

1. Die MDMS-Einheit ist mit Ihrer IP-Adresse, Ihrem Benutzernamen, dem gesperrten Speicherpool und der gemeinsam genutzten NFS-Ressource vorkonfiguriert. Das Benutzerkennwort und das Speicherpoolkennwort erhalten Sie über eine separate E-Mail.

2. Legen Sie den bestgeeigneten Standort für Ihre Einheit fest, von dem die Stromversorgung und die Ethernet-Verbindung (1GbE und 10GbE) sichergestellt sind und von dem die Einheit gut erreicht werden kann.

3. Positionieren Sie die Einheit dort, wo sie verbunden werden soll. Sie kann während der Nutzung in der Transportverpackung bleiben. Stellen Sie sicher, dass der Standort Raumtemperatur besitzt und dass keine Kondensation vorhanden ist. Schließen Sie die Einheit an die Stromversorgung an, indem Sie das mitgelieferte Netzkabel unter dem Gehäusedeckel verwenden. Schalten Sie die Einheit ein.<br/>
    Es gibt zwei Netzschalter.
    {: note}

    ![Netzschalter](/images/MDMSPowerSwitch.png)
    Die Einheit muss nicht aus der Transportverpackung genommen werden.
    {: note}

4. Nehmen Sie das CAT6A-Kabel aus dem Gehäusedeckel und schließen Sie es an den Eth3-Anschluss (10GbE-B) an, wie in der Abbildung dargestellt.
    ![Eth1- und Eth3-Anschlussposition](/images/MDMSNewEth1and3.png)

5. Verbinden Sie das CAT6A-Kabel mit dem SFP+-Adapter und dann mit dem Ihrem 10Gb-Switch.

6. Wenn die IP-Adresse, die für Eth3 konfiguriert wurde, über einen Browser `https://<your_Eth3_IP_Address>` erreicht werden kann, fahren Sie mit dem nächsten Schritt fort. 

   Stellen Sie anderenfalls eine Verbindung mit dem Eth1-Port (1GbE-B) her. Öffnen Sie Ihrem Browser und geben Sie Folgendes ein: `https://<your_Eth1_IP_Address>`. Geben Sie die Eth1-IP-Adresse für Ihre Netzkonfiguration ein. Akzeptieren Sie die Zertifikatsausnahme.<br/>
   Wenn Sie die IP-Einstellungen für Eth3 oder Eth1 ändern müssen, lesen Sie den Abschnitt [IP-Adresskonfiguration](#ip_cfg).
   {: note}

7. Verwenden Sie für die Anmeldung den Benutzernamen und das Kennwort, die Ihnen bereitgestellt wurden.<br/>
    ![Anmeldeseite](/images/Login.png)

8. Der Workflow-Assistent bietet Zugriff auf die spezifischen Elemente, die normalerweise in der Reihenfolge von links nach rechts verwendet werden.<br/>
    ![Workflow-Symbole](/images/workflow.png) <br/>
    Der Workflow kann erneut geöffnet werden, indem oben links in der Benutzeroberfläche der **Workflow-Manager** verwendet wird.
    {: note}

9. Aktivieren Sie den vorkonfigurierten Speicherpool:
    - Klicken Sie auf **Speicherpool entsperren und starten**.
    - Geben Sie die Kennphrase Ihres Speicherpools ein und klicken Sie auf **OK**.
    ![Speicherpool aktivieren](/images/UnlockPool.png)

10. Standardmäßig verfügt die Freigabe über NFS- und SMB-Protokolle, die ohne Zugriffsbeschränkungen für die Freigabe aktiviert sind. Um den Zugriff auf diese Freigabe (für NFS oder SMB) zu beschränken, klicken Sie mit der rechten Maustaste auf den Namen der Freigabe und wählen Sie das entsprechende Menüelement aus.<br/>
    ![Zugriff auf die Freigabe beschränken](/images/ShareControls.png)

11. Wenn der Speicherpool aktiviert ist, kann die gemeinsam genutzte NFS-Ressource bereitgestellt werden. Klicken Sie im Workflow auf **Netzfreigabe anzeigen**, um die Netzfreigaben anzuzeigen. Schließen Sie den Workflow, klicken Sie mit der rechten Maustaste auf die Freigabe und wählen Sie auf **Mountbefehl anzeigen**, um den Freigabenamen und die Mountinformationen anzuzeigen. Hängen Sie die Freigabe an Ihren Quellenserver an. Stellen Sie sicher, dass die IP-Adresse des 10-GB-Links beim Anhängen der Freigabe angegeben wird.
    ![Freigabe anhängen](/images/MountCommand.png)

## Schritt 4: Kopie der Daten und Versand
{: #copy-ship}

<!-- &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&

1. Run the DataShuttle copy to move the data. **[Editor's note: What is "DataShuttle"? Is "DataShuttle copy" a command that is run on PDA?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& -->

1. Kopieren Sie Ihre Daten zur gemeinsam genutzten NFS-Ressource. Wählen Sie eine der folgenden Methoden aus, um Ihre Daten aus Ihrer Netezza-Datenbank zu extrahieren:
    1. Führen Sie das folgende Beispiel des Dienstprogramms **nz_backup** aus:

       `/nz/support/contrib/bin/nz_backup –db <db_name> –d <target_directory>  ascii threads 4`

       **Hinweis**: `<target_directory>` ist die gemeinsam genutzte NFS-Ressource in der MDMS-Einheit, die an Ihren Netezza-Server angehängt wird.
   
    2. Führen Sie das folgende Beispiel der Anweisung CREATE EXTERNAL TABLE aus:

       `CREATE EXTERNAL TABLE '<path_to_mdms_device>/<file_name>' SELECT * FROM <table name>`

       **Hinweis:** Wenn Sie die Klauseloptionen `USING` für den Datenexport verwendet haben, notieren oder speichern Sie sich diese Klauseloptionen. Die Klausel wird später beim Laden der externen Tabelle von {{site.data.keyword.Bluemix_notm}} Object Storage erneut verwendet.

       Weitere Informationen zur SQL-Anweisung finden Sie unter: [Anweisung CREATE EXTERNAL TABLE ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.sql.ref.doc/doc/r_create_ext_table.html){:new_window}. 

<!--       - Provide the {{site.data.keyword.Bluemix_notm}} team with the "USING" clause that was used for data export. The clause is reused during the load process on {{site.data.keyword.Bluemix_notm}}.
       - Select FORMAT = "Text"
-->

2. Klicken Sie im Workflow auf **Netzaktivität anzeigen**, um die eingehende Ethernet-Last in der Benutzerschnittstelle anzuzeigen, während Daten über die 10-Gbit/s-Verbindung an die Einheit übertragen werden.
    ![Aktivität anzeigen](/images/UserGuide13.png)

3. Klicken Sie im Workflow auf **Speicherpool anzeigen**, um die Speicherbelegung und E/A-Operationen pro Sekunde der Einheit zu überwachen.
    ![Speicherpool anzeigen](/images/UserGuide14.png)

4. Wenn Sie das Kopieren beendet haben, schalten Sie das System ordnungsgemäß aus. Durch das Ausschalten der Einheit wird auch der Speicherpool gesperrt. Klicken Sie im Workflow auf **Einheit herunterfahren...**.  
    ![Schaltflächenposition zum Herunterfahren der Einheit](/images/Shutdown.png)

5. Trennen Sie die Verbindung zur Einheit. Legen Sie das Netzkabel, das Ethernet-Kabel und den SFP+-Adapter wieder in die entsprechenden Aufbewahrungsorte unter dem Deckel zurück.

6. Bringen Sie das mitgelieferte Versandetikett an der Einheit an. Benachrichtigen Sie den Versender und senden Sie die Einheit an das {{site.data.keyword.BluSoftlayer_full}}-Rechenzentrum zurück. Nach der Ankunft im Rechenzentrum werden Ihre Daten in Ihr {{site.data.keyword.cos_full_notm}}-Bucket geladen.

Nachdem die Einheit an das {{site.data.keyword.BluSoftlayer}}-Team zurückgegeben wurde, ändert sich der Anfragestatus zu *Einheit erhalten*.

## Schritt 5: Auslagerung und Zugriff
{: #offload}

Während des Datenübertragungsprozesses wird der Anfragestatus als *Daten werden ausgelagert* angezeigt. Der Status ändert sich erneut, wenn die Migration zum {{site.data.keyword.objectstorageshort}}-Bucket abgeschlossen ist (*Auslagerung abgeschlossen*). Ihre Daten sind sofort verfügbar, wenn die Hochgeschwindigkeitsauslagerung in Ihrem Cloud Object Storage-Bucket abgeschlossen ist. 

Wenn die Migration Ihrer Daten in den Cloud Object Storage-Bucket abgeschlossen ist, können Sie mit dem [Import Ihrer Daten in Ihre {{site.data.keyword.dashdbshort_notm}}-Datenbank fortfahren](#import).

## Schritt 6: Datenimport aus {{site.data.keyword.Bluemix_notm}} Object Storage
{: #import}

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

**Hinweise:** 
* Stellen Sie sicher, dass Sie die gleichen `USING`-Klauseloptionen verwenden, die Sie zum Extrahieren der Daten aus Ihrer PureData System für Analytics-Datenbank (Netezza) mithilfe der Anweisung CREATE EXTERNAL TABLE verwendet haben.
* Wenn Sie {{site.data.keyword.Bluemix_notm}} Object Storage zum Erstellen von HMAC-Anmeldeinformationen beim Erstellen neuer Dienstanmeldeinformationen verwenden möchten, geben Sie {"HMAC:true"} im Feld *Inline-Konfigurationsparameter* hinzufügen an.

Eine Anleitung zum Importieren von Daten aus {{site.data.keyword.Bluemix_notm}} Object Storage finden Sie in [IBM Db2 Warehouse on Cloud geführte Demo: Laden von Daten erkunden ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud/){:new_window}.

## Schritt 7: Löschen von Daten der MDMS-Einheit
{: #erase}

{{site.data.keyword.IBM}} implementiert eine Datenbereinigung auf der Ebene der Anforderungen des US-Verteidigungsministeriums, um Ihre Daten dauerhaft von der MDMS-Einheit zu löschen. Wenn Sie fertig sind, wird Ihr Anfragestatus als *Löschen abgeschlossen* angezeigt.

## Weitere Hinweise
{: #notes}

### Eindeutigkeit im Bucket

Um sicherzustellen, dass die Objektnamen eindeutig sind, wenn sie in den Bucket kopiert werden, wird der Dateipfad als Präfix in den Objektnamen eingefügt. Beispiel: Die Datei "config.ini" im Ordner `/root/user/` wird in "root/user/config.ini" umbenannt, wenn sie zum Bucket kopiert wird.

### Buckets

Wenn das Ziel-Bucket nicht vorhanden ist, wird es erstellt. Wenn es vorhanden ist, muss es leer sein, sonst kann der Kopiervorgang nicht fortgesetzt werden.

### Dateisysteme

Symbolische und feste Verbindungen werden während des Prüfvorgangs übersprungen.

### IP-Adresskonfiguration
{: #ip_cfg}

Über den LCD-Bildschirm an der Einheit können die IP-Adressen für die Ethernet-Ports konfiguriert werden. Sie navigieren im LCD-Bildschirm mit dem **Aufwärtspfeil**, **Abwärtspfeil** sowie mit der **ESC-Taste** und **Eingabetaste**. Mit der **Eingabetaste** rufen Sie ein Menü auf und mit der **ESC-Taste** verlassen Sie ein Menü.

![LCD-Bildschirm](/images/MDMSLCD.png)

Beim Bearbeiten einer IP-Adresse oder einer Teilnetzmaske können Sie mit der **Eingabetaste** jeweils ein Zeichen nach vorn blättern. Mit der **ESC-Taste** blättern Sie ein Zeichen zurück. Mit dem **Aufwärtspfeil** und **Abwärtspfeil** wechseln Sie zwischen den Zahlen der ausgewählten Position.

Verwenden Sie die **ESC-Taste**, um zum vorherigen Menü zurückzukehren.  

Gehen Sie zum Menüelement **Aktualisieren...** und drücken Sie die **Eingabetaste**, um die Einstellungen zu speichern.
