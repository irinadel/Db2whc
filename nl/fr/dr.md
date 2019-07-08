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

# Reprise après incident
{: #dr}

<!-- If your data warehouse instance is deployed in a data center that suffers a significant data center outage with an expected downtime of more than 8 hours, you will be sent a request to allow service operators to fail over your instance to another data center before disaster recovery actions can begin.
{: shortdesc}

A Db2 backup of your database is done every day, except for the Flex plan where a Db2 backup is done every 7 days and a snapshot backup is done daily. Daily backups are stored in the IBM Cloud Object Storage service from which it is replicated to multiple availability zones. If something should happen to your primary data center, our service operators will work with you to stand up your recovered database in a secondary data center. -->

La stratégie de reprise après incident dépend du type de plan et de la génération d'entrepôt de données que vous effectuez actuellement.
{: shortdesc}

## Première génération des plans SMP Small, Medium, Large et MPP Small
{: #sml_mpp}

Pour la première génération des plans SMP Small, Medium, Large et MPP Small, une sauvegarde est effectuée une fois par jour et déployée dans le service {{site.data.keyword.Bluemix_notm}} Object Storage. Ensuite, la sauvegarde est répliquée dans plusieurs zones de disponibilité. Si un événement catastrophique se produit sur le centre de données principal, nos opérateurs de service vous aideront à mettre en place un nouvel entrepôt de données dans un autre centre de données. Pour ce faire, ils utiliseront la sauvegarde quotidienne qui se trouve sur le service {{site.data.keyword.Bluemix_notm}} Object Storage.

## Seconde génération des plans Flex sur IBM Cloud
{: #flex_ibm_cloud}

Pour la seconde génération des plans Flex sur {{site.data.keyword.Bluemix_notm}}, une sauvegarde est effectuée une fois par semaine et déployée dans le service {{site.data.keyword.Bluemix_notm}} Object Storage. Ensuite, la sauvegarde est répliquée dans plusieurs zones de disponibilité. Si un événement catastrophique se produit sur le centre de données principal, nos opérateurs de service vous aideront à mettre en place un nouvel entrepôt de données dans un autre centre de données. Pour ce faire, ils utiliseront la sauvegarde hebdomadaire qui se trouve sur le service {{site.data.keyword.Bluemix_notm}} Object Storage.

## Seconde génération des plans Flex plans sur Amazon Web Services
{: #flex_aws}

Pour la seconde génération des plans Flex sur Amazon Web Services, une sauvegarde quotidienne en libre-service est automatiquement déchargée sur Amazon Web Services S3. En S3, la sauvegarde est répliquée dans plusieurs régions. Si un événement catastrophique se produit, la dernière sauvegarde est utilisée pour restaurer votre cluster dans un centre de données secondaire.

## **Brésil : règle supplémentaire n°14** (s'applique aux systèmes mis à disposition pour le gouvernement fédéral brésilien)
{: #rule_14}

Actuellement, l'option de reprise après incident des offres {{site.data.keyword.dashdbshort_notm}} n'est pas disponible au Brésil pour le gouvernement fédéral en raison de la règle supplémentaire n° 14.

