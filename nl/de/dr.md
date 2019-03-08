---

copyright:
  years: 2014, 2019
lastupdated: "2018-11-21"

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

# Disaster-Recovery (DR)
{: #dr}

Wenn Ihre Data-Warehouse-Instanz in einem Rechenzentrum bereitgestellt wird und ein nennenswerter Ausfall des Rechenzentrums mit einer erwarteten Ausfallzeit von mehr als 8 Stunden auftritt, wird Ihnen eine Anfrage zugesendet, ob Service-Betreiber Ihre Instanz in einem anderen Rechenzentrum übernehmen dürfen, bevor Disaster-Recovery-Aktionen ausgeführt werden.
{: shortdesc}

Eine Db2-Sicherung Ihrer Datenbank wird täglich durchgeführt. Eine Ausnahme bildet der Flex-Plan, bei dem alle 7 Tage eine Db2-Sicherung und täglich eine Momentaufnahmesicherung durchgeführt werden. Die täglichen Sicherungen werden über den Service 'IBM Cloud Object Storage' gespeichert und über diesen Service in Verfügbarkeitszonen repliziert. Sollte ein gravierender Fehler beim primären Rechenzentrum auftreten, werden die Servicebetreiber gemeinsam mit Ihnen für die Einrichtung der wiederhergestellten Datenbank in einem sekundären Rechenzentrum sorgen.

## **Brasilien: Zusatzregel 14** (betrifft für die Bundesregierung von Brasilien bereitgestellte Systeme)
{: #rule_14}

Die Option für Disaster-Recovery (DR) ist für Db2 Warehouse on Cloud-Angebote derzeit für die Bundesregierung in Brasilien aufgrund von Zusatzregel 14 nicht verfügbar.

