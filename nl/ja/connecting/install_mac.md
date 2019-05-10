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

# Mac OS X 上でのドライバー・パッケージのインストール
{: #install_dr_pkg_mac}

`installDSDriver.sh` スクリプトを使用して、{{site.data.keyword.dashdbshort_notm}} ドライバー・パッケージを Mac OS X にインストールできます。 
{: shortdesc}

## 前提条件
{: #prereq41}

{{site.data.keyword.dashdbshort_notm}} データベースへの接続を試行する前に、必要な[前提条件](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs)を満たしていることを確認します。

<!-- Download the Db2 driver package for your operating system from the web console and install it. -->

## 手順
{: #proc41}

- **新規インストールの場合**

  1. `macos_dsdriver.dmg` ファイルをダブルクリックして、ディスク・イメージをマウントします。
   
     新しい **Finder** ウィンドウが開いて、ディスク・イメージの内容が表示されます。

     **Finder** ウィンドウが開かない場合は、デスクトップにある `macos_dsdriver` アイコンをダブルクリックしてください。
  2. **Finder** ウィンドウで、`installDSDriver.sh` ファイルをダブルクリックします。

     ドライバー・パッケージは、デフォルトの場所である `/Applications/dsdriver` にインストールされます。

- **既存のドライバー・パッケージ・インストールの更新の場合**

  1. 現在の構成ファイルをバックアップします。

     a. `Applications/dsdriver/cfg` フォルダーに移動します。

     b. 以下のファイルを別のフォルダーにコピーします。 
    
        `db2cli.ini
`

        `db2dsdriver.cfg`
  2. `dsdriver` フォルダーを右クリックし、**「ごみ箱に移動 (Move to Trash)」**を選択して、現在インストールされているドライバー・パッケージを削除します。
  3. 前述の『**新規インストールの場合**』セクションの説明に従って、以下のように新規ドライバー・パッケージをインストールします。
     
     a. `macos_dsdriver.dmg` ファイルをダブルクリックして、ディスク・イメージをマウントします。
     b. **Finder** ウィンドウで、`installDSDriver.sh` ファイルをダブルクリックします。
  4. 以下のように構成ファイルをリストアします。

     ステップ 1 で保存した `db2cli.ini` ファイルと `db2dsdriver.cfg` ファイルを `/Applications/dsdriver/cfg` フォルダーにコピーします。

## 次の作業
{: #wn41}

ローカル・アプリケーションまたはクライアント・ツールを {{site.data.keyword.dashdbshort_notm}} データベースに接続できるようにするには、[ローカル環境を構成します](/docs/services/Db2whc?topic=Db2whc-cfg_loc_env#cfg_loc_env)。
