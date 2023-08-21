---

copyright:
  years: 2014, 2022
lastupdated: "2023-08-21"

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

# Auditing
{: #auditing}

You can monitor data access in your {{site.data.keyword.dashdblong}} instance with the built-in Db2 audit facility. Use the Db2 audit facility to generate and maintain an audit trail for a series of predefined database events, including attempts to access or manipulate database objects, user authentication, SQL statement execution, and even access to the audit log. Use the audit log to reveal usage patterns that would identify system misuse, and in turn, take action to eliminate such misuse.
{: shortdesc}

Before initial configuration, you must collect the following information:


## Cloud Object Storage credentials

[IBM Cloud Object Storage ](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main)

Example,

    cos_hmac_keys:
      access_key_id:      7exampledonotusea6440da12685eee02
      secret_access_key:  8not8ed850cddbece407exampledonotuse43r2d2586

    


[Amazon Simple Storage Service (S3) ](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html#Using_CreateAccessKey)


Example,

		access key ID: AKIAIOSFODNN7EXAMPLE
		secret access key: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY




## Cloud Object Storage bucket name

You must create a bucket that will store the audit records. You will need to save the bucket name during initial configuration. It is recommended that you do not use this bucket for other purposes. Consider securely configuring the bucket with appropriate encryption, access management, and data retention.

For cost control measures, you should set a quota to the [relevant bucket](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-quota) and set an [expiration rule](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-expiry).


Once the audit records have been successfully uploaded to the cloud object storage bucket, you can preview the files in the Console. To review larger subsets of the audit logs, refer to [Audit Policy](https://www.ibm.com/docs/en/db2woc?topic=features-audit-policy-guidelines). The [format](https://www.ibm.com/docs/en/db2/11.5?topic=format-example-del-file) of the archived audit logs is DEL which separates the text with commas. You can reformat and process this file in your system for further analysis.


For more information about auditing for {{site.data.keyword.dashdbshort_notm}}, see [Audit policy guidelines](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.security.doc/doc/audit_policy_guidelines.html){: external}.

