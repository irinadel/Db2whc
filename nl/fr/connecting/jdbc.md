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

# Connexion à JDBC à l'aide d'un programme

Définissez une connexion entre une application Java™ et la base de données {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

## Prérequis

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](connecting.html#prereqs) sont remplies.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procédure

Dans chaque application Java, spécifiez l'ID d'utilisateur et le mot de passe en incluant la méthode **DriverManager.getConnection**, puis incluez l'une des chaînes d'URL JDBC suivantes :

- Pour une connexion avec SSL :

  `jdbc:db2://<host_name>:50001/BLUDB:sslConnection=true;`

- Pour une connexion sans SSL :

  `jdbc:db2://<host_name>:50000/BLUDB`


