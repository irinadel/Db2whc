---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-24"

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

# Visualisation des données/Intelligence métier
{: #data_vis_bi}

Vous pouvez aussi connecter des outils et des applications externes à {{site.data.keyword.dashdbshort_notm}}
et les utiliser pour gérer ou analyser vos données. 
{: shortdesc}

## Cognos Analytics
{: #cognos}

Vous pouvez exécuter vos rapports IBM Cognos® avec des données stockées dans le cloud plutôt que dans une base de données sur site. Après avoir chargé vos données dans une base de données {{site.data.data.keyword.dashdbshort_notm}}, vous configurez le pilote JDBC, puis utilisez les outils d'administration Cognos pour créer la connexion de base de données. <!--These instructions explain how to connect to the database from Cognos version 10.2.1.-->
{: shortdesc}

Regardez cette vidéo pour voir comment créer une connexion.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Création d'une connexion à partir de Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TRUEPVHGi0s?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

Pour plus d'informations, voir [Connexions de Cognos Analytics ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/en/SSEP7J_11.0.0/com.ibm.swg.ba.cognos.ug_cra.doc/c_create_ds.html#create_ds){:new_window}

## Looker
{: #looker}

Vous pouvez connecter Looker à une base de données {{site.data.keyword.dashdbshort_notm}}. Looker est une application d'intelligence métier et une plateforme d'analyse des mégadonnées avec laquelle vous pouvez explorer, analyser et partager en temps réel des analyses commerciales.
{: shortdesc}

[Connexion de Looker ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.looker.com/setup-and-management/connecting-to-db){:new_window}

## Tableau
{: #tableau}

Ces instructions expliquent comment connecter Tableau à une base de données {{site.data.keyword.dashdbshort_notm}} et s'appliquent à Tableau Desktop<!--version 8.x-->, bien que la procédure soit similaire pour les autres outils de Tableau.
{: shortdesc}

### Prérequis
{: #prereq8}

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](/docs/services/Db2whc/connecting/connecting.html#prereqs) sont remplies.

### Procédure
{: #proc8}

1. Dans le tableau de bord de Tableau, ouvrez la fenêtre ou la page de votre outil qui est utilisée pour définir une connexion à la base de données.
2. Sur la page d'accueil, cliquez sur **Connect to data**.
3. Dans la liste **Data Sources** sélectionnez la source de données ou le pilote à utiliser pour votre connexion à la base de données. Dans la section **On a server** de la liste, sélectionnez **IBM Db2**.
4. Dans la fenêtre **IBM DB2 Connection**, entrez les informations de connexion à l'aide du tableau ci-dessous.

| Zone de Tableau | Zone d'information des connexions de Db2 |
|---------------|-----------------------------------|
| Etape 1 : entrez un nom de serveur | Nom d'hôte |
| Etape 2 : port | Numéro de port |
| Etape 3 : entrez une base de données sur le serveur | Nom de la base de données |
| Nom d'utilisateur | ID de l'utilisateur |
| Mot de passe | Mot de passe |
{: caption="Tableau 1. Zones de Tableau pour les informations de connexion" caption-side="top"}

5. Cliquez sur **Connect** pour établir la connexion. Tableau offre plusieurs options de connexion à vos données. Pour utiliser pleinement votre base de données {{site.data.keyword.dashdbshort_notm}}, choisissez l'option **Connect Live**.

## Microsoft Excel
{: #excel}

Ces instructions expliquent comment connecter Microsoft Excel <!--2010-->à une base de données {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Prérequis
{: #prereq9}

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](/docs/services/Db2whc/connecting/connecting.html#prereqs) sont remplies.

Vous devez avoir le module de pilote Db2 ou le module IBM® Data Server Driver Package installé sur votre ordinateur local. 

**Restriction** : les connexions entre Excel et {{site.data.keyword.dashdbshort_notm}} sont uniquement prises en charge sur le système d'exploitation Windows.

### Procédure
{: #proc9}

1. Dans la console Web, accédez à la page **Run SQL**.
    
2. Entrez une ou plusieurs instructions SELECT dans la boîte de texte de l'éditeur.

3. Cliquez sur l'une des options d'exécution.

4. Cliquez sur **Excel ODC File**.

5. Téléchargez le fichier `BLUExcel.odc` et ouvrez-le dans Excel. Si un avis de sécurité s'affiche, cliquez sur **Enable**.

6. Cliquez sur **Open** pour vous connecter à la base de données {{site.data.keyword.dashdbshort_notm}}. La boîte de dialogue **Connect To DB2 Database** s'ouvre.

7. Entrez l'ID d'utilisateur et le mot de passe que vous utilisez pour vous connecter à {{site.data.keyword.dashdbshort_notm}}. Pour obtenir l'ID d'utilisateur et le mot de passe, cliquez sur **Connect** ou sur **Connect > Connection information** dans la console Web.

8. Vérifiez que le mode de connexion est `Share`, puis cliquez sur **OK**.

### Résultats
{: #results2}

Les résultats de la requête s'affichent dans une feuille de calcul Excel. Ces résultats sont les mêmes que ceux qui s'affichent dans le visualiseur Résultats. Vous pouvez maintenant générer des graphiques et des rapports et analyser vos données avec Excel. Pour en savoir plus sur la manière de procéder et sur la façon dont vous pouvez exécuter des requêtes SQL sur vos données à partir de la console Web, voir : 
- [Tutoriel : Generating charts and reports by using Excel ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/explore_excel_reports.html){:new_window}
- [Analyse avec Excel ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/exploreexcel.html){:new_window}

## Esri ArcGIS for Desktop
{: #esri_arcgis}

Vous pouvez connecter Esri ArcGIS for Desktop <!--version 10.3.1 -->à une base de données {{site.data.keyword.dashdbshort_notm}} puis l'utiliser pour analyser et visualiser des données géospatiales.
{: shortdesc}

### Prérequis
{: #prereq10}

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](/docs/services/Db2whc/connecting/connecting.html#prereqs) sont remplies.

Vous devez avoir le module de pilote Db2 ou le module IBM® Data Server Driver Package installé sur votre ordinateur.

### Procédure
{: #proc10}

1. Déterminez votre nom de source de données ODBC à partir des [informations de connexion](/docs/services/Db2whc/connecting/credentials.html) obtenues précédemment.

2. Créez une nouvelle connexion :
      
   a. Dans l'arborescence du catalogue ArcCatalog, ouvrez le noeud Database Connections et cliquez sur **Add Database Connection**.
        
   b. Dans l'assistant de Database connections :
   - Sélectionnez **DB2** dans la liste déroulante de la plateforme de base de données.
   - Entrez la chaîne suivante dans la zone **Data source** :
     ```
     HostName=<hostname>;Port=<port>;Database=<database>;
     CLIENTBUFFERSUNBOUNDLOBS=1;LOBCACHESIZE=50000000;
     FET_BUF_SIZE=256K  
     ```

     où `<hostname>`, `<port>` et `<database>` sont des espaces réservés qui représentent le nom d'hôte, le numéro de port et le nom de la base de données que vous avez notés auparavant.
            
   - Sélectionnez **Database authentication** comme type d'authentification.
            
   - Spécifiez votre nom d'utilisateur et votre mot de passe (l'ID d'utilisateur et le mot de passe que vous avez notés auparavant) dans les zones correspondantes.
            
   - Appuyez sur **OK**.
        
     ![Assistant de connexion à la base de données](images/2_gs_conn.jpg)

### Résultats
{: #results3}

Le composant ArcCatalog de Esri ArcGIS for Desktop est maintenant connecté à votre base de données {{site.data.keyword.dashdbshort_notm}}. 


