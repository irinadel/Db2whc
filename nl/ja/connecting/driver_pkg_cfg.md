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

# ローカル環境の構成
{: #cfg_loc_env}

ローカル・アプリケーションやツールを {{site.data.keyword.dashdbshort_notm}} データベースに接続するには、環境を構成する必要があります。  
{: shortdesc}

## 前提条件
{: #prereq21}

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)を満たしていることを確認します。

<!-- 1. Install the Db2 driver package for your operating system.

   - [Installing on Windows](install_win.html)
   - [Installing on Linux or PowerLinux](install_linux.html)
   - [Installing on Mac OS X](install_mac.html)
2. Decide whether or not you will be using Secure Sockets Layer (SSL) to connect to your database.
3. Collect database details and connect credentials, including the host name of your server, and your database user ID and password. -->

## 手順
{: #proc21}

1. ドライバー構成ファイル `db2dsdriver.cfg` に、データベースに関する項目を追加します。

   構成ステップは、SSL を使用してデータベースに接続しようとしているかどうかに応じて異なります。

   **SSL を使用する場合**

   SSL を使用してアプリケーションやツールをデータベースに接続するには、Linux オペレーティング・システム上のコマンド・シェル、Windows コマンド・プロンプト、または DB2 コマンド・ウィンドウで以下のコマンドを入力します。 

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50001`

   `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

    ここで、

   - `<hostname>` は、サーバーのホスト名です。
   - `<alias>` は、選択した別名です。 この別名を、データベース名「`BLUDB`」と同じ名前にすることはできません。 別名にスペースを使用する場合は、その別名を二重引用符で囲みます。

   **SSL を使用しない場合**

   SSL を使用せずにアプリケーションやツールをデータベースに接続するには、Linux オペレーティング・システム上のコマンド・シェル、Windows コマンド・プロンプト、または DB2 コマンド・ウィンドウで以下のコマンドを入力します。 

   `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

   `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

    ここで、

   - `<hostname>` は、サーバーのホスト名です。
   - `<alias>` は、選択した別名です。 この別名を、データベース名「`BLUDB`」と同じ名前にすることはできません。 別名にスペースを使用する場合は、その別名を二重引用符で囲みます。

2. 以下のようにコマンド・プロンプトから **db2cli validate** コマンドを発行して、接続をテストします。

   `db2cli validate -dsn <alias> -connect -user <userid> -passwd <password>`

   ここで、 
   
   - `<alias>` は、**db2cli writecfg** コマンドを使用して作成した別名です。
   - `<userid>` は、Db2 のユーザー ID です。
   - `<password>` は、Db2 のパスワードです。

3. [*オプション*] ローカルの ODBC アプリケーションやツールをデータベースに接続できるようにするには、以下のように DSN を ODBC ドライバー・マネージャーに登録します。
 
   コマンド・ラインから以下のコマンドを実行します。 

   `db2cli registerdsn -add -dsn <alias>`

   ここで、 

   - `<alias>` は、**db2cli writecfg** コマンドを使用して作成した別名です。

   デフォルトでは、DSN はユーザー DSN として作成されます。

