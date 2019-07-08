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

# Connessione programmatica con .NET
{: #con_prog_net}

Definisci una connessione tra un'applicazione .NET e il tuo database {{site.data.keyword.dashdbshort_notm}}. 
{: shortdesc}

## Prerequisiti
{: #prereq71}

Prima di tentare di collegarti al tuo database {{site.data.keyword.dashdbshort_notm}}, verifica di avere i [prerequisiti](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) necessari.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedura
{: #proc71}

La seguente procedura mostra come collegare la tua applicazione al database con .NET.

1. Da un prompt di comandi, immetti i seguenti comandi: Questi comandi creano nuove voci nel file di configurazione del driver (`db2dsdriver.cfg`) sul tuo computer e impostano gli attributi di connessione. Hai bisogno di eseguire questo passo solo una volta.
        
   - Per una connessione con SSL:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     dove:

     `<hostname>` il nome host del server.
    
     `<alias>`: il nome di un alias DSN che vuoi utilizzare per stabilire la connessione .NET. Scegli un nome che sia per te significativo; ad esempio, `analytics`. 

   - Per una connessione senza SSL:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

2. [*Optional*]: To verifica la connessione .NET al database, immetti il seguente comando nel prompt dei comandi:

   `testconn40 "DATABASE=<alias>;UID=<user_id>;PWD=<password>;"`

   dove:

   `<alias>`: il nome dell'alias DSN che hai creato con il comando **db2cli writecfg** nel passo 1.
    
   `<user_id>`: il tuo ID utente {{site.data.keyword.dashdbshort_notm}}. 
    
   `<password>`: la password che hai utilizzato per il collegamento al tuo database {{site.data.keyword.dashdbshort_notm}}. 

## Esempio
{: #ex71}

La seguente sintassi mostra il codice C# di esempio che utilizza il driver .NET per effettuare una connessione al database.

```
using System;
using IBM.Data.DB2;

namespace dotNetSSLTest
{
    class Program
    {
        static void Main(string[] args)
        {
            DB2Command MyDB2Command = null;
            // Use the dsn alias that you defined in db2dsdriver.cfg with the db2cli writecfg command in step 1.
            String MyDb2ConnectionString = "database=alias;uid=userid;pwd=password;"; 
            DB2Connection MyDb2Connection = new DB2Connection(MyDb2ConnectionString);
            MyDb2Connection.Open();
            MyDB2Command = MyDb2Connection.CreateCommand();
            MyDB2Command.CommandText = "SELECT branch_code, city from GOSALES.BRANCH";
            Console.WriteLine(MyDB2Command.CommandText);

            DB2DataReader MyDb2DataReader = null;
            MyDb2DataReader = MyDB2Command.ExecuteReader();
            Console.WriteLine("BRANCH\tCITY");
            Console.WriteLine("============================");
            while (MyDb2DataReader.Read())
            {
                for (int i = 0; i <= 1; i++)
                {
                    try
                    {
                        if (MyDb2DataReader.IsDBNull(i))
                        {
                            Console.Write("NULL");
                        }
                        else
                        {
                            Console.Write(MyDb2DataReader.GetString(i));
                        }
                    }
                    catch (Exception e)
                    {
                        Console.Write(e.ToString());
                    }
                    Console.Write("\t"); 

                }
                Console.WriteLine("");
            }
            MyDb2DataReader.Close();
            MyDB2Command.Dispose();
            MyDb2Connection.Close();
        }
    }
}
```

