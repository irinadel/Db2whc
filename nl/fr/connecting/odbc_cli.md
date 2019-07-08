---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# Connexion à l'aide d'un programme avec ODBC ou une interface de ligne de commande
{: #con_prog_odbc_cli}

Définissez une connexion entre une application Microsoft Windows ODBC ou une application d'interface de ligne de commande et une base de données {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

## Prérequis
{: #prereq81}

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) sont remplies.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procédure
{: #proc81}

1. Dans un interpréteur de commandes sur les systèmes d'exploitation Linux, sur l'invite de commande Windows, ou dans la fenêtre de commande Db2 sur les systèmes d'exploitation Windows, entrez les commandes suivantes :

   **Remarque **: ces commandes créent de nouvelles entrées dans le fichier de configuration du pilote (`db2dsdriver.cfg`) sur votre ordinateur et définissent les attributs de connexion. Cette étape ne doit être effectuée qu'une seule fois.
   
   - Pour une connexion avec SSL :

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

   - Pour une connexion sans SSL :

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

   Où :

   `<hostname>` est le nom d'hôte du serveur

   `<alias>` est un alias de nom de source de données (DSN) que vous choisissez
    
2. [*Facultatif*] : Pour tester la connexion à la base de données, exécutez cette commande dans l'invite de commande :

   `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

   Où :

   `<alias>` est l'alias de nom de source de données (DSN) que vous avez créé avec la commande **db2cli writecfg**

   `<user_id>` provient des données d'identification de connexion que vous avez obtenues plus tôt

   `<password>` provient des données d'identification de connexion que vous avez obtenues plus tôt

3. [*Facultatif*] : Pour enregistrer le nom de source de données (DSN) auprès de Microsoft ODBC Driver Manager et pour travailler avec les applications Microsoft ODBC, exécutez la commande suivante. Par défaut, le DSN est créé en tant que DSN utilisateur.

   `db2cli registerdsn -add -dsn <alias>`

   Où :
        
   `<alias>` est l'alias de nom de source de données (DSN) que vous avez créé avec la commande **db2cli writecfg**



