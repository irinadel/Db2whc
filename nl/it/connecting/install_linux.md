---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# Installazione del pacchetto del driver su Linux o PowerLinux
{: #install_dr_pkg_linux}

Puoi installare il pacchetto del driver {{site.data.keyword.dashdbshort_notm}}su Linux o PowerLinux utilizzando `installDSDriver`. 
{: shortdesc}

## Prerequisiti
{: #prereq31}

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) necessari.

<!-- Download the Db2 driver package for your operating system from the web console and install it. -->

**Solo su PowerLinux**, completa la seguente procedura per installare il pacchetto di runtime del compilatore XL C/C++:

1. Scarica il pacchetto di runtime del compilatore XL C/C++ dal sito FTP. Ad esempio, per utilizzare lo strumento **wget** per scaricare il pacchetto di runtime per Linux little endian Ubuntu 14, immetti il seguente comando: 

   `wget ftp://public.dhe.ibm.com/software/server/POWER/Linux/rte/xlcpp/le/ubuntu/dists/trusty/main/binary-ppc64el/*`
2. Installa il pacchetto di runtime immettendo il seguente comando:

   `sudo dpkg -iG *.deb` 

## Procedura
{: #proc31}

1. Decomprimi il file del pacchetto del driver compresso che hai scaricato in precedenza.

   Esempio: 

   `gunzip file_name.tar.gz`

   `tar -xvf file_name.tar`

    Viene creata una sottodirectory `dsdriver` nella directory in cui hai eseguito i comandi di decompressione.
2. Estrai i driver Java e ODBC/CLI.

   a. Nella sottodirectory `dsdriver`, esegui il comando **installDSDriver** .
   
   Il comando **installDSDriver** crea i file script `db2profile` e `db2cshrc` nella directory `dsdriver`.

   b. Esegui uno dei seguenti file script in base al tuo ambiente shell:

   - **Shell Bash o Korn**: `source db2profile`
   - **Shell C**: `source db2cshrc`

## Operazioni successive
{: #wn}

Per poter collegare le tue applicazioni locali o i tuoi strumenti client al tuo database {{site.data.keyword.dashdbshort_notm}}, [configura il tuo ambiente locale](/docs/services/Db2whc?topic=Db2whc-cfg_loc_env#cfg_loc_env).   




