---

copyright:
  years: 2014, 2019
lastupdated: "2018-11-08"

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

# データ統合
{: #data_int}

また、外部アプリケーションやツールを {{site.data.keyword.dashdbshort_notm}} に接続して利用し、
データをさらに管理または分析することも可能です。 
{: shortdesc}

## DataStage
{: #datastage}

以下の手順では、IBM® InfoSphere® DataStage® <!--version 9.1 and later -->と {{site.data.keyword.dashdbshort_notm}} データベースの間において、データベースをカタログして接続オブジェクトを定義することによって SSL を使用しない接続を定義する方法、およびサード・パーティーが発行するデジタル証明書を使用することによって SSL を使用した接続を作成する方法について説明します。
{: shortdesc}

### 前提条件
{: #prereq1}

まだデータ・サーバー・クライアントをインストールしていない場合は、ご使用のクライアント・マシンのオペレーティング・システムに適切な IBM Data Server Client <!--Version 10.5 --> をダウンロードしてインストールします。 [IBM Data Server Client ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/marketing/iwm/iwm/web/preLogin.do?source=swg-idsc97){:new_window}。

SSL プロトコルを使用して接続するには、32 ビットの GSKit V8 をダウンロードしてインストールします。 [GSKit V8 - Install, Uninstall and Upgrade instructions ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/support/docview.wss?uid=swg21631462){:new_window} で、ご使用のクライアント・マシンのオペレーティング・システムに該当する OS タブをクリックします。 以下の各オペレーティング・システムについて、GSKit インストール・ディレクトリー・パスを OS 固有の PATH 環境変数に追加していることを確認してください。

- AIX®: **LIBPATH**
   - `/usr/opt/ibm/gsk8/lib`
- Linux: **LD_LIBRARY_PATH**
    - `/usr/local/ibm/gsk8/lib`
- UNIX: **LD_LIBRARY_PATH**
    - `/opt/ibm/gsk8/lib`
- Windows: **PATH**
    - `<installation_directory>\gsk8\bin`
    - `<installation_directory>\gsk8\lib`

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](/docs/services/Db2whc/connecting/connecting.html#prereqs)を満たしていることを確認します。

### 手順
{: #proc1}

- SSL を使用して接続を作成するには、次の手順を実行します。

  1. コマンド・ラインまたは端末を開き、SSL 証明書と鍵ファイルを保管するための新しいディレクトリーを DataStage システムに作成します。

     `# /home/db2inst2> mkdir SSL`

     `# /home/db2inst2> cd SSL`

  2. {{site.data.keyword.dashdbshort_notm}} Web コンソールで、**「データベースにアプリケーションを接続する」**ページから SSL 証明書をダウンロードします。

     a. メインメニューから、**「接続」**をクリックします。
     
     b. **「SSL を使用した接続」**をクリックしてから、**「SSL 証明書 (1 KB)」**リンクをクリックします。
     
     c. ステップ 1 で作成した SSL ディレクトリーに `DigiCertGlobalRootCA.crt` 証明書を保存します。
        
  3. **gsk8capicmd_64** ユーティリティーを使用して、DataStage システムにクライアント鍵ストア・データベースを作成します。

     `# /home/db2inst2/SSL> gsk8capicmd_64 -keydb -create -db <keystore_db.kdb> -pw <ks_db_password> -stash`

     ここで、`<keystore_db.kdb>` はクライアント鍵ストア・データベースを表し、`<ks_db_password>` はクライアント鍵ストア・データベースのパスワードを表します。
        
  4. 証明書をクライアント鍵ストア・データベースに追加します。

     `# /home/db2inst2/SSL> gsk8capicmd_64 -cert -add -db <keystore_db.kdb> -pw <ks_db_password> -label BLUDB_SSL -file DigiCertGlobalRootCA.crt`

     ここで、`<keystore_db.kdb>` はクライアント鍵ストア・データベースを表し、`<ks_db_password>` はクライアント鍵ストア・データベースのパスワードを表します。
    
  5. DataStage サーバー上で DB2 クライアントを構成します。
            
     a. データベース・マネージャー内で SSL 構成パラメーターを更新します。

     `# /home/db2inst2> db2 update dbm cfg using SSL_CLNT_KEYDB /home/db2inst2/SSL/<keystore_db.kdb>`

     ここで、`<keystore_db.kdb>` はクライアント鍵ストア・データベースを表します。

     `# /home/db2inst2> db2 update dbm cfg using SSL_CLNT_STASH /home/db2inst2/SSL/<keystore_db.sth>`

     ここで、`<keystore_db.sth>` はクライアント鍵ストア・データベースのパスワード・スタッシュを表します。
            
     b. SSL セキュリティー・オプションを使用してターゲット・ノードをカタログしてから、そのターゲット・ノードで BLUDB データベースをカタログします。

     `# /home/db2inst2> db2 catalog tcpip node <node_name> remote <IP_addr_of_BLUDB_database_server> server 50001 security SSL`

     ここで、`<node_name>` はターゲット・ノードの名前を表し、`<IP_addr_of_BLUDB_database_server>` は BLUDB データベース・サーバーの IP アドレスを表します。

     `# /home/db2inst2> db2 catalog db BLUDB as <db_alias> at node <node_name>`

     ここで、`<db_alias>` は {{site.data.keyword.dashdbshort_notm}} データベースの名前です。

  6. 全員が対象の、SSL ディレクトリー内のファイルに対する読み取り権限と実行権限を追加します。 ジョブを実行する DataStage ユーザーは、Db2 データベースへの SSL 接続を行うために、これらのファイルにアクセスする必要があります。

     `# /home/db2inst2/SSL> chmod 655 /home/db2inst2/SSL/*`

  7. 次のいずれかの方法で、SSL 接続をテストします。

     - CLP を使用して接続をテストします。 次のコマンドを発行して、{{site.data.keyword.dashdbshort_notm}} データベースに接続します。

       `db2 connect to <db_alias> user <user_id>`

       ここで、`<db_alias>` は {{site.data.keyword.dashdbshort_notm}} データベースの名前で、`<user_id>` は {{site.data.keyword.dashdbshort_notm}} ユーザー ID です。パスワードの入力を求めるプロンプトが出されます。
    
     - CLI を使用して接続をテストします。 次のコマンドを発行して、{{site.data.keyword.dashdbshort_notm}} データベースに接続します。

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

        ここで、`<alias>` は **db2cli writecfg** コマンドを使用して作成した別名、`<user_id>` は {{site.data.keyword.dashdbshort_notm}} ユーザー ID、`<password>` は {{site.data.keyword.dashdbshort_notm}} パスワードです。

- SSL を使用せずに接続を作成するには、次の手順を実行してターゲットの {{site.data.keyword.dashdbshort_notm}} データベースをカタログします。

  1. クライアント・アプリケーションから接続できるように、ターゲットの {{site.data.keyword.dashdbshort_notm}} ノードをカタログします。 以下の CLP コマンドを実行します。

     `db2 catalog tcpip node <node_name> remote <IP_address_of_BLUDB_database_server> server <port_number_of_BLUDB_database>`

     ここで、`<node_name>` はノードの名前を表し、`<IP_address_of_BLUDB_database_server>` は BLUDB データベース・サーバーの IP アドレスを表し、`<port_number_of_BLUDB_database>` は BLUDB データベースのポート番号を表します。

  2. クライアント・アプリケーションから接続できるように、リモート {{site.data.keyword.dashdbshort_notm}} データベースをカタログします。 次のコマンドを実行します。

     `db2 catalog db BLUDB as <db_alias> at node <node_name>`

     ここで、`<db_alias>` は {{site.data.keyword.dashdbshort_notm}} データベースの名前を表し、`<node_name>` はノードの名前を表します。

  3. 次のいずれかの方法で、非 SSL 接続をテストします。

      - CLP を使用して接続をテストします。 次のコマンドを発行して、{{site.data.keyword.dashdbshort_notm}} データベースに接続します。

        `db2 connect to <db_alias> user <user_id>`

        ここで、`<db_alias>` は {{site.data.keyword.dashdbshort_notm}} データベースの名前で、`<user_id>` は {{site.data.keyword.dashdbshort_notm}} ユーザー ID です。パスワードの入力を求めるプロンプトが出されます。

        `db2 list tables`

      - CLI を使用して接続をテストします。 次のコマンドを発行して、{{site.data.keyword.dashdbshort_notm}} データベースに接続します。

        `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

        ここで、`<alias>` は **db2cli writecfg** コマンドを使用して作成した別名、`<user_id>` は {{site.data.keyword.dashdbshort_notm}} ユーザー ID、`<password>` は {{site.data.keyword.dashdbshort_notm}} パスワードです。

  4. 事前に収集した[接続情報](/docs/services/Db2whc/connecting/credentials.html)を使用して、DataStage クライアント内で接続を定義します。 **「パラメーター」**タブで、**「ステージング・タイプを使用した接続 (Connect using Staging Type)」**フィールドに**「DB2 Connector」**を選択しなければなりません。

     DataStage での接続の定義について詳しくは、以下の DataStage 資料のトピックを参照してください。 
     
     - [データ接続オブジェクトの手動作成 ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/SSZJPZ_11.3.0/com.ibm.swg.im.iis.ds.design.doc/topics/t_ddesref_Creating_a_Data_Connection_Object_Manually.html){:new_window}
     - [DB2 データベースへのアクセスの構成 ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/en/SSZJPZ_11.7.0/com.ibm.swg.im.iis.conn.common.usage.doc/topics/t_configuring_db2conn.html){:new_window}

## Informatica
{: #informatica}

Informatica を {{site.data.keyword.dashdbshort_notm}} に接続して、データの管理に役立てることができます。
{: shortdesc}

{{site.data.keyword.dashdbshort_notm}} を Informatica Cloud に統合する方法を確認するには、このビデオを視聴してください。

<iframe class="embed-responsive-item" id="youtubeplayer1" title="DB2 Connections - Lightening Fast How-To with Informatica Cloud" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TUiS_HstLnU?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

<!-- To configure a native Db2 connection to connect to {{site.data.keyword.dashdbshort_notm}}, perform the following steps:

1. Run the `odbcad32.exe` file from your local system.
The ODBC Data Sources Administrator dialog box appears.

2. Create the 32-bit ODBC Data Source Name using the DataDirect Db2 drivers.

3. In the ODBC DB2 Wire Protocol Setup dialog box, click **Security** tab.

4. Set the value of the `Authentication Method` property as `1 -Encrypt Password`. The following image shows the **Security** tab in the ODBC DB2 Wire Protocol Setup dialog box where you can set the `Authentication Method` property:
             
   ![ODBC Db2 Wire Protocol Driver Setup - Security tab](images/odbc_driver.png)
       
5. In the ODBC DB2 Wire Protocol Setup dialog box, click **Modify Bindings** tab.

6. Enter your user name in the Package Collection property. The following image shows the **Modify Bindings** tab in the ODBC DB2 Wire Protocol Setup dialog box where you can set the `Package Collection` property: 

   ![ODBC Db2 Wire Protocol Driver Setup - Modify Bindings tab](images/odbc_driver_2.png)
            
7. In the PowerCenter Designer, use the data source name that you created to import the metadata.

8. In the PowerCenter Workflow Manager, create the required workflow.

9. Ensure that you have the {{site.data.keyword.dashdbshort_notm}} compatible 11.x Db2 clients when you run the workflow.

**Note**: If you want to set the authentication type when you create the Db2 client catalog, you could specify the value of the `AUTHENTICATION TYPE` property as `SERVER_ENCRYPT`. -->

<!-- Watch this video to see how to integrate Db2 and Salesforce with Informatica Cloud.

<iframe class="embed-responsive-item" id="youtubeplayer2" title="Integrate Db2 and Salesforce with Informatica Cloud" type="text/html" width="640" height="390" src="//www.youtube.com/watch?v=RGTLweZvKP8" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe> -->

<!-- [Informatica ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://kb.informatica.com/howto/6/Pages/20/522402.aspx?myk=Connect%20to%20Db2){:new_window} -->

## Lift
{: #lift}

Lift を使用して、データを {{site.data.keyword.dashdbshort_notm}} にマイグレーションします。

[Lift ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://lift.ng.bluemix.net/#docs){:new_window}

## InfoSphere Data Replication
{: #idr}

IBM® InfoSphere® Data Replication <!--version 11.3.3.3-36 or later -->を {{site.data.keyword.dashdbshort_notm}} データベースに接続できます。 この機能は、SMP 環境と MPP 環境の両方に適用されます。 {{site.data.keyword.dashdbshort_notm}} のエントリー・プランには適用されません。 
{: shortdesc}

### 概要
{: #overview2}

IBM InfoSphere Data Replication を {{site.data.keyword.dashdbshort_notm}} に接続する際は、IBM InfoSphere Data Replication が {{site.data.keyword.dashdbshort_notm}} と同じ {{site.data.keyword.Bluemix_notm}} データ・センター内にあるか、{{site.data.keyword.dashdbshort_notm}} と同じ場所に配置されているのが理想です。 IBM InfoSphere Data Replication は、ローカル・サーバーからリモート {{site.data.keyword.dashdbshort_notm}} インスタンスに接続します。

{{site.data.keyword.dashdbshort_notm}} を接続ターゲットとして使用する場合、IBM InfoSphere Data Replication のパフォーマンスは、そのターゲット・エンジンを {{site.data.keyword.dashdbshort_notm}} のインスタンスから分離するネットワークの帯域幅に一部依存します。 物理的な距離もパフォーマンスに影響します。IBM InfoSphere Data Replication が可能な限り {{site.data.keyword.dashdbshort_notm}} のインスタンスの近くにあるのが理想です。 ネットワーク・トポロジーもパフォーマンスに影響します。 例えば、IBM InfoSphere Data Replication ターゲット・エンジンがターゲット・インスタンスと同じ VPN (セキュリティー・ドメイン) 内の VM 上で実行されるのが理想です。 トラバースするネットワーク・ノード (ファイアウォールやルーターなど) を可能な限り少なくすることをお勧めします。 

### 前提条件
{: #prereq2}

SSL プロトコルを使用して接続しようとしている場合は、GSKit V8 をダウンロードしてインストールします。 [GSKit V8 - Install, Uninstall and Upgrade instructions ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/support/docview.wss?uid=swg21631462){:new_window} を参照してください。 ご使用のクライアント・マシンのオペレーティング・システムに適用するオペレーティング・システム・タブをクリックします。 GSKit を Windows コンピューターにインストールしようとしている場合は、**`PATH`** 環境変数に GSKit インストール・ディレクトリー・パス (`<installation_directory>\gsk8\bin`) を指定していることを確認してください。

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](/docs/services/Db2whc/connecting/connecting.html#prereqs)を満たしていることを確認します。

SSL プロトコルを使用して接続しようとしている場合は、Web コンソールからクライアント・マシンのディレクトリーに `DigiCertGlobalRootCA.crt` SSL 証明書をダウンロードします。 証明書をダウンロードするには、**「接続」>「接続情報」**をクリックしてから**「SSL を使用した接続」**タブをクリックします。

### 手順
{: #proc2}

1. 次のいずれかの接続方法を選択してください。

   - SSL を使用して接続を作成するには、次の手順を実行します。
            
     a. 次のコマンドを発行します。

     `cd /<ssl_directory_name>/ssl`

     `/<ssl_directory_name>/ssl` は、`DigiCertGlobalRootCA.crt` SSL 証明書をダウンロードしたディレクトリーへのパスです。

     b. **GSKCapiCmd** ツールを使用して、クライアント鍵データベースと stash ファイルを作成します。 例えば、以下のコマンドを使用すると、`dashclient.kdb` というクライアント鍵データベースと、`dashclient.sth` という stash ファイルが作成されます。

     `gsk8capicmd_64 -keydb -create -db "dashclient.kdb" -pw "passw0rdpw0" -stash`

     ここで、`passw0rdpw0` はパスワードです。 **-stash** オプションにより、クライアント鍵データベースのパスと同じパスに、ファイル拡張子 `.sth` を持つ stash ファイルが作成されます。 接続時に、GSKit は stash ファイルを使用して、クライアント鍵データベースへのパスワードを取得します。
            
     c. 証明書をクライアント鍵データベースに追加します。 例えば、以下の **gsk8capicmd** コマンドを使用すると `/<ssl_directory_name>/ssl/DigiCertGlobalRootCA.crt` ファイルの証明書が `dashclient.kdb` というクライアント鍵データベースにインポートされます。

     `gsk8capicmd_64 -cert -add -db "dashclient.kdb" -pw "passw0rdpw0" -label "DigiCert" -file "/<ssl_directory_name>/ssl/DigiCertGlobalRootCA.crt" -format ascii -fips`

     d. クライアント上の `SSL_CLNT_KEYDB` と `SSL_CLNT_STASH` のデータベース・マネージャー構成パラメーターの値を更新して、クライアント鍵データベースと stash ファイルを指定します。 次に例を示します。

     `db2 update dbm cfg using SSL_CLNT_KEYDB /<ssl_directory_name>/ssl/dashclient.kdb`

     `db2 update dbm cfg using SSL_CLNT_STASH /<ssl_directory_name>/ssl/dashclient.sth`

     e. クライアント・アプリケーションから接続できるように、{{site.data.keyword.dashdbshort_notm}} ノードをカタログします。 次のコマンドを発行します。

     `db2 catalog tcpip node <node_name> remote <Db2_Warehouse_IP_address> server <port_number> security ssl`

     ここで、
                
     `<node_name>` は、ノードのご使用の名前です。

     `<Db2_Warehouse_IP_address>` は、Db2 Warehouse on Cloud サーバーの IP アドレスです。

     `<port_number>` は、SSL 接続を使用して Db2 Warehouse に接続するのに使用するポートです。 デフォルトのポートを使用しようとしている場合は、`50001` を指定してください。
            
     f. クライアント・アプリケーションから接続できるように、リモート {{site.data.keyword.dashdbshort_notm}} データベースをカタログします。 次のコマンドを発行します。

     `db2 catalog database bludb as <db_alias> at node <node_name>`

     `db_alias` は、{{site.data.keyword.dashdbshort_notm}} データベースのご使用の名前です。
            
     g. 次のいずれかの方法で、SSL 接続をテストします。
                
     - 以下のコマンドを発行して {{site.data.keyword.dashdbshort_notm}} データベースに接続し、CLP を使用した接続をテストします。

       `db2 connect to <db_alias> user <user_id>`

       ここで、`<user_id>` は、{{site.data.keyword.dashdbshort_notm}} のユーザー ID です。パスワードの入力を求めるプロンプトが出されます。
                
     - 以下のコマンドを発行して {{site.data.keyword.dashdbshort_notm}} データベースに接続し、CLI を使用した接続をテストします。

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

       ここで、`<alias>` は、**db2cli writecfg** コマンドを使用して作成した DSN 別名です。`<user_id>` は {{site.data.keyword.dashdbshort_notm}} ユーザー ID で、`<password>` は {{site.data.keyword.dashdbshort_notm}} データベースのパスワードです。
        
   - SSL を使用せずに接続を作成するには、次の手順を実行します。

     a. クライアント・アプリケーションから接続できるように、{{site.data.keyword.dashdbshort_notm}} ノードをカタログします。 次のコマンドを発行します。

     `db2 catalog tcpip node <node_name> remote <Db2_Warehouse_IP_address> server <port_number>`

     ここで、
                
     `<node_name>` は、ノードのご使用の名前です。

     `<Db2_Warehouse_IP_address>` は、{{site.data.keyword.dashdbshort_notm}} サーバーの IP アドレスです。

     `<port_number>` は、SSL 接続を使用せずに {{site.data.keyword.dashdbshort_notm}} に接続するのに使用するポートです。 デフォルトのポートを使用しようとしている場合は、`50000` を指定してください。
            
     b. クライアント・アプリケーションから接続できるように、リモート {{site.data.keyword.dashdbshort_notm}} データベースをカタログします。 次のコマンドを発行します。

     `db2 catalog database bludb as <db_alias> at node <node_name>`

     ここで、`<db_alias>` は {{site.data.keyword.dashdbshort_notm}} データベースの名前です。

     c. 次のいずれかの方法で、非 SSL 接続をテストします。

     - 以下のコマンドを発行して {{site.data.keyword.dashdbshort_notm}} データベースに接続し、CLP を使用した接続をテストします。

       `db2 connect to <db_alias> user <user_id>`

       ここで、`<user_id>` は、{{site.data.keyword.dashdbshort_notm}} のユーザー ID です。パスワードの入力を求めるプロンプトが出されます。
                
     - 以下のコマンドを発行して {{site.data.keyword.dashdbshort_notm}} データベースに接続し、CLI を使用した接続をテストします。

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

       ここで、`<alias>` は、**db2cli writecfg** コマンドを使用して作成した DSN 別名です。`<user_id>` は {{site.data.keyword.dashdbshort_notm}} ユーザー ID で、`<password>` は Db2 Warehouse on Cloud のパスワードです。
    
2. InfoSphere Data Replication 構成ツールを起動し、次の手順を実行します。 画面取りで示されている値は例です。
        
   a. **「インスタンス構成」**タブを使用して、ソース・データベースを指すソース・インスタンスを追加します。

   ![IIDR 新規インスタンス - ソース・インスタンス](images/IIDR_source_instance.jpg)

   b. **「インスタンス構成」**タブを使用して、ターゲットの Db2 データベースを指すターゲット・インスタンスを追加します。 IBM InfoSphere Data Replication 11.3.3.3-50 以降を使用していない場合は、**「リフレッシュ・ローダー・パスの指定」**チェック・ボックスを選択しないでください。

   ![IIDR 新規インスタンス - ターゲット・インスタンス](images/IIDR_target_instance.jpg)

   c. 各インスタンスを開始します。

   ![IIDR 構成ツール](images/IIDR_instances.jpg)

3. InfoSphere Data Replication 管理コンソールを起動し、アクセス・マネージャーを使用して次の手順を実行します。
        
   a. **「データ・ストア」**タブを使用して、ソース・インスタンスに接続するデータ・ストアを作成します。 Db2 データベースはもともとソース・データベースとしてサポートされていないので、**「接続パラメーター」**をクリックして、ソース・データベースのユーザーとパスワードの情報を入力しなければなりません。

   ![データ・ストア・プロパティー - ソース](images/IIDR_source_datastore.jpg)

   b. **「データ・ストア」**タブを使用して、ターゲット・インスタンスに接続するデータ・ストアを作成します。 **「接続パラメーター」**をクリックして、ユーザーとパスワードの情報を入力しなければなりません。

   ![データ・ストア・プロパティー - ターゲット](images/IIDR_target_datastore.jpg)

   c. Access Server に接続するユーザー (admin など) がいない場合は、それを行うユーザーを作成します。

   ![新規ユーザー](images/IIDR_management_user.jpg)

   d. **「アクセス・マネージャー」**タブをクリックします。
        
   e. **「データ・ストアの管理」**タブで、各データ・ストアを右クリックしてから**「ユーザーの割り当て」**をクリックして、ユーザーをソースとターゲットの両方のデータ・ストアに割り当てます。 各インスタンスにアクセスするための資格情報が正しいことを確認してください。

   ![IIDR 管理コンソール - アクセス・マネージャー](images/IIDR_management_assign_user.jpg)

### 次の作業
{: #what2}

サブスクリプションを定義して、データのレプリケーションを実行します。 詳しくは、以下を参照してください。

- [InfoSphere Data Replication からのデータのロード ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/learn_how/loaddata_iidr.html){:new_window} 

## Segment
{: #segment}

Segment を {{site.data.keyword.dashdbshort_notm}} データベースに統合することができます。 Segment は、ユーザー・データを収集し、保管し、多数のツールに経路指定する単一プラットフォームです。
{: shortdesc}

[Segment ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://segment.com/docs/destinations/db2/){:new_window}

## Data Studio
{: #data_studio}

以下の手順では、IBM® Data Studio <!--version 4.1.x -->から {{site.data.keyword.dashdbshort_notm}} データベースへの接続を作成する方法について説明しています。
{: shortdesc}

### 前提条件
{: #prereq3}

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](/docs/services/Db2whc/connecting/connecting.html#prereqs)を満たしていることを確認します。

### 手順
{: #proc3}

1. Data Studio で、**「すべてのデータベース」>「データベースへの新規接続 (New Connection to a database)」**をクリックします。

2. **「ローカル」**タブで、データベース・マネージャーとして**「DB2 for Linux, UNIX, and Windows」**を選択します。
    
3. **「一般」**タブで、以下の値を入力します。
   - *データベース*: `BLUDB`
   - *ホスト*: ホスト名。
   - *ポート*: SSL を使用しない接続の場合、`50000` と入力します。 SSL を使用した接続の場合、`50001` と入力します。 
   - *ユーザー名*: ログインに使用するユーザー名。
   - *パスワード*: ログインに使用するパスワード。

4. SSL 接続の場合、**「オプション」**タブをクリックしてから、**「追加」**をクリックします。 `sslConnection` プロパティーに、`true` と指定します。

5. [*Optional*]: Click **「テスト接続」**をクリックして、接続が成功したことを確認します。

## Data Server Manager (DSM)
{: #dsm}

IBM® Data Server Manager と {{site.data.keyword.dashdbshort_notm}} データベースの間を接続すると、Data Server Manager の Web コンソールからデータベースをモニターしたり管理したりできます。 
{: shortdesc}

### 前提条件
{: #prereq4}

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](/docs/services/Db2whc/connecting/connecting.html#prereqs)を満たしていることを確認します。

### 手順
{: #proc4}

<!--The connection procedure was tested on Data Server Manager version 1.1. The same procedure applies to all of the other versions of the Data Server Manager software.
-->
接続を作成するには、次の手順を実行します。

1. Data Server Manager Web コンソールにログインします。
    
2. Data Server Manager の Web コンソールで、**「セットアップ」>「データベース接続」**に移動します。
    
3. ![円の中の + 符号](images/icon_R_plus.gif) アイコンをクリックして、データベース接続を追加します。 **「データベース接続」**タブの下の**「データベース接続の追加」**ページで、以下のフィールドに必要な情報を入力します。

   - *データベース接続名*: この名前は、Data Server Manager にとって固有でなければなりません。
   - *データ・サーバー・タイプ*: ドロップダウン・メニューから**「DB2 for Linux, UNIX, and Windows」**を選択します。
   - *データベース名*: `BLUDB`
   - *ホスト名*: {{site.data.keyword.dashdbshort_notm}} ホスト名を入力します。 
   - *ポート番号*: SSL を使用しない接続の場合、`50000` と入力します。 SSL を使用した接続の場合、`50001` と入力します。 
   - *JDBC セキュリティー*: ドロップダウン・メニューから**「平文パスワード」**を選択します。
   - *ユーザー ID*: {{site.data.keyword.dashdbshort_notm}} ユーザー ID 
   - *パスワード*: {{site.data.keyword.dashdbshort_notm}} パスワード 

4. SSL を使用した接続の場合、**「JDBC 拡張プロパティー」**タブを選択します。 以下のフィールドに必要な情報を入力します。

   - *プロパティー*: `sslConnection`
   - *値*: `true`

    **「追加」**ボタンをクリックします。 **「データベースの接続」**タブを選択します。
    
5. **「テスト接続」**ボタンをクリックして、接続をテストします。 接続が正常に行われたら、**「OK」**をクリックします。

## InfoSphere Data Architect
{: #ida}

以下の手順では、InfoSphere® Data Architect <!--version 9.1.x --> から {{site.data.keyword.dashdbshort_notm}} データベースへの接続を作成する方法について説明しています。
{: shortdesc}

### 前提条件
{: #prereq5}

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](/docs/services/Db2whc/connecting/connecting.html#prereqs)を満たしていることを確認します。

### 手順
{: #proc5}

1. InfoSphere Data Architect の「データ・ソース・エクスプローラー」ビューで、**「データベース接続」**を右クリックして、**「新規」**を選択します。
    
2. **「ローカル」**タブで、データベース・マネージャーとして**「DB2 for Linux, UNIX, and Windows」**を選択します。
    
3. **「一般」**タブで、以下の値を入力します。

   - *データベース*: `BLUDB`
   - *ホスト*: 事前に収集したホスト名。
   - *ポート*: SSL を使用しない接続の場合、`50000` と入力します。 SSL を使用した接続の場合、`50001` と入力します。 
   - *ユーザー名*: 事前に収集したユーザー ID。
   - *パスワード*: 事前に収集したパスワード。

4. SSL 接続の場合、**「オプション」**タブをクリックします。 `sslConnection` プロパティーを入力して、`true` の値を指定します。 **「追加」**をクリックします。
    
5. [*Optional*]: Click **「テスト接続」**をクリックして、接続が成功したことを確認します。

## Aginity Workbench
{: #aginity_wb}

以下の手順では、Aginity Workbench <!--4.3 -->を {{site.data.keyword.dashdbshort_notm}} データベースに接続する方法を説明します。 Aginity Workbench を使用して、IBM PureData for Analytics (Netezza) データ・モデルおよびデータを {{site.data.keyword.dashdbshort_notm}} にマイグレーションできます。
{: shortdesc}

### 前提条件
{: #prereq6}

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](/docs/services/Db2whc/connecting/connecting.html#prereqs)を満たしていることを確認します。

### 手順
{: #proc6}

1. Aginity Workbench をダウンロードしてインストールします。

2. 前もって記録しておいた接続情報から ODBC DSN を特定します。

3. Aginity Workbench を起動します。 データベース接続ダイアログ・ボックスが自動的に開かない場合は、ツールバーの**「接続」**をクリックして開きます。

4. [データベース接続を確立します ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.aginity.com/documentation/WB/dashDB/Default.htm#Aginity_Topics/Aginity_Workbench/Database_Connection_Dialog_Box.htm){:new_window}。 前もって記録しておいた接続情報にあるホスト名、ユーザー ID、およびパスワードを使用します。

## CLPPlus
{: #clpplus}

Command line processor plus (CLPPlus) は、Db2 ドライバー・パッケージに含まれています。 CLPPlus は、{{site.data.keyword.dashdbshort_notm}} データベースに接続するために使用できるコマンド行インターフェースを提供します。 CLPPlus を使用して、ステートメント、スクリプト、およびコマンドを定義、編集、および実行することができます。
{: shortdesc}

### 前提条件
{: #prereq7}

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](/docs/services/Db2whc/connecting/connecting.html#prereqs)を満たしていることを確認します。

CLPPlus を使用するには、ソフトウェア開発キット (SDK) または Javaランタイム環境 (JRE) for Java バージョン 1.5.0 以降がコンピューターにインストールされていること、および環境変数が以下のように設定されていることを確認してください。

- `JAVA_HOME` 環境変数が、コンピューターの Java インストール・ディレクトリーに設定されている。
- `PATH` 環境変数設定に、コンピューターの Java インストール・ディレクトリーの `bin` サブディレクトリーが含まれている。

### 手順
{: #proc7}

1. Linux オペレーティング・システムのコマンド・シェル、Windows コマンド・プロンプト、または Windows オペレーティング・システムの DB2 コマンド・ウィンドウに、以下のコマンドを実行します。

   これらのコマンドは、コンピューター上のドライバー構成ファイル (`db2dsdriver.cfg`) に新規エントリーを作成し、接続属性を設定します。 このステップは 1 回だけ実行する必要があります。

   - SSL を使用する接続の場合:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`  

     ここで、
     
     - `<hostname>` は、サーバーのホスト名です。
     - `<alias>` は、選択した別名です。

   - SSL を使用しない接続の場合:

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

2. `db2dsdriver.cfg` ファイルのエントリーを使用する {{site.data.keyword.dashdbshort_notm}} データベースへの接続を使用して CLPPlus を開始するには、次のコマンドを実行します。

   - Windows 環境: 

     `clpplus <userid>@<alias>`

   - Linux 環境:

     `clpplus -nw <userid>@<alias>`

     ここで、
     
     - `<userid>` は前もって収集しておいた接続資格情報の中のユーザー ID です。
     - `<alias>` は **db2cli writecfg** コマンドで作成したエイリアスです。

   以下のコマンドを実行すると、CLPPlus ウィンドウが開きます。

3. CLPPlus ウィンドウで、パスワードを入力します。 データベース情報が表示され、次いで SQL プロンプトが表示されます。 出力例を次に示します。

```
   Hostname = 192.0.2.0
   Database server = DB2/LINUXX8664  SQL10054
   SQL authorization ID = smith
   Local database alias = BLUDB
   Port = 50001
   
   SQL>
```

### 結果
{: #results7}

これで、CLPPlus コマンドまたは SELECT ステートメントを入力してスクリプトを実行することにより、データベース内のデータを処理することができるようになりました。

### 例

以下の例では、サンプル表 `GOSALES.BRANCH` から行を取得する短いスクリプトを使用します。 スクリプト・ファイルの名前は `cities.sql` で、これはローカル Windows コンピューターの `C:\temp ディレクトリー`にあります。 `cities.sql` ファイルには、以下のテキストが含まれています。

```
SET ECHO ON
SELECT branch_code, city from GOSALES.BRANCH;
```

#### 例 1 

スクリプトを対話式に実行する:

1. 以下のコマンドを実行して、`db2dsdriver.cfg` ファイルに作成したユーザー ID と別名を使用して CLPPlus を開始します。

   `clpplus <user_id>@<alias>`
2. パスワードを入力します。
3. SQL プロンプトで、以下のテキストを実行します。

   `start C:&#xa5;temp&#xa5;cities.sql`

#### 例 2

ユーザー ID および `db2dsdriver.cfg` ファイル内に作成したエイリアスを使用して CLPPlus を開始し、ステップ 1 のスクリプトを実行します。

`clpplus <user_id>/<password>@<alias> @C:\temp\cities.sql`

`cities.sql` スクリプトの出力例を以下に示します。

```
BRANCH_CODE CITY
----------- --------------------------------------------------
          6 Paris
          7 Milano
          9 Amsterdam
         13 Hamburg
         14 München
         15 Kista
         17 Calgary
         18 Toronto
         19 Boston
         20 Seattle
         21 Los Angeles
         22 Miami
         23 Lyon
         24 Distrito Federal
         25 Tokyo
         26 Osaka City
         28 Melbourne
         29 Bilbao
         30 Sao Paulo
         31 Kuopio
         32 Seoul
         33 Singapore

BRANCH_CODE CITY
----------- --------------------------------------------------
         34 Shanghai
         35 London
         36 Birmingham
         37 Zürich
         38 Heverlee
         39 Wien
         40 Geneve

29 rows were retrieved.
```


