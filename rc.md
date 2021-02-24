---

copyright:
  years: 2014, 2021
lastupdated: "2021-02-24"

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

# Resource controller (RC)
{: #rc}

In the coming days and weeks, the {{site.data.keyword.dashdblong}} service will be supporting resource controller (RC) across all regions. The RC is responsible for controlling and tracking the lifecycle of resources in an {{site.data.keyword.Bluemix_notm}} account. 
{: shortdesc}

Resources is a broad term that can mean anything from an instance of a service like {{site.data.keyword.dashdbshort_notm}}, a Cloud Foundry application, a virtual machine, a container, a software image, a data set, or other entity associated with an account.

After this change is made, all new {{site.data.keyword.dashdbshort_notm}} service instances that you create will be in a resource group. It is recommended that you create a migration plan to move your existing {{site.data.keyword.dashdbshort_notm}} service instances from their current Cloud Foundry org and space to a resource group.

To be able to use upcoming features such as IBM Key Protect, you must migrate your Cloud Foundry service instances to RC.
{: important}

## Migrating Cloud Foundry services to RC
{: #mig_cf_rc}

Available with the resource controller is the ability to manage your service and app resources by using *resource groups*. Resource groups provide finer-grained access control by using [IBM Cloud Identity and Access Management (IAM)](/docs/Db2whc?topic=Db2whc-iam){: external}, the ability to connect service instances to apps and services across different regions, and an easy way to view usage per group. After you migrate to resource groups, you must assign the "manager" service access role to other users to allow them to log in to {{site.data.keyword.dashdbshort_notm}}.

For more information about how and why you should migrate your Cloud Foundry service instances and apps to resource groups, see [Migrating Cloud Foundry service instances and apps to a resource group](/docs/account?topic=account-migrate){: external}.

## Additional information
{: #rc_add_info}

- [Creating resources](/docs/account?topic=account-manage_resource){:external}
- [Best practices for organizing resources and assigning access](/docs/account?topic=account-account_setup){: external} (includes several use case examples)
- [Managing resource groups](/docs/account?topic=account-rgs){: external}
- [Giving access to resources in resource groups](/docs/account?topic=account-rgs_manage_access){: external}
- [Managing connections](/docs/account?topic=account-connect_app){: external} (includes creating a service credential, and binding the resource to an app in the same or a different IBM Cloud region)
- [General CLI (ibmcloud) commands](/docs/cli?topic=cli-ibmcloud_cli){: external}
- [Creating, deleting, and binding Cloud Foundry services](/docs/account?topic=cli-ibmcloud_commands_services){: external} (lists IBM Cloud API replacement commands for older Cloud Foundry commands)

<!-- [IBM Key Protect](/docs/Db2onCloud?topic=Db2onCloud-key-protect)and [Copy Database](/docs/Db2onCloud?topic=Db2onCloud-cp_db)-->

