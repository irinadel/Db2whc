---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-15"

keywords:

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

# Dados científicos
{: #ds}

Também é possível conectar ferramentas e aplicativos externos ao {{site.data.keyword.dashdbshort_notm}} e utilizá-los para gerenciar ou analisar ainda mais os dados. 
{: shortdesc}

## Watson Studio
{: #watson_studio}

Depois de criar um projeto no IBM Watson Studio (anteriormente Data Science Experience), você incluirá ativos de dados nele para que seja possível trabalhar com dados. Todos os colaboradores no projeto são automaticamente autorizados a acessar os dados no projeto.
{: shortdesc}

A forma de inclusão de dados e de onde é possível incluí-los difere entre projetos anteriores e do IBM Watson. Os projetos IBM Watson usam o  {{site.data.keyword.Bluemix_notm}}  Armazenamento de Objeto. O projeto será um projeto anterior se usar o Object Storage OpenStack Swift. 

### Para criar uma nova conexão em um projeto do IBM Watson:

1. Clique em  ** Incluir no projeto > Conexão **.
    
2. Escolha uma origem de dados.
    
3. Insira as informações de conexão necessárias para sua origem de dados. Geralmente, é necessário fornecer informações como o host, o número da porta, o nome do usuário e a senha.
    
4. É possível descobrir ativos por meio de conexões com o {{site.data.keyword.dashdbshort_notm}}, o que fornece a capacidade de incluir todas as tabelas da conexão como ativos de dados em um projeto. Selecione **Descobrir ativos de dados** e escolha um projeto.
    
5. Clique em  ** Criar **. A conexão aparece na página **Ativos**.

Assista a este vídeo para ver como criar uma conexão e incluir dados conectados em um projeto.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Criar uma conexão e incluir dados conectados em um projeto" type="text/html" width="640" height="390" src="//www.youtube.com/embed/U7-gCbo4QtM?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

### Para criar uma nova conexão em um projeto anterior:

1. Na página **Ativos** de seu projeto, clique no ícone **Localizar e incluir dados**.
    
2. Na área de janela **Conexões**, clique em **Criar conexão**.

3. Insira um nome e uma descrição e escolha uma Categoria de serviço:

   ** Serviço de Dados **  =  {{site.data.keyword.Bluemix_notm}}  serviço de dados

   Quando você escolher **Serviço de dados**, os seus serviços de dados do {{site.data.keyword.Bluemix_notm}} existentes aparecerão na lista de **Instâncias de serviço**.

4. Escolha o serviço ou o servidor de banco de dados na lista.

5. Insira as informações de conexão:

   Quando você escolher **Serviço de dados**, os seus serviços de dados do {{site.data.keyword.Bluemix_notm}} existentes aparecerão na lista de **Instâncias de serviço**.
    
6. Clique em  ** Criar **. A conexão está disponível para todos os projetos anteriores.
    
7. Na área de janela **Conexões**, selecione a conexão e clique em **Aplicar**.

Para incluir uma conexão existente em um projeto anterior:

1. Na página **Ativos** de seu projeto, clique no ícone **Localizar e incluir dados**.
    
2. Na área de janela **Conexões**, selecione a conexão e clique em **Aplicar**.

## Estatísticas do SPSS
{: #spss_stats}

Estas instruções explicam como criar uma conexão do IBM® SPSS® Statistics com um banco de dados {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Pré-requisitos
{: #prereq11}

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) necessários.

### Procedimento
{: #proc11}

1. No SPSS Statistics, clique em **Arquivo > Abrir banco de dados > Nova consulta**.
    
2. No Assistente de banco de dados, clique em **Incluir origem de dados ODBC**.
    
3. Use a janela Administrador de origem de dados ODBC para incluir um nome de origem de dados (DSN) ODBC para o banco de dados {{site.data.keyword.dashdbshort_notm}}:
        
   a. Na guia **DSN do usuário**, clique em **Incluir**.

   b. Na janela Criar nova origem de dados, selecione o driver denominado **IBM DB2 ODBC DRIVER** e clique em **Concluir**.

   Certifique-se de que o driver selecionado não seja um driver com um nome semelhante, como `IBM DB2® ODBC DRIVER - DB2COPY`. Se o driver não aparecer na lista, saia do SPSS Statistics e, em seguida, faça download e instale o driver. Consulte [Pacote de drivers](/docs/services/Db2whc/connecting?topic=Db2whc-dr_pkg#dr_pkg).
        
   c. Na janela Driver ODBC IBM - Incluir, insira um nome de origem de dados (geralmente o nome do banco de dados ao qual você está se conectando) e clique em **Incluir**.
        
   d. Na janela Configurações de CLI/ODBC, na guia **Origem de dados**, insira o ID de usuário e a senha das [informações de conexão](/docs/services/Db2whc/connecting?topic=Db2whc-db_details_cxn_creds#db_details_cxn_creds) coletadas antecipadamente.
        
   e. Na página Configurações avançadas, para cada um dos parâmetros a seguir, clique em **Incluir** para abrir a janela Incluir parâmetro da CLI para iniciar a etapa e clique em **OK** para retornar à página Configurações avançadas:
            
   - Selecione o parâmetro `Database` e, em seguida, clique em **OK** para abrir a janela Configurações de CLI/ODBC. No campo **Valor pendente**, insira o nome do banco de dados por meio das informações de conexão coletadas antecipadamente.

   - Selecione o parâmetro `Hostname` e, em seguida, clique em **OK** para abrir a janela Configurações de CLI/ODBC. No campo **Valor pendente**, insira o nome do host por meio das informações de conexão coletadas antecipadamente.

   - Selecione o parâmetro `Port` e, em seguida, clique em **OK** para abrir a janela Configurações de CLI/ODBC. No campo **Valor pendente**, insira o número da porta por meio das informações de conexão coletadas antecipadamente.
            
   - Selecione o parâmetro `Protocol` e, em seguida, clique em **OK** para abrir a janela Configurações de CLI/ODBC. Selecione  ** TCP/IP **.
        
   f. Clique em **OK** para retornar para a janela Administrador da origem de dados ODBC.
        
   g. Na guia **DSN do usuário**, selecione o nome da origem de dados e, em seguida, clique em **Configurar**.
        
   h. Na janela Configurações de CLI/ODBC, clique em **Conectar** para testar a conexão.
            
   - Se a conexão for bem-sucedida, clique em **OK** para retornar para a janela Administrador da origem de dados ODBC e, em seguida, clique em **OK** para sair da janela.
            
   - Se a conexão não for bem-sucedida, observe e corrija quaisquer erros antes de testar a conexão novamente.

## SAS
{: #sas}

Estas instruções explicam como criar uma conexão do SAS com um banco de dados {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Pré-requisitos
{: #prereq12}

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) necessários.

### Procedimento
{: #proc12}

Para obter as etapas sobre como se conectar do SAS a um banco de dados {{site.data.keyword.dashdbshort_notm}}, consulte a documentação do SAS:
- [Interface SAS/ACCESS para o DB2 em Hosts UNIX e PC ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://documentation.sas.com/?docsetId=acreldb&docsetTarget=p1dzq4zjg1iycgn16l4xj9nnvibt.htm&docsetVersion=9.4&locale=en){:new_window}

## Ambiente de desenvolvimento R
{: #r_dev_env}

Em vez de usar o ambiente do RStudio® integrado ao IBM Watson Studio, talvez você prefira usar seu próprio ambiente de desenvolvimento R instalado localmente. Por exemplo, talvez você tenha sua própria instalação do RStudio ou talvez prefira usar alguma outra ferramenta de desenvolvimento, como Rcmdr ou Rattle. Estas instruções explicam como conectar um ambiente de desenvolvimento R a um banco de dados {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Pré-requisitos
{: #prereq13}

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) necessários.

### Procedimento
{: #proc13}

1. Em seu ambiente R local, instale o pacote `ibmdbR` inserindo o comando a seguir:

   ` install.packages ("ibmdbR") `

   Seu ambiente R local acessa a Comprehensive R Archive Network (CRAN), faz download automaticamente e instala o pacote `ibmdbR` e todos os pacotes obrigatórios que ainda não estejam instalados.
    
2. Crie uma conexão do driver ODBC entre seu ambiente de desenvolvimento R e seu banco de dados {{site.data.keyword.dashdbshort_notm}}:
        
   a. [Configure seu banco de dados como uma origem de dados ODBC ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_cli_and_odbc_applications.html){:new_window}.
        
   b. Abra seu ambiente de desenvolvimento R instalado localmente.
        
   c. No prompt de R, insira as instruções a seguir para criar a conexão. Substitua os itens temporários pelas [informações de conexão](/docs/services/Db2whc/connecting?topic=Db2whc-db_details_cxn_creds#db_details_cxn_creds) coletadas antecipadamente.

   - Se o seu ambiente de desenvolvimento R instalado localmente for executado no banco de dados {{site.data.keyword.dashdbshort_notm}}:

     ```
     library(ibmdbR)
     host.name <- "placeholderForYourHostName"
     port <-"placeholderForPortNumber" # 50000 if not using SSL or 50001 if using SSL
     user.name <-"placeholderForYourUserName"
     pwd <- "placeholderForYourPassword"
     con.text <- paste("placeholderForYourDSNName;DRIVER=BLUDB",
                       ";Database=BLUDB",
                       ";Hostname=",host.name,
                       ";Port=",port,
                       ";PROTOCOL=TCPIP",
                       ";UID=", user.name,
                       ";PWD=",pwd,sep="")
     # Connect to using a odbc Driver Connection string to a remote database con <- idaConnect(con.text)
     ```

   - Se o seu ambiente de desenvolvimento R instalado localmente não for executado no banco de dados {{site.data.keyword.dashdbshort_notm}}:

     ```
     library(ibmdbR)
     driver.name <- "{placeholderForYourDriverName}"
     db.name <- "placeholderForYourDatabaseName"
     host.name <- "placeholderForYourHostName"
     port <-"placeholderForYourPort"
     user.name <-"placeholderForYourUserName"
     pwd <- "placeholderForYourPassword"
     con.text <- paste("placeholderForYourDSNName;DRIVER=",driver.name,
                       ";Database=",db.name,
                       ";Hostname=",host.name,
                       ";Port=",port,
                       ";PROTOCOL=TCPIP",
                       ";UID=", user.name,
                       ";PWD=",pwd,sep="")
     # Connect to using a odbc Driver Connection string to a remote database con <- idaConnect(con.text)
     ```

     **Nota**: a instrução usada para criar o objeto de conexão usa o método `idaConnect()`, não os métodos `odbcConnect()` ou `odbcDriverConnect()`.
        
   d. Inicialize o pacote de analítica emitindo o comando R a seguir:

   ` idaInit (con) `

   e. Para testar se a conexão está funcionando, emita o comando R a seguir:

   ` idaShowTables () `

   O console exibe uma lista de todas as tabelas e visualizações no esquema atual.

