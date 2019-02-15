---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# データベースの詳細と接続資格情報
{: #db_details_cxn_creds}

ローカル開発環境を構成し、アプリケーションやツールを {{site.data.keyword.dashdbshort_notm}} データベースに接続するには、データベースの詳細と接続資格情報を知っている必要があります。
{: shortdesc}

## データベースの詳細
{: #db_details}

アプリケーションやツールをデータベースに接続するのに必要な、データベースの重要な詳細情報には以下があります。

- *ホスト名* - サーバーのホスト名。
- *ポート番号* - データベース・マネージャーで TCP/IP 通信に使用されます。 (Secure Socket Layer (SSL) を使用する接続と非 SSL 接続とでは、別個のポート番号を使用してサービスがプロビジョニングされることに注意してください。)

   必要に応じて、ホスト名を指定して ping コマンドか nslookup コマンドを使用し、サーバーの IP アドレスを取得できます。
- *データベース名* - Db2 データベース名。通常、BLUDB。

## 接続資格情報
{: #cxn_creds}

資格情報には次の 3 つのタイプがあります。

- *IBMid* - {{site.data.keyword.Bluemix_notm}} を使用する場合、これは {{site.data.keyword.Bluemix_notm}} へのログインに使用する ID です。 これは、アプリケーションやツールを Db2 Warehouse on Cloud データベースに接続するために使用するものではありません。
- *Db2 データベース資格情報* - アプリケーションやツールをデータベースに接続するのに使用できるデータベース・ユーザー ID とパスワードを使用して、サービスがプロビジョニングされます。
- *管理者が作成したユーザー* - 一部の {{site.data.keyword.dashdbshort_notm}} プランでは、管理ユーザーが新しいユーザーを作成できるようになっています。 これらの管理者が作成したユーザー ID とパスワードを使用すると、Web コンソールの URL に直接ログインし、アプリケーションやツールから Db2 データベースに接続できます。

## データベースの詳細と接続資格情報の入手先
{: #location}

以下の場所からこの情報を収集できます。

- *管理者* - Db2 インスタンスの所有者や管理者でない場合は、データベースの詳細と接続資格情報を管理者から入手できます。
- *Db2 Web コンソール* - Web コンソール内でデータベースの詳細と資格情報を入手できます。
- {{site.data.keyword.Bluemix_notm}} を使用している場合: 
   
   - *{{site.data.keyword.Bluemix_notm}} ダッシュボード* - {{site.data.keyword.Bluemix_notm}} ダッシュボードでサービスを表示する場合は、「サービス資格情報」域で、データベース・ユーザー ID やパスワードに加えてデータベースの詳細を表示できます。
   - *`VCAP_SERVICES`* - `VCAP_SERVICES` は、{{site.data.keyword.Bluemix_notm}} の環境変数であり、データベースの詳細と資格情報が JSON 形式で含まれています。 {{site.data.keyword.Bluemix_notm}} ダッシュボードでサービスのサービス資格情報を表示すると、`VCAP_SERVICES` の内容が表示されます。 サービスにその他の {{site.data.keyword.Bluemix_notm}} サービスかアプリをバインドすると、その他のサービスかアプリケーションが `VCAP_SERVICES` を読み取ってデータベースの詳細と資格情報にプログラマチックにアクセスできます。
