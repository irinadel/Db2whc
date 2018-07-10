---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-16"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Haute disponibilité : plan MPP
{: #ha_smp_mpp}

Le cluster du plan {{site.data.keyword.dashdblong}} MPP est mis à disposition avec la haute disponibilité.  
{: shortdesc}

Lorsqu'un noeud tombe en panne dans un plan MPP, le composant de haute disponibilité redémarre les partitions de votre base de données dans les noeuds sains restants. Le système connaît alors un bref temps d'indisponibilité. 

Une fois le noeud revenu dans le cluster, le moteur de base de données doit être redémarré pour pouvoir s'exécuter à pleine capacité. 

