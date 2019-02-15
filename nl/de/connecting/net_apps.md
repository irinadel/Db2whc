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

# Programmgestützte Verbindungsherstellung - .NET
{: #con_prog_net}

Definieren Sie eine Verbindung zwischen einer .NET-Anwendung und der {{site.data.keyword.dashdbshort_notm}}-Datenbank. 
{: shortdesc}

## Voraussetzungen

Stellen Sie sicher, bevor Sie eine Verbindung zu Ihrer {{site.data.keyword.dashdbshort_notm}}-Datenbank erstellen, dass die [erforderlichen Voraussetzungen](connecting.html#prereqs) erfüllt werden.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Vorgehensweise

Im Folgenden wird gezeigt, wie Sie Ihre Anwendung über .NET mit der Datenbank verbinden.

1. Geben Sie die im Folgenden angegebenen Befehle in einer Eingabeaufforderung ein. Mit diesen Befehlen werden neue Einträge in der Treiberkonfigurationsdatei `db2dsdriver.cfg` auf Ihrem Computer erstellt und die Verbindungsattribute festgelegt. Sie müssen diesen Schritt lediglich ein einziges Mal ausführen.
        
   - Für SSL-Verbindungen:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     Dabei gilt Folgendes:

     `<hostname>`: Der Hostname des Servers.
    
     `<alias>`: Der Name für einen DSN-Alias, der zum Herstellen einer .NET-Verbindung verwendet werden soll. Wählen Sie einen aussagekräftigen Namen aus, z. B. `analytics`. 

   - Für Verbindungen ohne SSL:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

2. [*Optional*]: To Zum Verifizieren der .NET-Verbindung zur Datenbank geben Sie den folgenden Befehl in einer Eingabeaufforderung ein:

   `testconn40 "DATABASE=<alias>;UID=<user_id>;PWD=<password>;"`

   Dabei gilt Folgendes:

   `<alias>`: Der Name des DSN-Alias, den Sie in Schritt 1 mit dem Befehl **db2cli writecfg** erstellt haben.
    
   `<user_id>`: Ihre {{site.data.keyword.dashdbshort_notm}}-Benutzer-ID. 
    
   `<password>`: Das Kennwort, das Sie für die Verbindung zu der {{site.data.keyword.dashdbshort_notm}}-Datenbank verwenden. 

## Beispiel

Die folgende Beispielsyntax enthält C#-Beispielcode, bei dem der .NET-Treiber zum Erstellen einer Verbindung zur Datenbank verwendet wird.

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
            // Verwenden Sie den DSN-Alias, den Sie in Schritt 1 mit dem Befehl 'db2cli writecfg' in der Datei 'db2dsdriver.cfg' definiert haben.
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

