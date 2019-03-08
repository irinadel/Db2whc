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

# ODBC データ ソース アドミニストレータでの接続
{: #con_prog_odbc_dsa}

Microsoft ODBC データ ソース アドミニストレータ・ツールを使用して、ODBC または CLI アプリケーションと {{site.data.keyword.dashdbshort_notm}} データベース間の接続を定義します。
{: shortdesc}

## 前提条件
{: #prereq91}

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](/docs/services/Db2whc/connecting/connecting.html#prereqs)を満たしていることを確認します。

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## 手順
{: #proc91}

1. [Db2 ドライバー・パッケージ](/docs/services/Db2whc/connecting/driver_pkg.html)をインストールします。

2. ODBC データ ソース アドミニストレータを開いて、Db2 ドライバー・パッケージのユーザー DSN またはシステム DSN を作成します。
    
3. **「詳細設定」**をクリックします。 **ホスト名**、**ポート**、**データベース**の CLI パラメーターに {{site.data.keyword.dashdbshort_notm}} サーバーの値を入力します。
    
4. SSL 接続の場合は、CLI パラメーター **Security** を、値 `SSL` を指定して入力します。
    
5. **「適用」**をクリックします。
    
6. 接続をテストするには、ODBC データ ソース アドミニストレータのメインページに戻ります。 作成した DSN で**「構成」**をクリックします。 サーバーのユーザー ID とパスワードを入力し、**「接続」**をクリックします。

