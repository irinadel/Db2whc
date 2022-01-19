---

copyright:
  years: 2014, 2022
lastupdated: "2022-01-17"

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

# Changing your Db2 Warehouse entitlements to a Cloud Pak for Data SaaS Subscription
{: #mig_standalone}

Migrating your stand-alone parts to a Cloud Pak for Data subscription gives you more flexibility to choose which offerings you want to consume, and how much you want to consume. 

{: shortdesc}

A subscription allows you to buy credits that you can use as quickly or slowly as you want to, based on your changing needs.  If you want to provision a new instance or scale up storage or compute for an existing instance, you can initiate the request within minutes, without the need for a charge agreement to be created or amended. A subscription also provides you with the opportunity to explore a larger portfolio of offerings.



## About
{: #migrate_abt}

This document describes the steps needed for the migration.  Note that the migration does not require any physical migration of data, and no downtime is required.  The functionality and user experience does not change after the migration.

#### Prerequisites
{: #migrate_prereq41}

- Purchase an IBM Cloud Pak for Data as-a-Service subscription.

- Apply this subscription to the IBM Cloud account that currently contains your Db2 Warehouse on Cloud instance.

- Migrate your Db2 Warehouse on Cloud instance from Cloud Foundry to Resource Controller by following the steps here: https://cloud.ibm.com/docs/account?topic=account-migrate#migrate_instances



## Migrating your instance to a subscription using the user interface
{: #migrate_instlng}

1)	Log in to IBM Cloud https://cloud.ibm.com
2)	Navigate to your Resource list by selecting View resources https://cloud.ibm.com/resources
3)	Under the “Services and software” resource list, locate the Db2 Warehouse instance that you purchased under a charge agreement and click on the service name.
4)	Select the Plan tab. Under Change pricing plan you will see your current Contract Plan and the new Digital Plan.
5)	Select the new Digital Plan and select Save.

For more information on these steps, see:
https://cloud.ibm.com/docs/billing-usage?topic=billing-usage-changing&interface=ui



### Migrating your instance to a subscription using the CLI
{: #migrate_CLI}

1)	Log in to IBM Cloud using the ibmcloud cli:

  `ibmcloud login -sso` 


2)	List all service instances:

  `ibmcloud resource service-instances` 


3)	Update the pricing plan for your service instance:

  `ibmcloud resource service-instance-update < service_instance_name> --service-plan-id < plan_id>` 

Example:

  `ibmcloud resource service-instance-update < service_instance_name> --service-plan-id “smp-flex-paygo”` 



For more information on these steps, see:
https://cloud.ibm.com/docs/billing-usage?topic=billing-usage-changing&interface=cli




