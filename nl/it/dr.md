---

copyright:
  years: 2014, 2019
lastupdated: "2019-04-16"

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

# Ripristino di emergenza (DR, Disaster Recovery)
{: #dr}

<!-- If your data warehouse instance is deployed in a data center that suffers a significant data center outage with an expected downtime of more than 8 hours, you will be sent a request to allow service operators to fail over your instance to another data center before disaster recovery actions can begin.
{: shortdesc}

A Db2 backup of your database is done every day, except for the Flex plan where a Db2 backup is done every 7 days and a snapshot backup is done daily. Daily backups are stored in the IBM Cloud Object Storage service from which it is replicated to multiple availability zones. If something should happen to your primary data center, our service operators will work with you to stand up your recovered database in a secondary data center. -->

La strategia di ripristino di emergenza dipende dal tipo di generazione del piano e del data warehouse che stai utilizzando al momento.
{: shortdesc}

Per i piani SMP Small, Medium, Large e MPP Small di prima generazione, viene eseguito un backup una volta al giorno e viene distribuito al servizio {{site.data.keyword.Bluemix_notm}} Object Storage. Da lì, il backup viene replicato in più zone di disponibilità. Se si verifica un evento di emergenza nel tuo data center primario, i nostri operatori del servizio lavoreranno con te per impostare un nuovo data warehouse in un data center diverso. Utilizzeremo il backup giornaliero che si trova nel servizio {{site.data.keyword.Bluemix_notm}} Object Storage. 

Per i piani Flex di seconda generazione su {{site.data.keyword.Bluemix_notm}}, viene eseguito un backup una volta a settimana e viene distribuito al servizio {{site.data.keyword.Bluemix_notm}} Object Storage. Da lì, il backup viene replicato in più zone di disponibilità. Se si verifica un evento di emergenza nel tuo data center primario, i nostri operatori del servizio lavoreranno con te per impostare un nuovo data warehouse in un data center diverso. Utilizzeremo il backup settimanale che si trova nel servizio {{site.data.keyword.Bluemix_notm}} Object Storage.

Per i piani Flex di seconda generazione su AWS (Amazon Web Services), viene scaricato automaticamente in AWS S3 un backup giornaliero automatico. Quando si trova in S3, il backup viene replicato in più regioni. Se si verifica un evento di emergenza, verrà utilizzato il backup più recente per ripristinare il tuo cluster in un data center secondario. 

## **Brasile: regola supplementare 14** (si applica ai sistemi forniti al governo federale brasiliano)
{: #rule_14}

In questo momento, l'opzione di ripristino di emergenza (DR) per le offerte {{site.data.keyword.dashdbshort_notm}} non è disponibile in Brasile per il governo federale a causa della regola supplementare 14. 

