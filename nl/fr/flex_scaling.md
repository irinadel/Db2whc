---

copyright:
  years: 2014, 2019
lastupdated: "2018-05-01"

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

# Mise à l'échelle flexible
{: #scale}

Le plan Flex Performance offre une mise à l'échelle du stockage et des coeurs de traitement, indépendante. 
{: shortdesc}

Avant de mettre à disposition votre système Flex Performance, vous pouvez effectuer des ajustements initiaux en anticipant vos besoins en matière de stockage et de coeurs de traitement puis soumettre vos choix.

Une fois le système mis à disposition, si vos besoins évoluent, vous pouvez modifier les exigences de stockage et de coeurs de traitement en lançant la page relative à l'instance de mise à l'échelle depuis la page de gestion du service et en utilisant les barres de curseur.

![Vue de la page des coeurs de traitement de la console Web](images/launch.png)

![Vue de la page des coeurs de traitement de la console Web](images/scaling_full.png)


## Coeurs de traitement
{: #cores}

Vous pouvez ajuster vos coeurs de traitement en les augmentant ou les diminuant. Un coeur de traitement change les résultats en cas de courte indisponibilité du système pouvant aller jusqu'à 45 minutes. Vous pouvez planifier ce temps d'indisponibilité à un moment qui vous convient ou lancer le changement des coeurs de traitement de manière immédiate.

![Vue de la page des coeurs de traitement de la console Web](images/cores.png)

## Stockage
{: #storage}

Vous pouvez augmenter votre stockage. Les changements liés au stockage n'entraînent aucun temps d'indisponibilité.

![Vue de la page de stockage de la console Web](images/storage.png)

## Mémoire
{: #ram}

La mémoire RAM est allouée proportionnellement avec un ratio fixe quand le nombre de coeurs de traitement est modifié.

