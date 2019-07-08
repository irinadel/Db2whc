---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-24"

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

# データ可視化/BI
{: #data_vis_bi}

また、外部アプリケーションやツールを {{site.data.keyword.dashdbshort_notm}} に接続して利用し、
データをさらに管理したり分析したりすることも可能です。 
{: shortdesc}

## Cognos Analytics
{: #cognos}

オンプレミス・データベース内のデータではなく、クラウド内のデータに対して IBM Cognos® レポートを実行できます。 データを {{site.data.keyword.dashdbshort_notm}} データベースにロードした後、JDBC ドライバーをセットアップしてから、Cognos 管理ツールを使用してデータベース接続を作成します。 <!--These instructions explain how to connect to the database from Cognos version 10.2.1.-->
{: shortdesc}

接続の作成方法を確認するには、このビデオを視聴してください。

<iframe class="embed-responsive-item" id="youtubeplayer" title="Creating a connection from Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TRUEPVHGi0s?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

詳しくは、[Connecting Cognos Analytics](https://www.ibm.com/support/knowledgecenter/en/SSEP7J_11.0.0/com.ibm.swg.ba.cognos.ug_cra.doc/c_create_ds.html#create_ds){:external} を参照してください。

## Looker
{: #looker}

Looker を {{site.data.keyword.dashdbshort_notm}} データベースに接続できます。 Looker は、ビジネス・インテリジェンス・アプリケーションでありかつビッグデータ分析プラットフォームで、これを使用してリアルタイム・ビジネス・アナリティクスを探索、分析、および共有することができます。
{: shortdesc}

[Looker の接続](https://docs.looker.com/setup-and-management/connecting-to-db){:external}

## Tableau
{: #tableau}

以下の手順では、Tableau を {{site.data.keyword.dashdbshort_notm}} データベースに接続する方法について説明しています。Tableau Desktop<!--version 8.x--> に適用していますが、その他の Tableau ツールでも同様のステップを使用できます。
{: shortdesc}

### 前提条件
{: #prereq8}

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)を満たしていることを確認します。

### 手順
{: #proc8}

1. Tableau Desktop で、データベース接続に使用するツールでウィンドウまたはページを開きます。
2. 開始ページから、**「データに接続 (Connect to data)」**をクリックします。
3. **データ・ソース**のリストから、データベース接続に使用するデータ・ソースまたはドライバーを選択します。 リストの**「サーバー上 (On a server)」**セクションで、**「IBM Db2」** を選択します。
4. **「IBM DB2 接続 (IBM DB2 Connection)」**ウィンドウで、以下の表を使用して接続情報を入力します。

| Tableau フィールド | Db2 接続情報フィールド |
|---------------|-----------------------------------|
| ステップ 1: サーバー名の入力 | ホスト名 |
| ステップ 2: ポート | ポート番号 |
| ステップ 3: サーバー上のデータベースの入力 | データベース名 |
| ユーザー名 | ユーザー ID |
| パスワード | パスワード |
{: caption="表 1. Tableau 内の接続情報のフィールド" caption-side="top"}

5. **「接続」**をクリックして、接続を確立します。 Tableau には、データに接続するためのいくつかのオプションがあります。 {{site.data.keyword.dashdbshort_notm}} データベースをフル活用するには、**「ライブ接続 (Connect Live)」**オプションを選択します。

## Microsoft Excel
{: #excel}

以下の手順では、Microsoft Excel <!--2010-->を {{site.data.keyword.dashdbshort_notm}} データベースに接続する方法について説明します。
{: shortdesc}

### 前提条件
{: #prereq9}

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)を満たしていることを確認します。

Db2 ドライバー・パッケージか IBM® Data Server Driver Package をローカル・コンピューターにインストールしていなければなりません。 

**制限事項**: Excel と {{site.data.keyword.dashdbshort_notm}} の間の接続は、Windows オペレーティング・システムに限りサポートされています。

### 手順
{: #proc9}

1. Web コンソールで、**「SQL の実行」**ページに移動します。
    
2. エディターのテキスト・ボックスで、1 つ以上の SELECT ステートメントを入力します。

3. いずれかの実行オプションをクリックします。

4. **「Excel ODC ファイル」**をクリックします。

5. `BLUExcel.odc` ファイルをダウンロードして Excel で開きます。 セキュリティー通知が表示されたら、**「有効にする」**をクリックします。

6. **「開く」**をクリックして、{{site.data.keyword.dashdbshort_notm}} データベースに接続します。 **「DB2 データベースに接続 (Connect To DB2 Database)」**ダイアログ・ボックスが開きます。

7. {{site.data.keyword.dashdbshort_notm}} へのログインに使用するユーザー ID とパスワードを入力します。 ユーザー ID とパスワードを入手するには、Web コンソールで**「接続」**をクリックするか、Web コンソールで**「接続」>「接続情報」**をクリックします。

8. 接続モードが `Share` (共有) であることを確認して**「OK」**をクリックします。

### 結果
{: #results2}

Excel スプレッドシートに照会結果が表示されます。 同じ結果が「結果」ビューアーにも表示されます。 この時点で、Excel を使用してグラフやレポートを生成したりデータを分析したりできます。 これを行う方法、および Web コンソールからデータに対して SQL 照会を実行する方法について詳しくは、以下を参照してください。 
- [チュートリアル: Excel を使用したグラフおよびレポートの生成](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/explore_excel_reports.html){:external}
- [Excel での分析](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/exploreexcel.html){:external}

## Esri ArcGIS for Desktop
{: #esri_arcgis}

Esri ArcGIS for Desktop <!--version 10.3.1 -->を {{site.data.keyword.dashdbshort_notm}} データベースに接続してから、地理空間データの分析や視覚化に使用できます。
{: shortdesc}

### 前提条件
{: #prereq10}

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)を満たしていることを確認します。

Db2 ドライバー・パッケージか IBM® Data Server Driver Package をコンピューターにインストールしていなければなりません。

### 手順
{: #proc10}

1. 事前に収集した[接続情報](/docs/services/Db2whc/connecting?topic=Db2whc-db_details_cxn_creds#db_details_cxn_creds)から ODBC DSN データを判別します。

2. 新規接続を作成します。
      
   a. ArcCatalog カタログ・ツリーで、「データベース接続」ノードを開いて、**「データベース接続の追加」**をクリックします。
        
   b. 「データベース接続」ウィザードで、以下のようにします。
   - 「データベース・プラットフォーム」ドロップダウン・リストから、**「DB2」**を選択します。
   - **「データ・ソース」**フィールドに以下のストリングを入力します。
     ```
     HostName=<hostname>;Port=<port>;Database=<database>;
     CLIENTBUFFERSUNBOUNDLOBS=1;LOBCACHESIZE=50000000;
     FET_BUF_SIZE=256K  
     ```

     ここで、`<hostname>`、`<port>`、および `<database>` は、以前に書き留めていたホスト名、ポート番号、およびデータベース名を表すプレースホルダーです。
            
   - 認証タイプとして**データベース認証**を選択します。
            
   - ご使用のユーザー名とパスワード (以前に書き留めておいたユーザーID とパスワード) を対応するフィールドに指定します。
            
   - **「OK」**を押します。
        
     ![データベース接続ウィザード](images/2_gs_conn.jpg "データベース接続ウィザード")

### 結果
{: #results3}

これで、Esri ArcGIS for Desktop の ArcCatalog コンポーネントが {{site.data.keyword.dashdbshort_notm}} データベースに接続されました。 


