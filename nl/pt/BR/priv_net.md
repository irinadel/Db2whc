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

# Ambiente de rede privada
{: #priv_net_env}

## Implementando
{: #deploy}

É possível solicitar que o serviço do {{site.data.keyword.dashdbshort_notm}} seja implementado em um ambiente isolado por
rede no {{site.data.keyword.Bluemix}}. Entre em contato com o [representante de vendas do {{site.data.keyword.IBM_notm}} Analytics ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window}.
{: shortdesc}

## Conectando
{: #connecting}

A seguir está uma lista de métodos pelos quais é possível se conectar ao seu ambiente de rede privada do plano Flex do {{site.data.keyword.dashdbshort_notm}}:

* [IP público](#pub_ip)
* [{{site.data.keyword.cloud_notm}} Service Endpoint](#serv_endpt)
* [{{site.data.keyword.cloud_notm}} Direct Link](#dl)
* [VPN](#vpn)
<!-- * [IP Whitelisting](#ip_wl) -->

### IP Público 
{: #pub_ip}

A implementação padrão para o plano Flex está no `Modo público` com um endereço IP público. O endereço IP público significa que seu ambiente de rede pública pode ser acessado de qualquer lugar no mundo. Entretanto, somente as portas que são necessárias para comunicação com o ambiente de rede pública são abertas em nosso firewall. Todos os outros tráfegos são bloqueados.

Após efetuar login no {{site.data.keyword.cloud_notm}}, você verá sua instância de serviço. Clique na instância de serviço e inclua suas credenciais para obter os detalhes de acesso necessários para acessar sua Instância pública do {{site.data.keyword.dashdbshort_notm}}.

### IBM Cloud Service Endpoint
{: #serv_endpt}

Se for preciso que todo o seu tráfego seja enviado junto com o SoftLayer Private Backplane por meio do seu ambiente IaaS, uma oferta chamada **{{site.data.keyword.cloud_notm}} Service Endpoint** fornecerá esse recurso. Para obter mais informações sobre a opção do {{site.data.keyword.cloud_notm}} Service Endpoint, consulte [Sobre o Service Endpoint](/docs/services/service-endpoint/getting-started.html).

O serviço de plano Flex deve ser provisionado com a **Conectividade privada** para usar o {{site.data.keyword.cloud_notm}} Service Endpoint. Neste momento, essa opção é obtida somente por solicitação por meio de uma Software Quote Order (SQO). 

Quando seu plano Flex é provisionado nesse modo, não há conectividade pública.
{: note} 

Após um ambiente Flex ser provisionado com **Conectividade privada**, deve-se fazer o seguinte para ativar a conectividade por meio de seu ambiente IaaS para seu ambiente de rede privada Flex: 

1. Para iniciar, consulte [Service Endpoint: introdução](/docs/services/service-endpoint/enable-servicepoint.html)

2. Configure a conectividade com seu ambiente IaaS usando o [{{site.data.keyword.cloud_notm}} Direct Link](#dl) ou a [VPN](#vpn).

### IBM Cloud Direct Link
{: #dl}

É possível conectar seu ambiente de rede privada Flex ao seu ambiente IaaS usando o {{site.data.keyword.cloud_notm}} Direct Link. Consulte [Introdução ao {{site.data.keyword.cloud_notm}} Direct Link](/docs/infrastructure/direct-link/getting-started.html).

### VPN
{: #vpn}

É possível conectar seu ambiente de rede privada Flex ao seu ambiente IaaS usando um túnel de rede privada virtual (VPN) para conectividade pública quando é necessário ter um método de conexão além da porta SSL segura de `50001`.

Para estabelecer uma conexão VPN com seu ambiente de rede privada, deve-se enviar suas informações de VPN a nossa equipe de rede do IBM Cloud preenchendo um formulário de VPN (formulário de solicitação do Suporte IBM) e anexar o formulário a um chamado [ServiceNow ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/unifiedsupport/cases/add){:new_window}. <!-- , attaching the form to a [ServiceNow ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/unifiedsupport/cases/add){:new_window} ticket, and providing the following VPN part number `xxxx-xxxx-xxxx`. --> Com essas informações em mãos, nossa equipe de rede do {{site.data.keyword.cloud_notm}} pode configurar nossa extremidade do terminal VPN. <!-- Ben to provide VPN part number -->

Para obter informações sobre como iniciar com uma VPN, consulte [Introdução a Virtual Private Networking (VPN)](/docs/infrastructure/iaas-vpn/getting-started.html).

<!-- **Gopal's text**:

> For public connectivity, customers can setup a VPN tunnel if they need to use something over and beyond the secure SSL port of `50001` and send VPN information to our Networking team to set up VPN endpoints. This requires filling up a VPN form and attaching it to a Service Now Ticket. Should we attach the form template here? Customers need to order a particular part number for this (VPN part number to be provided by Ben)


Can we use any of this documentation?  [Getting started with Virtual Private Networking (VPN)](/docs/infrastructure/iaas-vpn/getting-started.html). -->



<!-- ### IP Whitelisting
{: #ip_wl}

IP whitelisting gives you the ability to specify which trusted IP addresses are granted access to your private network environment.


**Writer's notes**:
I need step-by-step instructions. -->


