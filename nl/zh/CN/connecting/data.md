---

copyright:
  years: 2014, 2018
lastupdated: "2018-10-15"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 数据集成
{: #overview}

您还可以将外部应用程序和工具连接到 {{site.data.keyword.dashdbshort_notm}}，以使用其进一步管理或分析数据。
{: shortdesc}

## DataStage
{: #datastage}

以下指示信息说明如何通过编目数据库和定义连接对象，定义 IBM® InfoSphere® DataStage® <!--version 9.1 and later -->与 {{site.data.keyword.dashdbshort_notm}} 数据库之间不使用 SSL 的连接，或者如何使用第三方签发的数字证书来创建使用 SSL 的连接。
{: shortdesc}

### 先决条件

如果尚未安装数据服务器客户机，请下载并安装适合于您客户端机器操作系统的 IBM Data Server Client <!--Version 10.5 -->：[IBM Data Server Client ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/marketing/iwm/iwm/web/preLogin.do?source=swg-idsc97){:new_window}。

要使用 SSL 协议进行连接，请下载并安装 32 位 GSKit V8。单击适用于您客户端机器操作系统的“操作系统”选项卡：[GSKit V8 - 安装、卸载和升级指示信息 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/support/docview.wss?uid=swg21631462){:new_window}。对于以下操作系统，请确保将 GSKit 安装目录路径添加到特定于操作系统的路径环境变量：

- AIX®：**LIBPATH**
   - `/usr/opt/ibm/gsk8/lib`
- Linux：**LD_LIBRARY_PATH**
    - `/usr/local/ibm/gsk8/lib`
- UNIX：**LD_LIBRARY_PATH**
    - `/opt/ibm/gsk8/lib`
- Windows：**PATH**
    - `<installation_directory>\gsk8\bin`
    - `<installation_directory>\gsk8\lib`

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](connecting.html#prereqs)。

### 过程

- 要创建使用 SSL 的连接，请完成以下步骤：

  1. 打开命令行或终端，并在 DataStage 系统中创建一个新目录，以用于存储 SSL 证书和密钥文件。

     `# /home/db2inst2> mkdir SSL`

     `# /home/db2inst2> cd SSL`

  2. 在 Db2 控制台的“将应用程序连接到数据库”页面中，下载 SSL 证书。

     a. 在主菜单中，单击**连接**。
     
     b. 单击**使用 SSL 进行连接**，然后单击 **SSL 证书 (1 KB)** 链接。
     
     c. 将 `DigiCertGlobalRootCA.crt` 证书保存到在步骤 1 中创建的 SSL 目录中。
        
  3. 使用 **gsk8capicmd** 实用程序在 DataStage 系统中创建客户机密钥库数据库。Db2® 服务器安装中包含此实用程序。

     `# /home/db2inst2/SSL> gsk8capicmd -keydb -create -db <keystore_db.kdb> -pw <ks_db_password> -stash`

     其中，`<keystore_db.kdb>` 表示客户机密钥库数据库，`<ks_db_password>` 表示客户机密钥库数据库的密码。
        
  4. 将该证书添加到客户机密钥库数据库。

     `# /home/db2inst2/SSL> gsk8capicmd -cert -add -db <keystore_db.kdb> -pw <ks_db_password> -label BLUDB_SSL -file DigiCertGlobalRootCA.crt`

     其中，`<keystore_db.kdb>` 表示客户机密钥库数据库，`<ks_db_password>` 表示客户机密钥库数据库的密码。
    
  5. 在 DataStage 服务器上配置 Db2 客户机。
            
     a. 更新数据库管理器中的 SSL 配置参数。

     `# /home/db2inst2> db2 update dbm cfg using SSL_CLNT_KEYDB /home/db2inst2/SSL/<keystore_db.kdb>`

     其中，`<keystore_db.kdb>` 表示客户机密钥库数据库。

     `# /home/db2inst2> db2 update dbm cfg using SSL_CLNT_STASH /home/db2inst2/SSL/<keystore_db.sth>`

     其中，`<keystore_db.sth>` 表示客户机密钥库数据库密码隐藏文件。
            
     b. 使用 SSL 安全选项对目标节点进行编目，然后在该目标节点上编目 BLUDB 数据库。

     `# /home/db2inst2> db2 catalog tcpip node SSLCLOUD remote <IP_addr_of_BLUDB_database_server> server 50001 security SSL`

     其中，`<IP_addr_of_BLUDB_database_server>` 表示 BLUDB 数据库服务器的 IP 地址。

     `# /home/db2inst2> db2 catalog db BLUDB as BLUDB_S at node SSLCLOUD`

     `# /home/db2inst2> db2 terminate`

  6. 为每个人添加对 SSL 目录中各个文件的读取和执行许可权。运行作业的 DataStage 用户需要访问这些文件才能与 Db2 数据库建立 SSL 连接。

     `# /home/db2inst2/SSL> chmod 655 /home/db2inst2/SSL/*`

  7. 重新启动 DataStage 服务器。

- 要创建不使用 SSL 的连接，请通过完成以下步骤对 IBM InfoSphere DataStage 服务器上的目标 Db2 数据库进行编目：

  1. 使用 PuTTY 等 Telnet 客户机应用程序以缺省实例所有者（通常为 db2inst1）身份连接到 DataStage 服务器。
  2. 使用以下 Db2 命令创建目标 Db2 数据库的目录：

     `db2 catalog tcpip node nodename remote <IP_address_of_BLUDB_database_server> <port_number_of_BLUDB_database>`

     `db2 catalog db <BLUDB_db_name> at node <nodename>`

     `db2 connect to <BLUDB_db_name> user <BLUDB_db_user_name> using <BLUDB_db_password>`

     `db2 list tables`

     其中，`<IP_address_of_BLUDB_database_server>` 表示 BLUDB 数据库服务器的 IP 地址，`<port_number_of_BLUDB_database>` 表示 BLUDB 数据库的端口号，`<BLUDB_db_name>` 表示 BLUDB 数据库名称，`<nodename>` 表示节点的名称，`<BLUDB_db_user_name>` 表示 BLUDB 数据库用户名，`<BLUDB_db_password>` 表示 BLUDB 数据库密码。

  3. 使用预先收集的[连接信息](credentials.html)在 DataStage 客户机中定义连接。在**参数**选项卡上，必须为**使用登台类型进行连接**字段选择 **Db2 连接器**。

     有关在 DataStage 中定义连接的详细信息，请参阅以下 DataStage 文档主题： 
     
     - [手动创建数据连接对象 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/SSZJPZ_11.3.0/com.ibm.swg.im.iis.ds.design.doc/topics/t_ddesref_Creating_a_Data_Connection_Object_Manually.html){:new_window}

## Informatica
{: #informatica}

您可以将 Informatica 连接到 {{site.data.keyword.dashdbshort_notm}} 以帮助您管理数据。
{: shortdesc}

观看以下视频以了解如何将 {{site.data.keyword.dashdbshort_notm}} 与 Informatica Cloud 集成。

<iframe class="embed-responsive-item" id="youtubeplayer1" title="DB2 Connections - Lightening Fast How-To with Informatica Cloud" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TUiS_HstLnU?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

<!-- To configure a native Db2 connection to connect to {{site.data.keyword.dashdbshort_notm}}, perform the following steps:

1. Run the `odbcad32.exe` file from your local system.
The ODBC Data Sources Administrator dialog box appears.

2. Create the 32-bit ODBC Data Source Name using the DataDirect Db2 drivers.

3. In the ODBC DB2 Wire Protocol Setup dialog box, click **Security** tab.

4. Set the value of the `Authentication Method` property as `1 -Encrypt Password`. The following image shows the **Security** tab in the ODBC DB2 Wire Protocol Setup dialog box where you can set the `Authentication Method` property:
             
   ![ODBC Db2 Wire Protocol Driver Setup - Security tab](images/odbc_driver.png)
       
5. In the ODBC DB2 Wire Protocol Setup dialog box, click **Modify Bindings** tab.

6. Enter your user name in the Package Collection property. The following image shows the **Modify Bindings** tab in the ODBC DB2 Wire Protocol Setup dialog box where you can set the `Package Collection` property: 

   ![ODBC Db2 Wire Protocol Driver Setup - Modify Bindings tab](images/odbc_driver_2.png)
            
7. In the PowerCenter Designer, use the data source name that you created to import the metadata.

8. In the PowerCenter Workflow Manager, create the required workflow.

9. Ensure that you have the {{site.data.keyword.dashdbshort_notm}} compatible 11.x Db2 clients when you run the workflow.

**Note**: If you want to set the authentication type when you create the Db2 client catalog, you could specify the value of the `AUTHENTICATION TYPE` property as `SERVER_ENCRYPT`. -->

<!-- Watch this video to see how to integrate Db2 and Salesforce with Informatica Cloud.

<iframe class="embed-responsive-item" id="youtubeplayer2" title="Integrate Db2 and Salesforce with Informatica Cloud" type="text/html" width="640" height="390" src="//www.youtube.com/watch?v=RGTLweZvKP8" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe> -->

<!-- [Informatica ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://kb.informatica.com/howto/6/Pages/20/522402.aspx?myk=Connect%20to%20Db2){:new_window} -->

## Lift
{: #lift}

使用 Lift 将数据迁移到 {{site.data.keyword.dashdbshort_notm}} 中。

[Lift ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://lift.ng.bluemix.net/#docs){:new_window}

## InfoSphere Data Replication
{: #idr}

您可以将 IBM® InfoSphere® Data Replication <!--version 11.3.3.3-36 or later -->连接到 {{site.data.keyword.dashdbshort_notm}} 数据库。此功能适用于 SMP 和 MPP 环境，但不适用于 {{site.data.keyword.dashdbshort_notm}} 的入门套餐。
{: shortdesc}

### 概述

理想情况下，将 IBM InfoSphere Data Replication 连接到 {{site.data.keyword.dashdbshort_notm}} 时，IBM InfoSphere Data Replication 会与 {{site.data.keyword.dashdbshort_notm}} 位于同一 {{site.data.keyword.Bluemix_notm}} Data Center 中，或者与 {{site.data.keyword.dashdbshort_notm}} 共享托管。IBM InfoSphere Data Replication 可使本地服务器连接到远程 {{site.data.keyword.dashdbshort_notm}} 实例。

将 {{site.data.keyword.dashdbshort_notm}} 用作连接目标时，IBM InfoSphere Data Replication 的性能在一定程度上取决于其目标引擎与 {{site.data.keyword.dashdbshort_notm}} 实例之间网络的带宽。物理距离也会影响性能：理想情况下，IBM InfoSphere Data Replication 会尽可能接近 {{site.data.keyword.dashdbshort_notm}} 实例。网络拓扑也会影响性能。例如，理想情况下，IBM InfoSphere Data Replication 目标引擎会在目标实例所在的 VPN（安全域）中的 VM 上运行。要遍历的网络节点（例如，防火墙或路由器）越少，性能越好。 

### 先决条件

如果您打算使用 SSL 协议进行连接，请下载并安装 GSKit V8。请参阅 [GSKit V8 - 安装、卸载和升级指示信息 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://www.ibm.com/support/docview.wss?uid=swg21631462){:new_window}。单击适用于您的客户端机器操作系统的“操作系统”选项卡。如果要在 Windows 计算机上安装 GSKit，请确保为 **`PATH`** 环境变量指定 GSKit 安装目录路径 (`<installation_directory>\gsk8\bin`)。

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](connecting.html#prereqs)。

如果打算使用 SSL 协议进行连接，请通过 Web 控制台将 `DigiCertGlobalRootCA.crt` SSL 证书下载到客户端机器上的目录。要下载证书，请单击**连接 > 连接信息**，然后单击**使用 SSL 进行连接**选项卡。

### 过程

1. 选择下列其中一种方法来建立连接：

   - 要创建使用 SSL 的连接，请完成以下步骤：
            
     a. 发出以下命令：

     `cd /<ssl_directory_name>/ssl`

     其中，`/<ssl_directory_name>/ssl` 是 `DigiCertGlobalRootCA.crt` SSL 证书下载目录的路径。

     b. 使用 **GSKCapiCmd** 工具创建客户机密钥数据库和隐藏文件。例如，以下命令将创建名为 `dashclient.kdb` 的客户机密钥数据库和名为 `dashclient.sth` 的隐藏文件：

     `gsk8capicmd_64 -keydb -create -db "dashclient.kdb" -pw "passw0rdpw0" -stash`

     其中，`passw0rdpw0` 是密码。**-stash** 选项在客户机密钥数据库所在的路径中创建隐藏文件，其文件扩展名为
`.sth`。在连接时，GSKit 使用隐藏文件来获取客户机密钥数据库的密码。
            
     c. 将该证书添加到客户机密钥数据库。例如，以下 **gsk8capicmd** 命令将该证书从 `/<ssl_directory_name>/ssl/DigiCertGlobalRootCA.crt` 文件导入到名为 `dashclient.kdb` 的客户机密钥数据库：

     `gsk8capicmd_64 -cert -add -db "dashclient.kdb" -pw "passw0rdpw0" -label "DigiCert" -file "/<ssl_directory_name>/ssl/DigiCertGlobalRootCA.crt" -format ascii -fips`

     d. 更新客户机上 `SSL_CLNT_KEYDB` 和 `SSL_CLNT_STASH` 数据库管理器配置参数的值，以指定客户机密钥数据库和隐藏文件。示例如下：

     `db2 update dbm cfg using SSL_CLNT_KEYDB /<ssl_directory_name>/ssl/dashclient.kdb`

     `db2 update dbm cfg using SSL_CLNT_STASH /<ssl_directory_name>/ssl/dashclient.sth`

     e. 对 {{site.data.keyword.dashdbshort_notm}} 节点进行编目，以便客户机应用程序可以连接到该节点。请发出以下命令：

     `db2 catalog tcpip node <node_name> remote <Db2_Warehouse_IP_address> server <port_number> security ssl`

     其中：
                
     `<node_name>` 是节点的名称。

     `<Db2_Warehouse_IP_address>` 是 Db2 Warehouse on Cloud 服务器的 IP 地址。

     `<port_number>` 是用于通过 SSL 连接来连接到 Db2 Warehouse 的端口。如果要使用缺省端口，请指定 `50001`。
            
     f. 对远程 {{site.data.keyword.dashdbshort_notm}} 数据库进行编目，以便客户机应用程序可以连接到该数据库。请发出以下命令：

     `db2 catalog database bludb as <db_alias> at node <node_name>`

     其中，`db_alias` 是 {{site.data.keyword.dashdbshort_notm}} 数据库的名称。
            
     g. 通过下列其中一种方法测试 SSL 连接：
                
     - 使用 CLP 通过发出以下命令连接到 {{site.data.keyword.dashdbshort_notm}} 数据库来测试连接：

       `db2 connect to <db_alias> user <user_id>`

       其中，`<user_id>` 是您的 {{site.data.keyword.dashdbshort_notm}} 用户标识。系统会提示您输入密码。
                
     - 使用 CLI 通过发出以下命令连接到 {{site.data.keyword.dashdbshort_notm}} 数据库来测试连接：

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

       其中，`<alias>` 是您已使用 **db2cli writecfg** 命令创建的 DSN 别名，`<user_id>` 是您的 {{site.data.keyword.dashdbshort_notm}} 用户标识，`<password>` 是您的 {{site.data.keyword.dashdbshort_notm}} 数据库密码。
        
   - 要创建不使用 SSL 的连接，请完成以下步骤：

     a. 对 {{site.data.keyword.dashdbshort_notm}} 节点进行编目，以便客户机应用程序可以连接到该节点。请发出以下命令：

     `db2 catalog tcpip node <node_name> remote <Db2_Warehouse_IP_address> server <port_number>`

     其中：
                
     `<node_name>` 是节点的名称。

     `<Db2_Warehouse_IP_address>` 是 {{site.data.keyword.dashdbshort_notm}} 服务器的 IP 地址。

     `<port_number>` 是用于在不使用 SSL 连接的情况下连接到 {{site.data.keyword.dashdbshort_notm}} 的端口。如果要使用缺省端口，请指定 `50000`。
            
     b. 对远程 {{site.data.keyword.dashdbshort_notm}} 数据库进行编目，以便客户机应用程序可以连接到该数据库。请发出以下命令：

     `db2 catalog database bludb as <db_alias> at node <node_name>`

     其中，`<db_alias>`是 {{site.data.keyword.dashdbshort_notm}} 数据库的名称。

     c. 通过下列其中一种方法测试非 SSL 连接：

     - 使用 CLP 通过发出以下命令连接到 {{site.data.keyword.dashdbshort_notm}} 数据库来测试连接：

       `db2 connect to <db_alias> user <user_id>`

       其中，`<user_id>` 是您的 {{site.data.keyword.dashdbshort_notm}} 用户标识。系统会提示您输入密码。
                
     - 使用 CLI 通过发出以下命令连接到 {{site.data.keyword.dashdbshort_notm}} 数据库来测试连接：

       `db2cli validate -dsn <alias> -connect -user <user_id> -passwd <password>`

       其中，`<alias>` 是您已使用 **db2cli writecfg** 命令创建的 DSN 别名，`<user_id>` 是您的 {{site.data.keyword.dashdbshort_notm}} 用户标识，`<password>` 是您的 Db2 Warehouse on Cloud 密码。
    
2. 启动 InfoSphere Data Replication 配置工具并执行以下步骤。截屏中显示的值是示例。
        
   a. 通过使用**实例配置**选项卡，添加源实例以指向源数据库：

   ![IIDR 新建实例 - 源实例](images/IIDR_source_instance.jpg)

   b. 通过使用**实例配置**选项卡，添加目标实例以指向目标 Db2 数据库：如果使用的不是 IBM InfoSphere Data Replication 11.3.3.3-50 或更高版本，请勿选中**指定刷新装入程序路径**复选框。

   ![IIDR 新建实例 - 目标实例](images/IIDR_target_instance.jpg)

   c. 启动每个实例：

   ![IIDR 配置工具](images/IIDR_instances.jpg)

3. 启动 InfoSphere Data Replication 管理控制台，并使用 Access Manager 来完成以下步骤：
        
   a. 通过使用**数据存储**选项卡，创建数据存储以连接到源实例。由于 Db2 数据库初始不支持作为源数据库，因此必须通过单击**连接参数**来提供源数据库的用户和密码信息。

   ![数据存储属性 - 源](images/IIDR_source_datastore.jpg)

   b. 通过使用**数据存储**选项卡，创建数据存储以连接到目标实例。必须通过单击**连接参数**来提供用户和密码信息。

   ![数据存储属性 - 目标](images/IIDR_target_datastore.jpg)

   c. 如果要连接到 Access Server 的用户（例如，admin）不存在，请创建该用户：

   ![新建用户](images/IIDR_management_user.jpg)

   d. 单击 **Access Manager** 选项卡。
        
   e. 在**数据存储管理**选项卡上，通过右键单击每个数据存储，然后单击**分配用户**，将该用户分配给源数据存储和目标数据存储。请确保用于访问每个实例的凭证正确。

   ![IIDR 管理控制台 - Access Manager](images/IIDR_management_assign_user.jpg)

### 后续步骤

定义预订并执行数据复制。有关信息，请参阅：

- [从 InfoSphere Data Replication 装入数据 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/learn_how/loaddata_iidr.html){:new_window} 

## Segment
{: #segment}

您可以将 Segment 与 {{site.data.keyword.dashdbshort_notm}} 数据库集成。Segment 是一个单一平台，用于收集和存储用户数据，并将这些数据传递给数以百计的工具。
{: shortdesc}

[Segment ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://segment.com/docs/destinations/db2/){:new_window}

## Data Studio
{: #data_studio}

以下指示信息说明如何创建从 IBM® Data Studio <!--version 4.1.x -->到 {{site.data.keyword.dashdbshort_notm}} 数据库的连接。
{: shortdesc}

### 先决条件

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](connecting.html#prereqs)。

### 过程

1. 在 Data Studio 中，单击**所有数据库 > 新建数据库连接**。

2. 在**本地**选项卡上，将 **Db2 for Linux, UNIX, and Windows** 选作数据库管理器。
    
3. 在**常规**选项卡上，输入以下值：
   - *数据库*：`BLUDB`
   - *主机*：主机名。
   - *端口*：对于不使用 SSL 的连接，请输入 `50000`。对于使用 SSL 的连接，请输入 `50001`。 
   - *用户名*：用于登录的用户名。
   - *密码*：用于登录的密码。

4. 对于 SSL 连接，单击**可选**选项卡，然后单击**添加**。对于 `sslConnection` 属性，指定 `true`。

5. [*可选*]: 单击**测试连接**，以验证连接是否已成功。

## Data Server Manager (DSM)
{: #dsm}

通过 IBM® Data Server Manager 与 {{site.data.keyword.dashdbshort_notm}} 数据库之间的连接，您能够在 Data Server Manager Web 控制台中监视和管理数据库。
{: shortdesc}

### 先决条件

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](connecting.html#prereqs)。

### 过程

<!--The connection procedure was tested on Data Server Manager version 1.1. The same procedure applies to all of the other versions of the Data Server Manager software.
-->
要创建连接，请完成以下步骤：

1. 登录到 Data Server Manager Web 控制台。
    
2. 在 Data Server Manager Web 控制台中，转至**设置 > 数据库连接**。
    
3. 单击 ![带圆圈的 + 号](images/icon_R_plus.gif) 图标以添加数据库连接。在**添加数据库连接**页面上的**数据库连接**选项卡下，在以下字段中输入所需的信息：

   - *数据库连接名称*：名称必须对于 Data Server Manager 唯一
   - *数据服务器类型*：从下拉菜单中，选择 **Db2 for Linux, UNIX, and Windows**
   - *数据库名称*：`BLUDB`
   - *主机名*：输入 {{site.data.keyword.dashdbshort_notm}} 主机名 
   - *端口号*：对于不使用 SSL 的连接，请输入 `50000`。对于使用 SSL 的连接，请输入 `50001`。 
   - *JDBC 安全性*：从下拉菜单中，选择**明文密码**
   - *用户标识*：您的 {{site.data.keyword.dashdbshort_notm}} 用户标识 
   - *密码*：您的 {{site.data.keyword.dashdbshort_notm}} 密码 

4. 对于使用 SSL 的连接，请选择**高级 JDBC 属性**选项卡。在以下字段中输入所需的信息：

   - *属性*：`sslConnection`
   - *值*：`true`

    单击**添加**按钮。选择**数据库连接**选项卡。
    
5. 通过单击**测试连接**按钮来测试连接。如果连接成功，请单击**确定**。

## InfoSphere Data Architect
{: #ida}

以下指示信息说明如何创建从 InfoSphere® Data Architect <!--version 9.1.x -->到 {{site.data.keyword.dashdbshort_notm}} 数据库的连接。
{: shortdesc}

### 先决条件

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](connecting.html#prereqs)。

### 过程

1. 在 InfoSphere Data Architect 的“数据源资源管理器”视图中，右键单击**数据库连接**，然后选择**新建**。
    
2. 在**本地**选项卡上，将 **Db2 for Linux, UNIX, and Windows** 选作数据库管理器。
    
3. 在**常规**选项卡上，输入以下值：

   - *数据库*：`BLUDB`
   - *主机*：预先收集的主机名。
   - *端口*：对于不使用 SSL 的连接，请输入 `50000`。对于使用 SSL 的连接，请输入 `50001`。 
   - *用户名*：预先收集的用户标识。
   - *密码*：预先收集的密码。

4. 对于 SSL 连接，单击**可选**选项卡。输入 `sslConnection` 属性并指定值 `true`。单击**添加**。
    
5. [*可选*]: 单击**测试连接**，以验证连接是否已成功。

## Aginity Workbench
{: #aginity_wb}

以下指示信息说明如何将 Aginity Workbench <!--4.3 -->连接到 {{site.data.keyword.dashdbshort_notm}} 数据库。您可以使用 Aginity Workbench 将 IBM PureData for Analytics (Netezza) 数据模型和数据迁移到 {{site.data.keyword.dashdbshort_notm}}。
{: shortdesc}

### 先决条件

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](connecting.html#prereqs)。

### 过程

1. 下载并安装 Aginity Workbench。

2. 根据您先前记录的连接信息来确定 ODBC DSN。

3. 启动 Aginity Workbench。如果数据库连接对话框未自动打开，请通过单击工具栏上的**连接**将其打开。

4. [建立数据库连接 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.aginity.com/documentation/WB/dashDB/Default.htm#Aginity_Topics/Aginity_Workbench/Database_Connection_Dialog_Box.htm){:new_window}。使用您先前记录的连接信息中的主机名、用户标识和密码。

## CLPPlus
{: #clpplus}

Db2 驱动程序包中包含命令行处理器增强版 (CLPPlus)。CLPPlus 提供了可用于连接到 {{site.data.keyword.dashdbshort_notm}} 数据库的命令行界面。您可以使用 CLPPlus 来定义、编辑和运行语句、脚本和命令。
{: shortdesc}

### 先决条件

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](connecting.html#prereqs)。

要使用 CLPPlus，请确保在计算机上安装 Java V1.5.0 或更高版本的软件开发包 (SDK) 或 Java 运行时环境 (JRE)，并确保环境变量设置如下：

- `JAVA_HOME` 环境变量设置为计算机上的 Java 安装目录。
- `PATH` 环境变量设置包含计算机上 Java 安装目录的 `bin` 子目录。

### 过程

1. 在 Linux 操作系统上的命令 shell 中、Windows 命令提示符处或 Windows 操作系统上的 Db2 命令窗口中，运行以下命令：

   这些命令将在计算机上的驱动程序配置文件 (`db2dsdriver.cfg`) 中创建新条目，并设置连接属性。此步骤只需执行一次。

   - 对于使用 SSL 的连接：

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50001 -parameter "SecurityTransportMode=SSL"`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50001`  

     其中：
     
     - `<hostname>` 是服务器的主机名。
     - `<alias>` 是您选择的别名。

   - 对于不使用 SSL 的连接：

     `db2cli writecfg add -database BLUDB -host <hostname> -port 50000`

     `db2cli writecfg add -dsn <alias> -database BLUDB -host <hostname> -port 50000`

2. 要通过连接到使用 `db2dsdriver.cfg` 文件中条目的 {{site.data.keyword.dashdbshort_notm}} 数据库来启动 CLPPlus，请运行以下命令：

   - Windows 环境： 

     `clpplus <userid>@<alias>`

   - Linux 环境：

     `clpplus -nw <userid>@<alias>`

     其中：
     
     - `<userid>` 是您预先收集的连接凭证中的用户标识。
     - `<alias>` 是您已使用 **db2cli writecfg** 命令创建的别名。

   运行此命令将打开 CLPPlus 窗口。

3. 在 CLPPlus 窗口中，输入您的密码。这将显示数据库信息，后跟 SQL 提示符。样本输出如下所示：

```
   Hostname = 192.0.2.0
   Database server = DB2/LINUXX8664  SQL10054
   SQL authorization ID = smith
   Local database alias = BLUDB
   Port = 50001
   
   SQL>
```

### 结果

现在，您可以输入 CLPPlus 命令或 SELECT 语句，以及运行脚本来处理数据库中的数据。

### 示例

以下示例使用一个简短的脚本，该脚本从样本表 `GOSALES.BRANCH` 中检索行。该脚本文件名为 `cities.sql`，位于本地 Windows 计算机上的 `C:\temp` 目录中。`cities.sql` 文件包含以下文本：

```
SET ECHO ON
SELECT branch_code, city from GOSALES.BRANCH;
```

#### 示例 1 

要以交互方式运行该脚本，请执行以下操作：

1. 通过运行以下命令，使用您的用户标识以及在 `db2dsdriver.cfg` 文件中创建的别名来启动 CLPPlus：

   `clpplus <user_id>@<alias>`
2. 输入您的密码。
3. 在 SQL 提示符处，输入以下文本：

   `start C:\temp\cities.sql`

#### 示例 2

使用您的用户标识以及在 `db2dsdriver.cfg` 文件中创建的别名来启动 CLPPlus，然后在一步中运行该脚本：

`clpplus <user_id>/<password>@<alias> @C:\temp\cities.sql`

`cities.sql` 脚本的样本输出如下所示：

```
BRANCH_CODE CITY
----------- --------------------------------------------------
          6 Paris
          7 Milano
          9 Amsterdam
         13 Hamburg
         14 München
         15 Kista
         17 Calgary
         18 Toronto
         19 Boston
         20 Seattle
         21 Los Angeles
         22 Miami
         23 Lyon
         24 Distrito Federal
         25 Tokyo
         26 Osaka City
         28 Melbourne
         29 Bilbao
         30 Sao Paulo
         31 Kuopio
         32 Seoul
         33 Singapore

BRANCH_CODE CITY
----------- --------------------------------------------------
         34 Shanghai
         35 London
         36 Birmingham
         37 Zürich
         38 Heverlee
         39 Wien
         40 Geneve

29 rows were retrieved.
```


