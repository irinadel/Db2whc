---

copyright:
  years: 2014, 2019
lastupdated: "2019-04-01"

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

# Aperçu de la connexion
{: #connect_ov}

Vous pouvez connecter à votre base de données {{site.data.keyword.dashdbshort_notm}} des interfaces de ligne de commande, des applications et outils tiers ou propres à IBM®, ou encore des applications que vous créez. 
{: shortdesc}

## Prérequis
{: #prereqs}

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les conditions requises sont remplies. 

- Collectez les détails de la base de données et les données d'identification

   Pour vous connecter à votre base de données, vous avez besoin des détails de la base de données (comme par exemple le nom d'hôte), ainsi que des données d'identification (comme par exemple un ID d'utilisateur et un mot de passe.) Vous trouverez ces informations de connexion sur la console Web {{site.data.keyword.dashdbshort_notm}}.

- Vérifiez qu'un pilote pris en charge est installé

   - Si votre application ou outil contient déjà le module Db2 v11.1 IBM Data Server Driver Package, il ou elle peut se connecter à votre base de données {{site.data.keyword.dashdbshort_notm}} à l'aide de ce pilote.
   - Dans le cas contraire, installez le module de pilote Db2, que vous pouvez télécharger de la console Web {{site.data.keyword.dashdbshort_notm}}.

- Configurez votre environnement

  - Ajoutez des entrées pour votre base de données dans le fichier de configuration du pilote, `db2dsdriver.cfg`.
  - Secure Sockets Layer (SSL)

    Vous pouvez choisir de vous connecter avec ou sans SSL. Les détails de connexion comme le port à utiliser et la chaîne de connexion dépendent du fait que vous utilisez ou non les connexions SSL.

    Pour utiliser les connexions SSL, vous avez besoin d'un certificat de l'autorité de certification :
    - Si vous utilisez le dernier module de pilote {{site.data.keyword.dashdbshort_notm}}, le fichier de certificat est intégré au module et sera utilisé pour les connexions.
    - Si vous utilisez le module IBM Data Server Driver Package, vous pouvez télécharger le certificat SSL depuis la console Web {{site.data.keyword.dashdbshort_notm}}.

- Confirmez que les ports sont disponibles

   Si votre réseau se trouve derrière un pare-feu, confirmez que les communications sont autorisées sur le numéro de port `50000` (pour les protocoles standard) ou sur le numéro de port `50001` (pour les connexions SSL).

<!-- Before you can connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you completed downloading and installing the necessary components on the prerequisites checklist: 

- [Prerequisites checklist](prereqs.html) -->

### Collecte des informations de connexion
{: #collect_info}

- [Détails de la base de données et données d'identification de connexion](/docs/services/Db2whc/connecting?topic=Db2whc-db_details_cxn_creds#db_details_cxn_creds)

### Téléchargement et installation du module de pilote
{: #dl_install}

- [Téléchargement du module de pilote](/docs/services/Db2whc/connecting?topic=Db2whc-dr_pkg#dr_pkg)
- [Installation sur Linux ou PowerLinux](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_linux#install_dr_pkg_linux)
- [Installation sur Mac OS X](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_mac#install_dr_pkg_mac)
- [Installation sur Windows](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_windows#install_dr_pkg_windows)

### Configuration de votre environnement
{: #cfg_env}

- [Configuration de votre environnement](/docs/services/Db2whc/connecting?topic=Db2whc-cfg_loc_env#cfg_loc_env)
- [Prise en charge de SSL (Secure Sockets Layer)](/docs/services/Db2whc/connecting?topic=Db2whc-ssl_support#ssl_support)

## Options de connectivité
{: #connect_opts}

{{site.data.keyword.dashdbshort_notm}} offre plusieurs options de connexion sécurisée en fonction de vos besoins de connexion d'application.  
{: shortdesc}

Voir [Options de connectivité](/docs/services/Db2whc/connecting?topic=Db2whc-connect_options#connect_options).

## Connexion à l'aide d'un programme
{: #conx_prgrm}

Vous pouvez utiliser les langages de programmation communs pour créer des applications qui se connectent à une base de données {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

- [JDBC](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_jdbc#con_prog_jdbc)
- [Microsoft Windows ODBC ou CLI](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_odbc_cli#con_prog_odbc_cli)
- [.NET](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_net#con_prog_net)
- [ODBC Data Source Administrator](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_odbc_dsa#con_prog_odbc_dsa)
- [PHP](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_php#con_prog_php)
- [API REST](/docs/services/Db2whc/connecting?topic=Db2whc-con_rest_api#con_rest_api)
<!-- - [C++]() -->
<!-- - [Java]() -->
<!-- - [Node.js]() -->
<!-- - [Perl]() -->
<!-- - [Python]() -->

## Intégration des applications et des outils
{: #conx_apps_tools}

Vous pouvez aussi connecter des outils et des applications externes à {{site.data.keyword.dashdbshort_notm}}
et les utiliser pour gérer ou analyser vos données. Exemple :

### Intégration des données
{: #di}

- Connectez vos applications {{site.data.keyword.Bluemix_short}} qui nécessitent une base de données analytique.
- [DataStage](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#datastage)
- [Informatica](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#informatica)
- [Lift](https://www.lift-cli.cloud.ibm.com/#docs){:external}
- [InfoSphere Data Replication](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#idr)
- [Segment](https://segment.com/docs/destinations/db2/){:external}
- [Data Studio](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#data_studio)
- [Data Server Manager](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#dsm)
- [CLPPLUS](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#clpplus)
- [Aginity Workbench pour la migration des modèles de données Netezza® et des données vers {{site.data.keyword.dashdbshort_notm}}](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#aginity_wb)
- [InfoSphere Data Architect pour la conception et le déploiement de votre schéma de base de données](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#ida)

### Visualisation des données/Intelligence métier
{: #dvis_bi}

- [Cognos Analytics pour exécuter les rapports de Business Intelligence pour vos données](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#cognos)
- [Looker](https://docs.looker.com/setup-and-management/connecting-to-db){:external}
- [Tableau](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#tableau)
- [Microsoft Excel](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#excel)
- [Esri ArcGIS for Desktop pour la réalisation d'analyses géospatiales et de publications de cartes avec vos données](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#esri_arcgis)

### Data science
{: #dsci}

- [Watson Studio (avant : IBM Data Science Experience)](/docs/services/Db2whc/connecting?topic=Db2whc-ds#watson_studio)
- [SPSS Statistics](/docs/services/Db2whc/connecting?topic=Db2whc-ds#spss_stats)
- [SAS](/docs/services/Db2whc/connecting?topic=Db2whc-ds#sas)
- [Environnement de développement R local](/docs/services/Db2whc/connecting?topic=Db2whc-ds#r_dev_env)

## Connexion à une autre base de données Db2
{: #fed}

La virtualisation des données Db2 (qui porte également le nom de fédération) est prise en charge par {{site.data.keyword.dashdbshort_notm}}. Elle vous donne un accès de requête unique à toutes vos données situées dans des bases de données réparties partout dans votre organisation. Vous pouvez accéder aux données qui se trouvent dans toutes vos sources de données Db2 ou Informix, aussi bien sur le cloud que sur site. 

Cette fonction est prise en charge sur toutes les versions de {{site.data.keyword.dashdbshort_notm}}, à l'exception du plan Entry. Toutefois, vous pouvez utiliser le plan Entry comme cible à partir de laquelle extraire des données.

- [Virtualisation des données (fédération)](/docs/services/Db2whc?topic=Db2whc-data_virt_fed#data_virt_fed)


