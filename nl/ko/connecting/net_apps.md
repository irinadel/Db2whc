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

# .NET을 사용하여 프로그래밍 방식으로 연결
{: #con_prog_net}

.NET 애플리케이션과 {{site.data.keyword.dashdbshort_notm}} 데이터베이스 간의 연결을 정의합니다. 
{: shortdesc}

## 전제조건
{: #prereq71}

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)이 있는지 확인하십시오.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## 프로시저
{: #proc71}

다음 단계는 .NET을 사용하여 데이터베이스에 애플리케이션을 연결하는 방법을 보여줍니다.

1. 명령 프롬프트에서 다음 명령을 입력하십시오. 이 명령은 컴퓨터의 드라이버 구성 파일(`db2dsdriver.cfg`)에 새 항목을 작성하고 연결 속성을 설정합니다. 이 단계는 한 번만 수행해야 합니다.
        
   - SSL을 사용하는 연결의 경우:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     여기서,

     `<hostname>`: 서버의 호스트 이름입니다.
    
     `<alias>`: .NET 연결을 설정하는 데 사용할 DSN 별명의 이름입니다. 의미 있는 이름을 선택하십시오(예: `analytics`). 

   - SSL을 사용하지 않는 연결의 경우:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

2. [*선택사항*]: 데이터베이스에 대한 .NET 연결을 확인하려면 명령 프롬프트에서 다음 명령을 입력하십시오.

   `testconn40 "DATABASE=<alias>;UID=<user_id>;PWD=<password>;"`

   여기서,

   `<alias>`: 1단계에서 **db2cli writecfg** 명령을 사용하여 작성한 DSN 별명의 이름입니다.
    
   `<user_id>`: {{site.data.keyword.dashdbshort_notm}} 사용자 ID입니다. 
    
   `<password>`: {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하는 데 사용하는 비밀번호입니다. 

## 예
{: #ex71}

다음 구문은 .NET 드라이버를 사용하여 데이터베이스에 대한 연결을 작성하는 샘플 C# 코드를 보여줍니다.

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

