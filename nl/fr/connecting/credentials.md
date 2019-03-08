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

# Détails de la base de données et données d'identification de connexion
{: #db_details_cxn_creds}

Pour configurer votre environnement de développement local et pour connecter des applications et des outils à votre base de données {{site.data.keyword.dashdbshort_notm}}, vous devez connaître les détails de la base de données et les données d'identification de connexion.
{: shortdesc}

## Détails de la base de données
{: #db_details}

Certains détails importants de la base de données sont requis pour connecter des applications et des outils à votre base de données :

- *Nom d'hôte* - Nom d'hôte du serveur.
- *Numéro de port* - Utilisé par le gestionnaire de base de données pour la communication TCP/IP. (Notez que votre service est mis à disposition avec un numéro de port pour les connexions SSL et un numéro de port différent pour les connexions non SSL).

   Si besoin, vous pouvez obtenir l'adresse IP de votre serveur en utilisant la commande ping ou la commande nslookup, en spécifiant votre nom d'hôte.
- *Nom de la base de données* - Le nom de la base de données Db2, généralement BLUDB.

## Données d'identification de connexion
{: #cxn_creds}

Il existe trois types de données d'identification :

- *IBMid* - Si vous utilisez {{site.data.keyword.Bluemix_notm}}, il s'agit de l'ID que vous utilisez pour vous connecter à {{site.data.keyword.Bluemix_notm}}, et non celui que vous utilisez pour connecter les applications ou outils à votre base de données Db2 Warehouse on Cloud.
- *Données d'identification de la base de données Db2* - Votre service est mis à disposition avec un ID d'utilisateur de base de données et un mot de passe qui peuvent être utilisés pour connecter les applications et les outils à votre base de données.
- *Utilisateurs créés par l'administrateur* - Certains plans {{site.data.keyword.dashdbshort_notm}} permettent aux administrateurs de créer de nouveaux utilisateurs. Ces ID et mots de passe créés par les administrateurs peuvent être utilisés pour se connecter directement à l'URL de la console Web et pour se connecter à la base de données Db2 depuis les applications et les outils.

## Où trouver les détails de la base de données et les données d'identification de connexion ?
{: #location}

Vous pouvez obtenir ces informations des sources suivantes :

- *Votre administrateur* - Si vous n'êtes pas le propriétaire ou l'administrateur de votre instance Db2, vous pouvez obtenir vos détails de base de données et vos données d'identification de connexion de votre administrateur.
- *Console Web Db2* - Les détails de base de données et les données d'identification sont disponibles dans la console Web.
- Si vous utilisez {{site.data.keyword.Bluemix_notm}} : 
   
   - *Tableau de bord {{site.data.keyword.Bluemix_notm}}* - Lorsque vous affichez votre service sur votre tableau de bord {{site.data.keyword.Bluemix_notm}}, dans la zone "Données d'identification pour le service", vous pouvez afficher les détails de la base de données ainsi que l'ID d'utilisateur et le mot de passe de la base de données.
   - *`VCAP_SERVICES`* - Dans {{site.data.keyword.Bluemix_notm}}, `VCAP_SERVICES` est une variable d'environnement qui contient des détails de base de données et des données d'identification au format JSON. Lorsque vous affichez les données d'identification de votre service dans votre tableau de bord {{site.data.keyword.Bluemix_notm}}, le contenu de `VCAP_SERVICES` s'affiche. Lorsque vous associez d'autres services ou applications {{site.data.keyword.Bluemix_notm}} à votre service, ces autres services ou applications peuvent accéder aux détails de la base de données et aux données d'identification à l'aide d'un programme, en lisant la variable `VCAP_SERVICES`.
