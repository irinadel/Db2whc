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

# Treiberpaket unter Windows installieren
{: #install_dr_pkg_windows}

Sie können das {{site.data.keyword.dashdbshort_notm}}-Treiberpaket über das Installationsprogramm unter Windows installieren. 
{: shortdesc}

## Voraussetzungen
{: #prereq51}

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) erfüllt werden.

<!-- Download the driver package for your operating system from the web console and install it. -->

## Vorgehensweise
{: #proc51}

1. Führen Sie die heruntergeladene ausführbare Datei als Administrator aus.

   Standardmäßig wird für das Treiberpaket der folgende Installationspfad verwendet: `Programme\IBM\IBM DATA SERVER DRIVER`.
2. [*Optional*] Fügen Sie das Unterverzeichnis `bin` des Installationsverzeichnisses für das Treiberpaket zu der Umgebungsvariable `%PATH%` hinzu. Auf diese Weise können Sie den Befehl **db2cli** ohne Angabe des vollständigen Pfads zur ausführbaren Datei für den Befehl ausführen.

## Nächster Schritt
{: #wn51}

[Konfigurieren Sie die lokale Umgebung](/docs/services/Db2whc?topic=Db2whc-cfg_loc_env#cfg_loc_env), damit lokale Anwendungen und Client-Tools eine Verbindung zur {{site.data.keyword.dashdbshort_notm}}-Datenbank herstellen können.
