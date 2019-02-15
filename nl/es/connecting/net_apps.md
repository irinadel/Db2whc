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

# Conexión mediante programa con .NET
{: #con_prog_net}

Defina una conexión entre una aplicación .NET y la base de datos de {{site.data.keyword.dashdbshort_notm}}. 
{: shortdesc}

## Requisitos previos

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](connecting.html#prereqs) necesarios.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedimiento

Los pasos siguientes le muestran cómo conectar la aplicación a la base de datos con .NET.

1. Desde un indicador de mandatos, entre los mandatos siguientes. Estos mandatos crean nuevas entradas en el archivo de configuración del controlador (`db2dsdriver.cfg`) en el sistema y establecen los atributos de conexión. Solo debe realizar este paso una vez.
        
   - Para una conexión con SSL:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     donde:

     `<hostname>`: El nombre de host del servidor.
    
     `<alias>`: El nombre de un alias de DSN que desee utilizar para establecer la conexión .NET. Elija un nombre que sea significativo para usted; por ejemplo, `analytics`. 

   - Para una conexión sin SSL:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

2. [*Opcional*] Para verificar la conexión .NET con la base de datos, especifique el mandato siguiente en un indicador de mandatos:

   `testconn40 "DATABASE=<alias>;UID=<user_id>;PWD=<password>;"`

   donde:

   `<alias>`: El nombre del alias de DSN que ha creado con el mandato **db2cli writecfg** en el paso 1.
    
   `<user_id>`: El ID de usuario de {{site.data.keyword.dashdbshort_notm}}. 
    
   `<password>`: La contraseña que utiliza para conectarse a la base de datos de {{site.data.keyword.dashdbshort_notm}}. 

## Ejemplo

La sintaxis siguiente muestra código de ejemplo C# que utiliza el controlador .NET para establecer una conexión a la base de datos.

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

