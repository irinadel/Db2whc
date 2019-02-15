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

# Connessione con ODBC Data Source Administrator
{: #con_prog_odbc_dsa}

Utilizza lo strumento Microsoft ODBC Data Source Administrator per definire una connessione tra un'applicazione CLI o ODBC e un database {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

## Prerequisiti

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](connecting.html#prereqs) necessari.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedura

1. Installa il [Pacchetto del driver Db2](driver_pkg.html).

2. Apri ODBC Data Source Administrator e crea un DSN utente o sistema per il pacchetto del driver Db2.
    
3. Fa clic su **Advanced** Settings. Immetti i seguenti parametri CLI con i relativi valori per il server {{site.data.keyword.dashdbshort_notm}}: **Hostname**, **Port** e **Database**.
    
4. Per una connessione SSL, immetti il parametro CLI **Security** con il valore `SSL`.
    
5. Fai clic su **Apply**.
    
6. Per verificare la connessione, ritorna alla pagina principale di ODBC Data Source Administrator. Fai clic su **Configure** per il DSN che hai creato. Immetti l'ID utente e la password per il server e fai clic su **Connect**.

