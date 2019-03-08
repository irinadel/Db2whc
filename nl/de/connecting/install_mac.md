---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# Treiberpaket unter Mac OS X installieren
{: #install_dr_pkg_mac}

Sie können das {{site.data.keyword.dashdbshort_notm}}-Treiberpaket über das Script `installDSDriver.sh` unter MAC OS X installieren. 
{: shortdesc}

## Voraussetzungen
{: #prereq41}

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](/docs/services/Db2whc/connecting/connecting.html#prereqs) erfüllt werden.

<!-- Download the Db2 driver package for your operating system from the web console and install it. -->

## Vorgehensweise
{: #proc41}

- **Neue Installation**

  1. Hängen Sie das Plattenimage an, indem Sie doppelt auf die Datei `macos_dsdriver.dmg` klicken.
   
     Es wird ein neues **Finder**-Fenster mit dem Inhalt des Plattenimages geöffnet.

     Sollte das **Finder**-Fenster nicht angezeigt werden, klicken Sie doppelt auf das Symbol `macos_dsdriver` auf Ihrem Desktop.
  2. Klicken Sie im **Finder**-Fenster doppelt auf die Datei `installDSDriver.sh`.

     Das Treiberpaket wird in dem folgenden Standardverzeichnis installiert: `/Applications/dsdriver`.

- **Aktualisierungen für vorhandene Treiberpaketinstallation**

  1. Sichern Sie die aktuellen Konfigurationsdateien:

     a. Wechseln Sie zum Ordner `Applications/dsdriver/cfg`.

     b. Kopieren Sie die folgenden Dateien in einen anderen Ordner: 
    
        `db2cli.ini`

        `db2dsdriver.cfg`
  2. Entfernen Sie das derzeit installierte Treiberpaket, indem Sie mit der rechten Maustaste auf den Ordner `dsdriver` klicken und die Papierkorboption **** auswählen.
  3. Installieren Sie das neue Treiberpaket wie im vorherigen Abschnitt **Neue Installation** beschrieben:
     
     a. Hängen Sie das Plattenimage an, indem Sie doppelt auf die Datei `macos_dsdriver.dmg` klicken.
     b. Klicken Sie im **Finder**-Fenster doppelt auf die Datei `installDSDriver.sh`.
  4. Stellen Sie die Konfigurationsdateien wieder her:

     Kopieren Sie die Dateien `db2cli.ini` und `db2dsdriver.cfg`, die Sie in Schritt 1 im Ordner `/Applications/dsdriver/cfg` gesichert haben.

## Nächster Schritt
{: #wn41}

[Konfigurieren Sie die lokale Umgebung](/docs/services/Db2whc/connecting/driver_pkg_cfg.html), damit lokale Anwendungen und Client-Tools eine Verbindung zur {{site.data.keyword.dashdbshort_notm}}-Datenbank herstellen können.
