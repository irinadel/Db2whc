---

copyright:
  years: 2014, 2019
lastupdated: "2018-12-07"

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

# Plans et configurations
{: #plans_cfgs}

Vous pouvez choisir un plan {{site.data.keyword.dashdbshort_notm}} configuré et optimisé pour le travail que vous devez effectuer :
{: shortdesc}

   * Un plan d'entrée pour essayer le produit, qui propose un essai gratuit avec 1 Go de stockage maximum. Voir [Restrictions du plan Entry](#ep_restrictions)
   * Des plans flexibles dans lesquels vous pouvez mettre à l'échelle le stockage et calculer les ressources de manière indépendante.
   * Des plans SMP de tailles variées (petits, moyens et grands) pour la production, proposant un seul noeud et une instance unique.
   * Des configurations de cluster multi-noeud MPP pour un traitement parallèle et de hautes performances
   * Des plans configurés pour la haute disponibilité
   * Une compatibilité Oracle

Affichez tous les plans {{site.data.keyword.dashdbshort_notm}} disponibles dans le [catalogue {{site.data.keyword.Bluemix}}](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window}.
<!--   * Plans configured for data warehouse and online analytical processing (OLAP) workloads: [{{site.data.keyword.dashdbshort_notm}}](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window} -->
<!--   * Plans configured for high-speed, transactional processing (OLTP): [{{site.data.keyword.dashdbshort_notm}} for Transactions](https://console.ng.bluemix.net/catalog/services/dashdb-for-transactions-sql-database){:new_window} -->

Regardez cette vidéo pour voir une introduction au plan {{site.data.keyword.dashdbshort_notm}} Flex Performance.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Création d'une connexion depuis Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

Vous pouvez demander à ce que votre service {{site.data.keyword.dashdbshort_notm}} soit déployé dans un environnement isolé du réseau sur {{site.data.keyword.Bluemix}}. Contactez le [service commercial {{site.data.keyword.IBM_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/connect/ibm/fr/fr/?lnk=fcw){:new_window}.

Si, dans le catalogue, vous ne trouvez pas la configuration dont vous avez besoin, contactez [l'équipe commerciale {{site.data.keyword.IBM_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/connect/ibm/fr/fr/?lnk=fcw){:new_window} pour rechercher d'autres options.

## Disponibilité des plans dans les centres de données
{: #availability}

Le tableau suivant présente des informations sur la disponibilité des différents plans {{site.data.keyword.dashdbshort_notm}} en fonction des centres de données de différentes régions géographiques :


| Plans {{site.data.keyword.dashdbshort_notm}} | Asie/Pacifique | Europe    | Amérique du Nord/centrale     | Amérique du Sud |
|------------------------------|--------------|-----------|-----------------------    |---------------|
| Flex                         | *N/D          | Francfort | Washington D.C. (est des E.U.) | *N/D           |
|                              |              |           | Dallas (Sud des E.U.)         |               |  
|      |||||
| SMP                          | Hong Kong    | Amsterdam | Washington D.C. (est des E.U.) | São Paulo     |
|                              | Séoul        | Francfort | Dallas (Sud des E.U.)         |               | 
|                              | Singapour    | Londres    | Montréal                  |               | 
|                              | Sydney       | Milan     | Querétaro                 |               | 
|                              | Tokyo        | Oslo      | Toronto                   |               | 
|                              |              | Paris     |                           |               |
|      |||||
| MPP                          | Hong Kong    | Amsterdam | Washington D.C. (est des E.U.) | São Paulo     |
|                              | Séoul        | Francfort | Dallas (Sud des E.U.)         |               | 
|                              | Singapour    | Londres    | Montréal                  |               | 
|                              | Sydney       | Milan     | Querétaro                 |               | 
|                              | Tokyo        | Oslo      | Toronto                   |               | 
|                              |              | Paris     |                           |               |
{: caption="Tableau 1. Centre de données prenant en charge les plans de service Db2 Warehouse on Cloud" caption-side="top"}

*N/D = Non disponible actuellement

## Restrictions du plan Entry
{: #ep_restrictions}

Il est fortement recommandé d'utiliser un plan de service de niveau d'entreprise et non un plan de service Entry pour les charges de travail sensibles aux performances ou stratégiques.
{: important}

Le tableau suivant présente les restrictions du plan {{site.data.keyword.dashdbshort_notm}} Entry :

| Catégorie | Elément | Restriction | 
|----------|------|-------------|
| Ressources | Stockage | 20 Go de stockage par utilisateur. Le plan est gratuit uniquement lorsque moins d'1 Go de stockage est utilisé. |
|  | Connexions | 50 connexions par utilisateur. Cette limite peut être ajustée de manière dynamique afin de préserver l'intégrité du système de l'instance. |
|  | Performances | Les performances peuvent varier car des charges de travail peuvent être exécutées par d'autres utilisateurs sur le système à service partagé |
|  |  |
| Fonctions | Fédération | Pas de prise en charge |
|  | Compatibilité Oracle | Pas de prise en charge |
|  | Extensions définies par l'utilisateur (UDF) | Pas de prise en charge |
|  | Gestion des utilisateurs | L'utilisateur ne dispose pas de droits d'administration |
|  | Contrôle d'accès aux lignes et aux colonnes (RCAC) | Pas de prise en charge |
|  | IBM InfoSphere Data Replication à utiliser lors du chargement de données | Pas de prise en charge |
|  |  |
| Environnement réseau | IBM Cloud Integrated Analytics | Pas de prise en charge |
|  | IBM Cloud Dedicated | Pas de prise en charge |
|  |  |
| Conformité en matière de sécurité | Loi Health Information Portability and Accountability Act de 1996 (HIPAA) | Pas de prise en charge. Consultez la description de service. |
|  | Règlement général sur la protection des données (RGPD) européen | Aucune restriction spécifique |
|  |  |
| Gestion des comptes | Réactivation | Aucune exigence de réactivation |
{: caption="Tableau 1. Restrictions du plan {{site.data.keyword.dashdbshort_notm}} Entry" caption-side="top"}
