---

copyright:
  years: 2014, 2018
lastupdated: "2018-09-25"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Prise en charge de SSL (Secure Sockets Layer)

La base de données {{site.data.keyword.dashdbshort_notm}} utilise un certificat pour les connexions SSL qui est émis par une autorité de certification numérique tierce.
{: shortdesc}

Le certificat de l'autorité de certification est compris dans le module de pilote Db2. Si votre application se connecte avec un pilote du module de pilote Db2, vous n'avez pas besoin de télécharger le certificat séparément. Vous pouvez télécharger le module de pilote Db2 à partir de la console Web.

Par contre, si votre application possède son propre pilote, vous devrez probablement télécharger le certificat séparément. Vous pouvez télécharger le certificat à partir de la console Web.

SSL (Secure Sockets Layer) est un protocole de sécurité qui assure la confidentialité des communications. SSL permet aux applications client et serveur de communiquer en évitant
tout risque d'écoute clandestine, de contrefaçon et de falsification des messages. Les applications avec SSL utilisent des techniques de chiffrement standard qui assurent une communication sécurisée.

Le fait que vos applications soient configurées pour se connecter à votre base de données {{site.data.data.keyword.dashdbshort_notm}} avec SSL dépend de la politique de votre entreprise. Les protocoles standard et SSL que vous pouvez utiliser pour vous connecter à la base de données transmettent les noms d'utilisateur et les mots de passe sous forme de données chiffrées. Si vous voulez assurer une sécurité totale de bout en bout, vous devez transmettre toutes les informations de la base de données, y compris les données sensibles et les métadonnées, via une connexion SSL. Les administrateurs peuvent rendre les connexions SSL obligatoires en modifiant un paramètre sur la console Web.


