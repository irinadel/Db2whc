---

copyright:
  years: 2014, 2019
lastupdated: "2018-06-15"

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

# 从 IBM PureData System for Analytics (Netezza) 迁移
{: #pda}

{{site.data.keyword.Bluemix_notm}} Mass Data Migration Service (MDMS) 可用于将数据从约 25 TB 及更大的大型 IBM PureData Systems for Analytics (Netezza) 数据库迁移至 {{site.data.keyword.Bluemix_notm}} 上完全受管的 {{site.data.keyword.dashdblong}} 数据库。

MDMS 提供快速、简单且安全的方式将太字节级别到拍字节级别的数据物理传输至 {{site.data.keyword.Bluemix_notm}}。MDMS 是具有 120 TB 可用存储容量的移动存储设备。此设备使您只需采用单个服务，就能克服各种常规传输难题（例如，高成本、长传输时间和安全问题）。
{: shortdesc}

![Mass Data Migration Service 设备的视图](images/mdms.svg)

## 在请求设备时需要什么
{: #prereq}

1. 存储设备的网络设置
   - 静态 IP 地址
   - 用于启用数据传输的网络掩码
2. 远程计算机的网络设置
   - 静态 IP 地址
   - 网络掩码 
   - 用于访问用户界面 (UI) 的缺省网关
3. Cloud Object Storage 下载目标<br/>
   在美国交叉区域或美国南部区域中您必须至少有一个 {{site.data.keyword.cos_full}} 帐户和一个存储区，才能填写请求表单。如果您目前还没有 {{site.data.keyword.cos_full_notm}}} 帐户，请先创建一个帐户，然后再请求 MDMS 设备。有关更多信息，请参阅：[关于 {{site.data.keyword.cos_full}}](/docs/services/cloud-object-storage?topic=cloud-object-storage-about#about){:new_window}。
   {: important}

## 步骤 1：创建请求
{: #create-req}

1. 使用您的唯一凭证来登录到 [{{site.data.keyword.slportal}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://control.softlayer.com/){:new_window}。
2. 从“导航栏”中选择**存储 > 数据迁移 > Mass Data Migration** 以访问 MDMS 登录页面。
3. 单击**请求设备**以打开订购表单。
4. 填写 **Mass Data Migration** 订购表单中的每个字段。
   - **送货地址**：此表单不进行预填充，并且每个字段均可编辑。在“收件人”字段中提供将接受设备交付的人员的姓名。在选取交货位置时，请考虑设备重量（含箱子 30 千克（66 磅））和可达性。<br/>（**注**：设备配备有脚轮和弹出手柄以方便搬运。）
   - **主要迁移联系人**：此表单不进行预填充。每个字段均可编辑。可添加多个人员。
   - **数据中心网络配置**：装运前，针对 MDMS 设备上的 Eth3 端口的预先供应，提供网络配置详细信息。
   - **数据卸载目标**：从列表中选择现有目标帐户。
   - **请求名称**：输入名称以帮助跟踪订单。
5. 在阅读提供的每个服务协议后，选择**我已阅读并同意 Mass Data Migration 协议的完整条款**复选框。
6. 单击**提交请求**以提交请求。单击**取消**以完全放弃表单并返回至 MDMS 登录页面。

## 步骤 2：准备和装运
{: #prep-ship}

在提交请求后，请求凭单的状态显示为*正在处理请求*。在处理请求后，{{site.data.keyword.IBM}} 开始预先配置下一个可用设备，并且[请求 ![外部链接图表](../../icons/launch-glyph.svg "外部链接图标")](https://control.softlayer.com/storage/mdms){:new_window} 网格上的状态将显示*正在准备设备*，后跟*正在等待装运*。在请求进入*正在等待装运*状态后，将无法取消。 

承运方提取设备以发送到您的位置。此时，请求状态更新为*设备已发货*。将在[请求 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://control.softlayer.com/storage/mdms){:new_window} 网格的**订单详细信息**部分中与您共享跟踪编号。

## 步骤 3：接收和连接
{: #rec-con}

<!-- **[Editor's note: What to keep from this section immediately below?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
1. The device arrives pre-configured for you. Basic [powering/connectivity instructions](docs/infrastructure/mass-data-migration/user-instructions.html) are included.  **[Editor's note: Are the instructions included in the MDMS package? If so, are they different from the instructions found with the "powering/connectivity" link?]**<br/>
  **Note**: User name and storage pool password is provided separately. Check the **Request Details** in your [Requests ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/storage/mdms){:new_window} grid for the credentials.
2. Point your browser to the static IP address that you provided in the order form. **[Editor's note: Is this done on PDA? What system is the static IP address for?]**
3. Log in. Enter password to unlock the empty storage pool. **[Editor's note: How is this done?]**<br/>
   **Note**: See the **Request Details** of your [Requests ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/storage/mdms){:new_window} grid for the password.
4. Mount the NFS share on your server. **[Editor's note: How is this done?]**
5. Rerun your DataShuttle inventory to ensure any new files are captured. **[Editor's note: Is "DataShuttle inventory" a command that is run on PDA?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& -->

### 概述

{{site.data.keyword.cloud}} Mass Data Migration 设备是便携式存储设备，能够提供可安装网络文件系统 (NFS) 或 FileNet Content Federations Services (CF)S 共享，并且通过 Web 浏览器界面进行管理。设备将运至您的数据中心，现场装入数据，返回至 {{site.data.keyword.BluSoftlayer_full}} 数据中心，然后将数据装入您的 {{site.data.keyword.cos_full}} 帐户。

### 电源


设备随附一根 C13-US 电源线（[IEC 60320 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://en.wikipedia.org/wiki/IEC_60320){:new_window}）。如果在美国之外使用设备，那么可能需要电源适配器。

MDMS 设备接受所有标准功率范围。![功率范围](/images/PowerRating.png)

### 以太网连接

要建立两个以太网连接。一个用于通过浏览器来管理设备，另一个用于在源数据所在的同一子网上移动数据。

这两个端口在设备中以 RJ45 接口提供，并提供了 CAT6A 电缆。提供的铜缆 SFP+ 适配器用于转换 RJ45。适配器适用于所有交换机制造商的产品。这些适配器位于运输箱盖下方的小袋中。

- Eth1 (1GbE-B) 用于设备管理，因此，必须在 IP 地址配置中指定网关。在设备通电后可在 LCD 屏幕上进行查看（请参阅 [IP 地址配置](#ip_cfg)部分）。

- Eth3 (10GbE-B) 用于数据传输。此连接必须位于与源数据相同的子网上或者可直接连接到服务器（如果需要）。

如果需要不同外形规格的以太网连接，那么必须提供转换器。

### 用户的分步指示信息

1. MDMS 设备随预先配置的 IP 地址、用户名、锁定的存储池和 NFS 共享一起送达。用户密码和存储池密码将通过单独的电子邮件告知您。

2. 确定放置设备的最适合的位置；可接入电源和以太网（1GbE 和 10GbE）连接并且附近人流量很少。

3. 放置要连接的设备。在使用期间，可留在运输箱中。确保设备为室温并且无冷凝。使用箱盖下随附的电源线连接到电源。开启设备。<br/>
        有两个电源开关。
    {: note}

    ![电源开关](/images/MDMSPowerSwitch.png)
    该设备无需从便携式机箱中取出。
    {: note}

4. 从箱盖中取出 CAT6A 电缆，将其连接到图中所示的 Eth3 (10GbE-B) 端口。
    ![Eth1 和 Eth3 端口位置](/images/MDMSNewEth1and3.png)

5. 将提供的 CAT6A 连接到 SFP+ 适配器，然后再连接到 10Gb 交换机。

6. 如果可通过浏览器 `https://<your_Eth3_IP_Address>` 访问针对 Eth3 配置的 IP 地址，那么继续至下一步。 

   否则，连接到 Eth1 (1GbE-B) 端口。打开浏览器，输入 `https://<your_Eth1_IP_Address>`。输入网络配置的相应 Eth1 IP 地址。接受证书例外。<br/>   如果需要更改 Eth3 或 Eth1 的任何 IP 设置，请参阅 [IP 地址配置](#ip_cfg)部分。
   {: note}

7. 使用所提供的用户名和密码登录。<br/>
    ![登录页面](/images/Login.png)

8. 工作流程向导从左到右依次显示可访问的常用特定项。<br/>
    ![工作流程图标](/images/workflow.png) <br/>
        可使用 GUI 左上角的**工作流程管理器**重新打开工作流程。
    {: note}

9. 激活预配置的存储池：
    - 单击**解锁并启动存储池**。
    - 输入存储池口令，然后单击**确定**。
    ![激活存储池](/images/UnlockPool.png)

10. 缺省情况下，共享已启用 NFS 和 SMB 协议，并且共享无访问限制。要限制对此共享（NFS 或 SMB）的访问，请右键单击共享名称并选择相应的菜单项。<br/>
    ![限制共享访问](/images/ShareControls.png)

11. 启用存储池后，可安装 NFS 共享。在工作流程中，单击**查看网络共享**以查看网络共享视图。关闭工作流程，右键单击共享，然后选择**查看 Mount 命令**以查看共享名称和安装信息。在源服务器上安装共享。在安装共享时请确保指定 10 GB 链路的 IP 地址。
    ![安装共享](/images/MountCommand.png)

## 步骤 4：复制数据和装运
{: #copy-ship}

<!-- &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&

1. Run the DataShuttle copy to move the data. **[Editor's note: What is "DataShuttle"? Is "DataShuttle copy" a command that is run on PDA?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& -->

1. 将数据复制到 NFS 共享。选择以下一个方法以从 Netezza 数据库抽取数据：
    1. 运行 **nz_backup** 实用程序的以下示例：

       `/nz/support/contrib/bin/nz_backup –db <db_name> –d <target_directory>  ascii threads 4`

       **注**：`<target_directory>` 是安装到 Netezza 服务器的 MDMS 设备上的 NFS 共享。
   
    2. 运行 CREATE EXTERNAL TABLE 语句的以下示例：

       `CREATE EXTERNAL TABLE '<path_to_mdms_device>/<file_name>' SELECT * FROM <table name>`

       **注：**如果将 `USING` 子句选项用于数据导出，请记住或保存子句选项。稍后在从 {{site.data.keyword.Bluemix_notm}} Object Storage 执行的外部表装入过程中，将复用此子句。

       有关 SQL 语句的更多信息，请参阅：[CREATE EXTERNAL TABLE 语句 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.sql.ref.doc/doc/r_create_ext_table.html){:new_window}。 

<!--       - Provide the {{site.data.keyword.Bluemix_notm}} team with the "USING" clause that was used for data export. The clause is reused during the load process on {{site.data.keyword.Bluemix_notm}}.
       - Select FORMAT = "Text"
-->

2. 在工作流程中，单击**查看网络活动**以在 10Gb/秒链路上将数据传输到设备时在 GUI 中显示入站以太网负载。![查看活动](/images/UserGuide13.png)

3. 在工作流程中，单击**查看存储池**可监视设备上的存储用量和 IOPS。
    ![查看存储池](/images/UserGuide14.png)

4. 在复制完成时，正常关闭系统。关闭设备也会锁定存储池。在工作流程中，单击**关闭设备...**。  
    ![设备关闭 UI 按钮位置](/images/Shutdown.png)

5. 断开设备连接。将电源线、以太网电缆和 SFP+ 适配器放回盖子下面各自的存储位置。

6. 将随附的装运标签贴在设备上。通知托运人并将设备返回到 {{site.data.keyword.BluSoftlayer_full}} 数据中心。在到达数据中心后，会将数据装入到 {{site.data.keyword.cos_full_notm}} 存储区。

在将设备返回给 {{site.data.keyword.BluSoftlayer}} 团队后，请求状态更改为*设备已收到*。

## 步骤 5：卸载和访问
{: #offload}

在数据传输过程中，请求状态显示为*正在卸载数据*。在完成到 {{site.data.keyword.objectstorageshort}} 存储区的迁移后（*卸载完成*），状态再次发生更改。在完成到 Cloud Object Storage 存储区的高速卸载后，数据立即变为可访问。 

在完成到 Cloud Object Storage 存储区的数据迁移后，您可以继续[将数据导入到 {{site.data.keyword.dashdbshort_notm}} 数据库](#import)。

## 步骤 6：从 {{site.data.keyword.Bluemix_notm}} Object Storage 导入数据
{: #import}

要直接使用“外部表”从 {{site.data.keyword.Bluemix_notm}} Object Storage 装入数据，以下是示例 SQL 语句：

```
INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net', 
  '<S3-access-key-ID>',
  '<S3-secret-access-key>', 
  '<my_bucket>'
     )
  )      
```

**注：** 
* 请务必使用通过 CREATE EXTERNAL TABLE 语句从 PureData System for Analytics (Netezza) 数据库抽取数据时所用的相同 `USING` 子句选项。
* 对于 {{site.data.keyword.Bluemix_notm}} Object Storage，要在创建新服务凭证时创建 HMAC 凭证，请在*添加内联配置参数*字段中指定 {"HMAC:true"}。

有关从 {{site.data.keyword.Bluemix_notm}} Object Storage 导入数据的指导教程，请参阅：[IBM Db2 Warehouse on Cloud guided demo: Explore data loading ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud/){:new_window}。

## 步骤 7：擦除 MDMS 设备
{: #erase}

{{site.data.keyword.IBM}} 按照美国国防部要求的级别实施数据擦除以永久从 MDMS 设备擦除您的数据。完成后，请求状态显示为*擦除完成*。

## 其他注释
{: #notes}

### 存储区中的唯一性

为确保复制到存储区时对象名称唯一，请在对象名称中包含文件路径作为前缀。例如，在复制到存储区时，`/root/user/` 文件夹中的 config.ini 文件将重命名为“root/user/config.ini”。

### 存储区

如果目标存储区不存在，会进行创建。如果确实存在，那么该存储区必须为空，否则无法继续复制。

### 文件系统

在扫描过程中，将跳过符号链接和硬链接。

### IP 地址配置
{: #ip_cfg}

设备上的 LCD 显示屏可用于配置以太网端口的 IP 地址。通过使用**向上箭头**、**向下箭头**、**esc** 和 **enter** 按钮，浏览 LCD 显示屏。**enter** 按钮可使您进入菜单，而 **esc** 则使您退出菜单。

![LCD 显示屏](/images/MDMSLCD.png)

在编辑 IP 地址或子网掩码时，**enter** 使您一次前进一个字符；**esc** 则使您一次后退一个字符。**向上箭头**和**向下箭头**切换所选位置的数字。

使用 **esc** 可返回至先前菜单。  

转至**更新...** 菜单项，然后按 **enter** 以保存设置。
