---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

keywords:

subcollection: Db2whc

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

# Installation du module de pilote sur Windows
{: #install_dr_pkg_windows}

Vous pouvez installer le module de pilote {{site.data.keyword.dashdbshort_notm}} sur Windows à l'aide du programme d'installation. 
{: shortdesc}

## Prérequis
{: #prereq51}

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](/docs/services/Db2whc/connecting/connecting.html#prereqs) sont remplies.

<!-- Download the driver package for your operating system from the web console and install it. -->

## Procédure
{: #proc51}

1. Exécutez le fichier exécutable téléchargé en tant qu'administrateur.

   Le chemin d'installation par défaut du module de pilote est : `Program Files\IBM\IBM DATA SERVER DRIVER`
2. [*Facultatif*] Ajoutez le sous-répertoire `bin` du répertoire d'installation du module de pilote à votre variable d'environnement `%PATH%` (afin de pouvoir exécuter la commande **db2cli** sans avoir à spécifier le chemin d'accès complet à l'exécutable de commande.)

## Que faire ensuite ?
{: #wn51}

Pour pouvoir connecter vos applications locales ou vos outils clients à votre base de données {{site.data.keyword.dashdbshort_notm}}, [configurez votre environnement local](/docs/services/Db2whc/connecting/driver_pkg_cfg.html).
