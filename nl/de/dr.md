---

copyright:
  years: 2014, 2019
lastupdated: "2019-04-16"

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

# Disaster-Recovery (DR)
{: #dr}

<!-- If your data warehouse instance is deployed in a data center that suffers a significant data center outage with an expected downtime of more than 8 hours, you will be sent a request to allow service operators to fail over your instance to another data center before disaster recovery actions can begin.
{: shortdesc}

A Db2 backup of your database is done every day, except for the Flex plan where a Db2 backup is done every 7 days and a snapshot backup is done daily. Daily backups are stored in the IBM Cloud Object Storage service from which it is replicated to multiple availability zones. If something should happen to your primary data center, our service operators will work with you to stand up your recovered database in a secondary data center. -->

Die Disaster-Recovery-Strategie hängt vom Typ des Plans und der Data-Warehouse-Generation ab, die Sie aktuell ausführen.
{: shortdesc}

## Pläne der ersten Generation: SMP Small, Medium, Large und MPP Small
{: #sml_mpp}

Für die erste Generation (Pläne: SMP Small, Medium, Large und MPP Small) wird täglich einmal ein Backup erstellt und dem {{site.data.keyword.Bluemix_notm}} Object Storage-Service bereitgestellt. Von dort wird das Backup in mehrere verfügbare Zonen repliziert. Sollte im primären Rechenzentrum schwerwiegender Fehler auftreten, werden unsere Servicemitarbeiter gemeinsam mit Ihnen für die Einrichtung eines neuen Data-Warehouses in einem anderen Rechenzentrum sorgen. Wir verwenden dabei die tägliche Sicherung, die sich im {{site.data.keyword.Bluemix_notm}} Object Storage-Service befindet.

## Flex-Pläne der zweiten Generation in IBM Cloud
{: #flex_ibm_cloud}

Bei der zweiten Generation (Flex-Pläne in {{site.data.keyword.Bluemix_notm}}) wird einmal wöchentlich eine Sicherung erstellt und dem {{site.data.keyword.Bluemix_notm}} Object Storage-Service bereitgestellt. Von dort wird das Backup in mehrere verfügbare Zonen repliziert. Sollte im primären Rechenzentrum schwerwiegender Fehler auftreten, werden unsere Servicemitarbeiter gemeinsam mit Ihnen für die Einrichtung eines neuen Data-Warehouses in einem anderen Rechenzentrum sorgen. Wir verwenden dabei die wöchentliche Sicherung, die sich im {{site.data.keyword.Bluemix_notm}} Object Storage-Service befindet.

## Flex-Pläne der zweiten Generation in Amazon-Web-Services
{: #flex_aws}

Für die Flex-Pläne der zweiten Generation in Amazon-Web-Services wird automatisch ein tägliches Self-Service-Backup in Amazon-Web-Service S3 ausgelagert. Wenn das Backup in S3 ist, wird es in mehrere Regionen repliziert. Wenn ein schwerwiegender Fehler auftritt, wird das aktuellste Backup verwendet, um Ihre Cluster in einem zweiten Rechenzentrum wiederherzustellen.

## **Brasilien: Zusatzregel 14** (betrifft für die Bundesregierung von Brasilien bereitgestellte Systeme)
{: #rule_14}

Zum gegenwärtigen Zeitpunkt ist die DR-Option (Disaster Recovery) für {{site.data.keyword.dashdbshort_notm}}-Angebote aufgrund der ergänzenden Regel 14 für Systeme, die für die brasilianische Regierung eingerichtet werden, nicht verfügbar.

