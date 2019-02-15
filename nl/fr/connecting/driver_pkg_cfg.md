---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# Configuration de votre environnement local
{: #cfg_loc_env}

Pour connecter les applications locales et les outils à votre base de données {{site.data.keyword.dashdbshort_notm}}, vous devez configurer votre environnement.  
{: shortdesc}

## Prérequis

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](connecting.html#prereqs) sont remplies.

<!-- 1. Install the Db2 driver package for your operating system.

   - [Installing on Windows](install_win.html)
   - [Installing on Linux or PowerLinux](install_linux.html)
   - [Installing on Mac OS X](install_mac.html)
2. Decide whether or not you will be using Secure Sockets Layer (SSL) to connect to your database.
3. Collect database details and connect credentials, including the host name of your server, and your database user ID and password. -->

## Procédure

1. Ajoutez des entrées pour votre base de données dans le fichier de configuration du pilote, `db2dsdriver.cfg`.

   Les étapes de configuration sont différentes si vous souhaitez ou non que la connexion à votre base de données s'effectue via SSL :

   **Avec SSL**

   Pour connecter vos applications et vos outils à votre base de données via SSL, entrez les commandes suivantes dans un interpréteur de commande sur les systèmes d'exploitation Linux, sur l'invite de commande Windows, ou dans une fenêtre de commande DB2 : 

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50001`

   `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

    où :

   - `<hostname>` est le nom d'hôte de votre serveur.
   - `<alias>` est un alias que vous choisissez. L'alias ne peut pas être le même que le nom de la base de données, `BLUDB`. Si vous souhaitez inclure des espaces dans l'alias, placez-les entre guillemets doubles.

   **Sans SSL**

   Pour connecter vos applications et vos outils à votre base de données sans utiliser SSL, entrez les commandes suivantes dans un interpréteur de commande sur les systèmes d'exploitation Linux, sur l'invite de commande Windows ou dans une fenêtre de commande DB2 : 

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

   `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

    où :

   - `<hostname>` est le nom d'hôte de votre serveur.
   - `<alias>` est un alias que vous choisissez. L'alias ne peut pas être le même que le nom de la base de données, `BLUDB`. Si vous souhaitez inclure des espaces dans l'alias, placez-les entre guillemets doubles.

2. Testez la connexion en lançant la commande **db2cli validate** depuis l'invite de commande :

   `db2cli validate -dsn <alias> -connect -user <userid> -passwd <password>`

   où : 
   
   - `<alias>` est un alias que vous avez créé avec la commande **db2cli writecfg**.
   - `<userid>` est votre ID d'utilisateur Db2.
   - `<password>` est votre mot de passe Db2.

3. [*Facultatif*] Pour pouvoir connecter des outils et des applications ODBC locales à votre base de données, enregistrez le DSN avec le gestionnaire de pilote ODBC :
 
   Exécutez la commande suivante à partir d'une ligne de commande : 

   `db2cli registerdsn -add -dsn <alias>`

   où : 

   - `<alias>` est un alias que vous avez créé avec la commande **db2cli writecfg**.

   Par défaut, le DSN est créé en tant que DSN utilisateur.

