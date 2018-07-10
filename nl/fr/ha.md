---

copyright:
  years: 2014, 2018
lastupdated: "2018-04-30"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Haute disponibilité 
{: #ha}

La mesure de la réussite d'une solution de base de données est sa disponibilité. {{site.data.keyword.dashdblong}} propose des plans de haute disponibilité pour permettre à vos charges de travail de continuer à fonctionner.
{: shortdesc}

## Plan MPP
{: #ha_mpp}

Le cluster du plan {{site.data.keyword.dashdbshort_notm}} MPP est mis à disposition avec la haute disponibilité.  

Lorsqu'un noeud tombe en panne dans un plan MPP, le composant de haute disponibilité redémarre les partitions de votre base de données dans les noeuds sains restants. Le système connaît alors un bref temps d'indisponibilité. 

Une fois le noeud revenu dans le cluster, le moteur de base de données doit être redémarré pour pouvoir s'exécuter à pleine capacité. 

## Plan Flex Performance
{: #ha_flex}

En cas de défaillance de noeud inattendue, le cluster Flex Performance MPP est ramené à sa pleine capacité après un bref temps d'indisponibilité lié à l'utilisation d'IBM Container Service (basé sur Kubernetes). Les noeuds d'un pool sont utilisés pour déplacer les entités de noeud défaillantes. 

### Haute disponibilité de traitement
{: #compute_ha}

Les défaillances de noeud sont immédiatement détectées par le service de conteneur. Les conteneurs et les pods qui s'exécutent dans le noeud défaillant sont planifiés vers un nouveau noeud situé dans un pool de noeuds. Le système revient à un fonctionnement normal à 100 % après un bref temps d'indisponibilité.

### Haute disponibilité du stockage
{: #storage_ha}

Votre stockage est configuré avec une implémentation RAID6 à double parité qui offre une protection par rapport aux pannes de disque en double dans le même groupe RAID et fournit ainsi des performances élevées et un stockage haute disponibilité à votre système.

### Haute disponibilité du réseau
{: #net_ha}

Les connexions réseau sont hautement disponibles grâce à la mise à disposition de votre service avec une carte d'interface réseau redondante. 

Si le service de conteneur détecte un problème réseau, les pods et les conteneurs peuvent redémarrer automatiquement après un bref temps d'indisponibilité.
