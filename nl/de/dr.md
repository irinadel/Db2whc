---

copyright:
  years: 2014, 2018
lastupdated: "2018-10-22"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}

# Disaster-Recovery (DR)
{: #dr}

Wenn Ihre Data-Warehouse-Instanz in einem Rechenzentrum bereitgestellt wird und ein nennenswerter Ausfall des Rechenzentrums mit einer erwarteten Ausfallzeit von mehr als 8 Stunden auftritt, wird Ihnen eine Anfrage zugesendet, ob Service-Betreiber Ihre Instanz in einem anderen Rechenzentrum übernehmen dürfen, bevor Disaster-Recovery-Aktionen ausgeführt werden.
{: shortdesc}

Täglich wird eine Db2-Sicherung für Ihre Datenbank durchgeführt. Die täglichen Backups werden über den Service 'IBM Cloud Object Storage' gespeichert und über diesen Service in Verfügbarkeitszonen repliziert. Sollte ein gravierender Fehler beim primären Rechenzentrum auftreten, werden die Servicebetreiber gemeinsam mit Ihnen für die Einrichtung der wiederhergestellten Datenbank in einem sekundären Rechenzentrum sorgen. 

## **Brasilien: Zusatzregel 14** (betrifft für die Bundesregierung von Brasilien bereitgestellte Systeme)
{: #rule_14}

Die Option für Disaster-Recovery (DR) ist für Db2 Warehouse on Cloud-Angebote derzeit für die Bundesregierung in Brasilien aufgrund von Zusatzregel 14 nicht verfügbar. 

