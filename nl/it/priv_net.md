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

# Ambiente di rete privata
{: #priv_net_env}

## Distribuzione
{: #deploy}

Puoi richiedere che venga distribuito il tuo servizio {{site.data.keyword.dashdbshort_notm}} in un ambiente isolato dalla rete in {{site.data.keyword.Bluemix}}. Contatta il tuo [rappresentante delle vendite di {{site.data.keyword.IBM_notm}} Analytics ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window}.
{: shortdesc}

## Collegamento
{: #connecting}

Il seguente è un elenco di metodi con cui puoi connetterti al tuo ambiente di rete privato del piano {{site.data.keyword.dashdbshort_notm}} Flex:

* [IP pubblico](#pub_ip)
* [Endpoint servizio {{site.data.keyword.cloud_notm}} ](#serv_endpt)
* [{{site.data.keyword.cloud_notm}} Direct Link](#dl)
* [VPN](#vpn)
<!-- * [IP Whitelisting](#ip_wl) -->

### IP pubblico 
{: #pub_ip}

La distribuzione predefinita per il piano Flex è in modalità pubblica (`Public Mode`) con un indirizzo IP. L'indirizzo IP pubblico indica che è possibile accedere al tuo ambiente di rete pubblico da qualsiasi parte del mondo. Tuttavia, solo le porte necessarie per la comunicazione con l'ambiente di rete pubblico vengono aperte al nostro firewall. Tutte l'altro traffico è bloccato.

Dopo aver eseguito l'accesso a {{site.data.keyword.cloud_notm}}, visualizzerai la tua istanza del servizio. Fai clic sull'istanza del servizio, aggiungi le tue credenziali e riceverai i dettagli di accesso necessari per accedere alla tua istanza pubblica {{site.data.keyword.dashdbshort_notm}}.

### Endpoint servizio IBM Cloud
{: #serv_endpt}

Se hai bisogno che tutto il tuo traffico venga inviato insieme al Backplane privato SoftLayer dal tuo ambiente IaaS, un'offerta denominata **Endpoint servizio {{site.data.keyword.cloud_notm}}** fornisce questa funzionalità. Per ulteriori informazioni sull'opzione dell'endpoint del servizio {{site.data.keyword.cloud_notm}}, consulta [Endpoint servizio: informazioni](/docs/services/service-endpoint/getting-started.html).

Deve essere eseguito il provisioning del servizio del piano Flex con **Private Connectivity** per utilizzare l'endpoint del servizio {{site.data.keyword.cloud_notm}}. In questo momento, questa opzione può essere ottenuta soltanto richiedendola tramite un ordine della quota software (SQO). 

Dopo avere eseguito il provisioning del piano Flex in questa modalità, non c'è alcuna connettività pubblica.
{: note} 

Dopo aver eseguito il provisioning di un ambiente Flex con la connettività privata (**Private Connectivity**), devi effettuare le seguenti operazioni per abilitare la connettività dal tuo ambiente IaaS al tuo ambiente di rete privato Flex: 

1. Per iniziare, consulta [Endpoint servizio: introduzione](/docs/services/service-endpoint/enable-servicepoint.html)

2. Configura la connettività al tuo ambiente IaaS utilizzando [{{site.data.keyword.cloud_notm}} Direct Link](#dl) o la [VPN](#vpn).

### IBM Cloud Direct Link
{: #dl}

Puoi connettere il tuo ambiente di rete privato Flex al tuo ambiente IaaS utilizzando {{site.data.keyword.cloud_notm}} Direct Link. Consulta [Introduzione a {{site.data.keyword.cloud_notm}} Direct Link](/docs/infrastructure/direct-link/getting-started.html).

### VPN
{: #vpn}

Puoi connettere il tuo ambiente di rete privato Flex al tuo ambiente IaaS utilizzando un tunnel VPN (Virtual Private Network) per la connettività pubblica se devi avere un metodo di connessione oltre alla porta SSL protetta di `50001`.

Per stabilire una connessione VPN al tuo ambiente di rete privato, devi inviare le tue informazioni sulla VPN al nostro team di rete IBM Cloud compilando un modulo VPN (modulo di richiesta dal supporto IBM) e allegando il modulo a un ticket [ServiceNow ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/unifiedsupport/cases/add){:new_window}. <!-- , attaching the form to a [ServiceNow ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/unifiedsupport/cases/add){:new_window} ticket, and providing the following VPN part number `xxxx-xxxx-xxxx`. --> Con tutte le informazioni necessarie, il nostro team di rete {{site.data.keyword.cloud_notm}} può configurare il nostro lato dell'endpoint VPN. <!-- Ben to provide VPN part number -->

Per informazioni introduttive a una VPN, consulta [Introduzione alla VPN (Virtual Private Networking)](/docs/infrastructure/iaas-vpn/getting-started.html).

<!-- **Gopal's text**:

> For public connectivity, customers can setup a VPN tunnel if they need to use something over and beyond the secure SSL port of `50001` and send VPN information to our Networking team to set up VPN endpoints. This requires filling up a VPN form and attaching it to a Service Now Ticket. Should we attach the form template here? Customers need to order a particular part number for this (VPN part number to be provided by Ben)


Can we use any of this documentation?  [Getting started with Virtual Private Networking (VPN)](/docs/infrastructure/iaas-vpn/getting-started.html). -->



<!-- ### IP Whitelisting
{: #ip_wl}

IP whitelisting gives you the ability to specify which trusted IP addresses are granted access to your private network environment.


**Writer's notes**:
I need step-by-step instructions. -->


