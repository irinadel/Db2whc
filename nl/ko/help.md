---

copyright:
  years: 2014, 2018
lastupdated: "2017-07-27"

---

<!-- Attribute definitions --> 
{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 도움 및 지원
{: #help_support}

여기에서는 {{site.data.keyword.dashdblong}}의 사용과 관련된 일반적인 질문에 대한 답변을 찾을 수 있습니다.
{: shortdesc}

<!-- ##Cannot log in to RStudio
{: #r_studio}

Single sign-on (SSO) for RStudio is not available for {{site.data.keyword.dashdblong}}.
{: shortdesc}

You want to log in to RStudio from {{site.data.keyword.dashdbshort_notm}} by using SSO, but you are prompted for a password.
{: tsSymptoms}

SSO to RStudio is not available in {{site.data.keyword.dashdbshort_notm}}.
{: tsCauses}

To get your credentials for RStudio, consult your `VCAP_SERVICES` environment variable. Further information is available in [Getting started with {{site.data.keyword.dashdbshort_notm}}](/docs/services/dashDB/dashDB.html#dashDB){:new_window}.
{: tsResolve}


##Cannot find the `diag.log` file for troubleshooting
{: #diag_log}

The `diag.log` file is not available.
{: shortdesc}

You want to troubleshoot and cannot find the `diag.log` file for {{site.data.keyword.dashdbshort_notm}}.
{: tsSymptoms}

The `diag.log` file is not available on {{site.data.keyword.dashdbshort_notm}}, nor is any other log specific to DB2®.
{: tsCauses}

The application-specific logs can be accessed by the Cloud Foundry CLI (command line interface). From the CLI, enter **cf logs recent**. The logs can also be accessed on the {{site.data.keyword.Bluemix_notm}} site by selecting your app and going to **Files and Logs**.
{: tsResolve}

##Cannot find org or space: Bluemix ID mismatch
{: #org_space_id}

An organization or space cannot be found for a new {{site.data.keyword.dashdbshort_notm}} instance.
{: shortdesc}

You want to create a new {{site.data.keyword.dashdbshort_notm}} service instance in {{site.data.keyword.Bluemix_notm}} by using the warehousing feature in the Cloudant® dashboard, but you get the following error message: `Cannot find org or space.`
{: tsSymptoms}

To provision a new {{site.data.keyword.dashdbshort_notm}} service instance in {{site.data.keyword.Bluemix_notm}}, the Cloudant warehousing feature attempts to find the "best fit" {{site.data.keyword.Bluemix_notm}} target organization for the authenticated {{site.data.keyword.Bluemix_notm}} user. The warehousing feature typically looks for an organization that matches the {{site.data.keyword.Bluemix_notm}} ID, an ID that is usually the user’s email address. If a matching organization is not found and the user has access to only one organization, the warehousing feature selects that organization. There might be situations where the user does not have an organization that they can access or the user has access to multiple organizations. In those situations, Cloudant cannot determine where to provision the {{site.data.keyword.dashdbshort_notm}} instance and the error message is displayed.
{: tsCauses}

To resolve the problem, choose one of the following options:
{: tsResolve}

* From the drop-down list in the Cloudant dashboard, select the {{site.data.keyword.Bluemix_notm}} organization in which you want the {{site.data.keyword.dashdbshort_notm}} instance to be created. After you select the organization, select the appropriate space from the secondary drop-down list.
* Manually provision a {{site.data.keyword.dashdbshort_notm}} instance directly in {{site.data.keyword.Bluemix_notm}} and select the created {{site.data.keyword.dashdbshort_notm}} service instance from the drop-down list in the Cloudant dashboard.


##Cannot find org or space: Region mismatch
{: #org_space_region}

An organization or space cannot be found for a new {{site.data.keyword.dashdbshort_notm}} instance.
{: shortdesc}

You want to create a new {{site.data.keyword.dashdbshort_notm}} service instance, but the drop-down lists of existing {{site.data.keyword.dashdbshort_notm}} service instances or {{site.data.keyword.Bluemix_notm}} organizations is empty. A new {{site.data.keyword.dashdbshort_notm}} service instance cannot be provisioned and you get the following error message: `Cannot find org or space.`
{: tsSymptoms}

If the user’s {{site.data.keyword.Bluemix_notm}} account is in a different region than the Cloudant cluster, the provisioning request fails. For example, the {{site.data.keyword.Bluemix_notm}} account was on-boarded in the Europe United Kingdom region, but the Cloudant cluster works with the US South region. As a result, the existing service instance and organization drop-down lists in the Cloudant dashboard might be empty or show organizations and spaces that belong to a different region altogether.
{: tsCauses}

1. Log in to the {{site.data.keyword.Bluemix_notm}} dashboard and switch to your expected region. Follow any prompts to complete the onboarding in that region. As an alternative, create a {{site.data.keyword.Bluemix_notm}} account in the appropriate region.
2. Log in to the Cloudant dashboard to repeat the {{site.data.keyword.dashdbshort_notm}} service instance selection.
{: tsResolve}

##Exceeded services limit
{: #service_limit}

The {{site.data.keyword.dashdbshort_notm}} service in {{site.data.keyword.Bluemix_notm}} exceeded its limit.
{: shortdesc}

While you are using the {{site.data.keyword.dashdbshort_notm}} service in {{site.data.keyword.Bluemix_notm}}, the following error message is displayed: `Exceeded your organization’s services limit.`
{: tsSymptoms}

You are still on the no-cost {{site.data.keyword.Bluemix_notm}} trial, which has service limits.
{: tsCauses}

To resolve the problem, choose one of the following options:
{: tsResolve}

* To free up resources, drop services in your {{site.data.keyword.Bluemix_notm}} dashboard that you no longer use. Retry the provisioning request for a new {{site.data.keyword.dashdbshort_notm}} instance.
* Use the {{site.data.keyword.Bluemix_notm}} dashboard to manually provision a {{site.data.keyword.dashdbshort_notm}} instance in an appropriate organization or space that does not have service limits. Select that instance from the Cloudant dashboard. -->


## Db2 Warehouse on Cloud 서비스를 사용할 수 없음
{: #outages}

{{site.data.keyword.Bluemix_notm}}의 {{site.data.keyword.dashdbshort_notm}} 서비스를 사용할 수 없습니다.
{: shortdesc}

데이터 웨어하우스를 작성하려는 시도가 500 오류와 함께 실패하거나, SDP 로드에서 SQL 오류를 보고합니다.
{: tsSymptoms}

{{site.data.keyword.Bluemix_notm}}의 {{site.data.keyword.dashdbshort_notm}} 서비스가 스케줄된 유지보수 프로시저를 진행 중이거나 알려진 가동 중단이 발생했습니다.
{: tsCauses}

다음 상태 페이지를 확인하여 {{site.data.keyword.Bluemix_notm}}에서 {{site.data.keyword.dashdbshort_notm}} 서비스의 상태를 판별할 수 있습니다.
{: tsResolve}

* [{{site.data.keyword.Bluemix_notm}} 지원 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/bluemix/support/#status){:new_window}
* 상태 모니터링:
  * [모든 지역 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.eu-gb.bluemix.net/status?tags=platform,runtimes,services,ibm:yp:eu-gb,ibm:yp:eu-de,ibm:yp:us-south,ibm:yp:au-syd){:new_window}
  <!--[US - South region ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://estado.ng.bluemix.net/internalstatus){:new_window}
  [Europe - United Kingdom region ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://estado.eu-gb.bluemix.net/internalstatus){:new_window}
  [Europe - Germany region ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://estado.eu-de.bluemix.net/internalstatus){:new_window}
  [Australia - Sydney region ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://estado.au-syd.bluemix.net/internalstatus){:new_window}-->


## Db2 Warehouse on Cloud에 대한 도움 및 지원 받기
{: #gettinghelp}

{{site.data.keyword.dashdbshort_notm}} 사용 시 문제점 또는 질문이 있는 경우, 정보를 검색하거나 포럼을 통해 질문하여 도움을 받을 수 있습니다. 또한 지원 티켓을 열 수도 있습니다.
{: shortdesc}

포럼을 사용하여 질문하는 경우, {{site.data.keyword.Bluemix}} 개발 팀이 볼 수 있도록 질문에 태그를 지정하십시오.

* {{site.data.keyword.dashdbshort_notm}}에서 앱을 개발하거나 배치하는 방법에 대한 기술적인 질문이 있을 경우 [Stack Overflow ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://stackoverflow.com/search?q=dashdb+bluemix){:new_window}에 질문을 게시하고 해당 질문에 "bluemix" 및 "db2" 태그를 지정하십시오.
* 서비스 및 시작하기 지시사항에 대한 질문이 있는 경우에는 [IBM developerWorks® dW Answers ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/answers/topics/dashdb/?smartspace=bluemix){:new_window} 포럼을 이용하십시오. "bluemix" 및 "db2" 태그를 포함하십시오.

포럼 사용에 대한 자세한 내용은 [도움 받기](/docs/support/index.html#getting-help){:new_window}를 참조하십시오.

IBM 지원 티켓 열기에 대한 정보 또는 지원 레벨 및 티켓 심각도에 대한 정보는 [지원 문의](/docs/support/index.html#contacting-support){:new_window}를 참조하십시오.



