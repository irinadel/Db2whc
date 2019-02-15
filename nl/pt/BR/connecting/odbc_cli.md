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

# Conectando-se programaticamente com ODBC ou CLI
{: #con_prog_odbc_cli}

Defina uma conexão entre um aplicativo Microsoft Windows ODBC ou CLI e um banco de dados {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

## Pré-requisitos

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](connecting.html#prereqs) necessários.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedimento

1. Em um shell de comando em sistemas operacionais Linux, no prompt de comandos do Windows ou na janela de comando do Db2 em sistemas operacionais Windows, insira os comandos a seguir:

   **Nota**: esses comandos criam novas entradas no arquivo de configuração do driver (`db2dsdriver.cfg`) em seu computador e configuram os atributos de conexão. Você precisa executar essa etapa apenas uma vez.
   
   - Para uma conexão com SSL:

     ` db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode = SSL" `

     ` db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001 `

   - Para uma conexão sem SSL:

     ` db2cli writecfg add -database BLUDB -host <hostname> -port 50000 `

     ` db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000 `

   sendo:

   `<hostname>` é o nome do host do servidor

   `<alias>` é um alias do DSN que você escolhe
    
2. [*Optional*]: To testar a conexão com o banco de dados, execute este comando por meio do prompt de comandos:

   ` db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

   sendo:

   `<alias>` é o alias do DSN que você criou com o comando **db2cli writecfg**

   `<user_id>` é das credenciais de conexão que você coletou antecipadamente

   `<password>` é das credenciais de conexão que você coletou antecipadamente

3. [*Optional*]: To registrar o nome da origem de dados (DSN) com o Microsoft ODBC Driver Manager e para trabalhar com aplicativos Microsoft ODBC, execute o comando a seguir. Por padrão, o DSN é criado como o usuário DSN.

   `db2cli registerdsn -add -dsn <alias>`

   sendo:
        
   `<alias>` é o alias do DSN que você criou com o comando **db2cli writecfg**



