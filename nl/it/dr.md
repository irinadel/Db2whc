---

copyright:
  years: 2014, 2019
lastupdated: "2018-11-21"

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

# Ripristino di emergenza (DR, Disaster Recovery)
{: #dr}

Se la tua istanza data warehouse viene distribuita in un data center che risente di un'interruzione significativa del data center con un tempo di inattività previsto superiore alle 8 ore, ti verrà inviato un messaggio per consentire agli operatori del servizio di eseguire il failover a un altro data center prima che possano iniziare le azioni di ripristino di emergenza.
{: shortdesc}

Un backup Db2 del tuo database viene eseguito ogni giorno, con l'eccezione del piano Flex dove viene effettuato un backup Db2 ogni 7 giorni e un backup delle istantanee giornaliero. I backup giornalieri sono archiviati nel servizio IBM Cloud Object Storage da cui vengono replicati in più zone di disponibilità. Se dovesse capitare qualcosa al tuo data center primario, i nostri operatori del servizio lavoreranno con te per impostare il tuo database ripristinato in un data center secondario.

## **Brasile: regola supplementare 14** (si applica ai sistemi forniti al governo federale brasiliano)
{: #rule_14}

In questo momento, l'opzione di ripristino di emergenza (DR) per le offerte Db2 Warehouse on Cloud non è disponibile in Brasile per il governo federale a causa della regola supplementare 14.

