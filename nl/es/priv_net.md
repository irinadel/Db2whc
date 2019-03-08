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

# Entorno de red privada
{: #priv_net_env}

## Despliegue
{: #deploy}

Puede solicitar que se despliegue su servicio de {{site.data.keyword.dashdbshort_notm}} en un entorno con aislamiento de red en {{site.data.keyword.Bluemix}}. Póngase en contacto con el [representante de ventas de {{site.data.keyword.IBM_notm}} Analytics ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window}.
{: shortdesc}

## Conectando
{: #connecting}

La siguiente es una lista de métodos por los que puede conectarse a su entorno de red privada {{site.data.keyword.dashdbshort_notm}} Flex plan:

* [IP pública](#pub_ip)
* [Punto final de servicio de {{site.data.keyword.cloud_notm}}](#serv_endpt)
* [{{site.data.keyword.cloud_notm}} Direct Link](#dl)
* [VPN](#vpn)
<!-- * [IP Whitelisting](#ip_wl) -->

### IP pública 
{: #pub_ip}

El despliegue predeterminado del plan Flex es en `Modalidad pública` con una dirección IP pública. La dirección IP pública significa que se puede acceder a su entorno de red pública desde cualquier parte del mundo. Sin embargo, en nuestro cortafuegos sólo se abren los puertos necesarios para la comunicación con el entorno de red pública. El resto del tráfico está bloqueado.

Después de iniciar sesión en {{site.data.keyword.cloud_notm}}, verá su instancia de servicio. Pulse la instancia de servicio, añada sus credenciales y obtendrá los datos de acceso necesarios para acceder a su {{site.data.keyword.dashdbshort_notm}} Instancia pública.

### Punto final de servicio de IBM Cloud
{: #serv_endpt}

Si necesita que todo su tráfico sea enviado a lo largo del Backplane Privado SoftLayer desde su entorno IaaS, una oferta llamada **{{site.data.keyword.cloud_notm}} Punto final de servicio** proporciona esta capacidad. Para obtener más información sobre la opción {{site.data.keyword.cloud_notm}} Punto final de servicio, consulte [Punto final de servicio: Acerca de](/docs/services/service-endpoint/getting-started.html).

El servicio del plan Flex se debe proporcionar con **Conectividad privada** para utilizar el {{site.data.keyword.cloud_notm}} Punto final de servicio. En este momento, esta opción se obtiene sólo por solicitud a través de un pedido de presupuesto de software (SQO). 

Cuando su plan Flex se aprovisiona en esta modalidad, no hay conectividad pública en absoluto.
{: note} 

Después de que un entorno de Flex se aprovisione con **Conectividad privada**, debe hacer lo siguiente para habilitar la conectividad desde su entorno IaaS a su entorno de red privada de Flex: 

1. Para empezar, consulte [Punto final de servicio: Iniciación](/docs/services/service-endpoint/enable-servicepoint.html)

2. Configure la conectividad con su entorno IaaS utilizando [{{site.data.keyword.cloud_notm}} Direct Link](#dl) o [VPN](#vpn).

### IBM Cloud Direct Link
{: #dl}

Puede conectar su entorno de red privada de Flex a su entorno IaaS utilizando {{site.data.keyword.cloud_notm}} Direct Link. Consulte [Iniciación a {{site.data.keyword.cloud_notm}} Direct Link](/docs/infrastructure/direct-link/getting-started.html).

### VPN
{: #vpn}

Puede conectar su entorno de red privada de Flex a su entorno IaaS mediante un túnel de red privada virtual (VPN) para la conectividad pública si necesita un método de conexión más allá del puerto SSL seguro de `50001`.

Para establecer una conexión VPN a su entorno de red privada, debe enviar su información VPN a nuestro equipo de redes IBM Cloud rellenando un formulario VPN (formulario de solicitud de soporte de IBM) y adjuntando el formulario a una incidencia [ServiceNow ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace")](https://cloud.ibm.com/unifiedsupport/cases/add){:new_window}. <!-- , attaching the form to a [ServiceNow ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/unifiedsupport/cases/add){:new_window} ticket, and providing the following VPN part number `xxxx-xxxx-xxxx`. --> Con esa información en mano, nuestro equipo de networking {{site.data.keyword.cloud_notm}} puede entonces configurar nuestra VPN de punto final. <!-- Ben to provide VPN part number -->

Para obtener información sobre cómo empezar a utilizar una VPN, consulte [Iniciar una red privada virtual (VPN).](/docs/infrastructure/iaas-vpn/getting-started.html).

<!-- **Gopal's text**:

> For public connectivity, customers can setup a VPN tunnel if they need to use something over and beyond the secure SSL port of `50001` and send VPN information to our Networking team to set up VPN endpoints. This requires filling up a VPN form and attaching it to a Service Now Ticket. Should we attach the form template here? Customers need to order a particular part number for this (VPN part number to be provided by Ben)


Can we use any of this documentation?  [Getting started with Virtual Private Networking (VPN)](/docs/infrastructure/iaas-vpn/getting-started.html). -->



<!-- ### IP Whitelisting
{: #ip_wl}

IP whitelisting gives you the ability to specify which trusted IP addresses are granted access to your private network environment.


**Writer's notes**:
I need step-by-step instructions. -->


