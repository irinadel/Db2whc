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

# Linux または PowerLinux 上でのドライバー・パッケージのインストール
{: #install_dr_pkg_linux}

`installDSDriver` を使用して、Linux または PowerLinux 上で {{site.data.keyword.dashdbshort_notm}} ドライバー・パッケージをインストールできます。 
{: shortdesc}

## 前提条件
{: #prereq31}

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)を満たしていることを確認します。

<!-- Download the Db2 driver package for your operating system from the web console and install it. -->

**PowerLinux でのみ**、以下のステップを実行して XL C/C++ コンパイラーのランタイム・パッケージをインストールします。

1. FTP サイトから XL C/C++ コンパイラーのランタイム・パッケージをダウンロードします。 例えば、**wget** ツールを使用して Linux リトル・エンディアン Ubuntu 14 のランタイム・パッケージをダウンロードするには、以下のコマンドを発行します。 

   `wget ftp://public.dhe.ibm.com/software/server/POWER/Linux/rte/xlcpp/le/ubuntu/dists/trusty/main/binary-ppc64el/*`
2. 以下のコマンドを発行して、ランタイム・パッケージをインストールします。

   `sudo dpkg -iG *.deb ` 

## 手順
{: #proc31}

1. 先ほどダウンロードした圧縮ドライバー・パッケージ・ファイルを解凍します。

   次に例を示します。 

   `gunzip file_name.tar.gz`

   `tar -xvf file_name.tar`

    解凍コマンドを実行したディレクトリーに `dsdriver` サブディレクトリーが作成されます。
2. Java ドライバーと ODBC/CLI ドライバーを抽出します。

   a. `dsdriver` サブディレクトリーで、**installDSDriver** コマンドを実行します。
   
   **installDSDriver** コマンドにより、`db2profile` と `db2cshrc` のスクリプト・ファイルが `dsdriver` ディレクトリー内に作成されます。

   b. ご使用のシェル環境に基づいて、以下のいずれかのスクリプト・ファイルを実行します。

   - **Bash または Korn シェル**: `source db2profile`
   - **C シェル**: `source db2cshrc`

## 次の作業
{: #wn}

ローカル・アプリケーションまたはクライアント・ツールを {{site.data.keyword.dashdbshort_notm}} データベースに接続できるようにするには、[ローカル環境を構成します](/docs/services/Db2whc?topic=Db2whc-cfg_loc_env#cfg_loc_env)。   




