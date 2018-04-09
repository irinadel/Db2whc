---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-15"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Haute disponibilité (HA) : plan Flex Performance
{: #ha_flex}

En cas de défaillance de noeud inattendue, le cluster Flex Performance MPP est ramené à sa pleine capacité après un bref temps d'indisponibilité lié à l'utilisation d'IBM Container Service (basé sur Kubernetes). Les noeuds d'un pool sont utilisés pour déplacer les entités de noeud défaillantes.
{: shortdesc}

## Haute disponibilité de traitement
{: #compute_ha}

Les défaillances de noeud sont immédiatement détectées par le service de conteneur. Les conteneurs et les pods qui s'exécutent dans le noeud défaillant sont planifiés vers un nouveau noeud situé dans un pool de noeuds. Le système revient à un fonctionnement normal à 100 % après un bref temps d'indisponibilité.

## Haute disponibilité du stockage
{: #storage_ha}

Votre stockage est configuré avec une implémentation RAID6 à double parité qui offre une protection par rapport aux pannes de disque en double dans le même groupe RAID et fournit ainsi des performances élevées et un stockage haute disponibilité à votre système.

## Haute disponibilité du réseau
{: #net_ha}

Les connexions réseau sont hautement disponibles grâce à la mise à disposition de votre service avec une carte d'interface réseau redondante.  

Si le service de conteneur détecte un problème réseau, les pods et les conteneurs peuvent redémarrer automatiquement après un bref temps d'indisponibilité.
