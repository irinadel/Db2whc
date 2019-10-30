---

copyright:
  years: 2014, 2019
lastupdated: "2019-10-30"

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

# Driver package
{: #dr_pkg}

The {{site.data.keyword.dashdbshort_notm}} driver package contains software for connecting client applications to a {{site.data.keyword.dashdbshort_notm}} database. 
{: shortdesc}

## About
{: #abt}

- The driver package contains client interface tools, such as CLPPlus.
- The driver package also contains the following drivers: 
  - JDBC
  - Node.js
  - Ruby
  - ODBC
  - CLI
  - .Net
  - OLE DB
  - And more ...

## Already installed?
{: #alrdy_instld}

To verify that the driver package is already on your computer, or to determine the version number, you can use the [**db2level**](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.admin.cmd.doc/doc/r0009195.html){:external} command.

## Downloading
{: #dwnldng}

You can download the driver package for your operating system from the {{site.data.keyword.dashdbshort_notm}} web console. From your {{site.data.keyword.Bluemix_notm}} dashboard, open your {{site.data.keyword.dashdbshort_notm}} service. Log in to your {{site.data.keyword.dashdbshort_notm}} web console.

In the {{site.data.keyword.dashdbshort_notm}} web console, select **Connect > Connection info**. Select the tile that represents your operating system to download the appropriate driver.

## Installing
{: #instlng}

Install the driver package for your operating system:
- [Installing on Linux or PowerLinux](#install_dr_pkg_linux)
- [Installing on Mac OS X](#install_dr_pkg_mac)
- [Installing on Windows](#install_dr_pkg_windows)

### Installing the driver package on Linux or PowerLinux
{: #install_dr_pkg_linux}

You can install the {{site.data.keyword.dashdbshort_notm}} driver package on Linux or PowerLinux by using `installDSDriver`. 
{: shortdesc}

#### Prerequisites
{: #prereq31}

Before attempting to connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you have the [prerequisites](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs).

<!-- Download the Db2 driver package for your operating system from the web console and install it. -->

**On PowerLinux only**, complete the following steps to install the XL C/C++ compiler runtime package:

1. Download the XL C/C++ compiler runtime package from the FTP site. For example, to use the **wget** tool to download the runtime package for Linux little endian Ubuntu 14, issue the following command: 

   `wget ftp://public.dhe.ibm.com/software/server/POWER/Linux/rte/xlcpp/le/ubuntu/dists/trusty/main/binary-ppc64el/*`
2. Install the runtime package by issuing the following command:

   `sudo dpkg -iG *.deb` 

#### Procedure
{: #proc31}

1. Decompress the compressed driver package file that you downloaded earlier.

   Example: 

   `gunzip file_name.tar.gz`

   `tar -xvf file_name.tar`

    A `dsdriver` subdirectory is created in the directory where you ran the decompression commands.
2. Extract the Java and ODBC/CLI drivers.

   a. In the `dsdriver` subdirectory, run the **installDSDriver** command.
   
   The **installDSDriver** command creates the `db2profile` and `db2cshrc` script files in the `dsdriver` directory.

   b. Run one of the following script files based on your shell environment:

   - **Bash or Korn shell**: `source db2profile`
   - **C shell**: `source db2cshrc`

#### What's next?
{: #wn}

To be able to connect your local applications or client tools to your {{site.data.keyword.dashdbshort_notm}} database, [configure your local environment](/docs/services/Db2whc?topic=Db2whc-cfg_loc_env#cfg_loc_env).   

### Installing the driver package on Mac OS X
{: #install_dr_pkg_mac}

You can install the {{site.data.keyword.dashdbshort_notm}} driver package on Mac OS X by using the `installDSDriver.sh` script. 
{: shortdesc}

#### Prerequisites
{: #prereq41}

Before attempting to connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you have the [prerequisites](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs).

<!-- Download the Db2 driver package for your operating system from the web console and install it. -->

#### Procedure
{: #proc41}

- **For a new installation**

  1. Mount the disk image by double-clicking the `macos_dsdriver.dmg` file.
   
     A new **Finder** window opens with the contents of the disk image.

     If the **Finder** window does not open, double-click the `macos_dsdriver` icon on your desktop.
  2. In the **Finder** window, double-click the `installDSDriver.sh` file.

     The driver package is installed in the default location: `/Applications/dsdriver`.

- **For updates to your existing driver package installation**

  1. Back up current configuration files:

     a. Go the `Applications/dsdriver/cfg` folder.

     b. Copy the following files to a different folder: 
    
        `db2cli.ini`

        `db2dsdriver.cfg`
  2. Remove the currently installed driver package by right-clicking the `dsdriver` folder and selecting **Move to Trash**.
  3. Install the new driver package as described in the preceding **For a new installation** section:
     
     a. Mount the disk image by double-clicking the `macos_dsdriver.dmg` file.
     b. In the **Finder** window, double-click the `installDSDriver.sh` file.
  4. Restore the configuration files:

     Copy the `db2cli.ini` and `db2dsdriver.cfg` files that you saved from Step 1 to the `/Applications/dsdriver/cfg` folder.

#### What's next?
{: #wn41}

To be able to connect your local applications or client tools to your {{site.data.keyword.dashdbshort_notm}} database, [configure your local environment](/docs/services/Db2whc?topic=Db2whc-cfg_loc_env#cfg_loc_env).

### Installing the driver package on Windows
{: #install_dr_pkg_windows}

You can install the {{site.data.keyword.dashdbshort_notm}} driver package on Windows by using the installer. 
{: shortdesc}

#### Prerequisites
{: #prereq51}

Before attempting to connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you have the [prerequisites](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs).

<!-- Download the driver package for your operating system from the web console and install it. -->

#### Procedure
{: #proc51}

1. Run the downloaded executable file as an administrator.

   The default installation path of the driver package is: `Program Files\IBM\IBM DATA SERVER DRIVER`
2. (*Optional*): Add the `bin` subdirectory of the driver package installation directory to your `%PATH%` environment variable (so you can run the **db2cli** command without specifying the full path to the command executable.)

#### What's next?
{: #wn51}

To be able to connect your local applications or client tools to your {{site.data.keyword.dashdbshort_notm}} database, [configure your local environment](/docs/services/Db2whc?topic=Db2whc-cfg_loc_env#cfg_loc_env).


<!-- ## Configuring

To connect local applications or client tools to your {{site.data.keyword.dashdbshort_notm}} database, [configure your environment for your Db2 database](driver_pkg_cfg.html). -->


