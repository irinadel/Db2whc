---

copyright:
  years: 2014, 2019
lastupdated: "2019-04-01"

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

# 接続オプション
{: #connect_options}

アプリケーションの接続要件に応じて、{{site.data.keyword.dashdblong}} は複数のセキュア接続オプションを提供しています。  
{: shortdesc}

## パブリック・エンドポイントへの接続 (デフォルト・オプション)
{: #pub_endpt}

他のパブリック・クラウド・サービスの場合と同様に、サービスがプロビジョンされるときに提供されるパブリック・ホスト名を使用してアプリケーションを接続できます。 データへのアクセスは、強力な認証、膨大な Db2 の許可オプションとアクセス制御、送信時および保管時の暗号化、および開発と運用に対する IBM のセキュリティーとコンプライアンスの実施によって保護されています。 オプションの IP ホワイトリストが提供されています。 IP ホワイトリストを使用可能にする場合は、IBM サポート Case を作成します。

### パブリック・エンドポイントへの接続方法
{: #pub_endpt_steps}

データウェアハウスに接続する最も簡単な方法は、ウェルカム・レターで指定されているパブリック・ホスト名を使用することです。 以下の方法で、ホスト名と資格情報を取得することもできます。

1. {{site.data.keyword.cloud_notm}} にログインし、サービス・インスタンスをクリックします。
2. **「サービス資格情報」**をクリックします。
3. **「新規資格情報」**をクリックし、**「追加」**をクリックします。
4. 資格情報の作成後、`「アクション」`列の下で、**「資格情報の表示」**をクリックします。
5. 以下の JSON 文書の例で、「hostname」、「password」、「username」の各フィールドの内容を書き留めます。 これら 3 つのコンポーネントは、パブリック・エンドポイント接続で使用します。

   ```
   {
     "hostname": "db2whoc-flex-xxxxxxx.services.dal.bluemix.net",
     "password": "DTPY7KXxhp_pKtjLSt",
     "https_url": "https://db2whoc-flex-xxxxxxx.services.dal.bluemix.net",
     "port": 50000,
     "ssldsn": "DATABASE=BLUDB;HOSTNAME=db2whoc-flex-xxxxxx.services.dal.bluemix.net;PORT=50001;PROTOCOL=TCPIP;UID=bluadmin;PWD=DTPY7KXWxhp_pKtjLSt;Security=SSL;",
     "host": "db2whoc-flex-xxxxx.services.dal.bluemix.net",
     "jdbcurl": "jdbc:db2://db2whoc-flex-xxxx.services.dal.bluemix.net:50000/BLUDB",
     "uri": "db2://bluadmin:DTPY7KXx1p_pKtjLSt@db2whoc-flex-hyftpsb.services.dal.bluemix.net:50000/BLUDB",
     "db": "BLUDB",
     "dsn": "DATABASE=BLUDB;HOSTNAME=db2whoc-flex-xxxxx.services.dal.bluemix.net;PORT=50000;PROTOCOL=TCPIP;UID=bluadmin;PWD=DTPYZunlWxhp_pKtjLSt;",
     "username": "bluadmin",
     "ssljdbcurl": "jdbc:db2://db2whoc-flex-xxxx.services.dal.bluemix.net:50001/BLUDB:sslConnection=true;"
   }

   ```

   ![{{site.data.keyword.cloud_notm}} へのパブリック・ネットワーク・アクセス](images/public_connection.png "ユーザーのクラウド接続へのグラフィカル表現")

## プライベート・エンドポイントへの接続: IBM Cloud サービス・エンドポイント
{: #priv_endpt}

{{site.data.keyword.cloud_notm}} アカウントでデプロイしたアプリケーションがあり、データベース・トラフィックがパブリック・ネットワークを介して流れることなしにそのアプリケーションをデータベースに接続したい場合は、データベースを注文する際に**「{{site.data.keyword.cloud_notm}} サービス・エンドポイント」**オプションを使用できます。 サービスがプロビジョンされるときにプライベート・ホスト名が提供され、{{site.data.keyword.cloud_notm}} アカウント内からのみそれに接続できるようになります。  

{{site.data.keyword.cloud_notm}} サービス・エンドポイント・オプションについて詳しくは、[サービス・エンドポイント: 概要](/docs/services/service-endpoint?topic=service-endpoint-about#about)を参照してください。


### IBM Cloud サービス・エンドポイントを使用したプライベート・エンドポイントへの接続方法
{: #priv_endpt_steps}

プライベート・ネットワークとエンドポイントの通信は、{{site.data.keyword.cloud_notm}} サービス・エンドポイント・サービスによって行われます。 サービス・エンドポイント・サービスは、異なる {{site.data.keyword.cloud_notm}} サービスとウェアハウス・データベースの間で、{{site.data.keyword.cloud_notm}} プライベート・ネットワーク・バックプレーンを介したネットワーク・トラフィックの迅速かつ安全な経路指定を容易にします。 このネットワーク経路指定により、データがパブリック・インターネットに出て行かないようになります。 

サービス・エンドポイントを開始するには、{{site.data.keyword.cloud_notm}} アカウントで VRF (Virtual Routing and Forwarding) が有効になっている必要があります。 アカウントで有効になるようにするには、[IBM Cloud CLI を使用したサービス・エンドポイントの使用に対するアカウントの有効化 (Enabling your account for using Service Endpoint by using IBM Cloud CLI)](/docs/services/service-endpoint?topic=service-endpoint-getting-started#cs_cli_install_steps) を参照してください。

アカウントで VRF を有効にし、サービス・エンドポイントを有効にしたら、ウェルカム・レターで説明されている指示に従います。

次に、ウェルカム・レターで指定されているプライベート・ネットワーク・アドレスを使用して、{{site.data.keyword.cloud_notm}} アカウント内から {{site.data.keyword.dashdbshort_notm}} インスタンスに接続します。

## プライベート・エンドポイントへの接続: 仮想プライベート・ネットワーク (VPN)
{: #vpn}

パブリック・インターネットにアクセスすることなしに {{site.data.keyword.cloud_notm}} の外部にあるプライベート・ネットワークにデプロイしたアプリケーションがあり、そのアプリケーションを仮想プライベート・ネットワーク (VPN) 接続を介してデータベースに接続したい場合は、サービスを注文する際、または IBM サポート Case をオープンすることによって要求を行うことができます。 IBM のネットワーク・エンジニアは、お客様のネットワーク・エンジニアによるプライベート・ネットワークと {{site.data.keyword.cloud_notm}} 間の VPN トンネルのセットアップを支援します。

### VPN を使用したプライベート・エンドポイントへの接続方法
{: #priv_endpt_vpn_steps}

パブリック・エンドポイントの背後にあるクラウド・データウェアハウスへの VPN 接続を確立するには、以下の詳細を含む [{{site.data.keyword.cloud_notm}} サポート Case を作成します](https://cloud.ibm.com/unifiedsupport/cases/add){:external}。

* **サポート・タイプ (Type of support)**: 技術的 (Technical) 
* **カテゴリー (Category)**: データベース (Databases) 
* **オファリング (Offering)**: ご使用の {{site.data.keyword.dashdbshort_notm}} インスタンスを選択します 
* **件名 (Subject)**: VPN 接続要求 
* **説明 (Description)**: 以下の必須情報を入力します
  * **顧客側 VPN ピア・アドレス (Customer-side VPN Peer Address)** (ご使用の VPN エンドポイント): `<IP Address>`
  * **顧客側暗号化ドメイン (Customer-side Encryption Domain)** (必要なものを具体的に示します – 10 アドレッシングは {{site.data.keyword.cloud_notm}} 内でバックエンド・サービス用にも使用されているため、10.0.0.0/8 は使用できません): `<Domain>`
  * **顧客側 VPN ハードウェアとバージョン (Customer-side VPN Hardware & Version)**: `<Hardware and Version number>`
  * **顧客側 VPN 連絡先 (Customer-side VPN Contact)** (技術担当者の名前と E メール・アドレス): 
    * `<Name>` 
    * `<Title>` 
    * `<Email Address>`

  **オプション (Optional)** (以下のデフォルト値は適切でない場合にのみ変更します):

  *IKE/ISAKMP パラメーター (フェーズ I)*

  * **暗号化方式 (Encryption Method)**: IKEv1
  * **IKE 暗号化 / 暗号化アルゴリズム (IKE Encryption / Encryption Algorithm)**: AES-256
  * **認証アルゴリズム (Authentication Algorithm)**: SHA1
  * **DH グループ (DH-Group)**: グループ 5 (Group 5)
  * **セキュリティー・アソシエーション存続時間 (秒) (Security Association Lifetime (seconds))**: 1日 (86400 秒）(1d (86400 seconds))

  *IPSEC パラメーター (フェーズ II)*

  * **IPsec 暗号化 / 暗号化アルゴリズム (IPsec Encryption / Encryption Algorithm)**: AES-256
  * **認証アルゴリズム (Authentication Algorithm)**: SHA1
  * **DH グループ (DH-Group)** (PF-Secrecy を使用する場合): グループ 5 (Group 5)
  * **セキュリティー・アソシエーション存続時間 (秒) (Security Association Lifetime (seconds))**: 3600 秒 (3600 seconds)

要求を受け取ると、{{site.data.keyword.cloud_notm}} 技術者は適切なファイアウォール・ポートを開き、指定された IP アドレスをホワイトリストに登録します。 要求に関するコミュニケーションや解決は、{{site.data.keyword.cloud_notm}} サポート Case チケットを使用して行われます。

![VPN を介した {{site.data.keyword.cloud_notm}} へのパブリック・ネットワーク・アクセス](images/public_connection_vpn.png "ユーザーのクラウド接続へのグラフィカル表現")
