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

# Reprise après incident
{: #dr}

Si votre instance d'entrepôt de données est déployée dans un centre de données qui subit une panne importante avec un temps d'arrêt prévu de plus de 8 heures, une demande vous sera envoyée pour permettre aux opérateurs de service de basculer votre instance sur un autre centre de données avant toute intervention de reprise après incident.
{: shortdesc}

Une sauvegarde Db2 de votre base de données est effectuée chaque jour. Les sauvegardes quotidiennes sont stockées dans le service IBM Cloud Object Storage à partir duquel elles sont répliquées dans plusieurs zones de disponibilité. Si quelque chose devait arriver à votre centre de données principal, nos opérateurs de service travailleront avec vous pour mettre en place votre base de données récupérée dans un centre de données secondaire.

## **Brésil : règle supplémentaire n°14** (s'applique aux systèmes mis à disposition pour le gouvernement fédéral brésilien)
{: #rule_14}

Actuellement, l'option de reprise après incident des offres Db2 Warehouse on Cloud n'est pas disponible au Brésil pour le gouvernement fédéral en raison de la règle supplémentaire n°14.

