---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# Secure Sockets Layer (SSL) サポート
{: #ssl_support}

{{site.data.keyword.dashdbshort_notm}} データベースは、サード・パーティーのデジタル認証局 (CA) によって発行された証明書を SSL 接続に使用します。 
{: shortdesc}

CA 証明書は、Db2 ドライバー・パッケージの一部です。 アプリケーションが Db2 ドライバー・パッケージ内のドライバーを使用して接続する場合には、証明書を別途ダウンロードする必要はありません。 Db2 ドライバー・パッケージは、Web コンソールからダウンロードできます。

ただし、アプリケーションに独自のドライバーがある場合は、証明書を別途ダウンロードする必要が生じることがあります。 証明書は、Web コンソールからダウンロードできます。

Secure Sockets Layer (SSL) は、通信のプライバシーを提供するセキュリティー・プロトコルの 1 つです。 SSL により、クライアント・アプリケーションとサーバー・アプリケーションは、盗聴、改ざん、メッセージ偽造を防ぐために設計された方法で通信を行うことができます。 SSL を使用可能にしたクライアント・アプリケーションは、標準的な暗号化の手法を使用するので、確実にセキュア通信を行うのに役立ちます。

SSL を使用して {{site.data.keyword.dashdbshort_notm}} データベースに接続するためのアプリケーションの構成は、会社のポリシーに応じて異なります。 標準プロトコルと SSL プロトコルの両方とも、データベースへの接続に使用でき、ユーザー名とパスワードを暗号化されたデータとして伝送します。 エンドツーエンドのセキュリティーを完全なものにするには、SSL 接続を使用して、機密データやメタデータを含むすべてのデータベース情報を伝送してください。 管理者は、Web コンソール上で設定を変更して、SSL 接続を必須にすることができます。


