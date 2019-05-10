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

# 使用 .NET 以编程方式连接
{: #con_prog_net}

定义 .NET 应用程序与 {{site.data.keyword.dashdbshort_notm}} 数据库之间的连接。
{: shortdesc}

## 先决条件
{: #prereq71}

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)。

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## 过程
{: #proc71}

以下步骤显示如何使用 .NET 将应用程序连接到数据库。

1. 在命令提示符处输入以下命令。这些命令将在计算机上的驱动程序配置文件 (`db2dsdriver.cfg`) 中创建新条目，并设置连接属性。此步骤只需执行一次。
        
   - 对于使用 SSL 的连接：

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     其中：

     `<hostname>`：服务器的主机名。
    
     `<alias>`：要用于建立 .NET 连接的 DSN 别名。请选择对您有意义的名称；例如，`analytics`。 

   - 对于不使用 SSL 的连接：

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

2. [*可选*]: 要验证与数据库的 .NET 连接，请在命令提示符处输入以下命令：

   `testconn40 "DATABASE=<alias>;UID=<user_id>;PWD=<password>;"`

   其中：

   `<alias>`：步骤 1 中使用 **db2cli writecfg** 命令创建的 DSN 别名。
    
   `<user_id>`：您的 {{site.data.keyword.dashdbshort_notm}} 用户标识。 
    
   `<password>`：您用于连接到 {{site.data.keyword.dashdbshort_notm}} 数据库的密码。 

## 示例
{: #ex71}

以下语法显示使用 .NET 驱动程序来建立数据库连接的样本 C# 代码。

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

