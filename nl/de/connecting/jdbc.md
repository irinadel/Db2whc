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

# Programmgestützte Verbindungsherstellung - JDBC

Definieren Sie eine Verbindung zwischen einer Java™-Anwendung und der {{site.data.keyword.dashdbshort_notm}}-Datenbank.
{: shortdesc}

## Voraussetzungen

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](connecting.html#prereqs) erfüllt werden. 

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Vorgehensweise

Geben Sie in den einzelnen Java-Anwendungen die Benutzer-ID und das zugehörige Kennwort an, indem Sie die Methode **DriverManager.getConnection** einbeziehen, und fügen Sie dann eine der folgenden JDBC-URL-Zeichenfolgen ein: 

- Für SSL-Verbindungen: 

  `jdbc:db2://<host_name>:50001/BLUDB:sslConnection=true;`

- Für Verbindungen ohne SSL: 

  `jdbc:db2://<host_name>:50000/BLUDB`


