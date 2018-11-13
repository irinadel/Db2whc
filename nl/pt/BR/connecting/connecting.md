---

copyright:
  years: 2014, 2018
lastupdated: "2018-10-15"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Visão Geral de Conexão
{: #overview}

É possível conectar interfaces de linha de comandos, aplicativos e ferramentas IBM® ou de terceiros ou apps que você cria ao banco de dados {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

## Pré-requisitos
{: #prereqs}

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os pré-requisitos necessários. 

- Coletar Detalhes do Banco de Dados e Credenciais

   Para se conectar ao banco de dados, é necessário obter detalhes do banco de dados (como o nome do host), bem como credenciais (como um ID do usuário e uma senha.) É possível coletar essas informações de conexão por meio do console da web do {{site.data.keyword.dashdbshort_notm}}.

- Verifique se há um driver suportado instalado

   - Se o aplicativo ou a ferramenta já contiver o Db2 v11.1 IBM Data Server Driver Package, será possível conectar o aplicativo ou a ferramenta ao banco de dados {{site.data.keyword.dashdbshort_notm}} usando esse driver.
   - Caso contrário, instale o pacote de drivers do Db2, que pode ser transferido por download por meio do console da web do {{site.data.keyword.dashdbshort_notm}}.

- Configure seu ambiente

  - Inclua entradas no arquivo de configuração do driver, `db2dsdriver.cfg`, para o seu banco de dados.
  - SSL (Secure Sockets Layer)

    É possível optar pela conexão com ou sem SSL. Detalhes da conexão, como a porta a ser utilizada e a sequência de conexões, dependem do uso ou não de conexões SSL.

    Para usar conexões SSL, é necessário um certificado de autoridade de certificação:
    - Se você usar o pacote de drivers mais recente do {{site.data.keyword.dashdbshort_notm}}, o arquivo de certificado será empacotado com o pacote e será usado para conexões.
    - Se você usar o IBM Data Server Driver Package, será possível fazer download do certificado SSL por meio do console da web do {{site.data.keyword.dashdbshort_notm}}.

- Confirme que as portas estão disponíveis

   Se a sua rede estiver protegida por um firewall, confirme que as comunicações serão permitidas no número de porta `50000` para protocolos padrão ou no número de porta `50001` para conexões SSL.

<!-- Before you can connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you completed downloading and installing the necessary components on the prerequisites checklist: 

- [Prerequisites checklist](prereqs.html) -->

### Coletando informações de conexão
{: #collect_info}

- [ Detalhes do banco de dados e credenciais de conexão ](credentials.html)

### Fazendo download e instalando o pacote do driver
{: #dl_install}

- [ Fazer download do pacote do driver ](driver_pkg.html)
- [ Instalando no Linux ou PowerLinux ](install_linux.html)
- [ Instalando no Mac OS X ](install_mac.html)
- [ Instalando no Windows ](install_win.html)

### Configurando o seu ambiente
{: #cfg_env}

- [Configurando o seu ambiente](driver_pkg_cfg.html)
- [ Suporte ao Secure Sockets Layer (SSL) ](ssl.html)

## Conectando programaticamente
{: #conx_prgrm}

É possível usar linguagens de programação comuns para criar aplicativos que se conectam a um banco de dados {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

- [ JDBC ](jdbc.html)
- [ Microsoft Windows ODBC ou CLI ](odbc_cli.html)
- [ .NET ](net_apps.html)
- [ Administrador de Origem de Dados ODBC ](odbc_data_source_admin.html)
- [PHP](php.html)
- [API do REST](rest_api.html)
<!-- - [C++]() -->
<!-- - [Java]() -->
<!-- - [Node.js]() -->
<!-- - [Perl]() -->
<!-- - [Python]() -->

## Integrando apps e ferramentas
{: #conx_apps_tools}

Também é possível conectar ferramentas e aplicativos externos ao {{site.data.keyword.dashdbshort_notm}} e utilizá-los para gerenciar ou analisar ainda mais os dados. Por exemplo:

### Integração de dados
- Conecte seus aplicativos {{site.data.keyword.Bluemix_short}} que precisam de um banco de dados de análise.
- [ DataStage ](data.html#datastage)
- [ Informatica ](data.html#informatica)
- [Lift ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://lift.ng.bluemix.net/#docs){:new_window}
- [InfoSphere Data Replication](data.html#idr)
- [Segment ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://segment.com/docs/destinations/db2/){:new_window}
- [ Data Studio ](data.html#data_studio)
- [ Gerenciador do Servidor de Dados ](data.html#dsm)
- [ CLPPLUS ](data.html#clpplus)
- [Aginity Workbench para migrar modelos de dados do Netezza® e dados para o {{site.data.keyword.dashdbshort_notm}}](data.html#aginity_wb)
- [InfoSphere Data Architect para projetar e implementar seu esquema de banco de dados](data.html#ida)

### Visualização de dados / BI
- [Cognos Analytics para executar relatórios do Business Intelligence com relação a seus dados](vis_bi.html#cognos)
- [Looker ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.looker.com/setup-and-management/connecting-to-db){:new_window}
- [ Tableau ](vis_bi.html#tableau)
- [ Microsoft Excel ](vis_bi.html#excel)
- [Esri ArcGIS for Desktop para executar análise geoespacial e publicação de mapa com seus dados](vis_bi.html#esri_arcgis)

### Dados científicos
- [Watson Studio (anteriormente IBM Data Science Experience)](data_sci.html#watson_studio)
- [ Estatísticas do SPSS ](data_sci.html#spss_stats)
- [ SAS ](data_sci.html#sas)
- [ Ambiente de desenvolvimento R local ](data_sci.html#r_dev_env)

## Conectando-se a outro banco de dados Db2
{: #fed}

A virtualização de dados do Db2 (também conhecida como federação) é suportada pelo {{site.data.keyword.dashdbshort_notm}}. A virtualização de dados fornece acesso de consulta única a todos os seus dados que estão em múltiplos bancos de dados distribuídos em qualquer lugar em sua organização. É possível acessar dados que estão em qualquer uma de suas origens de dados do Db2 ou Informix, tanto na nuvem quanto no local. 

Essa função é suportada em todas as versões do {{site.data.keyword.dashdbshort_notm}}, exceto para o plano de Entrada. No entanto, é possível usar o plano de Entrada como um destino do qual é possível puxar dados.

- [Virtualização de dados (federação)](../federation.html)


