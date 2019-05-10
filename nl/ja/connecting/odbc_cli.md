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

# ODBC または CLI を使用したプログラムによる接続
{: #con_prog_odbc_cli}

Microsoft Windows ODBC または CLI アプリケーションと {{site.data.keyword.dashdbshort_notm}} データベースの間の接続を定義します。
{: shortdesc}

## 前提条件
{: #prereq81}

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)を満たしていることを確認します。

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## 手順
{: #proc81}

1. Linux オペレーティング・システムのコマンド・シェル、Windows コマンド・プロンプト、または Windows オペレーティング・システムの Db2 コマンド・ウィンドウに、以下のコマンドを入力します。

   **注**: これらのコマンドは、コンピューター上のドライバー構成ファイル (`db2dsdriver.cfg`) に新規エントリーを作成し、接続属性を設定します。 このステップは 1 回だけ実行する必要があります。
   
   - SSL を使用する接続の場合:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

   - SSL を使用しない接続の場合:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

   ここで、

   `<hostname>` は、サーバーのホスト名です。

   `<alias>` は、選択する DSN 別名です。
    
2. [*Optional*]: To データベースへの接続をテストするには、コマンド・プロンプトから次のコマンドを実行します。

   `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

   ここで、

   `<alias>` は、**db2cli writecfg** コマンドを使用して作成した DSN 別名です。

   `<user_id>` は前もって収集しておいた接続資格情報の中のパスワードです。

   `<password>` は前もって収集しておいた接続資格情報の中のパスワードです。

3. [*Optional*]: To Microsoft ODBC Driver Manger にデータ・ソース名 (DSN) を登録し、Microsoft ODBC アプリケーションと連携させるには、次のコマンドを実行します。 デフォルトでは、DSN はユーザー DSN として作成されます。

   `db2cli registerdsn -add -dsn <alias>`

   ここで、
        
   `<alias>` は、**db2cli writecfg** コマンドを使用して作成した DSN 別名です。



