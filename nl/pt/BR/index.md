---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-24"

keywords:

subcollection: Db2whc

---

<!-- Attribute definitions --> 
{:javascript: #javascript .ph data-hd-programlang='javascript'}
{:java: #java .ph data-hd-programlang='java'}
{:ruby: #ruby .ph data-hd-programlang='ruby'}
{:php: #php .ph data-hd-programlang='php'}
{:python: #python .ph data-hd-programlang='python'}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}

# Introdução
{: #getting_started}

O serviço gerenciado do {{site.data.keyword.dashdblong}} é um banco de dados SQL provisionado para você na nuvem. É possível usar o Db2 Warehouse da mesma maneira que você usaria qualquer software de banco de dados, mas sem o gasto adicional e as despesas de configuração de hardware ou de instalação e manutenção de software. 
{: shortdesc}

## Trial gratuito
{: #freetrial}

Você pode experimentar o plano Entry do {{site.data.keyword.dashdbshort_notm}} com até 1 GB de armazenamento, sem encargos. [Avaliação grátis ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window}

## Interfaces
{: #interfaces}

É possível trabalhar com o seu banco de dados de warehouse das maneiras a seguir:
{: shortdesc}

   * No console da web
   * API do REST
   * Conecte aplicativos ou suas ferramentas favoritas por meio do seu computador local
   * Use o {{site.data.keyword.dashdbshort_notm}} como uma origem de dados para seus apps ou serviços {{site.data.keyword.Bluemix_notm}}

### Console da web
{: #web_console}

O console da web fornece uma interface gráfica para tudo o que precisar para usar seu banco de dados, incluindo: instalações de carga, um editor de SQL, downloads de driver e mais.
{: shortdesc}

![Visualização da página do painel do console da web](images/console_v3.png)

<!-- Click the link to take a tour of the {{site.data.keyword.dashdbshort_notm}} for Analytics web console: [General tour ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ibm.biz/dashdb-general-quick-tour){:new_window}. -->

É possível acessar o seu console da web das maneiras a seguir:
   * No painel do {{site.data.keyword.Bluemix_notm}}: é possível abrir o console da web por meio da página Detalhes do serviço para seu serviço do {{site.data.keyword.dashdbshort_notm}}.
   * URL direta: é possível marcar como favorita a URL do console da web para seu serviço do {{site.data.keyword.dashdbshort_notm}}.

### API do REST
{: #api}

Com os planos de serviço do {{site.data.keyword.dashdbshort_notm}}, é possível executar tarefas relacionadas ao gerenciamento de arquivo e carregamento de dados usando a API de REST do
[{{site.data.keyword.dashdbshort_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://ibm.biz/db2whc_api){:new_window}.
{: shortdesc}

### Conecte aplicativos ou suas ferramentas favoritas por meio do seu computador local
{: #connect_apps}

Configure seu ambiente local para se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}} concluindo as etapas a seguir:
{: shortdesc}

1. Faça download do [pacote de drivers](/docs/services/Db2whc/connecting/driver_pkg.html) por meio do console da web do {{site.data.keyword.dashdbshort_notm}}.
2. Instale o pacote de drivers no computador em que seus apps ou ferramentas estão em execução:
   - [ Instalando no Linux ou PowerLinux ](/docs/services/Db2whc/connecting/install_linux.html)
   - [ Instalando no Mac OS X ](/docs/services/Db2whc/connecting/install_mac.html)
   - [ Instalando no Windows ](/docs/services/Db2whc/connecting/install_win.html)
3. [Configure os arquivos do driver](/docs/services/Db2whc/connecting/driver_pkg_cfg.html) para seu banco de dados {{site.data.keyword.dashdbshort_notm}}.

### Use o DB2 Warehouse on Cloud como uma origem de dados para seus apps ou serviços
{{site.data.keyword.Bluemix_notm}}
{: #data_src}

Apps hospedados no {{site.data.keyword.Bluemix_notm}} podem se conectar ao seu banco de dados {{site.data.keyword.dashdbshort_notm}} exatamente da mesma maneira que seus aplicativos locais se conectam ao seu banco de dados {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

Quando seus apps usam a plataforma {{site.data.keyword.Bluemix_notm}}, é possível aproveitar a variável de ambiente `VCAP _SERVICES` para simplificar a tarefa de especificar detalhes e credenciais do banco de dados:
1. Em seu painel do {{site.data.keyword.Bluemix_notm}}, na guia **Conexões** da página Detalhes do serviço para seu serviço do {{site.data.keyword.dashdbshort_notm}}, clique no botão **Criar conexão**.
2. Selecione o app {{site.data.keyword.Bluemix_notm}} para usar com o banco de dados {{site.data.keyword.dashdbshort_notm}} como uma origem de dados e, em seguida, clique no botão **Conectar**.
3. Atualize seu código do aplicativo para recuperar detalhes e credenciais do banco de dados por meio da variável de ambiente `VCAP_SERVICES`:

    **Exemplo sem `VCAP_SERVICES`**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    $database    = "BLUDB";         # Get these database details from
    $hostname    = "<Host-name>";   # the Connection info page of the
    $port        = 50000;           # web console.
    $user        = "<User-ID >";    #
    $password    = "<Password>";    #
    $dsn         = "DATABASE=$database;" .
                   "HOSTNAME=$hostname;" .
                   "PORT=$port;" .
                   "PROTOCOL=TCPIP;" .
                   "UID=$user;" .
                   "PWD=$password;";

    $conn_string = $driver . $dsn;

    $conn        = db2_connect( $conn_string, "", "" );
    ?>
    ```

    **Exemplo com `VCAP_SERVICES`**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    $vcap        = json_decode( getenv( "VCAP_SERVICES" ), true );
    $dsn         = $vcap[ "dashDB" ][0][ "credentials" ][ "dsn" ];

    $conn_string = $driver . $dsn;
                                   
    $conn        = db2_connect( $conn_string, "", "" );
    ?>
    ```

## Amostra
{: #samples}

Aqui estão os links para amostras que demonstram como se conectar programaticamente ao banco de dados {{site.data.keyword.dashdbshort_notm}} por meio de aplicativos em diferentes linguagens:
{: shortdesc}

- [JDBC](/docs/services/Db2whc/connecting/jdbc.html)
- [ Microsoft Windows ODBC ou CLI ](/docs/services/Db2whc/connecting/odbc_cli.html)
- [ .NET ](/docs/services/Db2whc/connecting/net_apps.html)
- [ Administrador de Origem de Dados ODBC ](/docs/services/Db2whc/connecting/odbc_data_source_admin.html)
- [PHP](/docs/services/Db2whc/connecting/php.html)
- [API do REST](/docs/services/Db2whc/connecting/rest_api.html)

## Vídeo: Introduzindo o Db2 Warehouse on Cloud
{: #intro_vid}

Assista a este vídeo para ver uma introdução ao {{site.data.keyword.dashdbshort_notm}}.

<iframe class="embed-responsive-item" id="youtubeplayer1" title="Introdução ao {{site.data.keyword.dashdbshort_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/0NO9OTFWzKs?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

## Vídeo: Introduzindo o Plano Flex Performance
{: #intro_vid_flex}

Assista a este vídeo para ver uma introdução ao plano de Desempenho do {{site.data.keyword.dashdbshort_notm}} Flex.

<iframe class="embed-responsive-item" id="youtubeplayer2" title="Criando uma conexão por meio do Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

## Vídeo: Conectando um aplicativo analítico
{: #cognos_vid}

Assista a este vídeo para ver como criar uma conexão por meio do Cognos Analytics.

<iframe class="embed-responsive-item" id="youtubeplayer3" title="Criando uma conexão por meio do Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TRUEPVHGi0s?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

