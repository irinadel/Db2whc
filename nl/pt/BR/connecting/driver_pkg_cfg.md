---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# Configurando seu Ambiente Local
{: #cfg_loc_env}

Para conectar aplicativos locais e ferramentas ao banco de dados {{site.data.keyword.dashdbshort_notm}}, é necessário configurar seu ambiente.  
{: shortdesc}

## Pré-requisitos
{: #prereq21}

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) necessários.

<!-- 1. Install the Db2 driver package for your operating system.

   - [Installing on Windows](install_win.html)
   - [Installing on Linux or PowerLinux](install_linux.html)
   - [Installing on Mac OS X](install_mac.html)
2. Decide whether or not you will be using Secure Sockets Layer (SSL) to connect to your database.
3. Collect database details and connect credentials, including the host name of your server, and your database user ID and password. -->

## Procedimento
{: #proc21}

1. Inclua entradas no arquivo de configuração do driver, `db2dsdriver.cfg`, para o seu banco de dados.

   As etapas de configuração serão diferentes, dependendo se você deseja ou não se conectar ao banco de dados usando SSL:

   ** Com SSL **

   Para conectar seus aplicativos e ferramentas ao banco de dados usando SSL, insira os comandos a seguir em um shell de comando em sistemas operacionais Linux, no prompt de comandos do Windows ou em uma janela de comando do DB2: 

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50001`

   `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

    sendo:

   - `<hostname>` é o nome do host de seu servidor.
   - `<alias>`  é um alias que você escolhe. O alias não pode ser o mesmo que o nome do banco de dados, `BLUDB`. Se você desejar ter espaços no alias, coloque o alias entre aspas duplas.

   ** Sem SSL **

   Para conectar seus aplicativos e ferramentas ao banco de dados sem usar SSL, insira os comandos a seguir em um shell de comando em sistemas operacionais Linux, no prompt de comandos do Windows ou em uma janela de comando do DB2: 

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

   `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

    sendo:

   - `<hostname>` é o nome do host de seu servidor.
   - `<alias>`  é um alias que você escolhe. O alias não pode ser o mesmo que o nome do banco de dados, `BLUDB`. Se você desejar ter espaços no alias, coloque o alias entre aspas duplas.

2. Teste a conexão emitindo o comando **db2cli validate** por meio do prompt de comandos:

   `db2cli validate -dsn <alias> -connect -user <userid> -passwd <password>`

   sendo: 
   
   - `<alias>` é um alias que você criou com o comando **db2cli writecfg**.
   - `<userid>`  é o ID do usuário do Db2.
   - `<password>`  é sua senha do Db2.

3. [*Opcional*] Para ser capaz de conectar aplicativos e ferramentas ODBC locais ao banco de dados, registre o DSN com o gerenciador de driver ODBC:
 
   Execute o comando a seguir por meio de uma linha de comandos: 

   `db2cli registerdsn -add -dsn <alias>`

   sendo: 

   - `<alias>` é um alias que você criou com o comando **db2cli writecfg**.

   Por padrão, o DSN é criado como um DSN do usuário.

