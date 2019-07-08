---

copyright:
  years: 2014, 2019
lastupdated: "2019-03-29"

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

# Intégration des données
{: #data_int}

Vous pouvez aussi connecter des outils et des applications externes à {{site.data.keyword.dashdbshort_notm}}
et les utiliser pour gérer ou analyser vos données. 
{: shortdesc}

## DataStage
{: #datastage}

Ces instructions expliquent comment définir une connexion sans SSL entre IBM® InfoSphere® DataStage® <!--version 9.1 and later -->et une base de données {{site.data.keyword.dashdbshort_notm}} en cataloguant la base de données et en définissant un objet de connexion, ou comment créer une connexion avec SSL à l'aide d'un certificat numérique émis par un tiers.
{: shortdesc}

### Prérequis
{: #prereq1}

Il est vivement recommandé d'effectuer une mise à jour de DataStage vers la version la plus récente de manière à bénéficier de tables externes pour charger vos données dans {{site.data.keyword.dashdbshort_notm}}.
{: important}

Si aucun client de serveur de données n'est installé, téléchargez et installez le client IBM Data Server Client <!--Version 10.5 -->approprié au système d'exploitation de votre ordinateur client : [IBM Data Server Client](https://www.ibm.com/marketing/iwm/iwm/web/preLogin.do?source=swg-idsc97){:external}.

Pour établir des connexions avec le protocole SSL, téléchargez et installez le GSKit V8 32 bits. Cliquez sur l'onglet Système d'exploitation correspondant au système d'exploitation de votre ordinateur client : [GSKit V8 - Install, Uninstall and Upgrade instructions](http://www.ibm.com/support/docview.wss?uid=swg21631462){:external}. Pour les systèmes d'exploitation suivants, veillez à ajouter le chemin d'accès au répertoire d'installation de GSKit à la variable d'environnement de chemin spécifique au système d'exploitation :

- AIX® : **LIBPATH**
   - `/usr/opt/ibm/gsk8/lib`
- Linux : **LD_LIBRARY_PATH**
    - `/usr/local/ibm/gsk8/lib`
- UNIX : **LD_LIBRARY_PATH**
    - `/opt/ibm/gsk8/lib`
- Windows : **PATH**
    - `<installation_directory>\gsk8\bin`
    - `<installation_directory>\gsk8\lib`

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) sont remplies.

### Procédure
{: #proc1}

- Pour créer une connexion avec SSL, effectuez les étapes suivantes :

  1. Ouvrez une ligne de commande ou un terminal et créez un nouveau répertoire dans le système DataStage pour stocker le certificat SSL et les fichiers de clés.

     `# /home/db2inst2> mkdir SSL`

     `# /home/db2inst2> cd SSL`

  2. Dans la console Web {{site.data.keyword.dashdbshort_notm}}, téléchargez le certificat SSL à partir de la page permettant de connecter vos applications à la base de données****.

     a. Dans le menu principal, cliquez sur **Connect**.
     
     b. Cliquez sur **Connection with SSL**, puis sur le lien **SSL certificate (1 KB)**.
     
     c. Sauvegardez le certificat `DigiCertGlobalRootCA.crt` dans le répertoire SSL que vous avez créé à l'étape 1.
        
  3. Créez une base de données de magasin de clés client dans le système DataStage à l'aide de l'utilitaire **gsk8capicmd_64**.

     `# /home/db2inst2/SSL> gsk8capicmd_64 -keydb -create -db <keystore_db.kdb> -pw <ks_db_password> -stash`

     Où `<keystore_db.kdb>` représente la base de données du magasin de clés client et `<ks_db_password>` le mot de passe de la base de données du magasin de clés client.
        
  4. Ajoutez le certificat à la base de données du magasin de clés client.

     `# /home/db2inst2/SSL> gsk8capicmd_64 -cert -add -db <keystore_db.kdb> -pw <ks_db_password> -label BLUDB_SSL -file DigiCertGlobalRootCA.crt`

     Où `<keystore_db.kdb>` représente la base de données du magasin de clés client et `<ks_db_password>` le mot de passe de la base de données du magasin de clés client.
    
  5. Configurez le client Db2 sur le serveur DataStage.
            
     a. Mettez à jour les paramètres de configuration SSL dans le gestionnaire de base de données.

     `# /home/db2inst2> db2 update dbm cfg using SSL_CLNT_KEYDB /home/db2inst2/SSL/<keystore_db.kdb>`

     Où `<keystore_db.kdb>` représente la base de données du magasin de clés client.

     `# /home/db2inst2> db2 update dbm cfg using SSL_CLNT_STASH /home/db2inst2/SSL/<keystore_db.sth>`

     Où `<keystore_db.sth>` représente le stockage de mot de passe de la base de données du magasin de clés client.
            
     b. Cataloguez le noeud cible avec l'option de sécurité SSL puis la base de données BLUDB sur le noeud cible.

     `# /home/db2inst2> db2 catalog tcpip node <node_name> remote <IP_addr_of_BLUDB_database_server> server 50001 security SSL`

     Où `<node_name>` représente le nom du noeud cible et `<IP_addr_of_BLUDB_database_server>` l'adresse IP du serveur de base de données BLUDB.

     `# /home/db2inst2> db2 catalog db BLUDB as <db_alias> at node <node_name>`

     Où `<db_alias>` est le nom de la base de données {{site.data.keyword.dashdbshort_notm}}.

  6. Ajoutez des droits de lecture et d'exécution aux fichiers dans le répertoire SSL pour tout le monde. L'utilisateur DataStage qui exécute les tâches doit accéder à ces fichiers pour effectuer des connexions SSL à la base de données Db2.

     `# /home/db2inst2/SSL> chmod 655 /home/db2inst2/SSL/*`

  7. Testez la connexion SSL de l'une des manières suivantes :

     - Testez la connexion en utilisant CLP. Entrez la commande suivante pour vous connecter à la base de données {{site.data.keyword.dashdbshort_notm}} :

       `db2 connect to <db_alias> user <user_id>`

       Où `<db_alias>` est le nom de la base de données {{site.data.keyword.dashdbshort_notm}} et `<user_id>` est votre ID d'utilisateur {{site.data.keyword.dashdbshort_notm}}. Vous êtes invité à entrer votre mot de passe.
    
     - Testez la connexion en utilisant l'interface de ligne de commande. Entrez la commande suivante pour vous connecter à la base de données {{site.data.keyword.dashdbshort_notm}} :

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

        Où `<alias>` est un alias que vous avez créé à l'aide de la commande **db2cli writecfg**, `<user_id>` est votre ID d'utilisateur {{site.data.keyword.dashdbshort_notm}} et `<password>` votre mot de passe {{site.data.keyword.dashdbshort_notm}}.

- Pour créer une connexion sans SSL, cataloguez la base de données {{site.data.keyword.dashdbshort_notm}} cible en procédant comme suit :

  1. Cataloguez le noeud {{site.data.keyword.dashdbshort_notm}} cible pour que les applications client puissent s'y connecter. Exécutez les commandes CLP suivantes :

     `db2 catalog tcpip node <node_name> remote <IP_address_of_BLUDB_database_server> server <port_number_of_BLUDB_database>`

     Où `<node_name>` représente le nom du noeud, `<IP_address_of_BLUDB_database_server>` l'adresse IP du serveur de base de données BLUDB et `<port_number_of_BLUDB_database>` le numéro de port de la base de données BLUDB.

  2. Cataloguez la base de données {{site.data.keyword.dashdbshort_notm}} distante pour que les applications client puissent s'y connecter. Exécutez la commande suivante :

     `db2 catalog db BLUDB as <db_alias> at node <node_name>`

     Où `<db_alias>` est le nom de la base de données {{site.data.keyword.dashdbshort_notm}} et `<node_name>` le nom du noeud.

  3. Testez la connexion non SSL de l'une des manières suivantes :

      - Testez la connexion en utilisant CLP. Entrez la commande suivante pour vous connecter à la base de données {{site.data.keyword.dashdbshort_notm}} :

        `db2 connect to <db_alias> user <user_id>`

        Où `<db_alias>` est le nom de la base de données {{site.data.keyword.dashdbshort_notm}} et `<user_id>` est votre ID d'utilisateur {{site.data.keyword.dashdbshort_notm}}. Vous êtes invité à entrer votre mot de passe.

        `db2 list tables`

      - Testez la connexion en utilisant l'interface de ligne de commande. Entrez la commande suivante pour vous connecter à la base de données {{site.data.keyword.dashdbshort_notm}} :

        `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

        Où `<alias>` est un alias que vous avez créé à l'aide de la commande **db2cli writecfg**, `<user_id>` est votre ID d'utilisateur {{site.data.keyword.dashdbshort_notm}} et `<password>` votre mot de passe {{site.data.keyword.dashdbshort_notm}}.

  4. Utilisez les [informations de connexion](/docs/services/Db2whc/connecting?topic=Db2whc-db_details_cxn_creds#db_details_cxn_creds) obtenues au préalable pour définir une connexion dans le client DataStage. Sur l'onglet **Parameters**, vous devez sélectionner le **connecteur DB2** dans la zone **Connect using Staging Type**.

     Pour plus d'informations sur la définition d'une connexion dans DataStage, consultez les rubriques suivantes de la documentation de DataStage : 
     
     - [Création manuelle d'un objet de connexion de données](https://www.ibm.com/support/knowledgecenter/SSZJPZ_11.3.0/com.ibm.swg.im.iis.ds.design.doc/topics/t_ddesref_Creating_a_Data_Connection_Object_Manually.html){:external}
     - [Configuration de l'accès aux bases de données Db2](https://www.ibm.com/support/knowledgecenter/en/SSZJPZ_11.7.0/com.ibm.swg.im.iis.conn.common.usage.doc/topics/t_configuring_db2conn.html){:external}

## Informatica
{: #informatica}

Vous pouvez connecter Informatica à {{site.data.keyword.dashdbshort_notm}} afin de mieux gérer vos données.
{: shortdesc}

Regardez cette vidéo pour voir comment intégrer {{site.data.keyword.dashdbshort_notm}} à Informatica Cloud.

<iframe class="embed-responsive-item" id="youtubeplayer1" title="DB2 Connections - Lightening Fast How-To with Informatica Cloud" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TUiS_HstLnU?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

<!-- To configure a native Db2 connection to connect to {{site.data.keyword.dashdbshort_notm}}, perform the following steps:

1. Run the `odbcad32.exe` file from your local system.
The ODBC Data Sources Administrator dialog box appears.

2. Create the 32-bit ODBC Data Source Name using the DataDirect Db2 drivers.

3. In the ODBC DB2 Wire Protocol Setup dialog box, click **Security** tab.

4. Set the value of the `Authentication Method` property as `1 -Encrypt Password`. The following image shows the **Security** tab in the ODBC DB2 Wire Protocol Setup dialog box where you can set the `Authentication Method` property:
             
   ![ODBC Db2 Wire Protocol Driver Setup - Security tab](images/odbc_driver.png)
       
5. In the ODBC DB2 Wire Protocol Setup dialog box, click **Modify Bindings** tab.

6. Enter your user name in the Package Collection property. The following image shows the **Modify Bindings** tab in the ODBC DB2 Wire Protocol Setup dialog box where you can set the `Package Collection` property: 

   ![ODBC Db2 Wire Protocol Driver Setup - Modify Bindings tab](images/odbc_driver_2.png)
            
7. In the PowerCenter Designer, use the data source name that you created to import the metadata.

8. In the PowerCenter Workflow Manager, create the required workflow.

9. Ensure that you have the {{site.data.keyword.dashdbshort_notm}} compatible 11.x Db2 clients when you run the workflow.

**Note**: If you want to set the authentication type when you create the Db2 client catalog, you could specify the value of the `AUTHENTICATION TYPE` property as `SERVER_ENCRYPT`. -->

<!-- Watch this video to see how to integrate Db2 and Salesforce with Informatica Cloud.

<iframe class="embed-responsive-item" id="youtubeplayer2" title="Integrate Db2 and Salesforce with Informatica Cloud" type="text/html" width="640" height="390" src="//www.youtube.com/watch?v=RGTLweZvKP8" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe> -->

<!-- [Informatica](https://kb.informatica.com/howto/6/Pages/20/522402.aspx?myk=Connect%20to%20Db2){:external} -->

## Lift
{: #lift}

Utilisez Lift pour faire migrer vos données dans {{site.data.keyword.dashdbshort_notm}}.

[Lift](https://www.lift-cli.cloud.ibm.com/#docs){:external}

## InfoSphere Data Replication
{: #idr}

Vous pouvez connecter IBM® InfoSphere® Data Replication <!--version 11.3.3.3-36 or later -->à une base de données {{site.data.keyword.dashdbshort_notm}}. Cette possibilité s'applique aussi bien aux environnements SMP qu'aux environnements MPP. Elle ne s'applique pas au plan Entry de {{site.data.keyword.dashdbshort_notm}}. 
{: shortdesc}

### Présentation
{: #overview2}

Idéalement, lorsque vous connectez IBM InfoSphere Data Replication à {{site.data.data.dashdbshort_notm}}, IBM InfoSphere Data Replication se trouve dans le même centre de données {{site.data.keyword.Bluemix_notm}} que {{site.data.keyword.dashdbshort_notm}} ou au même endroit que {{site.data.keyword.dashdbshort_notm}}. IBM InfoSphere Data Replication se connecte d'un serveur local à l'instance {{site.data.keyword.dashdbshort_notm}} distante.

Lorsque vous utilisez {{site.data.keyword.dashdbshort_notm}} en tant que cible de connexion, les performances d'IBM InfoSphere Data Replication dépendent en partie de la largeur de bande du réseau qui sépare son moteur cible de l'instance {{site.data.keyword.dashdbshort_notm}}. La distance physique affecte également la performance : dans une configuration idéale, IBM InfoSphere Data Replication est aussi proche que possible de l'instance {{site.data.keyword.dashdbshort_notm}}. Ensuite, la topologie du réseau est également un facteur déterminant. Par exemple, dans un cas idéal, le moteur cible d'IBM InfoSphere Data Replication s'exécute sur une machine virtuelle dans le même VPN (domaine de sécurité) que l'instance cible. Moins il y a de noeuds de réseau (par exemple, pare-feu ou routeurs) à traverser, mieux c'est. 

### Prérequis
{: #prereq2}

Si vous tentez de vous connecter à l'aide du protocole SSL, téléchargez et installez GSKit V8. Voir [GSKit V8 - Install, Uninstall and Upgrade instructions](http://www.ibm.com/support/docview.wss?uid=swg21631462){:external}. Cliquez sur l'onglet correspondant au système d'exploitation de la machine de votre client. Si vous installez GSKit sur un ordinateur Windows, veillez à spécifier le chemin d'accès au répertoire d'installation de GSKit (`<installation_directory>\gsk8\bin`) dans la variable d'environnement **`PATH`**.

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) sont remplies.

Si vous avez l'intention de vous connecter en utilisant le protocole SSL, téléchargez le certificat SSL `DigiCertGlobalRootCA.crt` de la console Web vers un répertoire de la machine client. Pour télécharger le certificat, cliquez sur **Connexion > Informations de connexion** puis sur l'onglet **Connexion avec SSL**.

### Procédure
{: #proc2}

1. Choisissez l'une des approches suivantes pour créer votre connexion :

   - Pour créer une connexion avec SSL, effectuez les étapes suivantes :
            
     a. Lancez la commande suivante :

     `cd /<ssl_directory_name>/ssl`

     Où `/<ssl_directory_name>/ssl` est le chemin d'accès au répertoire dans lequel vous avez téléchargé le certificat SSL `DigiCertGlobalRootCA.crt`.

     b. Créez une base de données de clés client et un fichier de dissimulation à l'aide de l'outil **GSKCapiCmd**. Par exemple, la commande suivante crée une base de données de clés client appelée `dashclient.kdb` et un fichier de dissimulation appelé `dashclient.sth` :

     `gsk8capicmd_64 -keydb -create -db "dashclient.kdb" -pw "passw0rdpw0" -stash`

     où `passw0rdpw0` est un mot de passe. L'option **-stash** crée un fichier de dissimulation au même endroit que la base de données de clés client, avec l'extension de fichier `.sth`. Lors de la connexion, GSKit utilise le fichier de dissimulation pour obtenir le mot de passe pour la base de données de clés client.
            
     c. Ajoutez le certificat à la base de données de clés client. Par exemple, la commande **gsk8capicmd** suivante importe le certificat depuis le fichier `/<ssl_directory_name>/ssl/DigiCertGlobalRootCA.crt` dans la base de données de clés client nommée `dashclient.kdb` :

     `gsk8capicmd_64 -cert -add -db "dashclient.kdb" -pw "passw0rdpw0" -label "DigiCert" -file "/<ssl_directory_name>/ssl/DigiCertGlobalRootCA.crt" -format ascii -fips`

     d. Mettez à jour les valeurs des paramètres de configuration `SSL_CLNT_KEYDB` et
`SSL_CLNT_STASH` du gestionnaire de base de données sur le client en spécifiant la base de données de clés client et le fichier de dissimulation. Exemples :

     `db2 update dbm cfg using SSL_CLNT_KEYDB /<ssl_directory_name>/ssl/dashclient.kdb`

     `db2 update dbm cfg using SSL_CLNT_STASH /<ssl_directory_name>/ssl/dashclient.sth`

     e. Cataloguez le noeud {{site.data.keyword.dashdbshort_notm}} pour que les applications client puissent s'y connecter. Lancez la commande suivante :

     `db2 catalog tcpip node <node_name> remote <Db2_Warehouse_IP_address> server <port_number> security ssl`

     Où :
                
     `<node_name>` est le nom que vous donnez au noeud.

     `<Db2_Warehouse_IP_address>` est l'adresse IP du serveur Db2 Warehouse on Cloud.

     `<port_number>` est le port qui est utilisé pour se connecter à Db2 Warehouse à l'aide d'une connexion SSL. Si vous utilisez le port par défaut, spécifiez `50001`.
            
     f. Cataloguez la base de données {{site.data.keyword.dashdbshort_notm}} distante pour que les applications client puissent s'y connecter. Lancez la commande suivante :

     `db2 catalog database bludb as <db_alias> at node <node_name>`

     Où `db_alias` est le nom que donnez à la base de données {{site.data.keyword.dashdbshort_notm}}.
            
     g. Testez la connexion SSL de l'une des manières suivantes :
                
     - Pour tester la connexion via l'interpréteur de commande (CLP), exécutez la commande suivante pour vous connecter à la base de données {{site.data.keyword.dashdbshort_notm}} :

       `db2 connect to <db_alias> user <user_id>`

       Où `<user_id>` est votre ID utilisateur {{site.data.keyword.dashdbshort_notm}}. Vous êtes invité à entrer votre mot de passe.
                
     - Pour tester la connexion via l'interface de ligne de commande (CLI), exécutez la commande suivante pour vous connecter à la base de données {{site.data.keyword.dashdbshort_notm}} :

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

       Où `<alias>` est un alias DSN que vous avez créé à l'aide de la commande **db2cli writecfg**, `<user_id>` est votre ID utilisateur {{site.data.keyword.dashdbshort_notm}} et `<password>` votre mot de passe de la base de données {{site.data.keyword.dashdbshort_notm}}.
        
   - Pour créer une connexion sans SSL, procédez comme suit :

     a. Cataloguez le noeud {{site.data.keyword.dashdbshort_notm}} pour que les applications client puissent s'y connecter. Lancez la commande suivante :

     `db2 catalog tcpip node <node_name> remote <Db2_Warehouse_IP_address> server <port_number>`

     Où :
                
     `<node_name>` est le nom que vous donnez au noeud.

     `<Db2_Warehouse_IP_address>` est l'adresse IP du serveur {{site.data.keyword.dashdbshort_notm}}.

     `<port_number>` est le port qui est utilisé pour se connecter à {{site.data.keyword.dashdbshort_notm}} sans connexion SSL. Si vous utilisez le port par défaut, spécifiez `50000`.
            
     b. Cataloguez la base de données {{site.data.keyword.dashdbshort_notm}} distante pour que les applications client puissent s'y connecter. Lancez la commande suivante :

     `db2 catalog database bludb as <db_alias> at node <node_name>`

     Où `<db_alias>` est le nom de la base de données {{site.data.keyword.dashdbshort_notm}}.

     c. Testez la connexion non SSL de l'une des manières suivantes :

     - Pour tester la connexion via l'interpréteur de commande (CLP), exécutez la commande suivante pour vous connecter à la base de données {{site.data.keyword.dashdbshort_notm}} :

       `db2 connect to <db_alias> user <user_id>`

       Où `<user_id>` est votre ID utilisateur {{site.data.keyword.dashdbshort_notm}}. Vous êtes invité à entrer votre mot de passe.
                
     - Pour tester la connexion via l'interface de ligne de commande (CLI), exécutez la commande suivante pour vous connecter à la base de données {{site.data.keyword.dashdbshort_notm}} :

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

       Où `<alias>` est un alias DSN que vous avez créé à l'aide de la commande **db2cli writecfg**, `<user_id>` est votre ID utilisateur {{site.data.keyword.dashdbshort_notm}} et `<password>` le mot de passe de votre serveur Db2 Warehouse on Cloud.
    
2. Lancez l'outil de configuration d'InfoSphere Data Replication et effectuez les étapes suivantes. Les valeurs qui s'affichent dans les captures d'écran sont des exemples.
        
   a. Ajoutez une instance source pointant vers votre base de données source à l'aide de l'onglet **Instance Configuration** :

   ![Nouvelle instance IIDR - Instance source](images/IIDR_source_instance.jpg "Configuration de l'instance source")

   b. Ajoutez une instance cible pointant vers votre base de données Db2 cible à l'aide de l'onglet **Instance Configuration**. Si vous n'utilisez pas IBM InfoSphere Data Replication 11.3.3.3-50 ou une version ultérieure, ne cochez pas la case **Specify refresh loader path**.

   ![Nouvelle instance IIDR - Instance cible](images/IIDR_target_instance.jpg "Configuration de l'instance cible")

   c. Démarrez chaque instance :

   ![Outil de configuration IIDR](images/IIDR_instances.jpg "Outil de configuration IIDR affichant les instances source et cible")

3. Lancez la console de gestion d'InfoSphere Data Replication et utilisez le gestionnaire d'accès pour effectuer les étapes suivantes :
        
   a. Créez un magasin de données pour le connecter à votre instance source à l'aide de l'onglet **Datastore**. Comme les bases de données Db2 n'étaient pas prises en charge en tant que bases de données source à l'origine, vous devez fournir un nom d'utilisateur et un mot de passe pour la base de données source en cliquant sur **Connection parameters**.

   ![Propriétés du magasin de données - Source](images/IIDR_source_datastore.jpg "Propriétés du magasin de données source")

   b. Créez un magasin de données pour le connecter à votre instance cible à l'aide de l'onglet **Datastore**. Vous devez fournir un nom d'utilisateur et un mot de passe en cliquant sur **Connection parameters**.

   ![Propriétés du magasin de données - Cible](images/IIDR_target_datastore.jpg "Propriétés du magasin de données cible")

   c. Si l'utilisateur (par exemple, l'administrateur) qui se connectera au serveur d'accès n'existe pas, créez cet utilisateur :

   ![Nouvel utilisateur](images/IIDR_management_user.jpg "Nouvel outil de création d'utilisateur")

   d. Cliquez sur l'onglet **Access Manager**.
        
   e. Sur l'onglet **Datastore Management**, affectez l'utilisateur au magasin de données source et au magasin de données cible en cliquant sur chaque magasin de données avec le bouton droit de la souris puis en cliquant sur **Assign User**. Vérifiez que les données d'identification permettant d'accéder à chaque instance sont correctes.

   ![Console de gestion IIDR - Gestionnaire d'accès](images/IIDR_management_assign_user.jpg "Console du gestionnaire d'accès")

### Que faire ensuite ?
{: #what2}

Définissez un abonnement et procédez à la réplication des données. Pour obtenir des informations, consultez :

- [Loading data from InfoSphere Data Replication](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/learn_how/loaddata_iidr.html){:external} 

## Segment
{: #segment}

Vous pouvez intégrer Segment à une base de données {{site.data.keyword.dashdbshort_notm}}. Segment est une plateforme unique qui collecte, stocke et achemine vos données d'utilisateur vers des centaines d'outils différents.
{: shortdesc}

[Segment](https://segment.com/docs/destinations/db2/){:external}

## Data Studio
{: #data_studio}

Ces instructions expliquent comment créer une connexion entre IBM® Data Studio <!--version 4.1.x -->et une base de données {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Prérequis
{: #prereq3}

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) sont remplies.

### Procédure
{: #proc3}

1. Dans Data Studio, cliquez sur **All Databases > New Connection to a database**.

2. Dans l'onglet **Local**, sélectionnez **DB2 for Linux, UNIX, and Windows** comme gestionnaire de base de données.
    
3. Sur l'onglet **General**, entrez les valeurs suivantes :
   - *Database* : `BLUDB`
   - *Host* : nom d'hôte.
   - *Port* : pour une connexion sans SSL, entrez `50000`. Pour une connexion avec SSL, entrez `50001`. 
   - *User name* : nom d'utilisateur que vous utilisez pour vous connecter.
   - *Password* : mot de passe que vous utilisez pour vous connecter.

4. Pour une connexion SSL, cliquez sur l'onglet **Optional**, puis sur **Add**. Pour la propriété `sslConnection`, spécifiez `true`.

5. [*Facultatif*] : Cliquez sur **Test Connection** pour vérifier que la connexion a réussi.

## Data Server Manager (DSM)
{: #dsm}

Une connexion entre votre console IBM® Data Server Manager et votre base de données {{site.data.keyword.dashdbshort_notm}} vous permet de surveiller et de gérer la base de données à partir de la console Web Data Server Manager. 
{: shortdesc}

### Prérequis
{: #prereq4}

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) sont remplies.

### Procédure
{: #proc4}

<!--The connection procedure was tested on Data Server Manager version 1.1. The same procedure applies to all of the other versions of the Data Server Manager software.
-->
Pour créer une connexion, procédez comme suit :

1. Connectez-vous à votre console Web Data Server Manager.
    
2. Dans la console Web Data Server Manager, accédez à **Set Up > Database Connections**.
    
3. Cliquez sur l'icône ![plus +](images/icon_R_plus.gif "icône d'ajout") pour ajouter une connexion de base de données. Sur la page **Add Database Connection** sous l'onglet **Database Connections**, entrez les informations requises dans les zones suivantes :

   - *Database connection name* : le nom doit être unique dans Data Server Manager
   - *Data server type* : dans le menu déroulant, sélectionnez **DB2 for Linux, UNIX, and Windows**
   - *Database name* : `BLUDB`
   - *Host name* : entrez le nom d'hôte de {{site.data.keyword.dashdbshort_notm}} 
   - *Port number* : pour une connexion sans SSL, entrez `50000`. Pour une connexion avec SSL, entrez `50001`. 
   - *JDBC security* : dans le menu déroulant, sélectionnez **Clear text password**
   - *User ID* : votre ID d'utilisateur pour {{site.data.keyword.dashdbshort_notm}} 
   - *Password* : votre mot de passe pour {{site.data.keyword.dashdbshort_notm}} 

4. Pour une connexion avec SSL, sélectionnez l'onglet **Advanced JDBC Properties**. Entrez les informations requises dans les zones suivantes :

   - *Property* : `sslConnection`
   - *Value* : `true`

    Cliquez sur le bouton **Add**. Sélectionnez l'onglet **Database Connection**.
    
5. Testez la connexion en cliquant sur le bouton **Test Connection**. Si la connexion réussit, cliquez sur **OK**.

## InfoSphere Data Architect
{: #ida}

Ces instructions expliquent comment créer une connexion entre InfoSphere® Data Architect <!--version 9.1.x -->et une base de données {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Prérequis
{: #prereq5}

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) sont remplies.

### Procédure
{: #proc5}

1. Dans l'explorateur de source de données d'InfoSphere Data Architect, cliquez avec le bouton droit de la souris sur **Database Connections**, puis sélectionnez **New**.
    
2. Dans l'onglet **Local**, sélectionnez **DB2 for Linux, UNIX, and Windows** comme gestionnaire de base de données.
    
3. Sur l'onglet **General**, entrez les valeurs suivantes :

   - *Database* : `BLUDB`
   - *Host* : nom d'hôte que vous avez obtenu au préalable.
   - *Port* : pour une connexion sans SSL, entrez `50000`. Pour une connexion avec SSL, entrez `50001`. 
   - *User name* : ID d'utilisateur que vous avez obtenu au préalable.
   - *Password* : mot de passe que vous avez obtenu au préalable.

4. Pour une connexion SSL, cliquez sur l'onglet **Optional**. Entrez une propriété `sslConnection` et spécifiez la valeur `true`. Cliquez sur **Add**.
    
5. [*Facultatif*] : Cliquez sur **Test Connection** pour vérifier que la connexion a réussi.

## Aginity Workbench
{: #aginity_wb}

Ces instructions expliquent comment connecter Aginity Workbench <!--4.3 -->à une base de données {{site.data.keyword.dashdbshort_notm}}. Vous pouvez utiliser Aginity Workbench pour faire migrer les modèles de données IBM PureData for Analytics (Netezza) et les données vers {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Prérequis
{: #prereq6}

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) sont remplies.

### Procédure
{: #proc6}

1. Téléchargez et installez Aginity Workbench.

2. Déterminez votre nom de source de données ODBC à partir des informations de connexion relevées plus tôt.

3. Lancez Aginity Workbench. Si la boîte de dialogue de connexion à la base de données ne s'ouvre pas automatiquement, ouvrez-là en cliquant sur **Connect** sur la barre d'outils.

4. [Etablissement d'une connexion à la base de données](https://www.aginity.com/documentation/WB/dashDB/Default.htm#Aginity_Topics/Aginity_Workbench/Database_Connection_Dialog_Box.htm){:external}. Utilisez le nom d'hôte, l'ID d'utilisateur et le mot de passe qui se trouvent dans les informations de connexion relevées plus tôt.

## CLPPlus
{: #clpplus}

CLPPlus (Command line processor plus) est inclus dans le module de pilote Db2. CLPPlus fournit une interface de ligne de commande que vous pouvez utiliser pour vous connecter à une base de données {{site.data.keyword.dashdbshort_notm}}. Vous pouvez utiliser CLPPlus pour définir, éditer et exécuter des instructions, des scripts et des commandes.
{: shortdesc}

### Prérequis
{: #prereq7}

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) sont remplies.

Pour utiliser CLPPlus, assurez-vous qu'un kit de développement logiciel (SDK) ou un environnement d'exécution Java (JRE) est installé sur votre ordinateur pour la version Java 1.5.0 ou une version ultérieure et que les variables d'environnement sont définies comme suit :

- La variable d'environnement `JAVA_HOME` est définie sur le répertoire d'installation Java de votre ordinateur.
- La configuration de la variable d'environnement `PATH` inclut le sous-répertoire `bin` du répertoire d'installation Java sur votre ordinateur.

### Procédure
{: #proc7}

1. Exécutez les commandes suivantes dans un interpréteur de commande sur les systèmes d'exploitation Linux, sur l'invite de commande Windows ou dans la fenêtre de commande DB2 sur les systèmes d'exploitation Windows :

   Ces commandes créent de nouvelles entrées dans le fichier de configuration du pilote (`db2dsdriver.cfg`) sur votre ordinateur et définissent les attributs de connexion. Cette étape ne doit être effectuée qu'une seule fois.

   - Pour une connexion avec SSL :

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`  

     Où :
     
     - `<hostname>` est le nom d'hôte du serveur.
     - `<alias>` est un alias que vous choisissez.

   - Pour une connexion sans SSL :

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

2. Pour démarrer CLPPlus avec une connexion à une base de données {{site.data.keyword.dashdbshort_notm}} qui utilise les entrées dans le fichier `db2dsdriver.cfg`, exécutez la commande suivante :

   - Environnements Windows : 

     `clpplus <userid>@<alias>`

   - Environnements Linux :

     `clpplus -nw <userid>@<alias>`

     Où :
     
     - `<userid>` est l'ID d'utilisateur des données d'identification de connexion obtenues au préalable.
     - `<alias>` est l'alias que vous avez créé avec la commande **db2cli writecfg**.

   L'exécution de cette commande ouvre une fenêtre CLPPlus.

3. Dans la fenêtre CLPPlus, entrez votre mot de passe. Les informations de base de données s'affichent, suivies d'une invite SQL. Exemple de sortie :

```
   Hostname = 192.0.2.0
   Database server = DB2/LINUXX8664  SQL10054
   SQL authorization ID = smith
   Local database alias = BLUDB
   Port = 50001
   
   SQL>
```

### Résultats
{: #results7}

Vous pouvez maintenant entrer des commandes CLPPlus ou des instructions SELECT et exécuter des scripts pour travailler avec les données dans la base de données.

### Exemples

Les exemples suivants utilisent un script court qui extrait les lignes de l'exemple de tableau `GOSALES.BRANCH`. Le fichier script est appelé `cities.sql` et il est situé sur l'ordinateur Windows local, dans le répertoire `C:\temp`. Le fichier `cities.sql` contient le texte suivant :

```
SET ECHO ON
SELECT branch_code, city from GOSALES.BRANCH;
```

#### Exemple 1 

Pour exécuter le script en mode interactif :

1. Démarrez CLPPlus avec votre ID d'utilisateur et l'alias que vous avez créé dans le fichier `db2dsdriver.cfg` en exécutant la commande suivante :

   `clpplus <user_id>@<alias>`
2. Entrez votre mot de passe.
3. A l'invite SQL, entrez le texte suivant :

   `start C:\temp\cities.sql`

#### Exemple 2

Démarrez CLPPlus avec votre ID d'utilisateur et l'alias que vous avez créé dans le fichier `db2dsdriver.cfg`, puis exécutez le script en une étape :

`clpplus <user_id>/<password>@<alias> @C:\temp\cities.sql`

Exemple de sortie du script `cities.sql` :

```
BRANCH_CODE CITY
----------- --------------------------------------------------
          6 Paris
          7 Milano
          9 Amsterdam
         13 Hamburg
         14 München
         15 Kista
         17 Calgary
         18 Toronto
         19 Boston
         20 Seattle
         21 Los Angeles
         22 Miami
         23 Lyon
         24 Distrito Federal
         25 Tokyo
         26 Osaka City
         28 Melbourne
         29 Bilbao
         30 Sao Paulo
         31 Kuopio
         32 Seoul
         33 Singapore

BRANCH_CODE CITY
----------- --------------------------------------------------
         34 Shanghai
         35 London
         36 Birmingham
         37 Zürich
         38 Heverlee
         39 Wien
         40 Geneve

29 rows were retrieved.
```


