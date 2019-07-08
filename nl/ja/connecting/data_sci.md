---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-15"

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

# Data Science
{: #ds}

また、外部アプリケーションやツールを {{site.data.keyword.dashdbshort_notm}} に接続して利用し、
データをさらに管理または分析することも可能です。 
{: shortdesc}

## Watson Studio
{: #watson_studio}

IBM Watson Studio (以前の Data Science Experience) にプロジェクトを作成したら、プロジェクトにデータ資産を追加して、データを処理できるようにします。 プロジェクトのすべてのコラボレーターは自動的にプロジェクト内のデータへのアクセスを許可されます。
{: shortdesc}

データの追加方法、およびどこからデータを追加できるかは、レガシー・プロジェクトと IBM Watson プロジェクトで異なります。 IBM Watson プロジェクトは、{{site.data.keyword.Bluemix_notm}} Object Storage を使用します。 Object Storage OpenStack Swift が使用されている場合、そのプロジェクトはレガシー・プロジェクトになります。 

### IBM Watson プロジェクトで新規接続を作成するには、以下のようにします。

1. **「プロジェクトに追加」>「接続」**をクリックします。
    
2. データ・ソースを選択します。
    
3. データ・ソースに必要な接続情報を入力します。 通常は、ホスト、ポート番号、ユーザー名、およびパスワードなどの情報を入力する必要があります。
    
4. 資産は、{{site.data.keyword.dashdbshort_notm}} への接続から検出できます。それにより、その接続からのすべての表をデータ資産としてプロジェクトに追加することができます。 **「データ資産の検出 (Discover data assets)」**を選択して、プロジェクトを選択します。
    
5. **「作成」**をクリックします。 **「資産 (Assets)」**ページに接続が表示されます。

接続の作成方法、および接続データをプロジェクトに追加する方法を確認するには、このビデオを視聴してください。

<iframe class="embed-responsive-item" id="youtubeplayer" title="Create a connection and add connected data to a project" type="text/html" width="640" height="390" src="//www.youtube.com/embed/U7-gCbo4QtM?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

### レガシー・プロジェクトで新規接続を作成するには、以下のようにします。

1. プロジェクトの**「資産 (Assets)」**ページで、**「データの検出および追加 (Find and add data)」**アイコンをクリックします。
    
2. **「接続」**ペインで、**「接続の作成」**をクリックします。

3. 名前と説明を入力し、以下のように「サービス・カテゴリー」を選択します。

   **データ・サービス** = {{site.data.keyword.Bluemix_notm}} データ・サービス

   **「データ・サービス」**を選択すると、既存の {{site.data.keyword.Bluemix_notm}} データ・サービスが**「サービス・インスタンス」**リストに表示されます。

4. リストからサービスまたはデータベース・サーバーを選択します。

5. 以下のように接続情報を入力します。

   **「データ・サービス」**を選択すると、既存の {{site.data.keyword.Bluemix_notm}} データ・サービスが**「サービス・インスタンス」**リストに表示されます。
    
6. **「作成」**をクリックします。 接続は、すべてのレガシー・プロジェクトで使用可能になります。
    
7. **「接続」**ペインで、接続を選択し、**「適用」**をクリックします。

既存の接続をレガシー・プロジェクトに追加するには、以下のようにします。

1. プロジェクトの**「資産 (Assets)」**ページで、**「データの検出および追加 (Find and add data)」**アイコンをクリックします。
    
2. **「接続」**ペインで、接続を選択し、**「適用」**をクリックします。

## SPSS Statistics
{: #spss_stats}

以下の手順では、IBM® SPSS® Statistics から {{site.data.keyword.dashdbshort_notm}} データベースへの接続の作成方法について説明します。
{: shortdesc}

### 前提条件
{: #prereq11}

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)を満たしていることを確認します。

### 手順
{: #proc11}

1. SPSS Statistics で、**「ファイル」>「データベースを開く (Open Database)」> 「新規照会 (New Query)」**をクリックします。
    
2. データベース・ウィザードで、**「ODBC データ・ソースを追加」**をクリックします。
    
3. 「ODBC データ ソース アドミニストレータ」ウィンドウを使用して、以下のように {{site.data.keyword.dashdbshort_notm}} データベースの ODBC データ・ソース名 (DSN)を追加します。
        
   a. **「ユーザー DSN」**タブで、**「追加」**をクリックします。

   b. 「新規データ ソースの作成」ウィンドウで、**IBM DB2 ODBC DRIVER** という名前のドライバーを選択し、**「完了」**をクリックします。

   `IBM DB2® ODBC DRIVER - DB2COPY` などの、似た名前のドライバーを選択していないことを確認してください。 このドライバーがリストに表示されない場合は、SPSS Statistics を終了してから、ドライバーをダウンロードしてインストールしてください。 [ドライバー・パッケージ](/docs/services/Db2whc/connecting?topic=Db2whc-dr_pkg#dr_pkg)を参照してください。
        
   c. 「ODBC IBM ドライバー - 追加 (ODBC IBM Driver - Add)」ウィンドウで、データ・ソース名 (通常は接続先のデータベースの名前) を入力し、**「追加」** をクリックします。
        
   d. 「CLI/ODBC 設定」ウィンドウの**「データ・ソース」**タブで、事前に収集した[接続情報](/docs/services/Db2whc/connecting?topic=Db2whc-db_details_cxn_creds#db_details_cxn_creds)にあるユーザー ID とパスワードを入力します。
        
   e. 「詳細設定」ページで、以下のパラメーターごとに、**「追加」**をクリックして「CLI パラメーターの追加 (Add CLI Parameter)」ウィンドウを開いてステップを開始し、**「OK」**をクリックして「詳細設定」ページに戻ります。
            
   - `「データベース」`パラメーターを選択してから、**「OK」**をクリックして、「CLI/ODBC 設定」ウィンドウを開きます。 **「保留値」**フィールドに、以前に収集した接続情報にあるデータベース名を入力します。

   - `「ホスト名」`パラメーターを選択してから、**「OK」**をクリックして、「CLI/ODBC 設定」ウィンドウを開きます。 **「保留値」**フィールドに、以前に収集した接続情報にあるホスト名を入力します。

   - `「ポート」`パラメーターを選択してから、**「OK」**をクリックして、「CLI/ODBC 設定」ウィンドウを開きます。 **「保留値」**フィールドに、以前に収集した接続情報にあるポート番号を入力します。
            
   - `「プロトコル」`パラメーターを選択してから、**「OK」**をクリックして、「CLI/ODBC 設定」ウィンドウを開きます。 **「TCP/IP」**を選択します。
        
   f. **「OK」**をクリックして、「ODBC データ ソース アドミニストレータ」ウィンドウに戻ります。
        
   g. **「ユーザー DSN」**タブで、データ・ソース名を選択してから**「構成」**をクリックします。
        
   h. 「CLI/ODBC 設定」ウィンドウで、**「接続」**をクリックして接続をテストします。
            
   - 接続が正常に行われたら、**「OK」**をクリックして、「ODBC データ ソース アドミニストレータ」ウィンドウに戻り、**「OK」**をクリックしてウィンドウを終了します。
            
   - 接続が正常に行われなかった場合は、エラーをメモして訂正してから、接続を再テストします。

## SAS
{: #sas}

以下の説明では、SAS から {{site.data.keyword.dashdbshort_notm}} データベースへの接続の作成方法について説明します。
{: shortdesc}

### 前提条件
{: #prereq12}

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)を満たしていることを確認します。

### 手順
{: #proc12}

SAS から {{site.data.keyword.dashdbshort_notm}} データベースへの接続方法の手順については、以下の SAS 資料を参照してください。
- [SAS/ACCESS Interface to DB2 under UNIX and PC Hosts](https://documentation.sas.com/?docsetId=acreldb&docsetTarget=p1dzq4zjg1iycgn16l4xj9nnvibt.htm&docsetVersion=9.4&locale=en){:external}

## R 開発環境
{: #r_dev_env}

IBM Watson Studio 内に統合されている RStudio® 環境を使用する代わりに、ローカルにインストールされた独自の R 開発環境を使用することもできます。 例えば、独自の RStudio インストール済み環境を保持したり、Rcmdr や Rattle などのその他の開発ツールを使用したりすることもできます。 以下の指示では、R 開発環境を {{site.data.keyword.dashdbshort_notm}} データベースに接続する方法について説明しています。
{: shortdesc}

### 前提条件
{: #prereq13}

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)を満たしていることを確認します。

### 手順
{: #proc13}

1. ローカル R 環境で、以下のコマンドを入力して `ibmdbR` パッケージをインストールします。

   `install.packages("ibmdbR")`

   ローカル R 環境は、Comprehensive R Archive Network (CRAN) にアクセスし、`ibmdbR` パッケージとまだインストールされていない前提条件パッケージを自動的にダウンロードしてインストールします。
    
2. R 開発環境と {{site.data.keyword.dashdbshort_notm}} データベースの間の ODBC ドライバー接続を作成します。
        
   a. [データベースを ODBC データ・ソースとしてセットアップします](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_cli_and_odbc_applications.html){:external}。
        
   b. ローカルにインストールされた R 開発環境を開きます。
        
   c. R プロンプトに以下のステートメントを入力して接続を作成します。 プレースホルダーを、事前に収集した[接続情報](/docs/services/Db2whc/connecting?topic=Db2whc-db_details_cxn_creds#db_details_cxn_creds)に置き換えます。

   - ローカルにインストールされた R 開発環境が {{site.data.keyword.dashdbshort_notm}} データベース内で実行される場合は、以下のようになります。

     ```
     library(ibmdbR)
     host.name <- "placeholderForYourHostName"
     port <-"placeholderForPortNumber" # 50000 if not using SSL or 50001 if using SSL
     user.name <-"placeholderForYourUserName"
     pwd <- "placeholderForYourPassword"
     con.text <- paste("placeholderForYourDSNName;DRIVER=BLUDB",
                       ";Database=BLUDB",
                       ";Hostname=",host.name,
                       ";Port=",port,
                       ";PROTOCOL=TCPIP",
                       ";UID=", user.name,
                       ";PWD=",pwd,sep="")
     # Connect to using a odbc Driver Connection string to a remote database
     con <- idaConnect(con.text)
     ```

   - ローカルにインストールされた R 開発環境が {{site.data.keyword.dashdbshort_notm}} データベース内で実行されない場合は、以下のようになります。

     ```
     library(ibmdbR)
     driver.name <- "{placeholderForYourDriverName}"
     db.name <- "placeholderForYourDatabaseName"
     host.name <- "placeholderForYourHostName"
     port <-"placeholderForYourPort"
     user.name <-"placeholderForYourUserName"
     pwd <- "placeholderForYourPassword"
     con.text <- paste("placeholderForYourDSNName;DRIVER=",driver.name,
                       ";Database=",db.name,
                       ";Hostname=",host.name,
                       ";Port=",port,
                       ";PROTOCOL=TCPIP",
                       ";UID=", user.name,
                       ";PWD=",pwd,sep="")
     # Connect to using a odbc Driver Connection string to a remote database
     con <- idaConnect(con.text)
     ```

     **注**: 接続オブジェクトの作成に使用されるステートメントでは、`odbcConnect()` メソッドでも `odbcDriverConnect()` メソッドでもなく、`idaConnect()` メソッドが使用されます。
        
   d. 以下の R コマンドを実行して、分析パッケージを初期設定します。

   `idaInit(con)`

   e. 接続が機能しているかどうかをテストするには、以下の R コマンドを発行します。

   `idaShowTables()`

   現行スキーマ内のすべての表とビューのリストがコンソールに表示されます。

