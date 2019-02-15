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

# Data science
{: #ds}

Vous pouvez aussi connecter des outils et des applications externes à {{site.data.keyword.dashdbshort_notm}}
et les utiliser pour gérer ou analyser vos données. 
{: shortdesc}

## Watson Studio
{: #watson_studio}

Après avoir créé un projet dans IBM Watson Studio (avant : Data Science Experience), vous devez y ajouter les actifs de données pour pouvoir travailler avec les données. Tous les collaborateurs du projet sont automatiquement autorisés à accéder aux données du projet.
{: shortdesc}

La façon dont vous ajoutez des données et à partir de quel endroit vous pouvez le faire diffère entre les projets IBM Watson et les projets existants. Les projets IBM Watson utilisent {{site.data.keyword.Bluemix_notm}} Object Storage. Le projet est un projet existant s'il utilise Object Storage OpenStack Swift. 

### Pour créer une nouvelle connexion dans un projet IBM Watson :

1. Cliquez sur **Add to project > Connection**.
    
2. Sélectionnez une source de données.
    
3. Entrez les informations de connexion requises pour votre source de données. Généralement, vous devrez fournir des informations telles que l'hôte, le numéro de port, le nom d'utilisateur et le mot de passe.
    
4. Vous pouvez détecter les actifs des connexions à {{site.data.keyword.dashdbshort_notm}}, ce qui vous donne la possibilité d'ajouter toutes les tables de la connexion en tant qu'actifs de données dans un projet. Sélectionnez **Discover data assets** et choisissez un projet.
    
5. Cliquez sur **Create**. La connexion apparaît sur la page **Assets**.

Regardez cette vidéo pour voir comment créer une connexion et ajouter les données connectées à un projet.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Create a connection and add connected data to a project" type="text/html" width="640" height="390" src="//www.youtube.com/embed/U7-gCbo4QtM?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

### Pour créer une nouvelle connexion dans un projet existant :

1. Sur la page **Assets** de votre projet, cliquez sur l'icône **Find and add data**.
    
2. Sur le panneau **Connections**, cliquez sur **Create Connection**.

3. Entrez un nom et une description et sélectionnez une catégorie de service :

   **Data Service** = service de données {{site.data.keyword.Bluemix_notm}}

   Lorsque vous sélectionnez **Data Service**, vos services de données {{site.data.keyword.Bluemix_notm}} existants apparaissent dans la liste **Service Instance**.

4. Sélectionnez le service ou le serveur de base de données dans la liste.

5. Entrez les informations de connexion :

   Lorsque vous sélectionnez **Data Service**, vos services de données {{site.data.keyword.Bluemix_notm}} existants apparaissent dans la liste **Service Instance**.
    
6. Cliquez sur **Create**. La connexion est disponible pour tous les projets existants.
    
7. Sur le panneau **Connections**, sélectionnez la connexion et cliquez sur **Apply**.

Pour ajouter une connexion existante à un projet existant :

1. Sur la page **Assets** de votre projet, cliquez sur l'icône **Find and add data**.
    
2. Sur le panneau **Connections**, sélectionnez la connexion et cliquez sur **Apply**.

## SPSS Statistics
{: #spss_stats}

Ces instructions expliquent comment créer une connexion entre IBM® SPSS® Statistics et une base de données {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Prérequis
{: #prereq1}

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](connecting.html#prereqs) sont remplies.

### Procédure
{: #proc1}

1. Dans SPSS Statistics, cliquez sur **File > Open Database > New Query**.
    
2. Dans l'assistant de base de données, cliquez sur **Add ODBC data source**.
    
3. Utilisez la fenêtre ODBC Data Source Administrator pour ajouter un nom de source de données ODBC pour la base de données {{site.data.keyword.dashdbshort_notm}} :
        
   a. Sur l'onglet **User DSN**, cliquez sur **Add**.

   b. Sur la fenêtre Create New Data Source, sélectionnez le pilote **IBM DB2 ODBC DRIVER** et cliquez sur **Finish**.

   Assurez-vous que le pilote que vous sélectionnez n'est pas un pilote avec un nom similaire comme `IBM DB2® ODBC DRIVER - DB2COPY`. Si le pilote n'apparaît pas dans la liste, sortez de SPSS Statistics, puis téléchargez et installez le pilote. Voir [Module de pilote Db2](driver_pkg.html).
        
   c. Dans la fenêtre ODBC IBM Driver - Add, entrez une nom de source de données (généralement le nom de la base de données à laquelle vous vous connectez) et cliquez sur **Add**.
        
   d. Dans la fenêtre CLI/ODBC Settings, sur l'onglet **Data Source**, entrez l'ID d'utilisateur et le mot de passe des [informations de connexion](credentials.html) que vous avez obtenues auparavant.
        
   e. Sur la page Advanced Settings, pour chacun des paramètres suivants, cliquez sur **Add** pour ouvrir la fenêtre Add CLI Parameter et commencer la procédure, puis cliquez sur **OK** pour revenir à la page Advanced Settings :
            
   - Sélectionnez le paramètre `Database` puis cliquez sur **OK** pour ouvrir la fenêtre CLI/ODBC Settings. Dans la zone **Pending Value**, entrez le nom de la base de données des informations de connexion que vous avez obtenues plus tôt.

   - Sélectionnez le paramètre `Hostname`, puis cliquez sur **OK** pour ouvrir la fenêtre CLI/ODBC Settings. Dans la zone **Pending Value**, entrez le nom d'hôte des informations de connexion que vous avez obtenues plus tôt.

   - Sélectionnez le paramètre `Port`, puis cliquez sur **OK** pour ouvrir la fenêtre CLI/ODBC Settings. Dans la zone **Pending Value**, entrez le nom de port des informations de connexion que vous avez obtenues plus tôt.
            
   - Sélectionnez le paramètre `Protocol`, puis cliquez sur **OK** pour ouvrir la fenêtre CLI/ODBC Settings. Sélectionnez **TCP/IP**.
        
   f. Cliquez sur **OK** pour revenir à la fenêtre ODBC Data Source Administrator.
        
   g. Sur l'onglet **User DSN**, sélectionnez le nom de la source de données puis cliquez sur **Configure**.
        
   h. Sur la fenêtre CLI/ODBC Settings, cliquez sur **Connect** pour tester la connexion.
            
   - Si la connexion a réussi, cliquez sur **OK** pour revenir à la fenêtre ODBC Data Source Administrator, puis cliquez sur **OK** pour sortir de la fenêtre.
            
   - Si la connexion a échoué, notez les erreurs et corrigez-les avant le tester à nouveau la connexion.

## SAS
{: #sas}

Ces instructions expliquent comment créer une connexion entre SAS et une base de données {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Prérequis
{: #prereq2}

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](connecting.html#prereqs) sont remplies.

### Procédure
{: #proc2}

Pour connaître la procédure à suivre pour connecter SAS à une base de données {{site.data.keyword.dashdbshort_notm}}, consultez la documentation SAS :
- [Interface SAS/ACCESS à DB2 sous hôtes UNIX et PC ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](https://documentation.sas.com/?docsetId=acreldb&docsetTarget=p1dzq4zjg1iycgn16l4xj9nnvibt.htm&docsetVersion=9.4&locale=en){:new_window}

## Environnement de développement R
{: #r_dev_env}

Au lieu d'utiliser l'environnement RStudio® intégré à IBM Watson Studio, vous pouvez utiliser votre propre environnement de développement R installé localement, si vous le souhaitez. Par exemple, vous pouvez avoir votre propre installation RStudio ou préférer utiliser un autre outil de développement tel que Rcmdr ou Rattle. Ces instructions expliquent comment connecter un environnement de développement R à une base de données {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Prérequis
{: #prereq3}

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](connecting.html#prereqs) sont remplies.

### Procédure
{: #proc3}

1. Dans votre environnement R local, installez le module `ibmdbR` en entrant la commande suivante :

   `install.packages("ibmdbR")`

   Votre environnement R local accède au réseau CRAN (Comprehensive R Archive Network), puis télécharge et installe automatiquement le module `ibmdbR` ainsi que tout module requis n'étant pas déjà installé.
    
2. Créez une connexion de pilote ODBC entre votre environnement de développement R et votre base de données {{site.data.keyword.dashdbshort_notm}} :
        
   a. [Configuration de votre base de données en tant que source de données ODBC![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_cli_and_odbc_applications.html){:new_window}.
        
   b. Ouvrez votre environnement de développement R installé localement.
        
   c. A l'invite R, entrez les instructions suivantes pour créer la connexion. Remplacez les espaces réservés par les [informations de connexion](credentials.html) obtenues plus tôt.

   - Si votre environnement de développement R installé localement s'exécute dans la base de données {{site.data.keyword.dashdbshort_notm}} :

     ```
     library(ibmdbR)
     host.name <- "placeholderForYourHostName"
     port <-"placeholderForPortNumber" # 50000 if not using SSL or 50001 if using SSL
     user.name <-"placeholderForYourUserName"
     pwd <- "placeholderForYourPassword"
     con.text <- paste("placeholderForYourDSNName;DRIVER=BLUDB",
                       ";Database=BLUDB",
                       ";Hostname=",host.name,
                       ";Port=",port,
                       ";PROTOCOL=TCPIP",
                       ";UID=", user.name,
                       ";PWD=",pwd,sep="")
     # Connect to using a odbc Driver Connection string to a remote database
     con <- idaConnect(con.text)
     ```

   - Si votre environnement de développement R installé localement ne s'exécute pas dans la base de données {{site.data.keyword.dashdbshort_notm}} :

     ```
     library(ibmdbR)
     driver.name <- "{placeholderForYourDriverName}"
     db.name <- "placeholderForYourDatabaseName"
     host.name <- "placeholderForYourHostName"
     port <-"placeholderForYourPort"
     user.name <-"placeholderForYourUserName"
     pwd <- "placeholderForYourPassword"
     con.text <- paste("placeholderForYourDSNName;DRIVER=",driver.name,
                       ";Database=",db.name,
                       ";Hostname=",host.name,
                       ";Port=",port,
                       ";PROTOCOL=TCPIP",
                       ";UID=", user.name,
                       ";PWD=",pwd,sep="")
     # Connect to using a odbc Driver Connection string to a remote database
     con <- idaConnect(con.text)
     ```

     **Remarque **: l'instruction qui est utilisée pour créer l'objet connexion utilise la méthode `idaConnect()`, et non les méthodes `odbcConnect()` ou `odbcDriverConnect()`.
        
   d. Initialisez le module d'analyse en émettant la commande R suivante :

   `idaInit(con)`

   e. Pour tester si la connexion fonctionne, exécutez la commande R suivante :

   `idaShowTables()`

   La console affiche une liste de toutes les tables et vues dans le schéma en cours.

