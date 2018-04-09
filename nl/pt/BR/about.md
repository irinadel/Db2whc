---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-15"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Sobre o Db2 Warehouse on Cloud
{: #overview}

O {{site.data.keyword.dashdblong}} é um warehouse de dados de nuvem totalmente gerenciado, de escala em petabyte e alto
desempenho.

Ele entrega elasticidade verdadeira com ajuste de escala independente de armazenamento e cálculo, um armazenamento de dados
colunar altamente otimizado, compactação acionável e processamento na memória, tudo funcionando junto para fortalecer ainda mais
suas cargas de trabalho analíticas.
{: shortdesc}

## Serviço gerenciado do Db2 Warehouse on Cloud
{: #managed_service}

O serviço totalmente gerenciado do {{site.data.keyword.dashdbshort_notm}} manipula de todos os upgrades de software, atualizações de sistema operacional e manutenção de hardware. O serviço inclui monitoramento de funcionamento 24x7 do banco de dados e da infraestrutura. No caso de falha de hardware ou software, o serviço é reiniciado automaticamente.
{: shortdesc}

<!-- ## User management
{: #user_mgmt}

Management of users that were given access to the database is the sole responsibility of the user or users with the administrator role. The administrator has the responsibility to manage how other users in your organization access your database. This capability does not apply to the Entry plan.
{: shortdesc}

The database administrator role manages the following types of user access: 
* Web console. From the web console, users can run queries against the database.
* Database. The administrator can grant granular access permissions to the database, including only being able to access certain tables, schemas, or even rows or columns. 

For more information about user management, see [Database user management ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.security.doc/doc/user_mgmnt.html){:new_window} -->

<!-- ## Flexible scaling
{: #scale}

Independent scaling of storage and compute cores.

Before provisioning your Flex Performance system, you adjust your anticipated storage and compute cores, then submit your choices.
{: shortdesc}

After your system is provisioned and whenever your needs change, you can adjust your compute cores up or down, and increase your storage. RAM is allocated proportionally as the number of compute cores is changed. A compute cores change results in a short system downtime. You can schedule the downtime to occur at a time that is more convenient or start the compute cores change immediately. Storage changes do not incur any downtime. -->

<!-- ## Backup and restore
{: #br}

An encrypted backup on the full {{site.data.keyword.dashdbshort_notm}} database is done once per day. For the Flex Performance plan, the last 7 daily backup snapshots are retained. For SMP and MPP plans, the last 2 daily backups are retained.
{: shortdesc}

In the Flex Performance plan, you can schedule your backups to run when it's most convenient and you can restore your database from any of your retained backup snapshots at any time that you choose. Your system is up and running within an hour. -->

<!-- In the case of the SMP and MPP plans, the retained backups are used exclusively by IBM for only system recovery purposes in the event of a disaster or system loss. A request to restore your database from a backup is not supported. You can export your data using Db2 tools such as IBM Data Studio or by using the **db2 export** command. -->

<!-- ## High availability (HA): Flex Performance plan
{: #ha_flex}

If an unexpected node failure does occur, your Flex Performance MPP cluster is brought back to full capacity after a short downtime due to using the IBM Container Service (based on Kubernetes). Nodes from a pool are used to move the failed node entities. 
{: shortdesc}

### Compute HA
{: #compute_ha}

Any node failure is immediately detected by the container service. The containers and pods that were running in the failed node are scheduled to a new node from a pool of nodes. The system is back to 100% normal operation after a short downtime.

### Storage HA
{: #storage_ha}

Your storage is configured with a dual-parity RAID6 implementation that provides protection against double disk failures in the same RAID group for high performance and highly available storage for your system.

### Network HA
{: #net_ha}

Network connections are made highly available by provisioning your service with a redundant network interface card (NIC). 

If the container service detects a network issue, pods and containers can automatically restart after a short downtime. -->

<!-- ## High availability (HA): SMP and MPP plans
{: #ha_smp_mpp}

**To do:** I need info about how HA is provided on other SMP and MPP plans.

{: shortdesc} -->


<!-- ## Plans and configurations
{: #plans_cfgs}

You can choose a {{site.data.keyword.dashdbshort_notm}} plan that is configured and optimized for the work that you need to do:
{: shortdesc}

   * An entry plan to try things out
   * A Flex Performance plan in which you can independently scale storage and compute resources
   * Small, medium, and large plans for production
   * MPP configurations for parallel processing
   * Plans configured for High Availability or for Oracle compatibility
   * And more ...

View available plans in the {{site.data.keyword.Bluemix}} catalog:
   * Plans configured for data warehouse and online analytical processing (OLAP) workloads: [{{site.data.keyword.dashdbshort_notm}}](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window} -->
<!--   * Plans configured for high-speed, transactional processing (OLTP): [{{site.data.keyword.dashdbshort_notm}} for Transactions](https://console.ng.bluemix.net/catalog/services/dashdb-for-transactions-sql-database){:new_window} -->

<!-- If you don't see a configuration in the catalog that you need, contact [{{site.data.keyword.IBM_notm}} Sales ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window} to discuss other options. -->

<!-- ## Provisioning of Db2 Warehouse on Cloud
{: #whse_provision}

The {{site.data.keyword.dashdbshort_notm}} database can be provisioned on {{site.data.keyword.BluSoftlayer_full}} and for AWS.
{: shortdesc}

If you want to have the data warehouse provisioned for AWS, select the **MPP Small for AWS** plan. -->

<!-- ## Loading data
{: #load}

You can load data from a data file in a delimited format such as CSV or TXT located on a local network, an object store (Amazon S3 or IBM Cloud Object Storage (formerly SoftLayer Swift)), or a Db2® server. You can also populate a database instance with data directly from a Cloudant® database or by performing a load process from an application such as InfoSphere® DataStage®.
{: shortdesc}

* [Loading data from PureData System for Analytics (Netezza) ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://lift.ng.bluemix.net/#docs){:new_window}
* [Loading data from Oracle ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://lift.ng.bluemix.net/#docs){:new_window}
* [Loading data from SQL Server ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://lift.ng.bluemix.net/#docs){:new_window}
* [Loading a CSV file ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://lift.ng.bluemix.net/#docs){:new_window}
* [Loading data from Amazon S3 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/learn_how/s3.html){:new_window}
* [Loading data from IBM Cloud Object Storage (formerly SoftLayer Swift) ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/learn_how/loaddata_swift.html){:new_window} -->

<!-- ## Connecting
{: #connect}

You can connect command-line interfaces, IBM® or third-party applications or tools, or apps that you create to your Db2® database. 
{: shortdesc}

### Prerequisites
{: #connect_prereq}

Before you can connect to your Db2 managed service database, complete the [prerequisites ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connecting_applications_to_dashdb_database.html){:new_window}.
{: shortdesc}

### Configuring your environment
{: #cfg_env}

To connect local applications and tools to your Db2 database, you need to [configure your environment ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_driver_package_config.html){:new_window}. 
{: shortdesc}

### Connecting programmatically
{: #conx_prgrm}

You can use common programming languages to create applications that connect to a Db2 database.
{: shortdesc}

* [Java ![External link icon](../../icons/launch-glyph.svg "External link icon"){}{:new_window}
* [JDBC ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_jdbc_applications.html){:new_window}
* [ODBC ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_cli_and_odbc_applications.html){:new_window}
* [.NET ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting__net_applications.html){:new_window}
* [PHP ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_php.html){:new_window}

### Connecting apps and tools
{: #conx_apps_tools}

You can also connect external applications and tools to {{site.data.keyword.dashdbshort_notm}} and use them to further manage or analyze your data. For example:
   * Connect your {{site.data.keyword.Bluemix_short}} applications that need an analytics database.
   * Connect from DSX
   * [Connect {{site.data.keyword.IBM_notm}} InfoSphere® Data Architect to design and deploy your database schema. ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_ibm_data_architect.html){:new_window} -->
<!--   * Connect Esri ArcGIS to perform geospatial analytics and map publishing with your data. -->
<!--   * [Connect an {{site.data.keyword.IBM_notm}} Cognos® server to run Cognos reports against your data. ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_cognos.html){:new_window}
   * Connect SQL-based tools such as Tableau or Microsoft Excel to manipulate, analyze, or visualize your data. 
       * [Tableau ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_tableau.html){:new_window}
       * [Microsoft Excel ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_excel.html){:new_window}
   * [Connect Aginity Workbench to migrate Netezza® data models and data to {{site.data.keyword.dashdbshort_notm}}. ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_aginity.html){:new_window} -->

<!-- ## Data visualization
{: #visualize}

Connecting Looker to Db2 Warehouse
Connecting Tableau to Db2 Warehouse
Connecting Watson Analytics...
Connecting Cognos Analytics... -->

<!-- ## Local development
{: #local_dev}

If you want to set up a local Db2 development environment, you can use [IBM Db2 Warehouse Developer-C for Non-Production ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://store.docker.com/images/ibm-db2-warehouse-dev){:new_window} that is available from Docker Store.
{: shortdesc}

For prerequisites and installation instructions, select the link for your operating system: 

* [Windows and Macintosh ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/en/SS6NHC/com.ibm.swg.im.dashdb.doc/admin/local_prereqs-Winmac_using_Linux.html){:new_window}
* [Linux ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/en/SS6NHC/com.ibm.swg.im.dashdb.doc/admin/local_prereqs-Linux.html){:new_window} -->

<!-- ## Communities
{: #communities}

There are user-driven communities that you can join for information, tutorials, discussions, and help from professional Db2 users. And it's free to join!
{: shortdesc}

* [International Db2 Users Group (IDUG) ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.idug.org/){:new_window} IDUG® is an independent, not-for-profit, user-run organization whose mission is to support and strengthen the information services community by providing the highest quality education and services designed to promote the effective utilization of Db2.
* [Db2 Community on developerWorks ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/data/db2/){:new_window} A Db2 developer community.
* [Stack Overflow ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://stackoverflow.com/users/login?ssrc=anon_ask&returnurl=https%3a%2f%2fstackoverflow.com%2fquestions%2fask%3ftags%3ddashdb){:new_window} A support forum and community for developers. -->

