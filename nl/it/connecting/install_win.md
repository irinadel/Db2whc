---

copyright:
  years: 2014, 2018
lastupdated: "2018-09-25"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Installazione del pacchetto del driver su Windows

Puoi installare il pacchetto del driver {{site.data.keyword.dashdbshort_notm}} su Windows utilizzando il programma di installazione.
{: shortdesc}

## Prerequisiti

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](connecting.html#prereqs) necessari.

<!-- Download the driver package for your operating system from the web console and install it. -->

## Procedura

1. Esegui il file eseguibile scaricato come amministratore.

   Il percorso di installazione predefinito del pacchetto del driver è: `Program Files\IBM\IBM DATA SERVER DRIVER`
2. [*Facoltativo*] Aggiungi la sottodirectory `bin` della directory di installazione del pacchetto del driver alla tua variabile di ambiente `%PATH%` (in modo da poter eseguire il comando **db2cli** senza specificare il percorso completo per l'eseguibile del comando.)

## Operazioni successive

Per poter collegare le tue applicazioni locali o i tuoi strumenti client al tuo database {{site.data.keyword.dashdbshort_notm}}, [configura il tuo ambiente locale](driver_pkg_cfg.html).
