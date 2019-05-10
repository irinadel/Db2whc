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

# 使用 .NET 以程式設計方式連接
{: #con_prog_net}

定義 .NET 應用程式與 {{site.data.keyword.dashdbshort_notm}} 資料庫之間的連線。
{: shortdesc}

## 必要條件
{: #prereq71}

在嘗試連接至您的 {{site.data.keyword.dashdbshort_notm}} 資料庫之前，請驗證您是否具有必要的[必備項目](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)。

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## 程序
{: #proc71}

下列步驟顯示如何使用 .NET 將您的應用程式連接至資料庫。

1. 從命令提示字元中，輸入下列指令。這些指令會在電腦的驅動程式配置檔 (`db2dsdriver.cfg`) 中建立新項目，並設定連線屬性。您只需執行此步驟一次。
        
   - 若為使用 SSL 的連線：

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     其中：

     `<hostname>`：伺服器的主機名稱。
    
     `<alias>`：您要用來建立 .NET 連線之 DSN 別名的名稱。選擇對您有意義的名稱；例如，`analytics`。 

   - 若為不使用 SSL 的連線：

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

2. [*選用*] 若要驗證資料庫的 .NET 連線，請在命令提示字元中輸入下列指令：

   `testconn40 "DATABASE=<alias>;UID=<user_id>;PWD=<password>;"`

   其中：

   `<alias>`：您在步驟 1 中使用 **db2cli writecfg** 指令所建立之 DSN 別名的名稱。
    
   `<user_id>`：您的 {{site.data.keyword.dashdbshort_notm}} 使用者 ID。 
    
   `<password>`：您用來連接至 {{site.data.keyword.dashdbshort_notm}} 資料庫的密碼。 

## 範例
{: #ex71}

下列語法所顯示的範例 C# 程式碼使用 .NET 驅動程式來建立與資料庫的連線。

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

