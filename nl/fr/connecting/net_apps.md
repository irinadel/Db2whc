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

# Connexion à .NET à l'aide d'un programme

Définissez une connexion entre une application .NET et votre base de données {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

## Prérequis

Avant de tenter une connexion à votre base de données {{site.data.keyword.dashdbshort_notm}}, vérifiez que les [conditions requises](connecting.html#prereqs) sont remplies.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procédure

Les étapes suivantes montrent comment vous pouvez connecter votre application à la base de données avec .NET.

1. Sur une invite de commande, entrez les commandes suivantes. Ces commandes créent de nouvelles entrées dans le fichier de configuration du pilote (`db2dsdriver.cfg`) sur votre ordinateur et définissent les attributs de connexion. Cette étape ne doit être effectuée qu'une seule fois.
        
   - Pour une connexion avec SSL :

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     où :

     `<hostname>`: nom d'hôte du serveur.
    
     `<alias>` : nom d'un alias de DSN que vous souhaitez utiliser pour établir la connexion .NET. Choisissez un nom qui signifie quelque chose pour vous, par exemple : `analytics`. 

   - Pour une connexion sans SSL :

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

2. [*Optional*]: To Pour vérifier la connexion .NET à la base de données, entrez la commande suivante sur une invite de commande :

   `testconn40 "DATABASE=<alias>;UID=<user_id>;PWD=<password>;"`

   où :

   `<alias>` : nom de l'alias DSN que vous avez créé avec la commande **db2cli writecfg** à l'étape 1.
    
   `<user_id>` : votre ID d'utilisateur {{site.data.keyword.dashdbshort_notm}}. 
    
   `<password>` : mot de passe que vous utilisez pour vous connecter à votre base de données {{site.data.keyword.dashdbshort_notm}}. 

## Exemple

La syntaxe suivante montre un exemple de code C# utilisant le pilote .NET pour établir une connexion avec la base de données.

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
                    try {
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

