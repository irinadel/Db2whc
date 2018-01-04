---

copyright:
  years: 2014, 2018
lastupdated: "2017-07-17"

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
{:pre: .pre}

# Introdução ao Db2 Warehouse on Cloud (anteriormente dashDB for Analytics)
{: #getting_started}

O serviço gerenciado {{site.data.keyword.IBM}} Db2 Warehouse on Cloud é um banco de dados SQL provisionado para você na nuvem. É possível usar o Db2 Warehouse da mesma maneira que você usaria qualquer software de banco de dados, mas sem o gasto adicional e as despesas de configuração de hardware ou de instalação e manutenção de software.
{: shortdesc}

## Interfaces
{: #interfaces}

É possível trabalhar com o seu banco de dados de warehouse das maneiras a seguir:
{: shortdesc}

   * No console da web
   * API do REST
   * Conecte aplicativos ou suas ferramentas favoritas por meio do seu computador local
   * Use o Db2 Warehouse on Cloud como uma origem de dados para os seus apps ou serviços do Bluemix

### Console da web
{: #web_console}

O console da web fornece uma interface gráfica para tudo o que precisar para usar seu banco de dados, incluindo: instalações de carga, um editor de SQL, downloads de driver e mais.
{: shortdesc}

![Visualização da página do painel do console da web](images/console_v2.png)

<!-- Click the link to take a tour of the {{site.data.keyword.dashdbshort_notm}} for Analytics web console: [General tour ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ibm.biz/dashdb-general-quick-tour "External link icon"){:new_window}. -->

É possível acessar o seu console da web das maneiras a seguir:
   * No painel do {{site.data.keyword.Bluemix_notm}} - é possível abrir o console da web pela página Detalhes do serviço para seu serviço Db2 Warehouse on Cloud.
   * URL direta - é possível marcar como favorita a URL do console da web para o seu serviço Db2 Warehouse on Cloud.

### API do REST
{: #api}

Com os planos de serviço do Db2 Warehouse on Cloud, é possível executar tarefas relacionadas a gerenciamento de arquivo, carregamento de dados e execução de scripts R usando a [API de REST do Db2 Warehouse on Cloud ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://ibm.biz/dashdb-api "Ícone de link externo"){:new_window}.
{: shortdesc}

### Conecte aplicativos ou suas ferramentas favoritas por meio do seu computador local
{: #connect_apps}

Configure o seu ambiente local para conectar-se ao seu banco de dados de warehouse Db2 concluindo as etapas a seguir:
{: shortdesc}

1. Faça download do [pacote de drivers ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_driver_package.html "Ícone de link externo"){:new_window} no console da web do Db2 Warehouse on Cloud.
2. [Instale o pacote de drivers ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_driver_package_install.html "Ícone de link externo"){:new_window} no computador em que seus apps ou ferramentas estão em execução.
3. [Configure os arquivos do driver ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/en/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_driver_package_config.html "Ícone de link externo"){:new_window} para o seu banco de dados de warehouse Db2.

### Use o Db2 Warehouse on Cloud como uma origem de dados para os seus apps ou serviços do Bluemix
{: #data_src}

Os apps hospedados no {{site.data.keyword.Bluemix_notm}} podem conectar-se ao seu banco de dados do Db2 Warehouse on Cloud exatamente da mesma maneira que os seus aplicativos locais se conectam ao banco de dados do Db2 Warehouse on Cloud.
{: shortdesc}

Quando seus apps usam a plataforma {{site.data.keyword.Bluemix_notm}}, é possível aproveitar a variável de ambiente `VCAP _SERVICES` para simplificar a tarefa de especificar detalhes e credenciais do banco de dados:
1. No painel do {{site.data.keyword.Bluemix_notm}}, na guia **Conexões** da página Detalhes do serviço do seu serviço Db2 Warehouse on Cloud, clique no botão **Criar conexão**.
2. Selecione o app {{site.data.keyword.Bluemix_notm}} a ser usado como uma origem de dados com o seu banco de dados do Db2 Warehouse on Cloud e, em seguida, clique no botão **Conectar**.
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

Veja a seguir alguns links para amostras que demonstram como se conectar ao seu banco de dados do Db2 Warehouse on Cloud usando aplicativos em diferentes idiomas:
{: shortdesc}

   * [.NET ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting__net_applications.html "Ícone de link externo"){:new_window}
<!-- * [JAVA ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_java.html "External link icon"){:new_window} -->
   * [JDBC ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_jdbc_applications.html "Ícone de link externo"){:new_window}
<!-- * [Node.js ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_nodejs.html "External link icon"){:new_window} -->
   * [PHP ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_php.html "Ícone de link externo"){:new_window}
<!-- * [Python ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_python.html "External link icon"){:new_window} -->
   * [Amostras do Db2 Warehouse on Cloud no GitHub ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/IBM-Bluemix/dashdb-nodejs-helloworld "Ícone de link externo"){:new_window}


