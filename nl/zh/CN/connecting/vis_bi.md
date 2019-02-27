---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-24"

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

# 数据可视化/BI
{: #data_vis_bi}

您还可以将外部应用程序和工具连接到 {{site.data.keyword.dashdbshort_notm}}，以使用其进一步管理或分析数据。
{: shortdesc}

## Cognos Analytics
{: #cognos}

您可以针对云中的数据而不是内部部署数据库中的数据来运行 IBM Cognos® 报告。将数据装入到 {{site.data.keyword.dashdbshort_notm}} 数据库后，可设置 JDBC 驱动程序，然后使用 Cognos 管理工具来创建数据库连接。<!--These instructions explain how to connect to the database from Cognos version 10.2.1.-->
{: shortdesc}

观看以下视频以了解如何创建连接。

<iframe class="embed-responsive-item" id="youtubeplayer" title="通过 Cognos Analytics 创建连接" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TRUEPVHGi0s?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

有关更多信息，请参阅[连接 Cognos Analytics ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/en/SSEP7J_11.0.0/com.ibm.swg.ba.cognos.ug_cra.doc/c_create_ds.html#create_ds){:new_window}

## Looker
{: #looker}

您可以将 Looker 连接到 {{site.data.keyword.dashdbshort_notm}} 数据库。Looker 是一个商业智能应用程序和大数据分析平台，通过该平台，您可以探索、分析和共享实时业务分析。
{: shortdesc}

[连接 Looker ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://docs.looker.com/setup-and-management/connecting-to-db){:new_window}

## Tableau
{: #tableau}

以下指示信息说明如何将 Tableau 连接到 {{site.data.keyword.dashdbshort_notm}} 数据库，并应用于 Tableau Desktop <!--version 8.x-->，而且类似的步骤可以用于其他 Tableau 工具。
{: shortdesc}

### 先决条件
{: #prereq1}

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](connecting.html#prereqs)。

### 过程
{: #proc1}

1. 在 Tableau Desktop 中，打开工具中用于定义数据库连接的窗口或页面。
2. 在开始页面中，单击**连接到数据**。
3. 从**数据源**列表中，选择要用于数据库连接的数据源或驱动程序。在列表的**服务器上**部分中，选择 **IBM Db2**。
4. 在 **IBM Db2 连接**窗口中，按下表输入连接信息。

|Tableau 字段|Db2 连接信息字段|
|---------------|-----------------------------------|
|步骤 1：输入服务器名称|主机名|
|步骤 2：端口|端口号|
|步骤 3：输入该服务器上的数据库|数据库名称|
|用户名|用户标识|
|密码|密码|
{: caption="表 1. Tableau 中用于连接信息的字段" caption-side="top"}

5. 单击**连接**以建立连接。Tableau 提供了多个选项用于连接到数据。要充分利用 {{site.data.keyword.dashdbshort_notm}} 数据库，请选择**连接实时**选项。

## Microsoft Excel
{: #excel}

以下指示信息说明如何将 Microsoft Excel <!--2010-->连接到 {{site.data.keyword.dashdbshort_notm}} 数据库。
{: shortdesc}

### 先决条件
{: #prereq2}

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](connecting.html#prereqs)。

您必须在本地计算机上安装 Db2 驱动程序包或 IBM® Data Server Driver Package。 

**限制**：仅 Windows 操作系统上支持 Excel 与 {{site.data.keyword.dashdbshort_notm}} 的连接。

### 过程
{: #proc2}

1. 在 Web 控制台中，转至**运行 SQL** 页面。
    
2. 在编辑器文本框中输入一个或多个 SELECT 语句。

3. 单击其中一个“运行”选项。

4. 单击 **Excel ODC 文件**。

5. 在 Excel 中下载并打开 `BLUExcel.odc` 文件。如果显示了安全通知，请单击**启用**。

6. 单击**打开**以连接到 {{site.data.keyword.dashdbshort_notm}} 数据库。这将打开**连接到 Db2 数据库**对话框。

7. 输入用于登录到 {{site.data.keyword.dashdbshort_notm}} 的用户标识和密码。要获取用户标识和密码，请单击 Web 控制台中的**连接**或 Web 控制台中的**连接 > 连接信息**。

8. 确保连接方式为`共享`，然后单击**确定**。

### 结果
{: #results2}

查询结果将显示在 Excel 电子表格中。这些结果与结果查看器中显示的结果相同。现在，您可以使用 Excel 来生成图表和报告并分析数据。有关如何执行此操作以及如何通过 Web 控制台对数据运行 SQL 查询的更多信息，请参阅： 
- [教程：使用 Excel 生成图表和报告 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/explore_excel_reports.html){:new_window}
- [使用 Excel 进行分析 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/exploreexcel.html){:new_window}

## Esri ArcGIS for Desktop
{: #esri_arcgis}

您可以将 Esri ArcGIS for Desktop <!--version 10.3.1 -->连接到 {{site.data.keyword.dashdbshort_notm}} 数据库，然后将其用于分析和可视化地理空间数据。
{: shortdesc}

### 先决条件
{: #prereq3}

在尝试连接到 {{site.data.keyword.dashdbshort_notm}} 数据库之前，请验证您是否具有必需的[先决条件](connecting.html#prereqs)。

您必须在计算机上安装 Db2 驱动程序包或 IBM® Data Server 驱动程序包。

### 过程
{: #proc3}

1. 根据预先收集的[连接信息](credentials.html)来确定 ODBC DSN 数据。

2. 创建新连接：
      
   a. 在 ArcCatalog 目录树中，打开“数据库连接”节点，然后单击**添加数据库连接**。
        
   b. 在“数据库连接”向导中，执行以下操作：
   - 从“数据库平台”下拉列表中选择 **Db2**。
   - 在**数据源**字段中输入以下字符串：
     ```
     HostName=<hostname>;Port=<port>;Database=<database>;
     CLIENTBUFFERSUNBOUNDLOBS=1;LOBCACHESIZE=50000000;
     FET_BUF_SIZE=256K  
     ```

     其中，`<hostname>`, `<port>` 和 `<database>` 是占位符，表示您先前记录的主机名、端口号和数据库名称。
            
   - 选择**数据库认证**作为认证类型。
            
   - 在相应的字段中指定您的用户名和密码（您先前记录的用户标识和密码）。
            
   - 按**确定**。
        
     ![“数据库连接”向导](images/2_gs_conn.jpg)

### 结果
{: #results3}

Esri ArcGIS for Desktop 的 ArcCatalog 组件现在已连接到 {{site.data.keyword.dashdbshort_notm}} 数据库。 


