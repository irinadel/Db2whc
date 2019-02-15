---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# Detalhes do banco de dados e credenciais de
{: #db_details_cxn_creds}

Para configurar seu ambiente de desenvolvimento local e para conectar aplicativos e ferramentas ao banco de dados {{site.data.keyword.dashdbshort_notm}}, é necessário saber os detalhes do banco de dados e as credenciais de conexão.
{: shortdesc}

## Detalhes do banco de
{: #db_details}

Há detalhes importantes do banco de dados necessários para conectar aplicativos e ferramentas ao banco de dados:

- *Nome do host* - O nome do host do servidor.
- *Número da porta* - Usado pelo gerenciador do banco de dados para comunicação TCP/IP. (Observe que seu serviço é provisionado com um número de porta para conexões que usam Secure Socket Layer (SSL) e uma porta diferente para conexão não SSL.)

   Se necessário, será possível obter o endereço IP de seu servidor usando o comando ping ou o comando nslookup, especificando o nome do host.
- *Nome do banco de dados* - O nome do banco de dados Db2, geralmente BLUDB.

## Credenciais de conexão
{: #cxn_creds}

Há três tipos de credenciais:

- *IBMid* - Se você usar o {{site.data.keyword.Bluemix_notm}}, este será o ID usado para efetuar login no {{site.data.keyword.Bluemix_notm}}. Ele não é o que você usa para conectar aplicativos ou ferramentas ao banco de dados Db2 Warehouse on Cloud.
- *Credenciais do banco de dados Db2* - Seu serviço é provisionados com um ID de usuário e uma senha do banco de dados que podem ser usados para conectar aplicativos e ferramentas ao banco de dados.
- *Usuários criados pelo administrador* - Alguns planos do {{site.data.keyword.dashdbshort_notm}} permitem que usuários administrativos criem novos usuários. Esses IDs de usuário e senhas criados pelo administrador podem ser usados para se registrar diretamente na URL do console da web e para se conectar ao banco de dados Db2 por meio de aplicativos ou ferramentas.

## Onde localizar detalhes do banco de dados e credenciais de conexão
{: #location}

É possível coletar essas informações nos locais a seguir:

- *Seu administrador* - Se você não for o proprietário ou o administrador da instância do Db2, será possível obter os detalhes do banco de dados e credenciais de conexão do seu administrador.
- *Console da web do Db2* - Detalhes do banco de dados e credenciais estão disponíveis no console da web.
- Se você estiver usando o  {{site.data.keyword.Bluemix_notm}}: 
   
   - *Painel do {{site.data.keyword.Bluemix_notm}}* - Ao visualizar seu serviço no painel do {{site.data.keyword.Bluemix_notm}}, na área "Credenciais de serviço", é possível visualizar os detalhes do banco de dados, bem como o ID do usuário e a senha do banco de dados.
   - *`VCAP_SERVICES`* - `VCAP_SERVICES` é uma variável de ambiente no {{site.data.keyword.Bluemix_notm}} que contém detalhes do banco de dados e credenciais no formato JSON. Ao visualizar as credenciais de serviço para seu serviço no painel do {{site.data.keyword.Bluemix_notm}}, o conteúdo de `VCAP_SERVICES` é o que é exibido. Ao ligar outros serviços ou apps {{site.data.keyword.Bluemix_notm}} a seu serviço, eles podem acessar detalhes do banco de dados e credenciais programaticamente, lendo `VCAP_SERVICES`.
