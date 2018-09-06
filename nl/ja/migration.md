---

copyright:
  years: 2014, 2018
lastupdated: "2018-05-08"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# IBM Cloud へのデータのマイグレーション
{: #migration}

ローカル・ネットワーク上またはオブジェクト・ストア内 (Amazon S3 または IBM Cloud Object Storage) にある、区切り文字で区切られた形式 (CSV または TXT) のデータ・ファイルから {{site.data.keyword.dashdblong}} にデータをロードできます。 オンプレミス・システムからデータをマイグレーションすることもできます。
{: shortdesc}

## オブジェクト・ストアからのデータのロード
{: #cos}

Amazon S3 からデータをロードするには、以下のいずれかの方法を選択します。
  * {{site.data.keyword.dashdbshort_notm}} Web コンソール。 **「ロード (Load)」 > 「Amazon S3」**。 
  * 外部のテーブルから直接。 次に、SQL ステートメントの例を示します。

    ```
    INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
      (CCSID 1208 s3('s3.amazonaws.com', 
      '<S3-access-key-ID>',
      '<S3-secret-access-key>', 
      '<my_bucket>'
         )
      )      
    ```

外部表を使用して、IBM Cloud Object Storage から直接データをロードする場合、以下のサンプル SQL ステートメントを使用できます。

```
INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net', 
  '<S3-access-key-ID>',
  '<S3-secret-access-key>', 
  '<my_bucket>'
     )
  )      
```

**注:** IBM Cloud Object Storage の場合、HMAC 資格情報を作成するために、新規サービス資格情報を作成する際、*「インラインの構成パラメーターの追加」*フィールドに {"HMAC:true"} を指定してください。

## オンプレミス・システムからのデータのマイグレーション
{: #onprem}

オンプレミス・システムからデータをマイグレーションするには、データ・セットのサイズに応じて、以下のいずれかの方式を選択します。
* 25 TB 未満のデータ: [IBM Lift](#lift)
* 25 TB 以上のデータ: [IBM Cloud Mass Data Migration Service](#mdms)

### Lift
{: #lift}

Lift は、表 1 にリストされている各種データ・ソースから {{site.data.keyword.Bluemix_notm}} にデータをマイグレーションするときに無料で使用できるアプリケーションです。 

| IBM Cloud 上のターゲット DB | データ・ソース |
|------------------------------|-------------|
| IBM Db2 Warehouse on Cloud   | IBM Db2 |
|                              | IBM Db2 Warehouse |
|                              | IBM Integrated Analytics System |
|                              | IBM PureData System for Analytics |
|                              | Oracle データベース |
|                              | Microsoft SQL Server |
|                              | CSV ファイル・フォーマット |
{: caption="表 1. マイグレーションのデータ・ソース" caption-side="top"}

Lift のダウンロードとインストールについては、[Download Lift ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://lift.ng.bluemix.net/#download){:new_window} を参照してください。

Lift を使用してデータを {{site.data.keyword.Bluemix_notm}} にマイグレーションする方法に関するステップバイステップの説明については、[{{site.data.keyword.dashdblong}} へのデータ・マイグレーション ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://lift.ng.bluemix.net/#docs){:new_window}を参照してください。

### IBM Cloud Mass Data Migration Service
{: #mdms}

IBM Cloud Mass Data Migration Service (MDMS) を使用して、大規模な (約 25 TB 以上) IBM PureData Systems for Analytics (Netezza) データベースから、{{site.data.keyword.Bluemix_notm}} 上の完全管理された {{site.data.keyword.dashdblong}} データベースにデータをマイグレーションできます。

MDMS は、テラバイト単位からペタバイト単位までのデータを {{site.data.keyword.Bluemix_notm}} に物理的に転送するための高速かつシンプルで安全な方法を提供します。 MDMS は、120 TB の使用可能な記憶容量を備えたモバイル・ストレージ・デバイスです。 このデバイスによって、高いコスト、長い転送時間、セキュリティー上の懸念など、転送に関わる一般的な課題を単一サービスですべて克服できます。

![Mass Data Migration Service デバイスの表示](images/mdms.svg)

MDMS デバイスについて詳しくは、[IBM Cloud Mass Data Migration の開始 (Getting started with IBM Cloud Mass Data Migration)](/docs/infrastructure/mass-data-migration/index.html#getting-started-with-ibm-cloud-mass-data-migration){:new_window} を参照してください。

MDMS デバイスを使用して IBM PureData System for Analytics (Netezza) データベースから {{site.data.keyword.dashdblong}} データベースにデータをマイグレーションする方法については、[IBM PureData System for Analytics (Netezza) からのマイグレーション](/docs/services/Db2whc/pda_db2whc_mdms.html)を参照してください。

