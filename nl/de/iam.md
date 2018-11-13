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

# Identitäts- und Zugriffsmanagement (IAM) in {{site.data.keyword.Bluemix_notm}}
{: #iam}

Das Identitäts- und Zugriffsmanagement (IAM = Identity and Access Management) ermöglicht es Ihnen, Benutzer sicher für Plattformservices zu authentifizieren und den Zugriff auf Ressourcen auf der gesamten {{site.data.keyword.Bluemix_notm}}-Plattform konsistent zu steuern. Sie haben z. B. mit einer einzigen Anmeldung bei {{site.data.keyword.Bluemix_notm}} mit Ihrer IBMid Zugriff auf Ihre gesamten Servicekonsolen und die zugehörigen Anwendungen, ohne dass Sie sich dazu jeweils separat anmelden müssen.
{: shortdesc}

## IAM-Aktivierung bei den Instanzen
{: #enabled}

Für eine gewisse Zeit ist die Verwendung von IAM für die Zugriffssteuerung bei den in {{site.data.keyword.dashdblong}} verwalteten Datenbankinstanzen in {{site.data.keyword.Bluemix_notm}} aktiviert. Überprüfen Sie mit der folgenden Abfrage, ob IAM für Ihre Instanz aktiviert ist: 

`SELECT CASE WHEN VALUE = 'IBMIAMauth' THEN 1 ELSE 0 END AS IAM_ENABLED FROM SYSIBMADM.DBMCFG WHERE NAME = 'srvcon_gssplugin_list'`

Wird für **IAM_ENABLED** der Wert 1 zurückgegeben, ist IAM für Ihre Instanz aktiviert. 

## Features von {{site.data.keyword.Bluemix_notm}} IAM
{: #features}

Die folgenden IAM-Features werden für den in {{site.data.keyword.dashdbshort_notm}} verwalteten Service mit zwei Typen unterstützter Identitäten implementiert: 

**IBMid**

Benutzer mit einer IBMid müssen vom Datenbankadministrator über die Konsole oder die REST-API zu den einzelnen Datenbankserviceinstanzen hinzugefügt werden, damit die betreffenden Benutzer eine Verbindung zu der jeweiligen Datenbankserviceinstanz herstellen können. Beim Hinzufügen eines IBMid-Benutzers muss wie bei einem Benutzer ohne IBMid gleichzeitig auch eine Benutzer-ID für die Datenbankserviceinstanz eingegeben werden. Diese Benutzer-ID muss innerhalb der Datenbankserviceinstanz eindeutig sein. Die Benutzer-ID ist gleichzeitig auch die Berechtigungs-ID (AUTH ID) innerhalb der Datenbank. Der Datenbankadministrator kann Berechtigungen basierend auf der Berechtigungs-ID erteilen und widerrufen. 

**Service-IDs**

Eine Service-ID identifiziert einen Service bzw. eine Anwendung ebenso, wie eine Benutzer-ID einen Benutzer identifiziert. Bei Service-IDs handelt es sich um IDs, die von Anwendungen für die Authentifizierung bei einem {{site.data.keyword.Bluemix_notm}}-Service verwendet werden können. Eine Service-ID stellt eine separate Entität gegenüber der IBMid dar, unter der die ID erstellt wurde. Es können deshalb andere Berechtigungen speziell für die Service-ID in der Datenbank erteilt werden. Für Service-IDs gibt es keine Kennwörter. Für die Verbindung zu der Datenbankserviceinstanz muss für jede Service-ID ein API-Schlüssel erstellt werden. Weitere Informationen zu Service-IDs finden Sie im Abschnitt zur [Einführung in {{site.data.keyword.Bluemix_notm}}-Service-IDs und -API-Schlüssel für IAM ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/2017/10/introducing-ibm-cloud-iam-service-ids-api-keys/){:new_window}. 

## Clientverbindungen und Benutzeranmeldungen
{: #connect}

**Voraussetzung**: Db2 Client Version 11.1 ab Fixpack 3. 

Für die IAM-Authentifizierung können die folgenden Methoden verwendet werden: 

**Zugriffstoken**

Ein Zugriffstoken kann von der Anwendung über die REST-API mithilfe eines API-Schlüssels direkt beim IAM-Service abgerufen werden. Weitere Informationen hierzu finden Sie im Abschnitt [{{site.data.keyword.Bluemix_notm}}-IAM-Token mithilfe eines API-Schlüssels abrufen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net/docs/iam/apikey_iamtoken.html#iamtoken_from_apikey){:new_window}. Das Zugriffstoken läuft standardmäßig nach einem Gültigkeitszeitraum von 60 Minuten ab. Ist ein Token abgelaufen, lässt der Db2-Server das Herstellen der Verbindung nicht zu. Nach dem Herstellen der Verbindung wird die Gültigkeit des Tokens nicht überprüft. Wie bereits vor der IAM-Integration wird die Verbindung aufrechterhalten, bis sie von der Anwendung getrennt oder anderweitig beendet wird. 

```
curl -k -X POST \
  --header "Content-Type: application/x-www-form-urlencoded" \
  --header "Accept: application/json" \
  --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
  --data-urlencode "apikey=<apikey>" \
  "https://iam.bluemix.net/identity/token"
```

Ein Zugriffstoken kennzeichnet einen IBMid-Benutzer oder eine Service-ID für die Datenbank. Bevor der Datenbankserver ein Zugriffstoken akzeptiert, überprüft der Server die Gültigkeit des Tokens. Bei Anwendungen, die Verbindungen zu mehreren Datenbankserviceinstanzen oder anderen {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen herstellen, ist dies die beste Methode, da auf diese Weise der für die Validierung des Zugriffstokens erforderliche Datenaustausch mit dem IAM-Service minimiert wird. 

**API-Schlüssel**

Für jeden IBMid-Benutzer und jede Service-ID können mehrere API-Schlüssel erstellt werden. Die einzelnen API-Schlüssel werden in der Regel für eine einzelne Anwendung erstellt. Der API-Schlüssel ermöglicht es der Anwendung, eine Verbindung zu der Datenbankserviceinstanz herzustellen, sofern die zugehörige IBMid oder Service-ID als Benutzer zu derselben Datenbankserviceinstanz hinzugefügt wurde. Der API-Schlüssel verfügt in der Datenbank über dieselben Berechtigungen wie die zugehörige IBMid bzw. Service-ID. Soll die Verbindung einer Anwendung zu der Datenbank nicht mehr zulässig sein, kann der entsprechende API-Schlüssel entfernt werden. Diese Authentifizierungsmethode erfordert weniger Änderungen in der Anwendung als die Verwendung eines Zugriffstokens, da die direkte Interaktion mit dem IAM-Service entfällt. Weitere Informationen zum Erstellen und Verwalten von API-Schlüsseln finden Sie im Abschnitt [API-Schlüssel für Benutzer verwalten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.bluemix.net/docs/iam/userid_keys.html#userapikey){:new_window}. 

**Kombination aus IBMid und Kennwort**

Die Kombination aus IBMid und Kennwort kann für die Anmeldung bei der Konsole verwendet werden. Sie kann außerdem in der Anwendung auf dieselbe Weise wie eine Kombination aus Benutzer-ID und Kennwort verwendet werden. Die einzige Ausnahme besteht in Bezug auf föderierte IBMids, da keine Weiterleitung zur Anmeldeseite Ihres Unternehmens erfolgen kann. Die empfohlene Methode für das Herstellen einer Verbindung zu der Datenbankserviceinstanz durch eine Anwendung besteht jedoch in der Verwendung eines Zugriffstokens. 

## Unterstützte Schnittstellen
{: #sup-if}

Die folgenden Datenbankclientschnittstellen werden unterstützt: 

* [ODBC](#odbc-clpplus)
* [CLPPlus](#odbc-clpplus)
* [JDBC](#jdbc)

### ODBC und CLPPlus
{: #odbc-clpplus}

Bevor eine ODBC-Anwendung oder ein Befehlszeilenclient (CLPPlus) unter Verwendung der IAM-Authentifizierung eine Verbindung zu einem Db2-Server herstellen kann, muss zunächst mit dem folgenden Befehl ein Datenquellenname (DSN = Data Source Name) in einer Konfigurationsdatei namens `db2dsdriver.cfg` konfiguriert werden: 

`db2cli writecfg add -dsn <dsn_alias> -database <database_name> -host <host_name_or_IP_address> -port 50001 -parameter "Authentication=GSSPLUGIN;SecurityTransportMode=SSL"`

Bei der Konfigurationsdatei `db2dsdriver.cfg` handelt es sich um eine XML-Datei, die sich in der Regel im Verzeichnis `sqllib/cfg` befindet und eine Liste von DSN-Aliasnamen mit den zugehörigen Eigenschaften enthält. 

Die folgende Beispielkonfigurationsdatei `db2dsdriver.cfg` enthält die Konfigurationen, über die ein Verbindung zu einer Datenbankserviceinstanz hergestellt wird. Die Konfigurationsdatei liefert die Werte für den DSN-Alias, den Datenbanknamen, den Hostnamen (bzw. die IP-Adresse), den Typ der **Authentifizierung** und den Parameter **SecurityTransportMode**: 

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

* Die ODBC-Verbindungszeichenfolge kann eines der folgenden Elemente enthalten: 

    **Zugriffstoken**

    `DSN=<dsn>;ACCESSTOKEN=<access_token>`

    **API-Schlüssel**

    `DSN=<dsn>;APIKEY=<api_key>`

    **Kombination aus IBMid und Kennwort**
    
    `DSN=<dsn>;UID=<ibmid>;PWD=<password>`

    Bei ODBC-Anwendungen kann **AUTHENTICATION=GSSPLUGIN** in der Konfigurationsdatei `db2dsdriver.cfg` oder in der Verbindungszeichenfolge der Anwendung angegeben werden. 

* Der CLPPlus-Verbindungsbefehl kann eines der folgenden Elemente enthalten: 

    **Zugriffstoken**

    Stellen Sie die Verbindung zum DSN-Alias (`@<data_source_name>`) her und übergeben Sie das Zugriffstoken, indem Sie den folgenden Befehl in der CLPPlus-Eingabeaufforderung oder einem Script ausführen:


    `connect @<data_source_name> using(accesstoken <access_token_string>)`

    **API-Schlüssel**

    Stellen Sie die Verbindung zum DSN-Alias (`@<data_source_name>`) mit einem API-Schlüssel her, indem Sie den folgenden Befehl in der CLPPlus-Eingabeaufforderung oder einem Script ausführen: 

    `connect @<data_source_name> using(apikey <api-key-string>)`

    **Kombination aus IBMid und Kennwort**

    Stellen Sie die Verbindung zum DSN-Alias (`@<data_source_name>`) mit einer Kombination aus IBMid und Kennwort her, indem Sie den folgenden Befehl in der CLPPlus-Eingabeaufforderung oder einem Script ausführen: 

    `connect <IBMid>/<password>@<data_source_name>`

    Weitere Informationen zum Herstellen einer Verbindung zu DSN-Aliasnamen über CLPPlus finden Sie im Abschnitt zu [DSN-Aliasnamen in CLPPlus![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/support/knowledgecenter/SSEPGG_11.1.0/com.ibm.swg.im.dbclient.clpplus.doc/doc/c0057148.html){:new_window}. 

### JDBC
{: #jdbc}

Der JDBC-Treiber des Typs 4 wird für die IAM-Authentifizierung unterstützt. 

Die folgenden Beispiele enthalten Verbindungssnippets für die drei Methoden: 

**Zugriffstoken**

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

**API-Schlüssel**

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

**Kombination aus IBMid und Kennwort**

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

## Benutzererfahrung für Konsolenbenutzer
{: #console-ux}

Auf der Anmeldeseite der Servicekonsole können Sie sich mit Ihrer IBMid und dem zugehörigen Kennwort anmelden. Nach einem Klick auf die Schaltfläche **Anmeldung über IBMid** wird der Benutzer zur Kennworteingabe an die IAM-Anmeldeseite weitergeleitet. Nach der Authentifizierung wird der Benutzer an die Konsole zurückgeleitet. Eine derartige Anmeldung ist erst möglich, wenn der IBMid-Benutzer zuvor vom Datenbankadministrator über die Konsole oder die REST-API zu den einzelnen Datenbankserviceinstanzen hinzugefügt wurde. Beim Hinzufügen eines IBMid-Benutzers muss wie bei einem Benutzer ohne IBMid gleichzeitig auch eine Benutzer-ID für die Datenbankserviceinstanz eingegeben werden. Die Benutzer-ID muss innerhalb der Datenbankserviceinstanz eindeutig sein. Die Benutzer-ID ist gleichzeitig auch die Berechtigungs-ID (AUTH ID) innerhalb der Datenbank. 

## Benutzererfahrung bei Verwendung der REST-API
{: #api}

Nach einer funktionalen Erweiterung akzeptiert auch die {{site.data.keyword.dashdbshort_notm}}-REST-API ein IAM-Zugriffstoken für die Funktionen, von denen zuvor ein von einem Datenbankservice generiertes Zugriffstoken akzeptiert wurde. 

* Führen Sie zum Hinzufügen eines neuen IBMid-Benutzers den folgenden API-Beispielaufruf aus: 

  `curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid>","ibmid":"<userid>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"`

  **Hinweis**: Die Werte für `<userid>` für `"id"` und `"ibmid"` müssen nicht übereinstimmen. Diese beiden IDs sind auf keine Weise miteinander verknüpft. 

* Löschen Sie zum Migrieren eines vorhandenen Datenbankbenutzers ohne IBMid (z. B. `abcuser`), der in einen IBMid-Benutzer geändert werden soll, zunächst die Benutzer-ID, bei der es sich nicht um eine IBMid handelt. Verwenden Sie dazu den folgenden API-Beispielaufruf: 

  `curl --tlsv1.2 -X DELETE "https://<IPaddress>/dbapi/v3/users/abcuser" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json"`

  Fügen Sie anschließend den Benutzer erneut hinzu, diesmal jedoch mit einer IBMid, die mit der vorherigen Benutzer-ID (`abcuser`) übereinstimmt. Verwenden Sie dazu den folgenden API-Beispielaufruf: 

  `curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"abcuser","ibmid":"abcuser@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"`

  Da die Benutzer-ID (`abcuser`) für die neue IBMid des betreffenden Benutzers beibehalten wird, ändern sich auch die dem Benutzer erteilten Datenbankberechtigungen nicht. Soll eine Liste vorhandener Datenbankbenutzer ohne IBMid migriert werden, damit die Benutzer zu IBMid-Benutzern werden, müssen Sie die beiden zuvor angegebenen API-Aufrufe für jeden einzelnen Benutzer ausführen. 

* Erstellen Sie eine Batchdatei, die für jeden einzelnen Benutzer die beiden folgenden API-Beispielaufrufe enthält, wenn mehrere neue IBMid-Benutzer gleichzeitig hinzugefügt werden sollen: 

  ```
  curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid1>","ibmid":"<userid1>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"
  curl --tlsv1.2 "https://<IPaddress>/dbapi/v3/users" -H "Authorization: Bearer <access_token>" -H "accept: application/json" -H "Content-Type: application/json" -d "{"id":"<userid2>","ibmid":"<userid2>@<email_address_domain>","role":"bluadmin","locked":"no","iam":true}"
  .
  .
  .
  ```

Nähere Informationen zu der API Ihres Service finden Sie im Abschnitt zur [{{site.data.keyword.dashdbshort_notm}}-REST-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://ibm.biz/db2whc_api){:new_window}. 

## IBMid-Föderierung
{: #fed}

Wenn ein eigener Identitätsprovider wie LDAP verwendet werden soll, müssen Sie den LDAP-Server zunächst in das IBMid-Konzept einbinden. Anweisungen zur Föderierung des LDAP-Servers mit IBMids finden Sie in der Veröffentlichung [IBMid Enterprise Federation Adoption Guide ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://ibm.ent.box.com/notes/78040808400?s=nhuzrhlsn0ly338zddomx329tlpmfghc){:new_window}. Wenn die IBMid-Föderierung abgeschlossen ist und die berechtigten Benutzer vom Datenbankadministrator zur Datenbankserviceinstanz hinzugefügt wurden, können sich die betreffenden Benutzer bei der Konsole mit der in ihrem Unternehmen verwendeten Benutzer-ID und dem zugehörigen Kennwort anmelden. Die betreffenden Benutzer können stattdessen auch für die Verbindung zu der Datenbankserviceinstanz über eine der unterstützten Datenbankclientschnittstellen ein Zugriffstoken oder einen API-Schlüssel, das bzw. der für die jeweilige Benutzer-ID steht, für die Verbindung zu der Datenbankserviceinstanz verwenden. 

## Einschränkungen
{: #restrictions}

Im Hinblick auf die IAM-Authentifizierung gelten die folgenden Einschränkungen: 

* Die IAM-Authentifizierung für einen Db2-Client, der eine Verbindung zu einem Db2-Server herstellt, wird nur über eine SSL-Verbindung unterstützt. 
* Die IBMid-Föderierung wird unterstützt, um den Einsatz eines angepassten Benutzermanagementportals oder -servers für die Authentifizierung zu ermöglichen. Diese Unterstützung schließt eine Gruppenföderierung nicht ein. 
* Die IAM-Authentifizierung für die Datenbankföderierung wird nicht unterstützt. 
* Das Ausführen von IDA- und UDX-Befehlen (UDX = User-Defined Extension, benutzerdefinierte Erweiterung) über CLPPlus wird nicht unterstützt. 
* JDBC-Treiber des Typs 2 werden nicht unterstützt. 




