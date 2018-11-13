---

copyright:
  years: 2014, 2018
lastupdated: "2018-09-25"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Conectando programaticamente com JDBC

Defina uma conexão entre um aplicativo Java™ e o banco de dados {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

## Pré-requisitos

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](connecting.html#prereqs) necessários.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedimento

Em cada aplicativo Java, especifique o ID do usuário e a senha incluindo o método **DriverManager.getConnection** e, em seguida, inclua uma das sequências URL JDBC a seguir:

- Para uma conexão com SSL:

  ` jdbc:db2: //<host_name>: 50001/BLUDB :sslConnection=true; `

- Para uma conexão sem SSL:

  ` jdbc:db2: //<host_name>: 50000/BLUDB `


