---

copyright:
  years: 2014, 2019
lastupdated: "2023-06-20"

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

# Connectivity options on Amazon Web Services
{: #connect_options_aws}

{{site.data.keyword.dashdblong}} offers secure connectivity options for your application connection requirements.  
{: shortdesc}

For application connections, do not use IP addresses to connect to the {{site.data.keyword.dashdbshort_notm}} instance, as the IP addresses resolved from the hostname may change. Use hostnames to reference your connection properties where it is available.
{: important}

## Connecting to Db2 Warehouse on Cloud with Amazon Web Services PrivateLink
{: #PrivateLink}

[Amazon Web Services (AWS) PrivateLink](https://aws.amazon.com/privatelink/){: external} gives you the ability to securely and privately connect to a {{site.data.keyword.dashdbshort_notm}} instance that is deployed on AWS from your own AWS VPCs, services, and applications. With AWS PrivateLink, traffic between {{site.data.keyword.dashdbshort_notm}} and your AWS VPCs, services, and applications does not traverse the public internet.

If you'd like to use AWS PrivateLink with {{site.data.keyword.dashdbshort_notm}}, complete the following steps:

1. Create an AWS principal to access {{site.data.keyword.dashdbshort_notm}}. The AWS principal can be AWS accounts, IAM users, or IAM roles.

2. In the console, navigate to the Settings --> Access restriction panel. Enable private endpoints. You can optionally also disable public endpoints. You can now grant permissions to your principals by adding them to the allow list.
    
3. Navigate to the **Connections Details** tab in your console to find your Db2 Warehouse on Cloud private endpoint service name. The service name begins with the string `com.amazonaws.vpce.xxxx`

4. Use the service name to Create an [Interface Endpoint](https://docs.aws.amazon.com/vpc/latest/privatelinkcreate-interface-endpoint.html#create-interface-endpoint) in your VPC. Ensure that TCP traffic is allowed through port 50001 on the VPC.

5. It is recommended that you use a private DNS to remap the endpoint to a company-specific hostname rather than consuming the endpoint directly. This will avoid the need to make updates across your applications if the endpoint later changes. For more information, see here: https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-to-vpc-interface-endpoint.html 
    
### Considerations and limitations

- AWS PrivateLink currently supports only TCP traffic. Tools that rely on UDP traffic are not supported by PrivateLink. To load data, load directly from Amazon S3 into {{site.data.keyword.dashdbshort_notm}}. See [Loading data from Amazon S3](/docs/Db2whc?topic=Db2whc-load_s3).

  Extra charges might apply when you transfer data by using the public endpoint.
  {: note}

- You must create the Endpoint Service for accessing {{site.data.keyword.dashdbshort_notm}} in the same AWS region where the {{site.data.keyword.dashdbshort_notm}} instance is deployed. To access your instance from other AWS regions, you can use VPC Peering. See [Example: Services Using AWS PrivateLink and VPC Peering](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-peer-region-example.html){: external}.

- For the current generation of plans on AWS, connectivity to the web UI is available only over the public network, even if you have enabled PrivateLink. This restriction is temporary, and will be removed in an upcoming update.

- The previous generation of plans on AWS does not support configuring PrivateLink through the console. If you'd like to set up PrivateLink, open a support case and provide the Amazon Resource Name (ARN) of the AWS principal you created in step 1.

For more information about AWS PrivateLink, see [Interface VPC Endpoints (AWS PrivateLink)](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html){: external}.
