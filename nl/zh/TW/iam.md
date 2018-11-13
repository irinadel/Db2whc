---

copyright:
  years: 2014, 2018
lastupdated: "2018-09-18"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}

# {{site.data.keyword.Bluemix_notm}} 上的 Identity and Access Management (IAM)
{: #iam}

Identity and Access Management (IAM) 可讓您安全地鑑別使用者以進行平台服務，以及跨 {{site.data.keyword.Bluemix_notm}} 平台一致地控制資源的存取。例如，只使用您的 IBMid 單一登入 {{site.data.keyword.Bluemix_notm}} 時，您可以存取任何服務主控台及其應用程式，而不必個別登入其中每一個。
{: shortdesc}

## 是否已在實例上啟用 IAM？
{: #enabled}

一段時間後，將啟用 {{site.data.keyword.Bluemix_notm}} 上的 {{site.data.keyword.dashdblong}} 受管理資料庫實例，以使用 IAM 進行存取控制。若要檢查是否已在實例上啟用 IAM ，請執行下列查詢：

`SELECT CASE WHEN VALUE = 'IBMIAMauth' THEN 1 ELSE 0 END AS IAM_ENABLED FROM SYSIBMADM.DBMCFG WHERE NAME = 'srvcon_gssplugin_list'`

如果 **IAM_ENABLED** 的回覆值為 1，表示已在實例上啟用 IAM。

## {{site.data.keyword.Bluemix_notm}} IAM 的特性
{: #features}

下列 IAM 特性是針對具有兩種類型之支援身分的 {{site.data.keyword.dashdbshort_notm}} 受管理服務來實作：

**IBM ID**

必須先透過主控台或 REST API，將具有 IBMid 的使用者新增至每一個資料庫服務實例，然後這些使用者才能連接至特定的資料庫服務實例。就像非 IBMid 使用者一樣，必須在新增 IBMid 使用者時，同時輸入資料庫服務實例的使用者 ID。此使用者 ID 在資料庫服務實例內必須是唯一的。這個使用者 ID 也是資料庫內的授權 (AUTH) ID。資料庫管理者可以根據 AUTH ID 授與及撤銷許可權。

**服務 ID**

服務 ID 識別服務或應用程式的方式，與使用者 ID 識別使用者的方式類似。服務 ID 是可供應用程式用來向 {{site.data.keyword.Bluemix_notm}} 服務進行鑑別的 ID。服務 ID 代表來自擁有 IBMid 的個別實體。因此，可以授與資料庫內服務 ID 特有的不同權限和許可權。服務 ID 沒有密碼。必須為每一個服務 ID 建立一個 API 金鑰，服務 ID 才能連接至資料庫服務實例。如需服務 ID 的相關資訊，請參閱：[簡介 {{site.data.keyword.Bluemix_notm}} IAM 服務 ID 及 API 金鑰 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/blogs/bluemix/2017/10/introducing-ibm-cloud-iam-service-ids-api-keys/){:new_window}。

## 用戶端連線和使用者登入
{: #connect}

**必備項目**：Db2 Client 11.1 版 FP3 以及更新版本

下列方法可用於 IAM 鑑別：

**存取記號**

應用程式可以使用 API 金鑰，透過 REST API 直接從 IAM 服務取得存取記號。如需相關資訊，請參閱[使用 API 金鑰取得 {{site.data.keyword.Bluemix_notm}} IAM 記號 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.bluemix.net/docs/iam/apikey_iamtoken.html#iamtoken_from_apikey){:new_window}。存取記號的預設有效期為 60 分鐘。如果記號過期， Db2 伺服器將不容許建立連線。建立連線之後，不會檢查記號是否到期。就像在 IAM 整合之前一樣，連線將保持連接狀態，直到應用程式中斷連線或連線由於其他原因而終止為止。

```
curl -k -X POST \
  --header "Content-Type: application/x-www-form-urlencoded" \
  --header "Accept: application/json" \
  --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
  --data-urlencode "apikey=<apikey>" \
  "https://iam.bluemix.net/identity/token"
```

存取記號會識別資料庫的 IBMid 使用者或服務 ID。資料庫伺服器會在接受存取記號之前驗證其是否有效。如果應用程式需要連接多個資料庫服務實例或其他 {{site.data.keyword.Bluemix_notm}} 服務實例，這是最佳方法，因為它會使 IAM 服務的通訊減至最少以驗證存取記號。

**API 金鑰**

可為每一個 IBMid 使用者或服務 ID 建立多個 API 金鑰。通常，會為單一應用程式建立每一個 API 金鑰。只要將擁有 IBMid 或服務 ID 當作使用者新增至資料庫服務實例，就會容許應用程式連接至相同的資料庫服務實例。API 金鑰在資料庫內具有與擁有 IBMid 或服務 ID 相同的權限及許可權。如果不應容許應用程式再連接至資料庫，您可以移除對應的 API 金鑰。這種鑑別方法在應用程式中需要比使用存取記號更少的變更，因為它不需要與 IAM 服務直接互動。如需建立及管理 API 金鑰的相關資訊，請參閱：[管理使用者 API 金鑰 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.bluemix.net/docs/iam/userid_keys.html#userapikey){:new_window}。

**IBMid/密碼**

IBMid/密碼可用來登入主控台，也可以在應用程式內以容許使用者 ID/密碼的相同方式來使用此 IBMid/密碼。聯合 IBMid 時會發生異常狀況，因為無法重新導向至組織的登入頁面。不過，應用程式建立與資料庫服務實例連線的建議方法是使用存取記號。

## 支援的介面
{: #sup-if}

支援下列資料庫用戶端介面：

* [ODBC](#odbc-clpplus)
* [CLPPLUS](#odbc-clpplus)
* [JDBC](#jdbc)

### ODBC 及 CLPPLUS
{: #odbc-clpplus}

如需使用 IAM 鑑別將 ODBC 應用程式或指令行用戶端 (CLPPLUS) 連接至 Db2 伺服器，首先需要在 `db2dsdriver.cfg` 配置檔中執行下列指令，來配置資料來源名稱 (DSN)：

`db2cli writecfg add -dsn <dsn_alias> -database <database_name> -host <host_name_or_IP_address> -port 50001 -parameter "Authentication=GSSPLUGIN;SecurityTransportMode=SSL"`

`db2dsdriver.cfg` 配置檔是 XML 檔，通常位於 `sqllib/cfg` 目錄，其中包含 DSN 別名及其內容的清單。

下列 `db2dsdriver.cfg` 配置檔範例顯示用來建立資料庫服務實例連線的配置。此配置檔提供 DSN 別名、資料庫名稱、主機名稱（或 IP 位址），以及**鑑別**類型及 **SecurityTransportMode** 參數值：

```
<?xml version="1.0" encoding="UTF-8" standalone="no" ?>
<configuration>
        <dsncollection>
        <dsn alias="<data_source_name>" name="bludb" host="<host_name_or_IP_address>" port="50001">
            <parameter name="Authentication" value="GSSPLUGIN"/>
            <parameter name="SecurityTransportMode" value="SSL"/>
        </dsn>
        </dsncollection>
        <databases>
            <database name="bludb" host="<host_name_or_IP_address>" port="50001"/>
        </databases>
</configuration>
```

* ODBC 連線字串可以包含下列其中一項：

    **存取記號**

    `DSN=<dsn>;ACCESSTOKEN=<access_token>`

    **API 金鑰**

    `DSN=<dsn>;APIKEY=<api_key>`

    **IBMid/密碼**
    
    `DSN=<dsn>;UID=<ibmid>;PWD=<password>`

    若為 ODBC，可在 `db2dsdriver.cfg` 配置檔在應用程式的連線字串中，指定 **AUTHENTICATION=GSSPLUGIN**。

* CLPPLUS connect 指令可以包含下列其中一項：

    **存取記號**

    在 CLPPLUS 命令提示字元或 Script 中執行下列指令，以連接至 DSN 別名 (`@<data_source_name>`)，並傳遞存取記號：

    `connect @<data_source_name> using(accesstoken <access_token_string>)`

    **API 金鑰**

    在 CLPPLUS 命令提示字元或 Script 中執行下列指令，搭配 API 金鑰以連接至 DSN 別名 (`@<data_source_name>`)：

    `connect @<data_source_name> using(apikey <api-key-string>)`

    **IBMid/密碼**

    在 CLPPLUS 命令提示字元或 Script 中執行下列指令，搭配 IBMid/密碼以連接至 DSN 別名 (`@<data_source_name>`)：

    `connect <IBMid>/<password>@<data_source_name>`

    如需使用 CLPPLUS 連接至 DSN 別名的詳細資料，請參閱：[CLPPlus 中的 DSN 別名 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/SSEPGG_11.1.0/com.ibm.swg.im.dbclient.clpplus.doc/doc/c0057148.html){:new_window}。

### JDBC
{: #jdbc}

支援「第 4 類 JDBC 驅動程式」進行 IAM 鑑別。

下列範例顯示三種方法的連線 Snippet：

**存取記號**

```
DB2SimpleDataSource dataSource;

dataSource.setDriverType( 4 );
dataSource.setDatabaseName( "BLUDB" );
dataSource.setServerName( "<host_name_or_IP_address>" );
dataSource.setPortNumber( 50001 );
dataSource.setSecurityMechanism( com.ibm.db2.jcc.DB2BaseDataSource.PLUGIN_SECURITY );
dataSource.setPluginName( "IBMIAMauth" );
dataSource.setAccessToken( "<access_token>" );
Connection conn = dataSource.getConnection( );
```

**API 金鑰**

```
DB2SimpleDataSource dataSource;

dataSource.setDriverType( 4 );
dataSource.setDatabaseName( "BLUDB" );
dataSource.setServerName( "<host_name_or_IP_address>" );
dataSource.setPortNumber( 50001 );
dataSource.setSecurityMechanism( com.ibm.db2.jcc.DB2BaseDataSource.PLUGIN_SECURITY );
dataSource.setPluginName( "IBMIAMauth" );
dataSource.setApiKey( "<api_key>" );
Connection conn = dataSource.getConnection( );
```

**IBMid/密碼**

```
DB2SimpleDataSource dataSource;

dataSource.setDriverType( 4 );
dataSource.setDatabaseName( "BLUDB" );
dataSource.setServerName( "<host_name_or_IP_address>" );
dataSource.setPortNumber( 50001 );
dataSource.setSecurityMechanism( com.ibm.db2.jcc.DB2BaseDataSource.PLUGIN_SECURITY );
dataSource.setPluginName( "IBMIAMauth" );
Connection conn = dataSource.getConnection( "<user_ID>", "<password>" );
```

## 主控台使用者體驗
{: #console-ux}

服務主控台登入頁面具有使用您的 IBMid 及密碼登入的選項。按一下**透過 IBMid 登入**按鈕之後，會將使用者導向至要在其上輸入密碼的 IAM 登入頁面。鑑別完成時，會將使用者重新導向回到主控台。資料庫管理者必須先透過主控台或 REST API，將 IBMid 使用者新增至每一個資料庫服務實例，然後這類登入才能成功。就像非 IBMid 使用者一樣，必須在新增 IBMid 使用者時，同時輸入資料庫服務實例的使用者 ID。使用者 ID 在資料庫服務實例內必須是唯一的。此使用者 ID 也是資料庫內的授權 (AUTH) ID。

## REST API 體驗
{: #api}

已加強 {{site.data.keyword.dashdbshort_notm}} REST API，也可接受先前接受資料庫服務所產生的存取記號之函數的 IAM 存取記號。

* 若要新增 IBMid 使用者，請執行下列範例 API 呼叫：

  `curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid>","ibmid":"<userid>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"`

  **附註**：`"id"` 及 `"ibmid"` 的 `<userid>` 值不得相同。這兩個不同 ID 無論如何都不會鏈結在一起。

* 若要移轉現有的非 IBMid 資料庫使用者（例如，`abcuser`），並讓他們成為 IBMid 使用者，請先執行下列範例 API 呼叫來刪除非 IBMid 使用者 I D：

  `curl --tlsv1.2 -X DELETE "https://<IPaddress>/dbapi/v3/users/abcuser" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json"`

  接下來，執行下列範例 API 呼叫，以重新新增其 IBMid 與前一個使用者 ID (`abcuser`) 相同的使用者：

  `curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"abcuser","ibmid":"abcuser@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"`

  因為使用者 ID (`abcuser`) 對於該使用者的新 IBMid 仍然相同，所以授與使用者的資料庫許可權保持不變。如果現有非 IBMid 資料庫使用者的清單需要進行移轉，以讓他們成為 IBMid 使用者，則您需要對每一個使用者執行前一對 API 呼叫。

* 若要一次新增多個新的 IBMid 使用者，請建立一個批次檔，列出下列範例 API 呼叫，每一個使用者一個範例 API 呼叫：

  ```
  curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid1>","ibmid":"<userid1>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"
  curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid2>","ibmid":"<userid2>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"
  .
  .
  .
  ```

如需服務 API 的詳細資料，請參閱：[{{site.data.keyword.dashdbshort_notm}} REST API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://ibm.biz/db2whc_api){:new_window}。

## IBMid 聯合
{: #fed}

若要使用您自己的身分提供者（例如 LDAP），首先必須聯合您的 LDAP 伺服器與 IBMid。如需聯合 LDAP 伺服器與 IBMid 的相關指示，請參閱：[IBMid Enterprise Federation Adoption Guide ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://ibm.ent.box.com/notes/78040808400?s=nhuzrhlsn0ly338zddomx329tlpmfghc){:new_window}。在完成 IBMid 聯合，而且資料庫管理者將容許的使用者新增至資料庫服務實例之後，這些使用者可以使用其公司使用者 ID 及密碼來登入主控台。或者，這些使用者可以使用代表其使用者 ID 的存取記號或 API 金鑰，透過其中一個支援的資料庫用戶端介面來連接至資料庫服務實例。

## 限制
{: #restrictions}

下列是 IAM 鑑別的相關限制：

* 只有透過 SSL 連線，才支援連接至 Db2 伺服器之 Db2 用戶端的 IAM 鑑別。
* 支援 IBMid 聯合，以容許自訂使用者管理入口網站或伺服器用於鑑別。這類支援不包括任何群組聯合。
* 不支援資料庫聯合的 IAM 鑑別。
* 不支援透過 CLPPlus 執行 IDA 及使用者定義的延伸 (UDX) 指令。
* 不支援「第 2 類 JDBC 驅動程式」。




