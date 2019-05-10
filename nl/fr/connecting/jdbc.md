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

# Connexion à JDBC à l'aide d'un programme
{: #con_prog_jdbc}

Définissez une connexion entre une application Java™ et la base de données {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

## Prérequis
{: #prereq61}

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) sont remplies.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procédure
{: #proc61}

Dans chaque application Java, spécifiez l'ID d'utilisateur et le mot de passe en incluant la méthode **DriverManager.getConnection**, puis incluez l'une des chaînes d'URL JDBC suivantes :

- Pour une connexion avec SSL :

  `jdbc:db2://<host_name>:50001/BLUDB:sslConnection=true;`

- Pour une connexion sans SSL :

  `jdbc:db2://<host_name>:50000/BLUDB`


