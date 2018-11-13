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

# Integração de dados
{: #overview}

Também é possível conectar ferramentas e aplicativos externos ao {{site.data.keyword.dashdbshort_notm}} e utilizá-los para gerenciar ou analisar ainda mais os dados. 
{: shortdesc}

## DataStage
{: #datastage}

Estas instruções explicam como definir uma conexão sem SSL entre o IBM® InfoSphere® DataStage® <!--version 9.1 and later -->e um banco de dados {{site.data.keyword.dashdbshort_notm}} catalogando o banco de dados e definindo um objeto de conexão ou como criar uma conexão com SSL usando um certificado digital emitido por um terceiro.
{: shortdesc}

### Pré-requisitos

Se você ainda não tiver um cliente de servidor de dados instalado, faça download e instale o IBM Data Server Client <!--Version 10.5 -->que for apropriado para o sistema operacional da máquina do cliente: [IBM Data Server Client ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/marketing/iwm/iwm/web/preLogin.do?source=swg-idsc97){:new_window}.

Para fazer conexões com o protocolo SSL, faça download e instale o GSKit V8 de 32 bits. Clique na guia S.O. que for apropriada para o sistema operacional da máquina do cliente: [GSKit V8 - Instruções de instalação, desinstalação e upgrade ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/support/docview.wss?uid=swg21631462){:new_window}. Para os sistemas operacionais a seguir, assegure-se de incluir o caminho do diretório de instalação do GSKit na variável de ambiente de caminho específica do S.O.:

- AIX ®:  ** LIBPATH **
   - ` /usr/opt/ibm/gsk8/lib `
- Linux:  ** LD_LIBRARY_PATH **
    - ` /usr/local/ibm/gsk8/lib `
- UNIX:  ** LD_LIBRARY_PATH **
    - `/opt/ibm/gsk8/lib`
- Windows:  ** PATH **
    - `<installation_directory>\gsk8\bin `
    - `<installation_directory>\gsk8\lib `

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](connecting.html#prereqs) necessários.

### Procedimento

- Para criar uma conexão com SSL, conclua as etapas a seguir:

  1. Abra uma linha de comandos ou um terminal e crie um novo diretório no sistema DataStage para armazenar o certificado SSL e os arquivos-chave.

     ` # /home/db2inst2> mkdir SSL `

     ` # /home/db2inst2> cd SSL `

  2. No console do Db2, faça download do certificado SSL por meio da página Conectar seus aplicativos ao banco de dados.

     a. A partir do menu principal, clique em  ** Conectar **.
     
     b. Clique em **Conexão com SSL** e, em seguida, clique no link **Certificado SSL (1 KB)**.
     
     c. Salve o certificado `DigiCertGlobalRootCA.crt` no diretório SSL criado na etapa 1.
        
  3. Crie um banco de dados de keystore do cliente no sistema DataStage usando o utilitário **gsk8capicmd**. Esse utilitário está incluído na instalação do servidor DB2®.

     ` # /home/db2inst2/SSL> gsk8capicmd -keydb -create -db <keystore_db.kdb> -pw <ks_db_password> -stash `

     em que  `<keystore_db.kdb>`  representa o banco de dados de keystore do cliente e  `<ks_db_password>` representa a senha para o banco de dados de keystore do cliente.
        
  4. Inclua o certificado no banco de dados de keystore do cliente.

     `# /home/db2inst2/SSL> gsk8capicmd -cert -add -db <keystore_db.kdb> -pw <ks_db_password> -label BLUDB_SSL -file DigiCertGlobalRootCA.crt `

     em que  `<keystore_db.kdb>`  representa o banco de dados de keystore do cliente e  `<ks_db_password>` representa a senha para o banco de dados de keystore do cliente.
    
  5. Configure o cliente DB2 no servidor DataStage.
            
     a. Atualize os parâmetros de configuração SSL no gerenciador do banco de dados.

     `# /home/db2inst2> db2 update dbm cfg using SSL_CLNT_KEYDB /home/db2inst2/SSL/<keystore_db.kdb>`

     em que  `<keystore_db.kdb>`  representa o banco de dados do keystore do cliente.

     `# /home/db2inst2> db2 update dbm cfg using SSL_CLNT_STASH /home/db2inst2/SSL/<keystore_db.sth>`

     em que  `<keystore_db.sth>` representa o stash de senha do banco de dados de keystore do cliente.
            
     b. Catalogue o nó de destino com a opção de segurança SSL e, em seguida, o banco de dados BLUDB nesse nó de destino.

     `# /home/db2inst2> db2 catalog tcpip node SSLCLOUD remote <IP_addr_of_BLUDB_database_server> servidor de segurança 50001 SSL `

     em que  `<IP_addr_of_BLUDB_database_server>` representa o endereço IP do servidor de banco de dados BLUDB,

     `# /home/db2inst2> db2 catalog db BLUDB as BLUDB_S at node SSLCLOUD`

     ` # /home/db2inst2> db2 terminate `

  6. Inclua permissões de leitura e execução nos arquivos no diretório SSL para todos. O usuário do DataStage que executa as tarefas precisa acessar esses arquivos para fazer conexões SSL com o banco de dados Db2.

     ` # /home/db2inst2/SSL> chmod 655 /home/db2inst2/SSL/ * `

  7. Reinicie o servidor DataStage.

- Para criar uma conexão sem SSL, catalogue o banco de dados Db2 de destino no servidor IBM InfoSphere DataStage concluindo as etapas a seguir:

  1. Use um aplicativo cliente telnet, como o PuTTY, para se conectar ao servidor DataStage como o proprietário da instância padrão (geralmente db2inst1).
  2. Crie um catálogo do banco de dados Db2 de destino usando os comandos do DB2 a seguir:

     ` db2 catalog tcpip node nodename remote <IP_address_of_BLUDB_database_server> <port_number_of_BLUDB_database>`

     ` db do catálogo db2 <BLUDB_db_name> no nó <nodename>`

     ` db2 connect to <BLUDB_db_name> usuário <BLUDB_db_user_name> utilizando <BLUDB_db_password>`

     ` Tabelas de lista de db2 `

     em que  `<IP_address_of_BLUDB_database_server>` representa o endereço IP do servidor de banco de dados BLUDB, `<port_number_of_BLUDB_database>` representa o número da porta do banco de dados BLUDB, `<BLUDB_db_name>`  representa o nome do banco de dados BLUDB,  `<nodename>`  representa o nome do nó,  `<BLUDB_db_user_name>` representa o nome do usuário do banco de dados BLUDB e `<BLUDB_db_password>`  representa a senha do banco de dados BLUDB.

  3. Use as [informações de conexão](credentials.html) coletadas antecipadamente para definir uma conexão no cliente DataStage. Na guia **Parâmetros**, deve-se selecionar o **Conector do DB2** para o campo **Conectar usando Tipo de preparação**.

     Para obter detalhes sobre como definir uma conexão no DataStage, consulte o tópico da documentação do DataStage a seguir: 
     
     - [Criando um objeto de conexão de dados manualmente ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/SSZJPZ_11.3.0/com.ibm.swg.im.iis.ds.design.doc/topics/t_ddesref_Creating_a_Data_Connection_Object_Manually.html){:new_window}

## Informatica
{: #informatica}

É possível conectar o Informatica ao {{site.data.keyword.dashdbshort_notm}} para ajudá-lo a gerenciar seus dados.
{: shortdesc}

Assista a este vídeo para ver como integrar o {{site.data.keyword.dashdbshort_notm}} ao Informatica Cloud.

<iframe class="embed-responsive-item" id="youtubeplayer1" title="DB2 Connections - Lightening Fast How-To with Informatica Cloud" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TUiS_HstLnU?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

<!-- To configure a native Db2 connection to connect to {{site.data.keyword.dashdbshort_notm}}, perform the following steps:

1. Run the `odbcad32.exe` file from your local system.
The ODBC Data Sources Administrator dialog box appears.

2. Create the 32-bit ODBC Data Source Name using the DataDirect Db2 drivers.

3. In the ODBC DB2 Wire Protocol Setup dialog box, click **Security** tab.

4. Set the value of the `Authentication Method` property as `1 -Encrypt Password`. The following image shows the **Security** tab in the ODBC DB2 Wire Protocol Setup dialog box where you can set the `Authentication Method` property:
             
   ![ODBC Db2 Wire Protocol Driver Setup - Security tab](images/odbc_driver.png)
       
5. In the ODBC DB2 Wire Protocol Setup dialog box, click **Modify Bindings** tab.

6. Enter your user name in the Package Collection property. The following image shows the **Modify Bindings** tab in the ODBC DB2 Wire Protocol Setup dialog box where you can set the `Package Collection` property: 

   ![ODBC Db2 Wire Protocol Driver Setup - Modify Bindings tab](images/odbc_driver_2.png)
            
7. In the PowerCenter Designer, use the data source name that you created to import the metadata.

8. In the PowerCenter Workflow Manager, create the required workflow.

9. Ensure that you have the {{site.data.keyword.dashdbshort_notm}} compatible 11.x Db2 clients when you run the workflow.

**Note**: If you want to set the authentication type when you create the Db2 client catalog, you could specify the value of the `AUTHENTICATION TYPE` property as `SERVER_ENCRYPT`. -->

<!-- Watch this video to see how to integrate Db2 and Salesforce with Informatica Cloud.

<iframe class="embed-responsive-item" id="youtubeplayer2" title="Integrate Db2 and Salesforce with Informatica Cloud" type="text/html" width="640" height="390" src="//www.youtube.com/watch?v=RGTLweZvKP8" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe> -->

<!-- [Informatica ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://kb.informatica.com/howto/6/Pages/20/522402.aspx?myk=Connect%20to%20Db2){:new_window} -->

## Lift
{: #lift}

Use o Lift para migrar seus dados para o {{site.data.keyword.dashdbshort_notm}}.

[Lift ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://lift.ng.bluemix.net/#docs){:new_window}

## InfoSphere Data Replication
{: #idr}

É possível conectar o IBM® InfoSphere® Data Replication <!--version 11.3.3.3-36 or later -->a um banco de dados {{site.data.keyword.dashdbshort_notm}}. Esse recurso se aplica aos ambientes SMP e MPP. Ele não se aplica ao plano de Entrada do {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Visão geral

Idealmente, ao conectar o IBM InfoSphere Data Replication ao {{site.data.keyword.dashdbshort_notm}}, o IBM InfoSphere Data Replication fica no mesmo Data Center do {{site.data.keyword.Bluemix_notm}} que o {{site.data.keyword.dashdbshort_notm}} ou é colocado com o {{site.data.keyword.dashdbshort_notm}}. O IBM InfoSphere Data Replication é conectado de um servidor local à instância remota do {{site.data.keyword.dashdbshort_notm}}.

Ao usar o {{site.data.keyword.dashdbshort_notm}} como um destino de conexão, o desempenho do IBM InfoSphere Data Replication depende parcialmente da largura de banda da rede que separa seu mecanismo de destino da instância do {{site.data.keyword.dashdbshort_notm}}. A distância física também afeta o desempenho: idealmente, o IBM InfoSphere Data Replication fica o mais próximo possível da instância do {{site.data.keyword.dashdbshort_notm}}. A topologia de rede também afeta o desempenho. Por exemplo, idealmente, o mecanismo de destino do IBM InfoSphere Data Replication é executado em uma VM na mesma VPN (domínio de segurança) que a instância de destino. Quanto menos os nós de rede (por exemplo, firewalls ou roteadores) se cruzarem, melhor. 

### Pré-requisitos

Se pretende se conectar usando o protocolo SSL, faça download e instale o GSKit V8. Consulte [GSKit V8 - Instruções de instalação, desinstalação e upgrade ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/support/docview.wss?uid=swg21631462){:new_window}. Clique na guia do sistema operacional que se aplica ao sistema operacional da máquina do cliente. Se você estiver instalando o GSKit em um computador do Windows, assegure-se de especificar o caminho do diretório de instalação do GSKit (`<installation_directory>\gsk8\bin`) da variável de ambiente **`PATH`**.

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](connecting.html#prereqs) necessários.

Se pretende se conectar usando o protocolo SSL, faça download do certificado SSL `DigiCertGlobalRootCA.crt` por meio do console da web para um diretório na máquina do cliente. Para fazer download do certificado, clique em **Conexão > Informações de conexão** e, em seguida, clique na guia **Conexão com SSL**.

### Procedimento

1. Escolha uma das abordagens a seguir para fazer sua conexão:

   - Para criar uma conexão com SSL, conclua as etapas a seguir:
            
     a. Emita o seguinte comando:

     `cd /<ssl_directory_name>/ssl `

     em que  ` /<ssl_directory_name>/ssl` é o caminho para o diretório no qual o certificado SSL `DigiCertGlobalRootCA.crt` foi transferido por download.

     b. Crie um banco de dados de chaves de clientes e um arquivo stash usando a ferramenta **GSKCapiCmd**. Por exemplo, o comando a seguir cria um banco de dados de chaves de clientes chamado `dashclient.kdb` e um arquivo stash chamado `dashclient.sth`:

     `gsk8capicmd_64 -keydb -create -db "dashclient.kdb" -pw "passw0rdpw0" -stash`

     em que `passw0rdpw0` é uma senha. A opção **-stash** cria um arquivo stash no mesmo caminho que aquele do banco de dados de chaves de clientes, com uma extensão de arquivo de `.sth`. No momento da conexão, o GSKit usa o arquivo stash para obter a senha para o banco de dados de chaves de clientes.
            
     c. Inclua o certificado no banco de dados de chaves de clientes. Por exemplo, o comando **gsk8capicmd** a seguir importa o certificado do arquivo `/<ssl_directory_name>/ssl/DigiCertGlobalRootCA.crt` para o banco de dados de chaves de clientes chamado `dashclient.kdb`:

     `gsk8capicmd_64 -cert -add -db "dashclient.kdb" -pw "passw0rdpw0" -label "DigiCert" -file "/<ssl_directory_name>/ssl/DigiCertGlobalRootCA.crt" -format ascii -fips`

     d. Atualize os valores dos parâmetros de configuração do gerenciador de banco de dados `SSL_CLNT_KEYDB` e `SSL_CLNT_STASH` no cliente para especificar o banco de dados de chaves de clientes e o arquivo stash. A seguir, exemplos:

     `db2 update dbm cfg using SSL_CLNT_KEYDB /<ssl_directory_name>/ssl/dashclient.kdb `

     `db2 update dbm cfg using SSL_CLNT_STASH /<ssl_directory_name>/ssl/dashclient.sth `

     e. Catalogue o nó do {{site.data.keyword.dashdbshort_notm}} para que os aplicativos clientes possam se conectar a ele. Emita o seguinte comando:

     ` nó tcpip do catálogo do db2 <node_name> remoto <Db2_Warehouse_IP_address> servidor <port_number> ssl de segurança `

     sendo:
                
     `<node_name>`  é o seu nome para o nó.

     `<Db2_Warehouse_IP_address>` é o endereço IP do servidor Db2 Warehouse on Cloud.

     `<port_number>` é a porta usada para se conectar ao Db2 Warehouse usando uma conexão SSL. Se você estiver usando a porta padrão, especifique `50001`.
            
     f. Catalogue o banco de dados do {{site.data.keyword.dashdbshort_notm}} remoto para que os aplicativos clientes possam se conectar a ele. Emita o seguinte comando:

     ` bludb do banco de dados do catálogo do db2 como <db_alias> no nó <node_name>`

     em que `db_alias` é o seu nome para o banco de dados {{site.data.keyword.dashdbshort_notm}}.
            
     g. Teste a conexão SSL de uma das maneiras a seguir:
                
     - Teste a conexão usando o CLP emitindo o comando a seguir para se conectar ao banco de dados do {{site.data.keyword.dashdbshort_notm}}:

       ` db2 connect to <db_alias> usuário <user_id>`

       em que  `<user_id>`  é seu  {{site.data.keyword.dashdbshort_notm}}  ID do usuário. Será solicitado que você insira a sua senha.
                
     - Teste a conexão usando a CLI emitindo o comando a seguir para se conectar ao banco de dados do {{site.data.keyword.dashdbshort_notm}}:

       ` db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

       em que  `<alias>` é um alias do DSN que você criou usando o comando **db2cli writecfg**, `<user_id>`  é o seu ID do usuário do  {{site.data.keyword.dashdbshort_notm}}  e  `<password>`  é a sua  {{site.data.keyword.dashdbshort_notm}}  senha do banco de dados.
        
   - Para criar uma conexão sem SSL, conclua as etapas a seguir:

     a. Catalogue o nó do {{site.data.keyword.dashdbshort_notm}} para que os aplicativos clientes possam se conectar a ele. Emita o seguinte comando:

     ` nó tcpip do catálogo do db2 <node_name> remoto <Db2_Warehouse_IP_address> servidor <port_number>`

     sendo:
                
     `<node_name>`  é o seu nome para o nó.

     `<Db2_Warehouse_IP_address>` é o endereço IP do servidor {{site.data.keyword.dashdbshort_notm}}.

     `<port_number>` é a porta usada para se conectar ao {{site.data.keyword.dashdbshort_notm}} sem usar uma conexão SSL. Se você estiver usando a porta padrão, especifique `50000`.
            
     b. Catalogue o banco de dados do {{site.data.keyword.dashdbshort_notm}} remoto para que os aplicativos clientes possam se conectar a ele. Emita o seguinte comando:

     ` bludb do banco de dados do catálogo do db2 como <db_alias> no nó <node_name>`

     em que  `<db_alias>`  é o seu nome para o banco de dados  {{site.data.keyword.dashdbshort_notm}} .

     c. Teste a conexão não SSL de uma das maneiras a seguir:

     - Teste a conexão usando o CLP emitindo o comando a seguir para se conectar ao banco de dados do {{site.data.keyword.dashdbshort_notm}}:

       ` db2 connect to <db_alias> usuário <user_id>`

       em que  `<user_id>`  é seu  {{site.data.keyword.dashdbshort_notm}}  ID do usuário. Será solicitado que você insira a sua senha.
                
     - Teste a conexão usando a CLI emitindo o comando a seguir para se conectar ao banco de dados do {{site.data.keyword.dashdbshort_notm}}:

       ` db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

       em que  `<alias>` é um alias do DSN que você criou usando o comando **db2cli writecfg**, `<user_id>`  é o seu ID do usuário do  {{site.data.keyword.dashdbshort_notm}}  e  `<password>` é a sua senha do Db2 Warehouse on Cloud.
    
2. Ative a ferramenta de configuração do InfoSphere Data Replication e execute as etapas a seguir. Os valores mostrados nas capturas de tela são exemplos.
        
   a. Inclua uma instância de origem para apontar para o banco de dados de origem usando a guia **Configuração da instância**:

   ![IIDR New Instance - Source instance](images/IIDR_source_instance.jpg)

   b. Inclua uma instância de destino para apontar para o banco de dados Db2 de destino usando a guia **Configuração da instância**. Se você não estiver usando o IBM InfoSphere Data Replication 11.3.3.3-50 ou mais recente, não marque a caixa de seleção **Especificar caminho do carregador de atualização**.

   ![Nova instância do IIDR - Instância de destino](images/IIDR_target_instance.jpg)

   c. Inicie cada instância:

   ![IIDR Configuration Tool](images/IIDR_instances.jpg)

3. Ative o console de gerenciamento do InfoSphere Data Replication e use o Access Manager para concluir as etapas a seguir:
        
   a. Crie um armazenamento de dados para se conectar à instância de origem usando a guia **Armazenamento de dados**. Como um banco de dados Db2 não era originalmente suportado como um banco de dados de origem, deve-se fornecer informações de usuário e de senha para o banco de dados de origem clicando em **Parâmetros de conexão**.

   ![Propriedades de armazenamento de dados - Origem](images/IIDR_source_datastore.jpg)

   b. Crie um armazenamento de dados para se conectar à instância de destino usando a guia **Armazenamento de dados**. Deve-se fornecer informações de usuário e de senha clicando em **Parâmetros de conexão**.

   ![Propriedades de armazenamento de dados - Destino](images/IIDR_target_datastore.jpg)

   c. Se o usuário (por exemplo, administrador) que se conectará ao Access Server não existir, crie esse usuário:

   ![New User](images/IIDR_management_user.jpg)

   d. Clique na guia  ** Access Manager ** .
        
   e. Na guia **Gerenciamento de armazenamento de dados**, designe o usuário aos armazenamentos de dados de origem e de destino clicando com o botão direito em cada armazenamento de dados e, em seguida, clicando em **Designar usuário**. Assegure-se de que as credenciais para acessar cada instância estejam corretas.

   ![IIDR Management Console - Access Manager](images/IIDR_management_assign_user.jpg)

### O que fazer a seguir

Defina uma assinatura e execute a replicação de dados. Para obter informações, consulte:

- [Carregando dados do InfoSphere Data Replication ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/learn_how/loaddata_iidr.html){:new_window} 

## Segmento
{: #segment}

É possível integrar o Segment a um banco de dados {{site.data.keyword.dashdbshort_notm}}. Segment é uma única plataforma que coleta, armazena e roteia os dados do usuário para centenas de ferramentas.
{: shortdesc}

[Segment ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://segment.com/docs/destinations/db2/){:new_window}

## Data Studio
{: #data_studio}

Estas instruções explicam como criar uma conexão do IBM® Data Studio <!--version 4.1.x -->com um banco de dados {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Pré-requisitos

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](connecting.html#prereqs) necessários.

### Procedimento

1. No Data Studio, clique em **Todos os bancos de dados > Nova conexão com um banco de dados**.

2. Na guia **Local**, selecione **DB2 for Linux, UNIX e Windows** como o gerenciador do banco de dados.
    
3. Na guia **Geral**, insira os valores a seguir:
   - * Banco de Dados *:  ` BLUDB `
   - * Host *: O nome do host.
   - *Porta*: para uma conexão sem SSL, insira `50000`. Para uma conexão com SSL, insira `50001`. 
   - *Nome do usuário*: o nome do usuário usado para efetuar login.
   - *Senha*: a senha usada para efetuar login.

4. Para uma conexão SSL, clique na guia **Opcional** e, em seguida, clique em **Incluir**. Para a propriedade  ` sslConnection ` , especifique  ` true `.

5. [*Optional*]: Click **Teste a conexão** para verificar se a conexão foi bem-sucedida.

## Data Server Manager (DSM)
{: #dsm}

Uma conexão entre o IBM® Data Server Manager e o banco de dados {{site.data.keyword.dashdbshort_notm}} permite monitorar e gerenciar o banco de dados por meio do console da web do Data Server Manager.
{: shortdesc}

### Pré-requisitos

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](connecting.html#prereqs) necessários.

### Procedimento

<!--The connection procedure was tested on Data Server Manager version 1.1. The same procedure applies to all of the other versions of the Data Server Manager software.
-->
Para criar uma conexão, conclua as etapas a seguir:

1. Efetue login no console da web do Data Server Manager.
    
2. No console da web do Data Server Manager, acesse **Configurar > Conexões com o banco de dados**.
    
3. Clique no ícone ![sinal de + dentro de um círculo](images/icon_R_plus.gif) para incluir uma conexão com o banco de dados. Na página **Incluir conexão com o banco de dados** na guia **Conexão com o banco de dados**, insira as informações necessárias nos campos a seguir:

   - *Nome da conexão com o banco de dados*: o nome deve ser exclusivo para o Data Server Manager
   - *Tipo de servidor de dados*: no menu suspenso, selecione **DB2 for Linux, UNIX e Windows**
   - * Nome do banco de dados *:  ` BLUDB `
   - * Nome do host *: Insira o  {{site.data.keyword.dashdbshort_notm}}  nome do host 
   - *Número da porta*: para uma conexão sem SSL, insira `50000`. Para uma conexão com SSL, insira `50001`. 
   - *Segurança JDBC*: no menu suspenso, selecione **Senha não criptografada**
   - *ID do usuário*: seu ID de usuário do {{site.data.keyword.dashdbshort_notm}} 
   - * Senha *: Sua  {{site.data.keyword.dashdbshort_notm}}  senha 

4. Para uma conexão com SSL, selecione a guia **Propriedades avançadas do JDBC**. Insira as informações necessárias nos campos a seguir:

   - * Propriedade *:  ` sslConnection `
   - *Valor*: `true`

    Clique no botão  ** Incluir ** . Selecione a guia  ** Conexão com o Banco de Dados ** .
    
5. Teste a conexão clicando no botão **Conexão de teste**. Se a conexão for bem-sucedida, clique em **OK**.

## InfoSphere Data Architect
{: #ida}

Estas instruções explicam como criar uma conexão do InfoSphere® Data Architect <!--version 9.1.x -->com um banco de dados {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Pré-requisitos

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](connecting.html#prereqs) necessários.

### Procedimento

1. Na visualização Data Source Explorer do InfoSphere Data Architect, clique com o botão direito em **Conexões com o banco de dados** e, em seguida, selecione **Novo**.
    
2. Na guia **Local**, selecione **DB2 for Linux, UNIX e Windows** como o gerenciador do banco de dados.
    
3. Na guia **Geral**, insira os valores a seguir:

   - * Banco de Dados *:  ` BLUDB `
   - *Host*: o nome do host coletado antecipadamente.
   - *Porta*: para uma conexão sem SSL, insira `50000`. Para uma conexão com SSL, insira `50001`. 
   - *Nome do usuário*: o ID de usuário coletado antecipadamente.
   - *Senha*: a senha coletada antecipadamente.

4. Para uma conexão SSL, clique na guia **Opcional**. Insira uma propriedade `sslConnection` e especifique um valor de `true`. Clique em  ** Incluir **.
    
5. [*Optional*]: Click **Teste a conexão** para verificar se a conexão foi bem-sucedida.

## Aginity Workbench
{: #aginity_wb}

Estas instruções explicam como conectar o Aginity Workbench <!--4.3 -->a um banco de dados {{site.data.keyword.dashdbshort_notm}}. É possível usar o Aginity Workbench para migrar modelos de dados e dados do IBM PureData for Analytics (Netezza) para o {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Pré-requisitos

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](connecting.html#prereqs) necessários.

### Procedimento

1. Faça download e instale o Aginity Workbench.

2. Determine o DSN do ODBC usando as informações de conexão observadas anteriormente.

3. Ative o Aginity Workbench. Se a caixa de diálogo de conexão com o banco de dados não abrir automaticamente, abra-a clicando em **Conectar** na barra de ferramentas.

4. [Estabeleça uma conexão com o banco de dados ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://www.aginity.com/documentation/WB/dashDB/Default.htm#Aginity_Topics/Aginity_Workbench/Database_Connection_Dialog_Box.htm){:new_window}. Use o nome do host, o ID de usuário e a senha usando as informações de conexão observadas anteriormente.

## CLPPlus
{: #clpplus}

O Command line processor plus (CLPPlus) está incluído no pacote de drivers do Db2. O CLPPlus fornece uma interface de linha de comandos que pode ser usada para se conectar a um banco de dados {{site.data.keyword.dashdbshort_notm}}. É possível usar o CLPPlus para definir, editar e executar instruções, scripts e comandos.
{: shortdesc}

### Pré-requisitos

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](connecting.html#prereqs) necessários.

Para usar o CLPPlus, assegure-se de que um kit de desenvolvimento de software (SDK) ou um Java Runtime Environment (JRE) for Java Versão 1.5.0 ou mais recente esteja instalado em seu computador e que as variáveis de ambiente sejam configuradas como a seguir:

- A variável de ambiente `JAVA_HOME` é configurada para o diretório de instalação Java em seu computador.
- A configuração da variável de ambiente `PATH` inclui o subdiretório `bin` do diretório de instalação Java em seu computador.

### Procedimento

1. Em um shell de comando em sistemas operacionais Linux, no prompt de comandos do Windows ou na janela de comando do DB2 em sistemas operacionais Windows, execute os comandos a seguir:

   Esses comandos criam novas entradas no arquivo de configuração do driver (`db2dsdriver.cfg`) em seu computador e configuram os atributos de conexão. Você precisa executar essa etapa apenas uma vez.

   - Para uma conexão com SSL:

     ` db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode = SSL" `

     ` db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001 `  

     sendo:
     
     - `<hostname>` é o nome do host do servidor.
     - `<alias>`  é um alias que você escolhe.

   - Para uma conexão sem SSL:

     ` db2cli writecfg add -database BLUDB -host <hostname> -port 50000 `

     ` db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000 `

2. Para iniciar o CLPPlus com uma conexão com um banco de dados {{site.data.keyword.dashdbshort_notm}} que usa as entradas no arquivo `db2dsdriver.cfg`, execute o comando a seguir:

   - Ambientes do Windows: 

     `clpplus <userid>@<alias>`

   - Ambientes Linux:

     `clpplus -nw <userid>@<alias>`

     sendo:
     
     - `<userid>` é o ID de usuário das credenciais de conexão coletadas antecipadamente.
     - `<alias>` é o alias criado com o comando **db2cli writecfg**.

   A execução desse comando abre uma janela CLPPlus.

3. Na janela CLPPlus, insira sua senha. As informações do banco de dados são exibidas, seguidas por um prompt SQL. Segue a saída da amostra:

```
   Hostname = 192.0.2.0
   Database server = DB2/LINUXX8664  SQL10054
   SQL authorization ID = smith
   Local database alias = BLUDB
   Port = 50001
   
   SQL>
```

### Resultados

Agora é possível inserir comandos CLPPlus ou instruções SELECT e executar scripts para trabalhar com os dados no banco de dados.

### Exemplos

Os exemplos a seguir usam um script curto que recupera linhas da tabela de amostra `GOSALES.BRANCH`. O arquivo de script é denominado `cities.sql` e está no computador local do Windows no diretório `C:\temp`. O arquivo `cities.sql` contém o texto a seguir:

```
SET ECHO ON
SELECT branch_code, city from GOSALES.BRANCH;
```

#### Exemplo 1 

Para executar o script interativamente:

1. Inicie o CLPPlus com seu ID de usuário e o alias criado no arquivo `db2dsdriver.cfg` executando o comando a seguir:

   `clpplus <user_id>@<alias>`
2. Digite sua senha.
3. No prompt de SQL, insira o texto a seguir:

   `start C:\temp\cities.sql`

#### Exemplo 2

Inicie o CLPPlus com seu ID de usuário e o alias criado no arquivo `db2dsdriver.cfg` e execute o script em uma etapa:

`clpplus <user_id>/<password>@<alias> @C:\temp\cities.sql`

A saída de amostra do script `cities.sql` é a seguinte:

```
BRANCH_CODE CITY
----------- --------------------------------------------------
          6 Paris
          7 Milano
          9 Amsterdam
         13 Hamburg
         14 München
         15 Kista
         17 Calgary
         18 Toronto
         19 Boston
         20 Seattle
         21 Los Angeles
         22 Miami
         23 Lyon
         24 Distrito Federal
         25 Tokyo
         26 Osaka City
         28 Melbourne
         29 Bilbao
         30 Sao Paulo
         31 Kuopio
         32 Seoul
         33 Singapore

BRANCH_CODE CITY
----------- --------------------------------------------------
         34 Shanghai
         35 London
         36 Birmingham
         37 Zürich
         38 Heverlee
         39 Wien
         40 Geneve

29 rows were retrieved.
```


