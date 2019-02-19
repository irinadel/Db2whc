---

copyright:
  years: 2014, 2019
lastupdated: "2019-02-08"

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
{: #connect}

The following is a list of methods by which you can connect to your {{site.data.keyword.dashdbshort_notm}} Flex plan private network environment:

* [Public IP](#pub_ip)
* [IBM Cloud Service Endpoint](#serv_endpt)
* [IBM Cloud Direct Link](#dl)
* [VPN](#vpn)
* [IP Whitelisting](#ip_wl)

### Public IP 
{: #pub_ip}

The default deployment for the Flex plan is in `Public Mode` with a public IP address. The public IP address means that your private network environment can be accessed from anywhere in the world. However, only the ports that are needed for communication with the private network environment are opened at our firewall. All other traffic is blocked.




**Writer's notes**:
After getting their public IP address, what do customers do next? 

Step-by-step instructions?




### IBM Cloud Service Endpoint
{: #serv_endpt}

If you require that all of your traffic must be sent along the SoftLayer Private Backplane from your IaaS environment, an offering called **IBM Cloud Service Endpoint** provides this capability. For more information about the IBM Cloud Service Endpoint option, see [Service Endpoint: About](/docs/services/service-endpoint/getting-started.html).

The Flex plan service must be provisioned with **Private Connectivity** to use the IBM Cloud Service Endpoint. At this time, this option is obtained only by request through a software quote order (SQO). 

When your Flex plan is provisioned in this mode, there is no public connectivity at all.
{: note} 

After a Flex environment is provisioned with **Private Connectivity**, you must do the following to enable connectivity from your IaaS environment to your Flex private network environment: 

1. To get started, see [Service Endpoint: Getting Started](/docs/services/service-endpoint/enable-servicepoint.html)

   **Writer's notes**:
   Do we need more than the above link to "getting started" instructions?

2. Set up connectivity to your IaaS environment by using either [IBM Cloud Direct Link](#dl) or [VPN](#vpn).

### IBM Cloud Direct Link
{: #dl}

You can connect your Flex private network environment to your IaaS environment by using IBM Cloud Direct Link. See [Get Started with IBM Cloud Direct Link](/docs/infrastructure/direct-link/getting-started.html).

**Writer's notes**:
Do we need more than the above link to instructions to make the DL connection?

Should step-by-step instructions be copied here instead?



### VPN
{: #vpn}

You can connect your Flex private network environment to your IaaS environment by using a virtual private network (VPN) tunnel for public connectivity if you must have a connection method over and beyond the secure SSL port of `50001`.



**Gopal's text**:

> For public connectivity, customers can setup a VPN tunnel if they need to use something over and beyond the secure SSL port of `50001` and send VPN information to our Networking team to set up VPN endpoints. This requires filling up a VPN form and attaching it to a Service Now Ticket. Should we attach the form template here? Customers need to order a particular part number for this (VPN part number to be provided by Ben)

**Writer's notes**:
I need step-by-step instructions.

Can we use any of this documentation? --> [Getting started with Virtual Private Networking (VPN)](/docs/infrastructure/iaas-vpn/getting-started.html).



### IP Whitelisting
{: #ip_wl}

IP whitelisting gives you the ability to specify which trusted IP addresses are granted access to your private network environment.


**Writer's notes**:
I need step-by-step instructions.


