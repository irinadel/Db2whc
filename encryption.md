---

copyright:
  years: 2014, 2020
lastupdated: "2020-04-15"

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

# Data security & encryption
{: #encryption}

The {{site.data.keyword.dashdblong}} service has security built into all levels of its architecture.
{: shortdesc}

The following methods are used to secure your data:
- Data at rest and database backups are encrypted using NIST SP 800-131A compliant cryptographic algorithms
- Data in motion is encrypted through SSL/TLS
- When deployed to IBM Cloud, backplane network connectivity is supported through IBM Cloud Service Endpoints
- When deployed to Amazon Web Services, backplane network connectivity is supported through Amazon Web Services PrivateLink
- Database-level security is supported through Role-Based Access Control (RBAC) and Row and Column Access Control (RCAC)

Encrypted connections are enforced by default. For more information, see [SSL connectivity](/docs/Db2whc?topic=Db2whc-ssl_support).





