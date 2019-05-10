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

# Treiberpaket unter Linux oder PowerLinux installieren
{: #install_dr_pkg_linux}

Sie können das {{site.data.keyword.dashdbshort_notm}}-Treiberpaket über das Script `installDSDriver` unter Linux oder PowerLinus installieren. 
{: shortdesc}

## Voraussetzungen
{: #prereq31}

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) erfüllt werden.

<!-- Download the Db2 driver package for your operating system from the web console and install it. -->

**Nur PowerLinux **: Führen Sie zum Installieren des Laufzeitpakets des C/C++-Compilers die folgenden Schritte aus:

1. Laden Sie das Laufzeitpaket des XL C/C++-Compilers von der FTP-Site herunter. Laden Sie das Laufzeitpaket für Linux, Little Endian, Ubuntu 14 mit dem Tool **wget** beispielsweise herunter, indem Sie den folgenden Befehl absetzen: 

   `wget ftp://public.dhe.ibm.com/software/server/POWER/Linux/rte/xlcpp/le/ubuntu/dists/trusty/main/binary-ppc64el/*`
2. Installieren Sie das Laufzeitpaket mit dem folgenden Befehl:

   `sudo dpkg -iG *.deb` 

## Vorgehensweise
{: #proc31}

1. Dekomprimieren Sie die Datei mit dem komprimierten Treiberpaket, die Sie zuvor heruntergeladen haben.

   Beispiel: 

   `gunzip file_name.tar.gz`

   `tar -xvf file_name.tar`

    In dem Verzeichnis, in dem Sie die Dekomprimierungsbefehle ausgeführt haben, wird ein Unterverzeichnis namens `dsdriver` erstellt.
2. Extrahieren Sie die Java- und ODBC/CLI-Treiber.

   a. Führen Sie im Unterverzeichnis `dsdriver` den Befehl **installDSDriver** aus.
   
   Über den Befehl **installDSDriver** werden die Scriptdateien `db2profile` und `db2cshrc` im Verzeichnis `dsdriver` erstellt.

   b. Führen Sie je nach Shellumgebung eine der folgenden Scriptdateien aus:

   - **Bash- oder Korn-Shell**: `source db2profile`
   - **C-Shell**: `source db2cshrc`

## Nächster Schritt
{: #wn}

[Konfigurieren Sie die lokale Umgebung](/docs/services/Db2whc?topic=Db2whc-cfg_loc_env#cfg_loc_env), damit lokale Anwendungen und Client-Tools eine Verbindung zur {{site.data.keyword.dashdbshort_notm}}-Datenbank herstellen können.   




