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

# 安全套接字层 (SSL) 支持
{: #ssl_support}

{{site.data.keyword.dashdbshort_notm}} 数据库使用由第三方数字认证中心 (CA) 签发的证书进行 SSL 连接。
{: shortdesc}

CA 证书是 Db2 驱动程序包的一部分。如果应用程序与 Db2 驱动程序包中的驱动程序连接，那么无需单独下载该证书。您可以通过 Web 控制台来下载 Db2 驱动程序包。

但是，如果应用程序有自己的驱动程序，那么您可能需要单独下载该证书。您可以通过 Web 控制台来下载该证书。

安全套接字层 (SSL) 是一种用于确保通信隐私的安全协议。SSL 使客户机和服务器应用程序能够以防止窃听、篡改和伪造消息的方式进行通信。支持 SSL 的客户机应用程序使用标准的加密技术来帮助确保通信安全。

将应用程序配置为使用 SSL 连接到 {{site.data.keyword.dashdbshort_notm}} 数据库取决于您公司的策略。可用于连接到数据库的标准协议和 SSL 协议都以加密数据形式传输用户名和密码。如果要确保完全的端到端安全性，请通过 SSL 连接来传输所有数据库信息，包括敏感数据和元数据。管理员可以通过更改 Web 控制台上的设置来强制执行 SSL 连接。


