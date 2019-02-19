---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# Installing the driver package on Windows
{: #install_dr_pkg_windows}

You can install the {{site.data.keyword.dashdbshort_notm}} driver package on Windows by using the installer. 
{: shortdesc}

## Prerequisites

Before attempting to connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you have the necessary [prerequisites](/docs/services/Db2whc/connecting/connecting.html#prereqs).

<!-- Download the driver package for your operating system from the web console and install it. -->

## Procedure

1. Run the downloaded executable file as an administrator.

   The default installation path of the driver package is: `Program Files\IBM\IBM DATA SERVER DRIVER`
2. [*Optional*] Add the `bin` subdirectory of the driver package installation directory to your `%PATH%` environment variable (so you can run the **db2cli** command without specifying the full path to the command executable.)

## What's next?

To be able to connect your local applications or client tools to your {{site.data.keyword.dashdbshort_notm}} database, [configure your local environment](/docs/services/Db2whc/connecting/driver_pkg_cfg.html).