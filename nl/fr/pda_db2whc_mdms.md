---

copyright:
  years: 2014, 2019
lastupdated: "2018-06-15"

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

# Migration depuis IBM PureData System for Analytics (Netezza)
{: #pda}

Le périphérique {{site.data.keyword.Bluemix_notm}} MDMS (Mass Data Migration Service) peut-être utilisé pour migrer les données provenant de grosses bases de données IBM PureData Systems for Analytics (Netezza) de 25 To et plus vers une base de données {{site.data.keyword.dashdblong}} sur {{site.data.keyword.Bluemix_notm}}.

MDMS offre un moyen simple, rapide et sécurisé de transférer physiquement d'importants volumes de données (mesurés en téraoctets ou pétaoctets) vers {{site.data.keyword.Bluemix_notm}}. MDMS est un périphérique de stockage mobile proposant 120 To de capacité de stockage utilisable. Il vous permet de relever les défis posés quotidiennement par le transfert de gros volumes d'informations : coûts élevés, temps de transfert longs et problèmes de sécurité – tout ceci, dans un seul et même service.
{: shortdesc}

![Vue du périphérique Mass Data Migration Service](images/mdms.svg)

## De quoi avez-vous besoin quand vous demandez un périphérique ?
{: #prereq}

1. Paramètres réseau pour le périphérique de stockage
   - Adresse IP statique
   - Masque de réseau pour permettre le transfert de données
2. Paramètres réseau pour l'ordinateur distant
   - Adresse IP statique
   - Masque de réseau 
   - Passerelle par défaut pour accéder à l'interface utilisateur
3. Destination de téléchargement de Cloud Object Storage <br/>
   Vous devez disposer d'au moins un compte {{site.data.keyword.cos_full}} et un compartiment dans un emplacement US Cross Region ou US South pour compléter le formulaire de demande. Si vous n'avez pas encore de compte {{site.data.keyword.cos_full_notm}}, créez-en un avant de demander un périphérique MDMS. Pour plus d'informations, voir : [About {{site.data.keyword.cos_full}}](/docs/services/cloud-object-storage/about-cos.html){:new_window}.
   {: important}

## Etape 1 : création d'une demande
{: #create-req}

1. Connectez-vous au portail [{{site.data.keyword.slportal}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://control.softlayer.com/){:new_window} en utilisant vos données d'identification uniques.
2. Sélectionnez **Storage > Data Migration > Mass Data Migration** dans la barre de navigation pour accéder à la page d'arrivée MDMS.
3. Cliquez sur **Request Device** afin d'ouvrir le formulaire de commande.
4. Remplissez chaque zone du formulaire de commande **Mass Data Migration**.
   - **Shipping Address** : ce formulaire n'est pas prérempli et chaque zone est éditable. Indiquez le nom de la personne qui acceptera la livraison du périphérique dans la zone Attention. Quand vous sélectionnez le lieu de livraison, tenez compte du poids du périphérique (30 kg avec sa mallette) et de l'accessibilité. <br/> (**Remarque** : Le périphérique est équipé de roues et de poignées rétractables pour une meilleure maniabilité.)
   - **Key Migration Contacts** : ce formulaire n'est pas prérempli. Chaque zone est modifiable. Plusieurs personnes peuvent être ajoutées.
   - **Data Center Network Configuration** : fournit des détails de configuration réseau pour la mise à disposition préalable du port Eth3 sur le périphérique MDMS avant l'expédition.
   - **Data Offload Destination** : sélectionnez dans la liste votre compte cible existant.
   - **Request Name** : entrez un nom pour vous permettre de suivre votre commande.
5. Cochez la case **I have read and agree to the full terms of the Mass Data Migration Agreement** après avoir lu chaque contrat de service fourni.
6. Cliquez sur **Place Request** pour soumettre la demande. Cliquez sur **Cancel** pour abandonner complètement le formulaire et retourner sur la page d'arrivée MDMS.

## Etape 2 : préparation et expédition
{: #prep-ship}

Une fois la demande soumise, le statut du ticket de demande apparaît en tant que *Processing Request*. Quand votre demande a été traitée, {{site.data.keyword.IBM}} commence la préconfiguration du prochain périphérique disponible et le statut de la grille [Requests ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://control.softlayer.com/storage/mdms){:new_window} affiche *Prepping Device* puis *Awaiting Shipment*. Une fois que votre requête entre dans le statut *Awaiting Shipment*, elle ne peut plus être annulée. 

Un coursier vient chercher le périphérique qui doit être livré à l'emplacement que vous avez indiqué. A ce stade, le statut de la demande est mis à jour en *Device Shipped*. Le numéro de suivi est partagé avec vous dans la section **Order Details** de la grille [Requests ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://control.softlayer.com/storage/mdms){:new_window}.

## Etape 3 : réception et connexion
{: #rec-con}

<!-- **[Editor's note: What to keep from this section immediately below?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
1. The device arrives pre-configured for you. Basic [powering/connectivity instructions](docs/infrastructure/mass-data-migration/user-instructions.html) are included.  **[Editor's note: Are the instructions included in the MDMS package? If so, are they different from the instructions found with the "powering/connectivity" link?]**<br/>
  **Note**: User name and storage pool password is provided separately. Check the **Request Details** in your [Requests ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/storage/mdms){:new_window} grid for the credentials.
2. Point your browser to the static IP address that you provided in the order form. **[Editor's note: Is this done on PDA? What system is the static IP address for?]**
3. Log in. Enter password to unlock the empty storage pool. **[Editor's note: How is this done?]**<br/>
   **Note**: See the **Request Details** of your [Requests ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/storage/mdms){:new_window} grid for the password.
4. Mount the NFS share on your server. **[Editor's note: How is this done?]**
5. Rerun your DataShuttle inventory to ensure any new files are captured. **[Editor's note: Is "DataShuttle inventory" a command that is run on PDA?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& -->

### Présentation

Le périphérique {{site.data.keyword.cloud}} MDMS (Mass Data Migration Service) est un périphérique de stockage, capable de présenter des partages montables NFS (Network File System) ou FileNet CFS (Content Federations Services), qui est géré via une interface de navigateur Web. Le périphérique est expédié vers votre centre de données, chargé avec des données sur site, retourné vers un centre de données {{site.data.keyword.BluSoftlayer_full}} et vos données sont chargées dans votre compte {{site.data.keyword.cos_full}}.

### Alimentation

Le périphérique inclut un cordon d'alimentation C13-US ([IEC 60320 ![Icône d lien externe](../../icons/launch-glyph.svg "Icône d lien externe")](https://en.wikipedia.org/wiki/IEC_60320){:new_window}). Si le périphérique est utilisé en dehors des Etats-Unis, un adaptateur d'alimentation peut s'avérer nécessaire.

Le périphérique MDMS accepte toutes les gammes de puissance standard.
![Gamme de puissance](/images/PowerRating.png)

### Connectivité Ethernet

Deux connexions Ethernet doivent être effectuées, la première pour la gestion du périphérique via un navigateur, et la deuxième pour le transfert de données sur le même sous-réseau que celui où résident les données source.

Les deux ports proviennent du périphérique car les câbles RJ45 et CAT6A sont fournis. Des adaptateurs SFP+ cuivre sont fournis pour la conversion à partir de RJ45. Les adaptateurs sont compatibles avec tous les fabricants d'interrupteur. Ces adaptateurs se trouvent dans une pochette dans la section inférieure du couvercle du carton d'expédition.

- Eth1 (1GbE-B) est utilisé pour la gestion du périphérique et, en tant que tel, doit avoir une passerelle spécifiée dans la configuration d'adresse IP, visible sur l'écran LCD une fois le périphérique mis sous tension (voir la section [Configuration d'adresse IP](#ip_cfg)).

- Eth3 (10GbE-B) est utilisé pour le transfert des données. Cette connexion doit se trouver sur le même sous-réseau que les données source ou peut être connectée directement au serveur, si nécessaire.

Si un facteur de forme différent est requis pour la connexion Ethernet, vous devez fournir le convertisseur.

### Instructions utilisateur étape par étape

1. Le périphérique MDMS arrive préconfiguré avec votre adresse IP, votre nom d'utilisateur, un pool de stockage verrouillé et un partage NFS. Le mot de passe utilisateur et le mot de passe du pool de stockage vous sont communiqués dans un e-mail distinct.

2. Déterminez l'endroit le plus approprié pour placer le périphérique, pas trop loin de l'alimentation et de vos connexions Ethernet (1GbE et 10GbE) et avec le moins de passage possible.

3. Positionnez le périphérique à connecter. Il peut rester dans sa mallette de transport lors de son utilisation. Assurez-vous que le périphérique est à température ambiante et qu'il n'y a pas de condensation. Connectez-le à l'alimentation en utilisant le câble fourni sous le couvercle de la mallette. Mettez le périphérique sous tension.<br/>
    Deux interrupteurs d'alimentation sont présents.
    {: note}

    ![Interrupteurs d'alimentation](/images/MDMSPowerSwitch.png)
    Il n'est pas nécessaire de sortir le périphérique de la mallette portable.
    {: note}

4. Retirez le câble CAT6A de son logement dans le couvercle de la mallette et connectez-le au port Eth3 (10GbE-B) repéré dans l'image ci-dessous. ![Emplacement des ports Eth1 et Eth3](/images/MDMSNewEth1and3.png)

5. Connectez l'adaptateur CAT6A vers SFP+ et reliez-le à votre interrupteur 10Gb.

6. Si l'adresse IP configurée pour Eth3 peut être atteinte via un navigateur `https://<your_Eth3_IP_Address>`, passez à l'étape suivante. 

   Sinon, effectuez une connexion au port Eth1 (1GbE-B). Ouvrez votre navigateur et entrez `https://<your_Eth1_IP_Address>`. Entrez l'adresse IP Eth1 appropriée à votre configuration réseau. Acceptez l'exception de certificat.<br/>
   Si vous devez modifier un ou plusieurs paramètres IP pour Eth3 ou Eth1, voir la section [Configuration d'adresse IP](#ip_cfg).
   {: note}

7. Utilisez le nom d'utilisateur et le mot de passe fournis pour vous connecter.<br/>
    ![Page de connexion](/images/Login.png)

8. L'assistant de flux de travaux présente l'accès à des éléments spécifiques généralement utilisés dans l'ordre de gauche à droite.<br/>
    ![Icône de flux de travaux](/images/workflow.png) <br/>
    Le flux de travaux peut être rouvert en utilisant **Workflow Manager** dans l'angle supérieur gauche de l'interface utilisateur graphique.
    {: note}

9. Activez le pool de stockage préconfiguré :
    - Cliquez sur **Unlock and Start Storage Pool**.
    - Entrez la phrase de passe de votre pool de stockage et cliquez sur **OK**.
    ![Activation du pool de stockage](/images/UnlockPool.png)

10. Par défaut, les deux protocoles NFS et SMB sont activés sur le partage, sans restrictions d'accès. Pour restreindre l'accès à ce partage (pour NFS ou SMB), cliquez avec le bouton droit de la souris sur le nom du partage et sélectionnez l'élément de menu approprié.<br/>
    ![Restriction de l'accès au partage](/images/ShareControls.png)

11. Lorsque le pool de stockage est activé, le partage NFS est disponible pour montage. Dans le flux de travaux, cliquez sur **View Network Shares** afin d'afficher la vue des partages de réseau. Fermez le flux de travail, cliquez avec le bouton droit de la souris sur le partage et sélectionnez **View Mount Command** pour voir le nom de partage et les informations de montage. Montez le partage sur votre serveur source. Veillez à spécifier l'adresse IP du lien 10 Go lors du montage du partage.
    ![Montage du partage](/images/MountCommand.png)

## Etape 4 : copie des données et expédition
{: #copy-ship}

<!-- &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&

1. Run the DataShuttle copy to move the data. **[Editor's note: What is "DataShuttle"? Is "DataShuttle copy" a command that is run on PDA?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& -->

1. Copiez vos données dans le partage NFS. Choisissez l'une des méthodes suivantes pour extraire vos données de votre base de données Netezza :
    1. Exécutez l'exemple suivant de l'utilitaire **nz_backup** :

       `/nz/support/contrib/bin/nz_backup –db <db_name> –d <target_directory>  ascii threads 4`

       ****Remarque : la valeur `<target_directory>` est le partage NFS du périphérique MDMS qui est monté sur votre serveur Netezza.
   
    2. Exécutez l'exemple d'une instruction CREATE EXTERNAL TABLE ci-après :

       `CREATE EXTERNAL TABLE '<path_to_mdms_device>/<file_name>' SELECT * FROM <table name>`

       **Remarque :** si vous avez utilisé les options de clause `USING` pour l'exportation de données, souvenez-vous en ou sauvegardez-les. La clause est réutilisée plus tard lors du processus de chargement depuis {{site.data.keyword.Bluemix_notm}} Object Storage.

       Pour plus d'informations sur l'instruction SQL, voir : [CREATE EXTERNAL TABLE statement ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.sql.ref.doc/doc/r_create_ext_table.html){:new_window}. 

<!--       - Provide the {{site.data.keyword.Bluemix_notm}} team with the "USING" clause that was used for data export. The clause is reused during the load process on {{site.data.keyword.Bluemix_notm}}.
       - Select FORMAT = "Text"
-->

2. Dans le flux de travaux, cliquez sur **View Network Activity** pour afficher la charge Ethernet entrante dans l'interface utilisateur graphique pendant que les données sont transférées vers le périphérique sur la liaison 10 Go/sec.
    ![Affichage de l'activité](/images/UserGuide13.png)

3. Dans le flux de travaux, cliquez sur **View Storage Pools** pour surveiller l'utilisation du stockage et la mesure IOPS (Input/Output Operations Per Second) sur le périphérique.
    ![Vue des pools de stockage](/images/UserGuide14.png)

4. Quand la copie est terminée, pensez à éteindre le système. En procédant ainsi, vous verrouillez également le pool de stockage. Dans le flux de travaux, cliquez sur **Shutdown Appliance...**.  
    ![Emplacement dans l'interface utilisateur du bouton d'arrêt de l’appareil](/images/Shutdown.png)

5. Déconnectez le périphérique. Remettez le câble d'alimentation, le câble Ethernet et l'adaptateur SFP+ dans leurs emplacements de stockage respectifs, sous le couvercle.

6. Fixez l'étiquette d'expédition fournie sur l'appareil. Notifiez l'expéditeur et retournez l'appareil au centre de données {{site.data.keyword.BluSoftlayer_full}}. Vos données, une fois qu'elles sont arrivées au centre de données, sont chargées dans votre compartiment {{site.data.keyword.cos_full_notm}}.

Après le retour de l'appareil à l'équipe {{site.data.keyword.BluSoftlayer}}, le statut de la demande passe à *Device Received*.

## Etape 5 : déchargement et accès
{: #offload}

Lors du processus de transfert des données, le statut de la demande est à *Offloading Data*. Il change à nouveau quand la migration vers le compartiment {{site.data.keyword.objectstorageshort}} est terminée (*Offload Complete*). Vos données sont immédiatement accessibles une fois achevé le déchargement haut débit dans votre compartiment Cloud Object Storage. 

Quand la migration de vos données vers le compartiment Cloud Object Storage est terminée, vous pouvez [importer vos données dans vos bases de données {{site.data.keyword.dashdbshort_notm}}](#import).

## Etape 6 : importation des données depuis {{site.data.keyword.Bluemix_notm}} Object Storage
{: #import}

Pour charger les données depuis {{site.data.keyword.Bluemix_notm}} Object Storage en utilisant directement les tables externes, utilisez l'exemple d'instruction SQL ci-dessous :

```
INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net', 
  '<S3-access-key-ID>',
  '<S3-secret-access-key>', 
  '<my_bucket>'
     )
  )      
```

**Remarques :** 
* Prenez soin d'utiliser les mêmes options de clause `USING` que celles dont vous vous êtes servi pour extraire les données de votre base de données PureData System for Analytics (Netezza) via l'instruction CREATE EXTERNAL TABLE.
* Pour {{site.data.keyword.Bluemix_notm}} Object Storage, pour créer des données d'identification HMAC lors de la création de nouvelles données d'identification de service, spécifiez {"HMAC:true"} dans la zone *Ajouter des paramètres de configuration en ligne*.

Pour savoir comment importer des données depuis {{site.data.keyword.Bluemix_notm}} Object Storage, consultez le tutoriel suivant : [IBM Db2 Warehouse on Cloud guided demo: Explore data loading ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud/){:new_window}.

## Etape 7 : effacement du contenu du périphérique MDMS
{: #erase}

{{site.data.keyword.IBM}} implémente un nettoyage de données, en respectant les exigences de l'US Department of Defense pour effacer de façon permanente vos données du périphérique MDMS. Une fois cette opération terminée, le statut de la demande est à *Erase Complete*.

## Notes supplémentaires
{: #notes}

### Unicité dans le compartiment

Pour garantir que les noms des objets sont uniques quand ils sont copiés dans le compartiment, le chemin d'accès au fichier est inclus en tant que préfixe dans le nom d'objet. Ainsi, le fichier config.ini du dossier `/root/user/` est renommé "root/user/config.ini" quand il est copié dans le compartiment.

### Compartiments

Si le compartiment cible n'existe pas, il est créé. S'il existe, il doit être vide, sinon la copie ne peut pas se poursuivre.

### Système de fichiers

Les liens symboliques et les liens fixes sont ignorés durant le processus d'analyse.

### Configuration d'adresse IP
{: #ip_cfg}

L'écran LCD du périphérique peut être utilisé pour configurer les adresses IP pour les ports Ethernet. Vous naviguez sur cet écran en utilisant les boutons **flèche vers le haut**, **flèche vers le bas**, **échap** et **entrée**. Le bouton **entrée** affiche un menu et **échap** vous en fait sortir.

![Ecran LCD](/images/MDMSLCD.png)

Quand vous éditez une adresse IP ou un masque de sous-réseau, le bouton **entrée** vous fait avancer caractère par caractère ; **échap** vous fait reculer de la même façon. Les boutons **flèche vers le haut** et **flèche vers le bas** basculent entre les nombres de l'emplacement sélectionné.

Utilisez **échap** pour revenir au menu précédent.  

Revenez à l'élément de menu **Mettre à jour...** et appuyez sur **Entrée** pour sauvegarder les paramètres.
