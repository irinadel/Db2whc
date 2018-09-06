---

copyright:
  years: 2014, 2018
lastupdated: "2018-05-10"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Sauvegarde et restauration
{: #br}

Une sauvegarde chiffrée de la totalité de la base de données {{site.data.keyword.dashdbshort_notm}} est réalisée quotidiennement.
{: shortdesc}

| Plan              | Fréquence de sauvegarde | Nombre de sauvegardes conservées | Période de conservation des sauvegardes   | Libre service |
|-------------------|------------------|----------------------------|---------------------------|--------------|
| MPP               | 1 / jour          | 2                          | 2 jours ; FIFO*   | Non           |
| Flex Performance  | 1 / jour          | 7                          | 7 jours ; FIFO*   | Oui          |
{: caption="Tableau 1. Fréquence et conservation des sauvegardes" caption-side="top"}

*First in, first out

## Plans SMP et MPP
{: #smp_mpp}

Les 2 dernières sauvegardes quotidiennes sont conservées.

Les sauvegardes conservées sont utilisées exclusivement par IBM, à des fins de restauration uniquement, dans le cas d'incident ou de perte de données. Les demandes de restauration de votre base de données à partir d'une sauvegarde ne sont pas prises en compte. Vous pouvez exporter vos données à l'aide d'outils Db2 tels qu'IBM Data Studio ou de la commande **db2 export**. 

## Plan Flex Performance
{: #flex}

Les 7 dernières images instantanées de sauvegarde quotidienne sont conservées.

Depuis la console {{site.data.keyword.dashdbshort_notm}}, vous pouvez planifier l'exécution de vos sauvegardes au moment qui vous convient le mieux et restaurer votre base de données à partir de l'une des images instantanées de sauvegarde conservées, au moment que vous choisissez. Le système s'arrête pendant la restauration. Un courrier électronique vous avertit ensuite que l'opération de restauration est terminée.

![Vue de la page de sauvegarde et de restauration de la console Web](images/br.png)

