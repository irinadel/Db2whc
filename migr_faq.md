---

copyright:
  years: 2024, 2023
lastupdated: "2024-10-16"

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
{:video: .video}

# Migration FAQs
{: #migr_faq}

## What do I need to do with my applications before the migration?
{: #q_appl}

### For users of the Db2 Warehouse on Cloud REST API

Ensure your application is using v4 of the {{site.data.keyword.dashdbshort_notm}} on Cloud REST API. Additionally, all API requests must include the `x-deployment-id` header, or an error will be returned when using the next-generation warehouse. More information about the REST API can be found [here]( https://cloud.ibm.com/docs/Db2whc?topic=Db2whc-con_rest_api).

### For users of the Db2 runtime client

Please ensure you are using Db2 version 11 clients or later. If you are using a connectivity driver supplied by a third party, verify with the vendor that it is compatible with Db2 version 11. Also, ensure that all connections use SSL via port `50001`, as non-SSL connections are not supported in the next-generation warehouse.

### CLPPlus IDA functionality

The IDA functionality of CLPPlus (which allows development and registration of UDX in C++, R, Python) is no longer supported for use with {{site.data.keyword.dashdbshort_notm}}.

### For users of IBM Lift

Lift users will need to download the latest version of the Lift tool from IBM. This will be required after the tool is updated to use the v4 DBAPI.

## What items will IBM retain for me, and what will I need to recreate?
{: #q_recreate}

### Database-level objects:

All your database-level objects, such as tables, views, statistics, and procedures, will remain intact after the migration.

### User Credentials:

All user credentials will be migrated. 

### UDXes (User-Defined Extensions):

UDXes written in C++ will be migrated successfully. However, new UDXes *cannot be registered* after the upgrade.

### Server Connections:

   * Incoming connections to your Gen 2 instance (created via `CREATE SERVER`) may need to be reestablished.
   * Outgoing connections from your Gen 2 instance (created via `CREATE SERVER`) will be migrated. For private/vpn, you need to ensure the two machines can communicate.

### Landing Zone Files:

Files stored in your Gen 2 landing zone will *not be persisted* during the upgrade. Be sure to download and back up any files prior to migration, as IBM will not be responsible for lost contents in the landing zone.

### Auditing:

Your audit policies and data will be retained. During the migration, auditing on your v2 instance will be halted and started on the v3 instance with the same policies. Any audit data stored outside the AUDIT tables will be copied asynchronously. If you are auditing to tables, support for this configuration will end, and it’s recommended to reconfigure your audit data to be written to an S3 cloud object storage (COS) instance. If you’re already auditing to COS, your configuration will be migrated, but you may notice a change in audit report format. For more details, see our [documentation](https://www.ibm.com/docs/en/db2woc?topic=activities-viewing-archived-audit-records){:external}. To reconfigure to COS, follow [these steps](https://cloud.ibm.com/docs/Db2whc?topic=Db2whc-auditing#enable-auditing). If unsure of your current configuration, go to Audit under Administration, where you’ll be prompted if you’re using audit to tables.

### Key Protect:

Your Key Protect Integration configuration will be retained.

## What is the testing period after the new system is created?
{: #q_test_period}

After successfully creating the new system (Step 1), you have a 14-day period to test and complete the final upgrade process (Step 3). The trial end date will be displayed, and once the 14-day period is over, billing for the new instance will automatically begin. If the prior system has not been deleted by this point, it will also continue to incur charges.

## What should I do if I encounter an error during any of the steps?
{: #q_error}

While the upgrade process is robust, in the event an error does happen, you will receive a prompt stating, *“There was an error during this process. Please open a support ticket.”*. In such cases, simply open a support ticket as usual, and our support team will assist you in resolving the issue promptly.

## What should I expect after the upgrade?
{: #q_after_upgrade}

The self-service migration tool, will migrate your system to the new generation of {{site.data.keyword.dashdbshort_notm}} and VPC Gen2 infrastructure on IBM Cloud. It will retain all other levels of software, including the underlying database. In order to take advantage of the capabilities in the new generation of the product, a database update option will be available to be applied. 

For most customers, you can resume working with your data as before. However, certain customers may encounter specific circumstances requiring further actions:

*Private Connections from IBM Cloud VPC:* If you have workloads running on IBM Cloud VPC, you can leverage private connectivity (Private Link) to connect securely to your Db2 Warehouse instances using IBM Cloud’s private network. Follow the steps outlined [here](https://cloud.ibm.com/docs/Db2whc?topic=Db2whc-connect_options#connecting-to-db2-warehouse-on-cloud-with-private-link).

To enable private connectivity:
   * First, enable private connectivity through the console.
   * Then, create a *Virtual Private Endpoint Gateway* on your VPC. The private endpoint and port will be provided in the Connections section of the console.

Private connectivity is a *regional service*, meaning that the Virtual Private Endpoint Gateway must be created in the same region as your Db2 Warehouse on Cloud instance.
{: note}

*VPN Connectivity:* If you currently connect via VPN, follow the instructions in the [VPN Connectivity guide](https://cloud.ibm.com/docs/Db2whc?topic=Db2whc-connect_options#vpn) to ensure proper setup after the upgrade.
