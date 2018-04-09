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

# Sauvegarde et restauration
{: #br}

Une sauvegarde chiffrée de la totalité de la base de données {{site.data.keyword.dashdbshort_notm}} est réalisée quotidiennement. Dans le cas du plan Flex Performance, les 7 dernières images instantanées de sauvegarde quotidienne sont conservées. Dans le cas des plans SMP et MPP, les 2 dernières sauvegardes quotidiennes sont conservées.
{: shortdesc}

Le plan Flex Performance vous permet de planifier l'exécution de vos sauvegardes au moment qui vous convient le mieux et de restaurer votre base de données à partir de n'importe quelle image instantanée de sauvegarde conservée à n'importe quel moment. Le système s'arrête pendant la restauration. Un courrier électronique vous avertit ensuite que l'opération de restauration est terminée.

Dans le cas de plans SMP et MPP, les sauvegardes conservées sont utilisées exclusivement par IBM uniquement à des fins de restauration dans le cas d'incident ou de perte de données. Les demandes de restauration de votre base de données à partir d'une sauvegarde ne sont pas prises en compte. Vous pouvez exporter vos données à l'aide d'outils Db2 tels qu'IBM Data Studio ou de la commande **db2 export**. 
