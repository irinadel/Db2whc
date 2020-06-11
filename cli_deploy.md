---

copyright:
  years: 2014, 2020
lastupdated: "2020-02-28"

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

# Order and deploy with {{site.data.keyword.cloud_notm}} CLI
{: #deploy_with_cli}

You can order and deploy an {{site.data.keyword.dashdblong}} service by using the {{site.data.keyword.cloud_notm}} CLI.
{: shortdesc}

Complete the following steps to order and deploy a {{site.data.keyword.dashdbshort_notm}} service:

1. Ensure that your **Account Type** is upgraded from a trial type to a **Pay-As-You-Go** or to a **Subscription** type:

   [Verify your account settings](https://cloud.ibm.com/account/settings){: external}

2. Create a Cloud Foundry **Organization** and **Space** or ensure there's an existing organization and space to use:

   [Create a Cloud Foundry organization](https://cloud.ibm.com/account/cloud-foundry){: external}

3. Install the {{site.data.keyword.cloud_notm}} CLI:

   [Getting started with the {{site.data.keyword.cloud_notm}} CLI and Developer Tools](/docs/cli?topic=cli-getting-started){: external}

   [Installing the stand-alone {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli){: external}

4. Order and deploy your service by running the following generalized example {{site.data.keyword.cloud_notm}} CLI commands:

   ```
   ibmcloud login -sso -a API -r REGION
   ```

   ```
   ibmcloud target --cf-api ENDPOINT -o ORG -s SPACE
   ```

   ```
   ibmcloud cf create-service SERVICE PLAN SERVICE_INSTANCE -c 'PARAMETERS_AS_JSON'
   ```

   where **API** is the {{site.data.keyword.cloud_notm}} API endpoint URL `https://cloud.ibm.com`, 
   
   **REGION** is one of the following data center regions (list of data center regions is subject to change when more become available):

   `us-south` - (Dallas, Toronto, Washington DC)

   `au-syd` - (Sydney, Tokyo)

   `eu-gb` - (London)

   `eu-de` - (Frankfurt)

   **ENDPOINT** is one of the following targeted Cloud Foundry API endpoint URLs:

   `https://api.ng.bluemix.net/` - (us-south)

   `https://api.au-syd.bluemix.net/` - (au-syd)

   `https://api.eu-gb.bluemix.net/` - (eu-gb)

   `https://api.eu-de.bluemix.net/` - (eu-de)
   
   **ORG** is your {{site.data.keyword.cloud_notm}} organization,
   
   **SPACE** is your {{site.data.keyword.cloud_notm}} space in the organization,
   
   **SERVICE** is `"dashdb"`,
   
   **PLAN** is one of the following {{site.data.keyword.dashdbshort_notm}} plans:

   `"Flex One"`

   `"Flex"`

   `"Flex Performance"`

   **SERVICE INSTANCE** is what you want to name your service instance,
   
   and **'PARAMETERS_AS_JSON'** gives you the ability to specify any of the following service deployment and configuration parameters (list of data centers is subject to change when more become available):

   `"datacenter": "us-south:dallas"`

   `"datacenter": "us-south:toronto"`  (Flex One)

   `"datacenter": "us-south:washington d.c"`

   `"datacenter": "au-syd:sydney"`  (Flex One)

   `"datacenter": "au-syd:tokyo"`

   `"datacenter": "eu-gb:london"`

   `"datacenter": "eu-de:frankfurt"`
   
   `"oracle_compatible": "no"`

   `"oracle_compatible": "yes"`

   For example: `'{"datacenter": "us-south:dallas", "oracle_compatible": "no"}'`
   
   Your choice of data center must match the region of your {{site.data.keyword.cloud_notm}} space in your organization.
   {: note}

   Parameters that are specific to **Flex** and **Flex Performance** plans - select your plan of choice in the [Db2 Warehouse catalog](https://cloud.ibm.com/catalog/services/db2-warehouse){: external} for available core and storage options:

   `"processors": "<number_of_cores>"`
   
   `"storage": "<amount_of_storage_in_GB>"`

   For example: `'{"datacenter": "us-south:dallas", "oracle_compatible": "no", "processors": "48", "storage": "9600"}'`

   ## Example
   {: #cli_example}

   The following commands show how to order and deploy a {{site.data.keyword.dashdbshort_notm}} Flex service plan in the US South, Dallas data center region, without Oracle compatibility, with 48 cores, and with 96.0 TB of storage:

   ```
   ibmcloud login -sso -a https://cloud.ibm.com -r us-south
   ```
   {: codeblock}

   ```
   ibmcloud target --cf-api https://api.ng.bluemix.net -o flex -s dev
   ```
   {: codeblock}

   ```
   ibmcloud cf create-service "dashdb" "Flex" "Db2 Warehouse-az1" -c '{"datacenter": "us-south:dallas", "oracle_compatible": "no", "processors": "48", "storage": "9600"}'
   ```
   {: codeblock}



