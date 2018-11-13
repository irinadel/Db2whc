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

# Data Science
{: #overview}

您还可以将外部应用程序和工具连接到 {{site.data.keyword.dashdbshort_notm}}，以使用其进一步管理或分析数据。
{: shortdesc}

## Watson Studio
{: #watson_studio}

在 IBM Watson Studio（原先的 Data Science Experience）中创建项目后，可向其添加数据资产，以便您可以使用数据。项目中的所有合作者都自动有权访问项目中的数据。
{: shortdesc}

旧项目和 IBM Watson 项目的数据添加方式以及可以从中添加数据的位置有所不同。IBM Watson 项目使用的是 {{site.data.keyword.Bluemix_notm}} Object Storage。如果项目使用的是 Object Storage OpenStack Swift，说明该项目是旧项目。 

### 要在 IBM Watson 项目中创建新连接，请执行以下操作：

1. 单击**添加到项目 > 连接**。
    
2. 选择数据源。
    
3. 输入数据源所需的连接信息。通常，您需要提供主机、端口号、用户名和密码等信息。
    
4. 您可以通过连接到 {{site.data.keyword.dashdbshort_notm}} 来发现资产，借此您有能力通过该连接将所有表作为数据资产添加到项目。选择**发现数据资产**，然后选择项目。
    
5. 单击**创建**。该连接将显示在**资产**页面上。

观看以下视频以了解如何创建连接并将连接的数据添加到项目。

<iframe class="embed-responsive-item" id="youtubeplayer" title="创建连接并将连接的数据添加到项目" type="text/html" width="640" height="390" src="//www.youtube.com/embed/U7-gCbo4QtM?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

### 要在旧项目中创建新连接，请执行以下操作：

1. 在项目的**资产**页面中，单击**查找并添加数据**图标。
    
2. 在**连接**窗格上，单击**创建连接**。

3. 输入名称和描述，然后选择服务类别：

   **数据服务** = {{site.data.keyword.Bluemix_notm}} 数据服务

   选择**数据服务**时，现有 {{site.data.keyword.Bluemix_notm}} 数据服务会显示在**服务实例**列表中。

4. 从列表中选择该服务或数据库服务器。

5. 输入连接信息：

   选择**数据服务**时，现有 {{site.data.keyword.Bluemix_notm}} 数据服务会显示在**服务实例**列表中。
    
6. 单击**创建**。连接可用于所有旧项目。
    
7. 在**连接**窗格上，选择连接并单击**应用**。

要将现有连接添加到旧项目，请执行以下操作：

1. 在项目的**资产**页面中，单击**查找并添加数据**图标。
    
2. 在**连接**窗格上，选择连接并单击**应用**。

## SPSS Statistics
{: #spss_stats}

以下指示信息说明如何创建从 IBM® SPSS® Statistics 到 {{site.data.keyword.dashdbshort_notm}} 数据库的连接。
{: shortdesc}

### 先决条件

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](connecting.html#prereqs)。

### 过程

1. 在 SPSS Statistics 中，单击**文件 > 打开数据库 > 新建查询**。
    
2. 在“数据库向导”中，单击**添加 ODBC 数据源**。
    
3. 使用“ODBC 数据源管理器”窗口为 {{site.data.keyword.dashdbshort_notm}} 数据库添加 ODBC 数据源名称 (DSN)：
        
   a. 在**用户 DSN** 选项卡上，单击**添加**。

   b. 在“创建新数据源”窗口中，选择名为 **IBM DB2 ODBC DRIVER** 的驱动程序，然后单击**完成**。

   确保选择的驱动程序不是名称类似的驱动程序，例如 `IBM DB2® ODBC DRIVER - DB2COPY`。如果该驱动程序未出现在列表中，请退出 SPSS Statistics，然后下载并安装该驱动程序。请参阅 [Db2 驱动程序包](driver_pkg.html)。
        
   c. 在“ODBC IBM 驱动程序 - 添加”窗口中，输入数据源名称（通常是所要连接的数据库的名称），然后单击**添加**。
        
   d. 在“CLI/ODBC 设置”窗口的**数据源**选项卡上，输入预先收集的[连接信息](credentials.html)中的用户标识和密码。
        
   e. 在“高级设置”页面中，针对以下每个参数，单击**添加**以打开“添加 CLI 参数”窗口开始执行步骤，然后单击**确定**以返回到“高级设置”页面：
            
   - 选择`数据库`参数，然后单击**确定**以打开“CLI/ODBC 设置”窗口。在**暂挂值**字段中，输入预先收集的连接信息中的数据库名称。

   - 选择`主机名`参数，然后单击**确定**以打开“CLI/ODBC 设置”窗口。在**暂挂值**字段中，输入预先收集的连接信息中的主机名。

   - 选择`端口`参数，然后单击**确定**以打开“CLI/ODBC 设置”窗口。在**暂挂值**字段中，输入预先收集的连接信息中的端口号。
            
   - 选择`协议`参数，然后单击**确定**以打开“CLI/ODBC 设置”窗口。选择 **TCP/IP**。
        
   f. 单击**确定**以返回到“ODBC 数据源管理器”窗口。
        
   g. 在**用户 DSN** 选项卡上，选择数据源名称，然后单击**配置**。
        
   h. 在“CLI/ODBC 设置”窗口上，单击**连接**以测试连接。
            
   - 如果连接成功，请单击**确定**以返回到“ODBC 数据源管理器”窗口，然后单击**确定**以退出该窗口。
            
   - 如果连接不成功，请记下任何错误并进行更正，然后再次测试该连接。

## SAS
{: #sas}

以下指示信息说明如何创建从 SAS 到 {{site.data.keyword.dashdbshort_notm}} 数据库的连接。
{: shortdesc}

### 先决条件

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](connecting.html#prereqs)。

### 过程

有关如何从 SAS 连接到 {{site.data.keyword.dashdbshort_notm}} 数据库的步骤，请参阅 SAS 文档：
- [SAS/ACCESS Interface to DB2 under UNIX and PC Hosts ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://documentation.sas.com/?docsetId=acreldb&docsetTarget=p1dzq4zjg1iycgn16l4xj9nnvibt.htm&docsetVersion=9.4&locale=en){:new_window}

## R 开发环境
{: #r_dev_env}

您可能会首选使用自己的本地安装的 R 开发环境，而不使用集成在 IBM Watson Studio 中的 RStudio® 环境。例如，您可能有自己的 RStudio 安装，或者您可能首选使用其他某个开发工具（如 Rcmdr 或 Rattle）。以下指示信息说明如何将 R 开发环境连接到 {{site.data.keyword.dashdbshort_notm}} 数据库。
{: shortdesc}

### 先决条件

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](connecting.html#prereqs)。

### 过程

1. 在本地 R 环境中，通过输入以下命令安装 `ibmdbR` 软件包：

   `install.packages("ibmdbR")`

   本地 R 环境将访问 Comprehensive R Archive Network (CRAN)，然后自动下载并安装 `ibmdbR` 软件以及任何尚未安装的必备软件包。
    
2. 在 R 开发环境和 {{site.data.keyword.dashdbshort_notm}} 数据库之间创建 ODBC 驱动程序连接：
        
   a. [将数据库设置为 ODBC 数据源 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_cli_and_odbc_applications.html){:new_window}。
        
   b. 打开安装在本地的 R 开发环境。
        
   c. 在 R 提示符处，输入以下语句以创建连接。将占位符替换为预先收集的[连接信息](credentials.html)。

   - 如果本地安装的 R 开发环境在 {{site.data.keyword.dashdbshort_notm}} 数据库中运行，请运行以下语句：

     ```
     library(ibmdbR)
     host.name <- "placeholderForYourHostName"
     port <-"placeholderForPortNumber" # 50000 if not using SSL or 50001 if using SSL
     user.name <-"placeholderForYourUserName"
     pwd <- "placeholderForYourPassword"
     con.text <- paste("placeholderForYourDSNName;DRIVER=BLUDB",
                       ";Database=BLUDB",
                       ";Hostname=",host.name,
                       ";Port=",port,
                       ";PROTOCOL=TCPIP",
                       ";UID=", user.name,
                       ";PWD=",pwd,sep="")
     # Connect to using a odbc Driver Connection string to a remote database
     con <- idaConnect(con.text)
     ```

   - 如果本地安装的 R 开发环境并非在 {{site.data.keyword.dashdbshort_notm}} 数据库中运行，请运行以下语句：

     ```
     library(ibmdbR)
     driver.name <- "{placeholderForYourDriverName}"
     db.name <- "placeholderForYourDatabaseName"
     host.name <- "placeholderForYourHostName"
     port <-"placeholderForYourPort"
     user.name <-"placeholderForYourUserName"
     pwd <- "placeholderForYourPassword"
     con.text <- paste("placeholderForYourDSNName;DRIVER=",driver.name,
                       ";Database=",db.name,
                       ";Hostname=",host.name,
                       ";Port=",port,
                       ";PROTOCOL=TCPIP",
                       ";UID=", user.name,
                       ";PWD=",pwd,sep="")
     # Connect to using a odbc Driver Connection string to a remote database
     con <- idaConnect(con.text)
     ```

     **注**：用于创建连接对象的语句使用的是 `idaConnect()` 方法，而不是 `odbcConnect()` 或 `odbcDriverConnect()` 方法。
        
   d. 通过发出以下 R 命令，初始化分析软件包：

   `idaInit(con)`

   e. 要测试该连接是否有效，请发出以下 R 命令：

   `idaShowTables()`

   控制台会显示当前模式中所有表和视图的列表。

