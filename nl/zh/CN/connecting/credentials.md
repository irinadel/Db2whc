---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# 数据库详细信息和连接凭证
{: #db_details_cxn_creds}

要配置本地开发环境以及将应用程序和工具连接到 {{site.data.keyword.dashdbshort_notm}} 数据库，您需要了解数据库详细信息和连接凭证。
{: shortdesc}

## 数据库详细信息
{: #db_details}

下面是将应用程序和工具连接到数据库时需要的重要数据库详细信息：

- *主机名* - 服务器的主机名。
- *端口号* - 供数据库管理器用于 TCP/IP 通信。（请注意，服务随附两个端口号，其中一个用于安全套接字层 (SSL) 连接，另一个端口用于非 SSL 连接。）

   如果需要，可以使用 ping 命令或 nslookup 命令并指定主机名，以获取服务器的 IP 地址。
- *数据库名称* - Db2 数据库名称，通常为 BLUDB。

## 连接凭证
{: #cxn_creds}

有三种类型的凭证：

- *IBM 标识* - 如果使用的是 {{site.data.keyword.Bluemix_notm}}，这是您用于登录到 {{site.data.keyword.Bluemix_notm}} 的标识。但并不是您用于将应用程序或工具连接到 Db2 Warehouse on Cloud 数据库的标识。
- *Db2 数据库凭证* - 服务随附可用于将应用程序和工具连接到数据库的数据库用户标识和密码。
- *管理员创建的用户* - 某些 {{site.data.keyword.dashdbshort_notm}} 套餐允许管理用户创建新用户。这些管理员创建的用户标识和密码可用于直接登录到 Web 控制台 URL，并可用于从应用程序或工具连接到 Db2 数据库。

## 在何处可找到数据库详细信息和连接凭证
{: #location}

您可以从以下位置收集这些信息：

- *管理员* - 如果您不是 Db2 实例的所有者或管理员，那么可以从管理员获取数据库详细信息和连接凭证。
- *Db2 Web 控制台* - Web 控制台中提供了数据库详细信息和凭证。
- 如果使用的是 {{site.data.keyword.Bluemix_notm}}： 
   
   - *{{site.data.keyword.Bluemix_notm}} 仪表板* - 在 {{site.data.keyword.Bluemix_notm}}“仪表板”上查看服务时，可在“服务凭证”区域中查看数据库详细信息以及数据库用户标识和密码。
   - *`VCAP_SERVICES`* - `VCAP_SERVICES` 是 {{site.data.keyword.Bluemix_notm}} 中的环境变量，其中包含 JSON 格式的数据库详细信息和凭证。在 {{site.data.keyword.Bluemix_notm}}“仪表板”中查看服务的服务凭证时，显示的就是 `VCAP_SERVICES` 的内容。将其他 {{site.data.keyword.Bluemix_notm}} 服务或应用程序与服务绑定后，这些其他服务或应用程序就可以通过读取 `VCAP_SERVICES` 以编程方式访问数据库详细信息和凭证。
