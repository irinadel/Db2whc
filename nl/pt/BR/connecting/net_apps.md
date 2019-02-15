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

# Conectando programaticamente com .NET
{: #con_prog_net}

Defina uma conexão entre um aplicativo .NET e o banco de dados {{site.data.keyword.dashdbshort_notm}}. 
{: shortdesc}

## Pré-requisitos

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](connecting.html#prereqs) necessários.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedimento

As etapas a seguir mostram como conectar seu aplicativo ao banco de dados com .NET.

1. Em um prompt de comandos, insira os comandos a seguir. Esses comandos criam novas entradas no arquivo de configuração do driver (`db2dsdriver.cfg`) em seu computador e configuram os atributos de conexão. Você precisa executar essa etapa apenas uma vez.
        
   - Para uma conexão com SSL:

     ` db2cli writecfg add -database BLUDB -host <hostname> -port 50001 `

     ` db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001 `

     ` db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode = SSL" `

     sendo:

     `<hostname>`: O nome do host do servidor.
    
     `<alias>`: o nome de um alias do DSN que você deseja usar para estabelecer a conexão .NET. Escolha um nome que seja significativo para você, por exemplo, `analytics`. 

   - Para uma conexão sem SSL:

     ` db2cli writecfg add -database BLUDB -host <hostname> -port 50000 `

     ` db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000 `

2. [*Optional*]: To verificar a conexão .NET com o banco de dados, insira o comando a seguir em um prompt de comandos:

   `testconn40 "DATABASE=<alias>;UID=<user_id>;PWD=<password>;"`

   sendo:

   `<alias>`: o nome do alias do DSN criado com o comando **db2cli writecfg** na etapa 1.
    
   `<user_id>`: Seu ID do usuário do  {{site.data.keyword.dashdbshort_notm}} . 
    
   `<password>`: a senha usada para se conectar ao banco de dados {{site.data.keyword.dashdbshort_notm}}. 

## Exemplo

A sintaxe a seguir mostra o código C# de amostra que usa o driver .NET para fazer uma conexão com o banco de dados.

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

