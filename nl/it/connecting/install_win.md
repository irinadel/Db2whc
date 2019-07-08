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

# Installazione del pacchetto del driver su Windows
{: #install_dr_pkg_windows}

Puoi installare il pacchetto del driver {{site.data.keyword.dashdbshort_notm}} su Windows utilizzando il programma di installazione. 
{: shortdesc}

## Prerequisiti
{: #prereq51}

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) necessari.

<!-- Download the driver package for your operating system from the web console and install it. -->

## Procedura
{: #proc51}

1. Esegui il file eseguibile scaricato come amministratore.

   Il percorso di installazione predefinito del pacchetto del driver è: `Program Files\IBM\IBM DATA SERVER DRIVER`
2. [*Facoltativo*] Aggiungi la sottodirectory `bin` della directory di installazione del pacchetto del driver alla tua variabile di ambiente `%PATH%` (in modo da poter eseguire il comando **db2cli** senza specificare il percorso completo per l'eseguibile del comando.)

## Operazioni successive
{: #wn51}

Per poter collegare le tue applicazioni locali o i tuoi strumenti client al tuo database {{site.data.keyword.dashdbshort_notm}}, [configura il tuo ambiente locale](/docs/services/Db2whc?topic=Db2whc-cfg_loc_env#cfg_loc_env).
