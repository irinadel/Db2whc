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

# .NET を使用したプログラムによる接続

.NET アプリケーションと {{site.data.keyword.dashdbshort_notm}} データベースの間の接続を定義します。 
{: shortdesc}

## 前提条件

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](connecting.html#prereqs)を満たしていることを確認します。

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## 手順

以下のステップは、.NET を使用してアプリケーションをデータベースに接続する方法を示しています。

1. コマンド・プロンプトから、以下のコマンドを入力します。 これらのコマンドは、コンピューター上のドライバー構成ファイル (`db2dsdriver.cfg`) に新規エントリーを作成し、接続属性を設定します。 このステップは 1 回だけ実行する必要があります。
        
   - SSL を使用する接続の場合:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     ここで、

     `<hostname>`: サーバーのホスト名。
    
     `<alias>`: .NET 接続を確立するために使用する DSN 別名の名前。何を指すのかがわかる名前にしてください (例、`analytics`)。 

   - SSL を使用しない接続の場合:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

2. [*Optional*]: To データベースへの .NET 接続を検証するには、コマンド・プロンプトから以下のコマンドを実行します。

   `testconn40 "DATABASE=<alias>;UID=<user_id>;PWD=<password>;"`

   ここで、

   `<alias>`: ステップ 1 で **db2cli writecfg** コマンドを使用して作成した DSN 別名の名前。
    
   `<user_id>`: {{site.data.keyword.dashdbshort_notm}} のユーザー ID。 
    
   `<password>`: {{site.data.keyword.dashdbshort_notm}} データベースに接続するために使用するパスワード。 

## 例

以下の構文は、.NET ドライバーを使用してデータベースへの接続を行うサンプルの C# コードです。

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

