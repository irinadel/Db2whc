---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# Conectando-se ao Administrador de origem de dados ODBC
{: #con_prog_odbc_dsa}

Use a ferramenta Administrador de origem de dados ODBC da Microsoft para definir uma conexão entre um aplicativo ODBC ou CLI e um banco de dados {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

## Pré-requisitos
{: #prereq91}

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](/docs/services/Db2whc/connecting/connecting.html#prereqs) necessários.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedimento
{: #proc91}

1. Instale o  [ pacote do driver Db2 ](/docs/services/Db2whc/connecting/driver_pkg.html).

2. Abra o Administrador de origem de dados ODBC e crie um DSN do usuário ou um DSN do sistema para o pacote de drivers do Db2.
    
3. Clique em Configurações  ** Avançadas ** . Insira os parâmetros da CLI a seguir com seus valores do servidor {{site.data.keyword.dashdbshort_notm}}: **Hostname**, **Port** e **Database**.
    
4. Para uma conexão SSL, insira o parâmetro da CLI **Security** com o valor `SSL`.
    
5. Clique em  ** Aplicar **.
    
6. Para testar a conexão, retorne à página principal do Administrador de origem de dados ODBC. Clique em **Configurar** para o DSN criado. Insira o ID de usuário e a senha do servidor e clique em **Conectar**.

