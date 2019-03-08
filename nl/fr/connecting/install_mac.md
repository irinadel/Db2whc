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

# Installation du module de pilote sur Mac OS X
{: #install_dr_pkg_mac}

Vous pouvez installer le module de pilote {{site.data.keyword.dashdbshort_notm}} sur Mac OS X à l'aide du script `installDSDriver.sh`. 
{: shortdesc}

## Prérequis
{: #prereq41}

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](/docs/services/Db2whc/connecting/connecting.html#prereqs) sont remplies.

<!-- Download the Db2 driver package for your operating system from the web console and install it. -->

## Procédure
{: #proc41}

- **Pour une nouvelle installation**

  1. Montez l'image de disque en double-cliquant sur le fichier `macos_dsdriver.dmg`.
   
     Une nouvelle fenêtre de recherche**** s'ouvre avec le contenu de l'image de disque.

     Si la fenêtre de recherche**** ne s'ouvre pas, double-cliquez sur l'icône `macos_dsdriver` sur votre bureau.
  2. Dans la fenêtre de recherche****, double-cliquez sur le fichier `installDSDriver.sh`.

     Le module de pilote est installé dans l'emplacement par défaut `/Applications/dsdriver`.

- **Pour obtenir des mises à jour de votre installation existante du module de pilote**

  1. Sauvegardez les fichiers de configuration en cours :

     a. Accédez au dossier `Applications/dsdriver/cfg`.

     b. Copiez les fichiers suivants vers un dossier différent : 
    
        `db2cli.ini`

        `db2dsdriver.cfg`
  2. Supprimez le module de pilote actuellement installé en cliquant sur le dossier `dsdriver` avec le bouton droit de la souris et en sélectionnant **Move to Trash**.
  3. Installez le nouveau module de pilote conformément à la description de la section **Pour une nouvelle installation** (ci-dessus) :
     
     a. Montez l'image de disque en double-cliquant sur le fichier `macos_dsdriver.dmg`.
     b. Dans la fenêtre de recherche****, double-cliquez sur le fichier `installDSDriver.sh`.
  4. Restaurez les fichiers de configuration :

     Copiez les fichiers `db2cli.ini` et `db2dsdriver.cfg` sauvegardés à l'étape 1 dans le dossier `/Applications/dsdriver/cfg`.

## Que faire ensuite ?
{: #wn41}

Pour pouvoir connecter vos applications locales ou vos outils clients à votre base de données {{site.data.keyword.dashdbshort_notm}}, [configurez votre environnement local](/docs/services/Db2whc/connecting/driver_pkg_cfg.html).
