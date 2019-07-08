---

copyright:
  years: 2014, 2019
lastupdated: "2019-04-01"

keywords:

subcollection: Db2whc

---

<!-- Attribute definitions --> 
{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}

# Opções de conectividade
{: #connect_options}

O {{site.data.keyword.dashdblong}} oferece várias opções de conectividade segura, dependendo dos seus requisitos de conexão de aplicativo.  
{: shortdesc}

## Conectando-se a um terminal público (opção padrão)
{: #pub_endpt}

Como com qualquer serviço de nuvem pública, é possível conectar seu aplicativo por meio de um nome de host público que é fornecido a você no momento em que seu serviço é provisionado. O acesso aos seus dados é protegido por autenticação forte, vastas opções de autorização e controles de acesso do Db2, criptografia por ligação e em repouso e práticas de segurança e conformidade da IBM para desenvolvimento e operações. A lista de aplicativos confiáveis de IP opcional é oferecida. Crie um caso de Suporte IBM se desejar ativar a lista de aplicativos confiáveis de IP.

### Como conectar-se a um terminal público:
{: #pub_endpt_steps}

A maneira mais fácil de se conectar ao data warehouse é por meio do nome do host público que foi fornecido em sua carta de boas-vindas. Também é possível obter o nome do host e as credenciais da maneira a seguir:

1. Efetue login no {{site.data.keyword.cloud_notm}} e clique em sua instância de serviço.
2. Clique em **Credenciais de serviço**.
3. Clique em **Nova credencial** e, em seguida, clique em **Incluir**.
4. Após as credenciais serem criadas, na coluna `Actions`, clique em **Visualizar credenciais**.
5. No documento JSON de exemplo a seguir, anote o conteúdo dos campos nome do host, senha e nome do usuário. Você usa esses três componentes para fazer a conexão de terminal público:

   ```
   {
     "hostname": "db2whoc-flex-xxxxxxx.services.dal.bluemix.net",
     "password": "DTPY7KXxhp_pKtjLSt",
     "https_url": "https://db2whoc-flex-xxxxxxx.services.dal.bluemix.net",
     "port": 50000,
     "ssldsn": "DATABASE=BLUDB;HOSTNAME=db2whoc-flex-xxxxxx.services.dal.bluemix.net;PORT=50001;PROTOCOL=TCPIP;UID=bluadmin;PWD=DTPY7KXWxhp_pKtjLSt;Security=SSL;",
     "host": "db2whoc-flex-xxxxx.services.dal.bluemix.net",
     "jdbcurl": "jdbc:db2://db2whoc-flex-xxxx.services.dal.bluemix.net:50000/BLUDB",
     "uri": "db2://bluadmin:DTPY7KXx1p_pKtjLSt@db2whoc-flex-hyftpsb.services.dal.bluemix.net:50000/BLUDB",
     "db": "BLUDB",
     "dsn": "DATABASE=BLUDB;HOSTNAME=db2whoc-flex-xxxxx.services.dal.bluemix.net;PORT=50000;PROTOCOL=TCPIP;UID=bluadmin;PWD=DTPYZunlWxhp_pKtjLSt;",
     "username": "bluadmin",
     "ssljdbcurl": "jdbc:db2://db2whoc-flex-xxxx.services.dal.bluemix.net:50001/BLUDB:sslConnection=true;"
   }

   ```

   ![Acesso de rede pública ao {{site.data.keyword.cloud_notm}}](images/public_connection.png "Representação gráfica da conexão do usuário com a nuvem")

## Conectando-se a um terminal privado: IBM Cloud Service Endpoint
{: #priv_endpt}

Se você tiver um aplicativo implementado em sua conta do {{site.data.keyword.cloud_notm}} e desejar conectá-lo a seu banco de dados sem que o tráfego do banco de dados flua sobre quaisquer redes públicas, será possível usar a opção **{{site.data.keyword.cloud_notm}} Service Endpoint** ao solicitar seu banco de dados. Você receberá um nome de host privado no momento em que o serviço for provisionado e será possível conectar-se apenas a ele de dentro de sua conta do {{site.data.keyword.cloud_notm}}.  

Para saber mais sobre a opção {{site.data.keyword.cloud_notm}} Service Endpoint, consulte [Service Endpoint: Sobre](/docs/services/service-endpoint?topic=service-endpoint-about#about).


### Como conectar-se a um terminal privado com o IBM Cloud Service Endpoint
{: #priv_endpt_steps}

A comunicação entre rede privada e terminal acontece por meio do serviço {{site.data.keyword.cloud_notm}} Service Endpoint. O serviço Service Endpoint facilita a rota rápida e segura do tráfego de rede entre diferentes serviços do {{site.data.keyword.cloud_notm}} e seu banco de dados de warehouse por meio do painel traseiro de rede privada do {{site.data.keyword.cloud_notm}}. Esse roteamento de rede assegura que seus dados nunca sejam direcionados para a Internet pública. 

Para iniciar o Service Endpoint, sua conta do {{site.data.keyword.cloud_notm}} deve ser ativada para roteamento virtual e encaminhamento (VRF). Para que sua conta seja ativada, consulte [Ativando sua conta para usar o Service Endpoint usando a CLI do IBM Cloud](/docs/services/service-endpoint?topic=service-endpoint-getting-started#cs_cli_install_steps).

Após a sua conta ser ativada por VRF e o Service Endpoint estiver ativado, siga as instruções que foram fornecidas em sua carta de boas-vindas.

Agora, é hora de se conectar à sua instância do {{site.data.keyword.dashdbshort_notm}} de dentro da sua conta do {{site.data.keyword.cloud_notm}} por meio do endereço de rede privada que foi fornecido em sua carta de boas-vindas.

## Conectando-se a um terminal privado: rede privada virtual (VPN)
{: #vpn}

Se você tiver um aplicativo implementado em uma rede privada que esteja fora do {{site.data.keyword.cloud_notm}} sem acesso à Internet pública e quiser conectá-lo ao banco de dados por meio de uma conexão de rede privada virtual (VPN), será possível fazer a solicitação no momento em que você solicita o serviço ou abrindo um caso de Suporte IBM. Os engenheiros de rede da IBM ajudarão seus engenheiros de rede a configurar o túnel VPN entre a sua rede privada e o {{site.data.keyword.cloud_notm}}.

### Como conectar-se a um terminal privado com uma VPN
{: #priv_endpt_vpn_steps}

Para estabelecer uma conexão VPN com seu data warehouse de nuvem atrás de um terminal
público, [crie um caso de suporte do {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/unifiedsupport/cases/add){:external} que inclua
os detalhes a seguir:

* **Tipo de suporte**: técnico 
* **Categoria**: bancos de dados 
* **Oferta**: selecione sua instância do {{site.data.keyword.dashdbshort_notm}} 
* **Assunto**: solicitação de conexão VPN 
* **Descrição**: forneça as informações necessárias a seguir
  * **Endereço do peer da VPN do lado do cliente** (seu terminal da VPN): `<IP Address>`
  * **Domínio de criptografia do lado do cliente** (ser específico no que é necessário – 10.0.0.0/8 é não funcional porque 10 endereçamentos também são usados no {{site.data.keyword.cloud_notm}} para serviços de back-end): `<Domain>`
  * **Hardware e Versão de VPN do lado do cliente**: `<Hardware and Version number>`
  * **Contato da VPN do lado do cliente** (nome e endereço de e-mail do contato técnico): 
    * `<Name>` 
    * `<Title>` 
    * `<Email Address>`

  **Opcional** (mude somente se os valores padrão a seguir não forem adequados):

  *Parâmetros do IKE/ISAKMP (Fase I)*

  * **Método de criptografia**: IKEv1
  * **Criptografia de IKE / Algoritmo de criptografia**: AES-256
  * **Algoritmo de autenticação**: SHA1
  * **Grupo DH**: grupo 5
  * **Security Association Lifetime (segundos)**: 1d (86.400 segundos)

  *Parâmetros do IPSEC (Fase II)*

  * **Criptografia de IPsec / Algoritmo de criptografia**: AES-256
  * **Algoritmo de autenticação**: SHA1
  * **Grupo DH** (se estiver usando o PF-Secrecy): grupo 5
  * **Security Association Lifetime (segundos)**: 3.600 segundos

Após o recebimento de sua solicitação, os técnicos do {{site.data.keyword.cloud_notm}} abrirão as portas de firewall apropriadas e a lista de desbloqueio do endereço IP fornecido. A comunicação e a resolução para a solicitação serão feitas por meio do chamado de caso do Suporte {{site.data.keyword.cloud_notm}}.

![Acesso de rede pública ao {{site.data.keyword.cloud_notm}} por meio de uma VPN](images/public_connection_vpn.png "Representação gráfica da conexão do usuário com a nuvem")
