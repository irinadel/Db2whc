---

copyright:
  years: 2014, 2019
lastupdated: "2019-02-26"

keywords: private network, public IP, VPN, IBM Cloud Service Endpoint, IBM Cloud Direct Link, Flex

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

# Environnement réseau privé
{: #priv_net_env}

## Déploiement
{: #deploy}

Vous pouvez demander à ce que votre service {{site.data.keyword.dashdbshort_notm}} soit déployé dans un environnement isolé du réseau sur {{site.data.keyword.Bluemix}}. Contactez votre [interlocuteur {{site.data.keyword.IBM_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/connect/ibm/fr/fr/?lnk=fcw){:new_window}.
{: shortdesc}

## Connexion
{: #connecting}

La liste suivante indique les méthodes vous permettant de vous connecter à votre environnement réseau privé du plan {{site.data.keyword.dashdbshort_notm}} Flex : 

* [Adresse IP publique](#pub_ip)
* [{{site.data.keyword.cloud_notm}} Service Endpoint](#serv_endpt)
* [{{site.data.keyword.cloud_notm}} Direct Link](#dl)
* [Réseau privé virtuel](#vpn)
<!-- * [IP Whitelisting](#ip_wl) -->

### Adresse IP publique 
{: #pub_ip}

Le déploiement par défaut du plan Flex s'effectue en `mode public`, à l'aide d'une adresse IP publique. Cette adresse IP publique signifie que votre environnement réseau public est accessible de partout dans le monde. Toutefois, seuls les ports nécessaires à la communication avec l'environnement réseau public sont ouverts au niveau de notre pare-feu. Tout autre type de trafic est bloqué.

Une fois connecté à {{site.data.keyword.cloud_notm}}, vous verrez vos instances de service. Cliquez sur une instance de service, ajoutez vos données d'identification, et vous obtiendrez les détails nécessaires pour accéder à votre instance publique {{site.data.keyword.dashdbshort_notm}}.

### IBM Cloud Service Endpoint
{: #serv_endpt}

Si vous avez besoin que tout le trafic suive le circuit SoftLayer Private Backplane depuis votre environnement IaaS, une offre appelée **{{site.data.keyword.cloud_notm}} Service Endpoint** fournit cette fonction. Pour plus d'informations sur l'option {{site.data.keyword.cloud_notm}} Service Endpoint, voir [Service Endpoint : A propos](/docs/services/service-endpoint/getting-started.html).

Le service de plan Flex doit être mis à disposition avec **Private Connectivity** (connectivité privée) pour pouvoir utiliser l'option {{site.data.keyword.cloud_notm}} Service Endpoint. Actuellement, pour obtenir cette option, vous devez envoyer une demande via l'outil de devis et de commande de logiciels (SQO).  

Une fois votre plan Flex mis à disposition dans ce mode, il n'existe aucune connectivité publique.
{: note} 

Après qu'un environnement Flex a été mis à disposition avec **Private Connectivity**, vous devez procéder comme suit pour activer la connectivité depuis votre environnement IaaS vers votre environnement réseau privé Flex : 

1. Pour une initiation, voir [Service Endpoint : Initiation](/docs/services/service-endpoint/enable-servicepoint.html)

2. Configurez la connectivité sur votre environnement IaaS en utilisant [{{site.data.keyword.cloud_notm}} Direct Link](#dl) ou [VPN](#vpn).

### IBM Cloud Direct Link
{: #dl}

Vous pouvez connecter votre environnement réseau privé Flex à votre environnement IaaS en utilisant {{site.data.keyword.cloud_notm}} Direct Link. Voir [Initiation à {{site.data.keyword.cloud_notm}} Direct Link](/docs/infrastructure/direct-link/getting-started.html).

### Réseau privé virtuel (VPN)
{: #vpn}

Vous pouvez connecter votre environnement réseau privé Flex à votre environnement IaaS en utilisant un tunnel VPN (réseau privé virtuel) pour la connectivité publique si vous devez disposer d'une méthode de connexion via et au-delà du port SSL sécurisé `50001`.

Pour établir une connexion VPN à votre environnement réseau privé, vous devez envoyer vos informations VPN à notre équipe réseau IBM Cloud en remplissant un formulaire VPN (formulaire de demande de support IBM) et en joignant le formulaire à un ticket [ServiceNow ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/unifiedsupport/cases/add){:new_window}. <!-- , attaching the form to a [ServiceNow ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/unifiedsupport/cases/add){:new_window} ticket, and providing the following VPN part number `xxxx-xxxx-xxxx`. --> Munie de ces informations, notre équipe réseau {{site.data.keyword.cloud_notm}} peut alors configurer notre extrémité du noeud final VPN. <!-- Ben to provide VPN part number -->

Pour des informations sur la mise en route d'un réseau privé virtuel, voir [Initiation au VPN (réseau privé virtuel)](/docs/infrastructure/iaas-vpn/getting-started.html).

<!-- **Gopal's text**:

> For public connectivity, customers can setup a VPN tunnel if they need to use something over and beyond the secure SSL port of `50001` and send VPN information to our Networking team to set up VPN endpoints. This requires filling up a VPN form and attaching it to a Service Now Ticket. Should we attach the form template here? Customers need to order a particular part number for this (VPN part number to be provided by Ben)


Can we use any of this documentation?  [Getting started with Virtual Private Networking (VPN)](/docs/infrastructure/iaas-vpn/getting-started.html). -->



<!-- ### IP Whitelisting
{: #ip_wl}

IP whitelisting gives you the ability to specify which trusted IP addresses are granted access to your private network environment.


**Writer's notes**:
I need step-by-step instructions. -->


