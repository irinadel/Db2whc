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

# Umgebung mit privatem Netz
{: #priv_net_env}

## Bereitstellung
{: #deploy}

Sie können anfordern, dass Ihr {{site.data.keyword.dashdbshort_notm}}-Service in einer Umgebung mit Netzisolierung in {{site.data.keyword.Bluemix}} bereitgestellt wird. Wenden Sie sich an Ihren [{{site.data.keyword.IBM_notm}} Analytics-Vertriebsbeauftragten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window}.
{: shortdesc}

## Verbindung herstellen
{: #connecting}

In der folgenden Liste sind Methoden aufgeführt, die Sie verwenden können, um eine Verbindung zur privaten Netzumgebung im Rahmen des {{site.data.keyword.dashdbshort_notm}}-Flex-Plans herzustellen: 

* [Öffentliche IP-Adresse](#pub_ip)
* [{{site.data.keyword.cloud_notm}}-Serviceendpunkt](#serv_endpt)
* [{{site.data.keyword.cloud_notm}} Direct Link](#dl)
* [VPN](#vpn)
<!-- * [IP Whitelisting](#ip_wl) -->

### Öffentliche IP-Adresse 
{: #pub_ip}

Die Standardbereitstellungsmethode für den Flex-Plan ist der `öffentliche Modus` mit einer öffentlichen IP-Adresse. Die Verwendung einer öffentlichen IP-Adresse bedeutet, dass von jedem beliebigen Standort aus auf die öffentliche Netzumgebung zugegriffen werden kann. Es sind jedoch nur die für die Kommunikation mit der öffentlichen Netzumgebung erforderlichen Ports in unserer Firewall geöffnet. Der gesamte übrige Datenverkehr ist blockiert. 

Nach der Anmeldung bei {{site.data.keyword.cloud_notm}} wird Ihre Serviceinstanz angezeigt. Klicken Sie auf die Serviceinstanz und fügen Sie Ihre Berechtigungsnachweise hinzu; daraufhin erhalten Sie die Zugriffsdetails, die für den Zugriff auf die öffentliche {{site.data.keyword.dashdbshort_notm}}-Instanz erforderlich sind. 

### IBM Cloud-Serviceendpunkt
{: #serv_endpt}

Wenn Ihr gesamter Datenverkehr von der IaaS-Umgebung über die private SoftLayer-Backplane gesendet werden soll, kann mit dem Angebot **{{site.data.keyword.cloud_notm}}-Serviceendpunkt** diese Funktionalität bereitgestellt werden. Weitere Informationen zur Option des {{site.data.keyword.cloud_notm}}-Serviceendpunkts finden Sie in [Serviceendpunkt: Produktinformationen](/docs/services/service-endpoint/getting-started.html). 

Der Flex-Plan-Service muss mit **privater Konnektivität** bereitgestellt werden, damit der {{site.data.keyword.cloud_notm}}-Serviceendpunkt verwendet werden kann. Zum gegenwärtigen Zeitpunkt ist diese Option nur über eine SQO-Anforderung (Software Quote and Order, Softwareangebot und -bestellung) erhältlich.  

Wenn der Flex-Plan in diesem Modus bereitgestellt wird, besteht keinerlei öffentliche Konnektivität.
{: note} 

Nach der Bereitstellung einer Flex-Umgebung mit **privater Konnektivität** müssen Sie wie folgt vorgehen, um die Konnektivität von Ihrer IaaS-Umgebung zu Ihrer privaten Flex-Netzumgebung zu aktivieren:  

1. Lesen Sie die Informationen zum Einstieg in [Serviceendpunkt: Einführung](/docs/services/service-endpoint/enable-servicepoint.html). 

2. Richten Sie die Konnektivität zur IaaS-Umgebung ein, indem Sie entweder [{{site.data.keyword.cloud_notm}} Direct Link](#dl) oder [VPN](#vpn) verwenden. 

### IBM Cloud Direct Link
{: #dl}

Sie können eine Verbindung von Ihrer privaten Flex-Netzumgebung zu Ihrer IaaS-Umgebung über {{site.data.keyword.cloud_notm}} Direct Link herstellen. [{{site.data.keyword.cloud_notm}} Direct Link - Einführung](/docs/infrastructure/direct-link/getting-started.html) enthält weitere Informationen hierzu. 

### VPN
{: #vpn}

Sie können eine Verbindung von Ihrer privaten Flex-Netzumgebung zu Ihrer IaaS-Umgebung herstellen, indem Sie einen VPN-Tunnel (Virtual Private Network) für die öffentliche Konnektivität verwenden, falls eine Verbindungsmethode erforderlich ist, die über den sicheren SSL-Port `50001` hinaus geht. 

Wenn Sie eine VPN-Verbindung zur privaten Netzumgebung einrichten möchten, müssen Sie die VPN-Informationen an das für den Netzbetrieb zuständige IBM Cloud-Team senden. Füllen Sie hierzu ein VPN-Formular (kann beim IBM Support angefordert werden) aus und fügen Sie es an ein [ServiceNow-Ticket ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/unifiedsupport/cases/add){:new_window} an. <!-- , attaching the form to a [ServiceNow ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/unifiedsupport/cases/add){:new_window} ticket, and providing the following VPN part number `xxxx-xxxx-xxxx`. --> Anhand dieser Informationen kann das für den Netzbetrieb zuständige {{site.data.keyword.cloud_notm}}-Team dann den VPN-Endpunkt auf unserer Seite der Verbindung einrichten. <!-- Ben to provide VPN part number -->

Informationen zum Einstieg in die Verwendung eines VPN finden Sie in [Virtual Private Networking (VPN) - Einführung](/docs/infrastructure/iaas-vpn/getting-started.html). 

<!-- **Gopal's text**:

> For public connectivity, customers can setup a VPN tunnel if they need to use something over and beyond the secure SSL port of `50001` and send VPN information to our Networking team to set up VPN endpoints. This requires filling up a VPN form and attaching it to a Service Now Ticket. Should we attach the form template here? Customers need to order a particular part number for this (VPN part number to be provided by Ben)


Can we use any of this documentation?  [Getting started with Virtual Private Networking (VPN)](/docs/infrastructure/iaas-vpn/getting-started.html). -->



<!-- ### IP Whitelisting
{: #ip_wl}

IP whitelisting gives you the ability to specify which trusted IP addresses are granted access to your private network environment.


**Writer's notes**:
I need step-by-step instructions. -->


