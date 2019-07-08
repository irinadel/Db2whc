---

copyright:
  years: 2014, 2019
lastupdated: "2018-06-15"

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

# IBM PureData System for Analytics (Netezza) からのマイグレーション
{: #pda}

{{site.data.keyword.Bluemix_notm}} Mass Data Migration Service (MDMS) を使用して、大規模な (約 25 TB 以上) IBM PureData Systems for Analytics (Netezza) データベースから、{{site.data.keyword.Bluemix_notm}} 上の完全管理された {{site.data.keyword.dashdblong}} データベースにデータをマイグレーションできます。

MDMS は、テラバイト単位からペタバイト単位までのデータを {{site.data.keyword.Bluemix_notm}} に物理的に転送するための高速かつシンプルで安全な方法を提供します。 MDMS は、120 TB の使用可能な記憶容量を備えたモバイル・ストレージ・デバイスです。 このデバイスによって、高いコスト、長い転送時間、セキュリティー上の懸念など、転送に関わる一般的な課題を単一サービスですべて克服できます。
{: shortdesc}

![Mass Data Migration Service デバイスの表示](images/mdms.svg)

## デバイスの要求時に必要になる情報
{: #prereq}

1. ストレージ・デバイスのネットワーク設定
   - 静的 IP アドレス
   - データ転送を有効にするためのネットマスク
2. リモート・コンピューターのネットワーク設定
   - 静的 IP アドレス
   - ネットマスク 
   - ユーザー・インターフェース (UI) にアクセスするためのデフォルト・ゲートウェイ
3. クラウド・オブジェクト・ストレージのダウンロード宛先 <br/>
   要求フォームの入力を完了するには、少なくとも 1 つの {{site.data.keyword.cos_full}} アカウントと、米国クロス・リージョンまたは米国南部のロケーションに少なくとも 1 つのバケットを保持している必要があります。まだ {{site.data.keyword.cos_full_notm}} アカウントがない場合は、アカウントを作成してから MDMS デバイスを申請してください。 詳しくは、[{{site.data.keyword.cos_full}} について](/docs/services/cloud-object-storage?topic=cloud-object-storage-about#about){:external}を参照してください。
   {: important}

## ステップ 1: 要求の作成
{: #create-req}

1. ユーザー固有の資格情報を使用して、[{{site.data.keyword.slportal}}](https://control.softlayer.com/){:external} にログインします。
2. ナビゲーション・バーから**「ストレージ」>「データ・マイグレーション」>「大量データ・マイグレーション (Mass Data Migration)」**を選択して、MDMS ランディング・ページにアクセスします。
3. **「デバイスの要求 (Request Device)」**をクリックして、注文フォームを開きます。
4. **「大量データ・マイグレーション (Mass Data Migration)」**注文フォームの各フィールドに入力します。
   - **配送先住所 (Shipping Address)**: このフォームは事前に入力されておらず、各フィールドが編集可能です。 デバイスの配送の受け取り人の名前を「宛先 (Attention)」フィールドに入力します。 配送場所を選択するときは、デバイスの重量 (ケース込みで 30 kg (66 ポンド)) やアクセスのことを考慮に入れてください。 <br/> (**注**: デバイスには、移動のためのホイールとポップアップ・ハンドルが付いています。)
   - **マイグレーションの主要な連絡先 (Key Migration Contacts)**: このフォームは事前に入力されていません。 どのフィールドも編集可能です。 複数の人を追加できます。
   - **データ・センター・ネットワーク構成 (Data Center Network Configuration)**: 配送前に MDMS デバイスの Eth3 ポートを事前プロビジョニングするためのネットワーク構成の詳細情報を入力します。
   - **データ・オフロードの宛先 (Data Offload Destination)**: リストから既存のターゲット・アカウントを選択します。
   - **要求者名 (Request Name)**: 注文を追跡しやすくするように名前を入力します。
5. 提示された各サービスのご使用条件を読んでから、**「契約書を読み、そのすべての条件に同意します: 大量データ・マイグレーションのサービス契約書 (I have read and agree to the full terms of the Mass Data Migration Agreement)」**チェック・ボックスを選択します。
6. **「要求する (Place Request)」**をクリックして、要求を送信します。 **「キャンセル」**をクリックすると、フォームが完全に破棄され、MDMS ランディング・ページに戻ります。

## ステップ 2: 準備と配送
{: #prep-ship}

要求を送信した後、要求チケットの状況は*「要求の処理中 (Processing Request)」*と表示されます。 要求の処理が完了すると、{{site.data.keyword.IBM}} が次の利用可能なデバイスの事前構成を開始し、[「要求」](https://control.softlayer.com/storage/mdms){:external}グリッドの状況が*「デバイスの準備中 (Prepping Device)」*になり、その後、*「配送待機中 (Awaiting Shipment)」*になります。*「配送待機中 (Awaiting Shipment)」*状況になった要求は取り消すことができません。 

デバイスは配送業者によって集荷され、お客様のロケーションに送られます。 この時点で、要求の状況は*「デバイス配送済み (Device Shipped)」*に更新されます。 [「要求」](https://control.softlayer.com/storage/mdms){:external}グリッドの**「注文の詳細 (Order Details)」**セクションで追跡番号を確認できます。

## ステップ 3: 受け取りと接続
{: #rec-con}

<!-- **[Editor's note: What to keep from this section immediately below?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
1. The device arrives pre-configured for you. Basic [powering/connectivity instructions](docs/infrastructure/mass-data-migration/user-instructions.html) are included.  **[Editor's note: Are the instructions included in the MDMS package? If so, are they different from the instructions found with the "powering/connectivity" link?]**<br/>
  **Note**: User name and storage pool password is provided separately. Check the **Request Details** in your [Requests](https://control.softlayer.com/storage/mdms){:external} grid for the credentials.
2. Point your browser to the static IP address that you provided in the order form. **[Editor's note: Is this done on PDA? What system is the static IP address for?]**
3. Log in. Enter password to unlock the empty storage pool. **[Editor's note: How is this done?]**<br/>
   **Note**: See the **Request Details** of your [Requests](https://control.softlayer.com/storage/mdms){:external} grid for the password.
4. Mount the NFS share on your server. **[Editor's note: How is this done?]**
5. Rerun your DataShuttle inventory to ensure any new files are captured. **[Editor's note: Is "DataShuttle inventory" a command that is run on PDA?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& -->

### 概要

{{site.data.keyword.cloud}} Mass Data Migration デバイスは、マウント可能なネットワーク・ファイル・システム (NFS) 共有または FileNet Content Federation Services (CFS) 共有を提供できるポータブル・ストレージ・デバイスです。このデバイスの管理には、Web ブラウザー・インターフェースを使用します。 このデバイスがお客様のデータ・センターに配送されたら、オンサイトでデータをロードし、{{site.data.keyword.BluSoftlayer_full}} データ・センターに送り返してください。その後、弊社がお客様の {{site.data.keyword.cos_full}} アカウントにデータをロードします。

### 電源

デバイスには、C13-US 電源コード ([IEC 60320](https://en.wikipedia.org/wiki/IEC_60320){:external}) が付いています。米国以外の場所でデバイスを使用する場合は、電源アダプターが必要になる可能性があります。

MDMS デバイスは、標準的なすべての電力範囲に対応しています。
![電力範囲](/images/PowerRating.png)

### イーサネット接続

2 つのイーサネット接続を作成する必要があります。 1 つは、ブラウザーでデバイスを管理するための接続、もう 1 つは、ソース・データと同じサブネットでデータを移動するための接続です。

このデバイスのどちらのポートも RJ45 に対応していて、CAT6A ケーブルが同梱されています。 RJ45 から変換する場合の SFP+ 銅線用のアダプターも用意されています。 このアダプターは、すべてのメーカーのスイッチに対応しています。 配送用のふたの底面にあるポケットにアダプターが入っています。

- Eth1 (1GbE-B) はデバイス管理用です。したがって、IP アドレス構成にゲートウェイを指定する必要があります。 これは、デバイスの電源を入れた後に LCD 画面に表示されます ([IP アドレスの構成](#ip_cfg)セクションを参照してください)。

- Eth3 (10GbE-B) はデータ転送用です。 この接続は、ソース・データと同じサブネットで行いますが、必要であればサーバーに直接接続することも可能です。

イーサネット接続で別のフォーム・ファクターが必要な場合は、お客様の側でコンバーターを用意してください。

### ステップバイステップの操作手順

1. MDMS デバイスは、IP アドレス、ユーザー名、ロックされたストレージ・プール、NFS 共有が事前に構成された状態で届けられます。 ユーザーのパスワードとストレージ・プールのパスワードは、E メールで別途通知されます。

2. デバイスの最適な設置場所を決めます。電源とイーサネット接続 (1GbE と 10GbE) の両方に届く距離で、できるだけ周囲に人が近づかない場所を選択してください。

3. 接続のためにデバイスを配置します。 移送ケースに入れたままでも使用できます。 デバイスが室温の状態で、結露がないことを確認してください。 収納ケースのふたの裏にある電源ケーブルを使用して、電源に接続します。 デバイスの電源をオンにします。<br/>
    電源スイッチは 2 つあります。
    {: note}

    ![電源スイッチ](/images/MDMSPowerSwitch.png "電源スイッチは丸で囲まれている")
    ポータブル・ケースからデバイスを取り出す必要はありません。
    {: note}

4. 収納ケースのふたから CAT6A ケーブルを取り出して、以下の図に示す Eth3 (10GbE-B) ポートに接続します。
    ![Eth1 ポートと Eth3 ポートの場所](/images/MDMSNewEth1and3.png "Eth1 ポートと Eth3 ポートの場所が強調表示されている")

5. 付属の CAT6A を SFP+ アダプターに接続し、それを 10Gb スイッチに接続します。

6. Eth3 用に構成されている IP アドレスにブラウザーからアクセスできる場合 (`https://<your_Eth3_IP_Address>`) は、次のステップに進みます。 

   できない場合は、Eth1 (1GbE-B) ポートに接続します。 ブラウザーを開いて、`https://<your_Eth1_IP_Address>` と入力します。 ご使用のネットワーク構成に合った適切な Eth1 IP アドレスを入力してください。 証明書の例外は、そのまま受け入れます。<br/>
   Eth3 または Eth1 の IP 設定を変更する必要がある場合は、[IP アドレスの構成](#ip_cfg) セクションを参照してください。
   {: note}

7. 通知されたユーザー名とパスワードを使用してログインします。<br/>
    ![ログイン・ダイアログ](/images/Login.png "ログイン・ダイアログ")

8. ワークフロー・ウィザードに具体的な項目へのアクセスが表示されます。通常は、左から右の順に使用します。<br/>
    ![ ワークフロー・アイコン](/images/workflow.png "ワークフロー・ウィザード。ワークフロー・アイコンが表示されている") <br/>
    このワークフローは、GUI の左上にある**「ワークフロー・マネージャー (Workflow Manager)」**を使用して再度開くことができます。
    {: note}

9. 事前構成されたストレージ・プールをアクティブにします。
    - **「ストレージ・プールのロックを解除して開始 (Unlock and Start Storage Pool)」**をクリックします。
    - ストレージ・プール・パスフレーズを入力して、**「OK」**をクリックします。
    ![ストレージ・プールのアクティブ化](/images/UnlockPool.png "丸で囲まれたフィールドにパスフレーズを入力する")

10. デフォルトでは、NFS プロトコルと SMB プロトコルの両方の共有が有効になり、共有へのアクセスに関する制限はありません。 この共有 (NFS または SMB) へのアクセスを制限する場合は、共有名を右クリックし、該当するメニュー項目を選択してください。<br/>
    ![共有アクセスの制限](/images/ShareControls.png "共有アクセスの制限")

11. ストレージ・プールが有効になると、NFS 共有のマウントが可能になります。 ワークフローで**「ネットワーク共有の表示 (View Network Shares)」**をクリックすると、ネットワーク共有のビューが表示されます。 ワークフローを閉じて、共有を右クリックし、**「マウント・コマンドの表示 (View Mount Command)」**を選択すると、共有名とマウント情報が表示されます。 ソース・サーバーに共有をマウントします。 共有をマウントするときは、必ず 10 GB リンクの IP アドレスを指定してください。
    ![共有のマウント](/images/MountCommand.png "共有のマウント")

## ステップ 4: データのコピーと配送
{: #copy-ship}

<!-- &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&

1. Run the DataShuttle copy to move the data. **[Editor's note: What is "DataShuttle"? Is "DataShuttle copy" a command that is run on PDA?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& -->

1. データを NFS 共有にコピーします。 以下のいずれかの方法を選択して、Netezza データベースからデータを抽出します。
    1. 以下の **nz_backup** ユーティリティーの例を実行します。

       `/nz/support/contrib/bin/nz_backup –db <db_name> –d <target_directory>  ascii threads 4`

       **注**: `<target_directory>` は、Netezza サーバーにマウントされる MDMS デバイス上の NFS 共有です。
   
    2. 以下の CREATE EXTERNAL TABLE ステートメントの例を実行します。

       `CREATE EXTERNAL TABLE '<path_to_mdms_device>/<file_name>' SELECT * FROM <table name>`

       **注:** データ・エクスポート時に `USING` 節オプションを使用した場合、節オプションを覚えておくか、保存しておいてください。 後ほど、{{site.data.keyword.Bluemix_notm}} Object Storage から外部表をロードするプロセスでその節を再利用します。

       SQL ステートメントについて詳しくは、[CREATE EXTERNAL TABLE ステートメント](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.sql.ref.doc/doc/r_create_ext_table.html){:external}を参照してください。 

<!--       - Provide the {{site.data.keyword.Bluemix_notm}} team with the "USING" clause that was used for data export. The clause is reused during the load process on {{site.data.keyword.Bluemix_notm}}.
       - Select FORMAT = "Text"
-->

2. ワークフローで**「ネットワーク・アクティビティーの表示 (View Network Activity)」**をクリックすると、インバウンド・イーサネット・ロードが GUI に表示され、10 Gb/秒リンクでデータがデバイスに転送されるのを確認できます。
    ![アクティビティーの表示](/images/UserGuide13.png "GUI は、インバウンド・イーサネット・ロードを示す")

3. ワークフローで**「ストレージ・プールの表示 (View Storage Pools)」**をクリックすると、デバイスのストレージ使用状況と IOPS をモニターできます。
    ![ストレージ・プールの表示](/images/UserGuide14.png "GUI はストレージの使用状況を示す")

4. コピーが完了したら、システムの電源を正常にオフにします。 デバイスを電源遮断すると、ストレージ・プールもロックされます。 ワークフローで**「アプライアンスのシャットダウン... (Shutdown Appliance...)」**をクリックします。  
    ![「アプライアンスのシャットダウン」ボタン](/images/Shutdown.png "「アプライアンスのシャットダウン」UI ボタン")

5. デバイスの接続を切断します。 電源ケーブル、イーサネット・ケーブル、SFP+ アダプターをふたの裏のそれぞれの保管場所に戻します。

6. 付属の配送ラベルをデバイスに取り付けます。 荷送人に通知し、デバイスを {{site.data.keyword.BluSoftlayer_full}} データ・センターに返送します。 データ・センターにデバイスが到着すると、データは、お客様の {{site.data.keyword.cos_full_notm}} バケットにロードされます。

デバイスが {{site.data.keyword.BluSoftlayer}} チームの元に戻ると、要求の状況は*「デバイス受領済み (Device Received)」*に変わります。

## ステップ 5: オフロードとアクセス
{: #offload}

データ転送プロセス中は、要求の状況に*「データのオフロード中 (Offloading Data)」*と表示されます。 {{site.data.keyword.objectstorageshort}} バケットへのマイグレーションが完了すると、状況が再度変わります (*「オフロード完了 (Offload Complete)」*)。 Cloud Object Storage バケットへの高速オフロードが完了すると、すぐにデータにアクセスできるようになります。 

Cloud Object Storage バケットへのデータのマイグレーションが完了したら、[{{site.data.keyword.dashdbshort_notm}} データベースへのデータのインポート](#import)に進むことができます。

## ステップ 6: {{site.data.keyword.Bluemix_notm}} Object Storage からのデータのインポート
{: #import}

外部表を使用して、{{site.data.keyword.Bluemix_notm}} Object Storage から直接データをロードする場合、以下のサンプル SQL ステートメントを使用できます。

```
INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net', 
  '<S3-access-key-ID>',
  '<S3-secret-access-key>', 
  '<my_bucket>'
     )
  )      
```

**注:** 
* CREATE EXTERNAL TABLE ステートメントを使用して PureData System for Analytics (Netezza) データベースからデータを抽出するときに使用したのと同じ `USING` 節オプションを必ず使用してください。
* {{site.data.keyword.Bluemix_notm}} Object Storage の場合、HMAC 資格情報を作成するために、新規サービス資格情報を作成する際、*「インラインの構成パラメーターの追加」*フィールドに {"HMAC:true"} を指定してください。

{{site.data.keyword.Bluemix_notm}} Object Storage からデータをインポートする方法に関するガイド付きのチュートリアルについては、[IBM Db2 Warehouse on Cloud guided demo: Explore data loading](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud/){:external}を参照してください。

## ステップ 7: MDMS デバイスのデータ消去
{: #erase}

{{site.data.keyword.IBM}} は、MDMS デバイスからお客様のデータを永久に消去するために、米国国防総省が定める要件レベルのデータ・ワイプを実装しています。 消去が完了すると、要求の状況は*「消去完了 (Erase Complete)」*と表示されます。

## 追加のメモ
{: #notes}

### バケット内での固有性

オブジェクトがバケットにコピーされるとき、オブジェクト名の固有性を確保するために、ファイル・パスがプレフィックスとしてオブジェクト名に組み込まれます。 例えば、`/root/user/` フォルダー内の config.ini ファイルであれば、バケットにコピーされるとき、「root/user/config.ini」と名前変更されます。

### バケット

ターゲット・バケットが存在しない場合は、作成されます。 存在する場合は、空のバケットでなければなりません。空でないと、コピー処理ができません。

### ファイル・システム

シンボリック・リンクとハード・リンクは、スキャン・プロセスでスキップされます。

### IP アドレスの構成
{: #ip_cfg}

デバイスの LCD ディスプレイを使用して、イーサネット・ポートの IP アドレスを構成できます。 LCD ディスプレイ内をナビゲートするには、**上矢印**、**下矢印**、**esc**、および **enter** の各ボタンを使用します。 **enter** ボタンを押すと、メニューが表示され、**esc** を押すと、メニューが終了します。

![LCD 表示](/images/MDMSLCD.png "システム・コントロール表示")

IP アドレスやサブネット・マスクの編集中は、**enter** で 1 文字ずつ前に移動し、**esc** で 1 文字ずつ後に移動します。 **上矢印**と**下矢印**は、選択された位置で数字を切り替えます。

前のメニューに戻るには、**esc** を使用します。  

設定を保存するには、**「更新... (Update...)」**メニュー項目に移動し、**enter** を押します。
