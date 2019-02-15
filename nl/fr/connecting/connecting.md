---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-15"

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

# Aperçu de la connexion
{: #connect}

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

- [Détails de la base de données et données d'identification de connexion](credentials.html)

### Téléchargement et installation du module de pilote
{: #dl_install}

- [Téléchargement du module de pilote](driver_pkg.html)
- [Installation sur Linux ou PowerLinux](install_linux.html)
- [Installation sur Mac OS X](install_mac.html)
- [Installation sur Windows](install_win.html)

### Configuration de votre environnement
{: #cfg_env}

- [Configuration de votre environnement](driver_pkg_cfg.html)
- [Prise en charge de SSL (Secure Sockets Layer)](ssl.html)

## Connexion à l'aide d'un programme
{: #conx_prgrm}

Vous pouvez utiliser les langages de programmation communs pour créer des applications qui se connectent à une base de données {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

- [JDBC](jdbc.html)
- [Microsoft Windows ODBC ou CLI](odbc_cli.html)
- [.NET](net_apps.html)
- [ODBC Data Source Administrator](odbc_data_source_admin.html)
- [PHP](php.html)
- [API REST](rest_api.html)
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
- Connectez vos applications {{site.data.keyword.Bluemix_short}} qui nécessitent une base de données analytique.
- [DataStage](data.html#datastage)
- [Informatica](data.html#informatica)
- [Lift ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](https://lift.ng.bluemix.net/#docs){:new_window}
- [InfoSphere Data Replication](data.html#idr)
- [Segment ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](https://segment.com/docs/destinations/db2/){:new_window}
- [Data Studio](data.html#data_studio)
- [Data Server Manager](data.html#dsm)
- [CLPPLUS](data.html#clpplus)
- [Aginity Workbench pour la migration des modèles de données Netezza® et des données vers {{site.data.keyword.dashdbshort_notm}}](data.html#aginity_wb)
- [InfoSphere Data Architect pour la conception et le déploiement de votre schéma de base de données](data.html#ida)

### Visualisation des données/Intelligence métier
- [Cognos Analytics pour exécuter les rapports de Business Intelligence pour vos données](vis_bi.html#cognos)
- [Looker ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.looker.com/setup-and-management/connecting-to-db){:new_window}
- [Tableau](vis_bi.html#tableau)
- [Microsoft Excel](vis_bi.html#excel)
- [Esri ArcGIS for Desktop pour la réalisation d'analyses géospatiales et de publications de cartes avec vos données](vis_bi.html#esri_arcgis)

### Data science
- [Watson Studio (avant : IBM Data Science Experience)](data_sci.html#watson_studio)
- [SPSS Statistics](data_sci.html#spss_stats)
- [SAS](data_sci.html#sas)
- [Environnement de développement R local](data_sci.html#r_dev_env)

## Connexion à une autre base de données Db2
{: #fed}

La virtualisation des données Db2 (qui porte également le nom de fédération) est prise en charge par {{site.data.keyword.dashdbshort_notm}}. Elle vous donne un accès de requête unique à toutes vos données situées dans des bases de données réparties partout dans votre organisation. Vous pouvez accéder aux données qui se trouvent dans toutes vos sources de données Db2 ou Informix, aussi bien sur le cloud que sur site. 

Cette fonction est prise en charge sur toutes les versions de {{site.data.keyword.dashdbshort_notm}}, à l'exception du plan Entry. Toutefois, vous pouvez utiliser le plan Entry comme cible à partir de laquelle extraire des données.

- [Virtualisation des données (fédération)](../federation.html)


