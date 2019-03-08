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

# Windows 上でのドライバー・パッケージのインストール
{: #install_dr_pkg_windows}

インストーラーを使用して、Windows 上で {{site.data.keyword.dashdbshort_notm}} ドライバー・パッケージをインストールできます。 
{: shortdesc}

## 前提条件
{: #prereq51}

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](/docs/services/Db2whc/connecting/connecting.html#prereqs)を満たしていることを確認します。

<!-- Download the driver package for your operating system from the web console and install it. -->

## 手順
{: #proc51}

1. ダウンロードした実行可能ファイルを管理者として実行します。

   ドライバー・パッケージのデフォルト・インストール・パスは `Program Files\IBM\IBM DATA SERVER DRIVER` です。
2. [*オプション*] ドライバー・パッケージのインストール・ディレクトリーの `bin` サブディレクトリーを `%PATH%` 環境変数に追加します (コマンド実行可能ファイルへの絶対パスを指定せずに **db2cli** コマンドを実行できるようになります)。

## 次の作業
{: #wn51}

ローカル・アプリケーションまたはクライアント・ツールを {{site.data.keyword.dashdbshort_notm}} データベースに接続できるようにするには、[ローカル環境を構成します](/docs/services/Db2whc/connecting/driver_pkg_cfg.html)。
