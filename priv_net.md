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

# Private network environment
{: #priv_net_env}

## Deploying
{: #deploy}

You can request to have your {{site.data.keyword.dashdbshort_notm}} service deployed in a network-isolated environment on the {{site.data.keyword.Bluemix}}. Contact your [{{site.data.keyword.IBM_notm}} Analytics Sales representative ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window}.
{: shortdesc}

## Connecting
{: #connecting}

The following is a list of methods by which you can connect to your {{site.data.keyword.dashdbshort_notm}} Flex plan private network environment:

* [Public IP](#pub_ip)
* [{{site.data.keyword.cloud_notm}} Service Endpoint](#serv_endpt)
* [{{site.data.keyword.cloud_notm}} Direct Link](#dl)
* [VPN](#vpn)
<!-- * [IP Whitelisting](#ip_wl) -->

### Public IP 
{: #pub_ip}

The default deployment for the Flex plan is in `Public Mode` with a public IP address. The public IP address means that your public network environment can be accessed from anywhere in the world. However, only the ports that are needed for communication with the public network environment are opened at our firewall. All other traffic is blocked.

After logging in to {{site.data.keyword.cloud_notm}}, you'll see your service instance. Click on the service instance, add your credentials, and you'll get the access details that are required to access your {{site.data.keyword.dashdbshort_notm}} Public Instance.

### IBM Cloud Service Endpoint
{: #serv_endpt}

If you require that all of your traffic must be sent along the {{site.data.keyword.cloud_notm}} Private Backplane from your IaaS environment, an offering called **{{site.data.keyword.cloud_notm}} Service Endpoint** provides this capability. For more information about the {{site.data.keyword.cloud_notm}} Service Endpoint option, see [Service Endpoint: About](/docs/services/service-endpoint/getting-started.html).

The Flex plan service must be provisioned with **Private Connectivity** to use the {{site.data.keyword.cloud_notm}} Service Endpoint. At this time, this option is obtained only by request through a software quote order (SQO). 

When your Flex plan is provisioned in this mode, there is no public connectivity at all.
{: note} 

After a Flex environment is provisioned with **Private Connectivity**, you must do the following to enable connectivity from your IaaS environment to your Flex private network environment: 

1. To get started, see [Service Endpoint: Getting Started](/docs/services/service-endpoint/enable-servicepoint.html)

2. Set up connectivity to your IaaS environment by using either [{{site.data.keyword.cloud_notm}} Direct Link](#dl) or [VPN](#vpn).

### IBM Cloud Direct Link
{: #dl}

You can connect your Flex private network environment to your IaaS environment by using {{site.data.keyword.cloud_notm}} Direct Link. See [Get Started with {{site.data.keyword.cloud_notm}} Direct Link](/docs/infrastructure/direct-link/getting-started.html).

### VPN
{: #vpn}

You can connect your Flex private network environment to your IaaS environment by using a virtual private network (VPN) tunnel for public connectivity if you must have a connection method over and beyond the secure SSL port of `50001`.

To establish a VPN connection to your private network environment, you must send your VPN information to our IBM Cloud networking team by filling out a VPN form (request form from IBM Support), attaching the form to a [ServiceNow ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/unifiedsupport/cases/add){:new_window} ticket, and providing the following ICIAE VPN part number `D1Q35LLVPN`. With that information in hand, our {{site.data.keyword.cloud_notm}} networking team can then set up our end of the VPN endpoint. 

For information about getting started with a VPN, see [Getting started with Virtual Private Networking (VPN)](/docs/infrastructure/iaas-vpn/getting-started.html).

<!-- ### IP Whitelisting
{: #ip_wl}

IP whitelisting gives you the ability to specify which trusted IP addresses are granted access to your private network environment.


**Writer's notes**:
I need step-by-step instructions. -->


