---

copyright:
  years: 2014, 2018
lastupdated: "2018-04-30"

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

# Hilfe und Unterstützung
{: #help_support}

In diesem Abschnitt finden Sie Antworten zu häufig gestellten Fragen zur Verwendung von {{site.data.keyword.dashdblong}}.
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


## Der Db2 Warehouse on Cloud-Service ist nicht verfügbar.
{: #outages}

Der Service {{site.data.keyword.dashdbshort_notm}} in {{site.data.keyword.Bluemix_notm}} ist möglicherweise nicht verfügbar.
{: shortdesc}

Ein Versuch, ein Data-Warehouse zu erstellen, schlägt mit dem Fehler 500 fehl, oder ein SDP-Load meldet einen SQL-Fehler.
{: tsSymptoms}

Der Service {{site.data.keyword.dashdbshort_notm}} in {{site.data.keyword.Bluemix_notm}} wird momentan einer geplanten Wartung unterzogen oder es kam zu einer geplanten Unterbrechung.
{: tsCauses}

Sie können den Status des Service {{site.data.keyword.dashdbshort_notm}} in {{site.data.keyword.Bluemix_notm}} durch Überprüfen der folgenden Statusseiten feststellen:
{: tsResolve}

* [{{site.data.keyword.Bluemix_notm}}-Support ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/bluemix/support/#status){:new_window}
* Statusüberwachung:
  * [Alle Regionen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.eu-gb.bluemix.net/status?tags=platform,runtimes,services,ibm:yp:eu-gb,ibm:yp:eu-de,ibm:yp:us-south,ibm:yp:au-syd){:new_window}
  <!--[US - South region ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://estado.ng.bluemix.net/internalstatus){:new_window}
  [Europe - United Kingdom region ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://estado.eu-gb.bluemix.net/internalstatus){:new_window}
  [Europe - Germany region ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://estado.eu-de.bluemix.net/internalstatus){:new_window}
  [Australia - Sydney region ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://estado.au-syd.bluemix.net/internalstatus){:new_window}-->


## Hilfe und Unterstützung für Db2 Warehouse on Cloud anfordern
{: #gettinghelp}

Sollten bei der Verwendung von {{site.data.keyword.dashdbshort_notm}} Probleme auftreten oder Fragen entstehen, können Sie nach Informationen suchen oder Fragen in einem Forum stellen. Sie haben auch die Möglichkeit, ein Support-Ticket zu öffnen.
{: shortdesc}

Wenn Sie in den Foren eine Frage stellen, versehen Sie Ihre Frage mit einem Tag, um die {{site.data.keyword.Bluemix}}-Entwicklungsteams auf die Frage aufmerksam zu machen.

* Wenn Sie technische Fragen zur Entwicklung oder Bereitstellung einer App mit {{site.data.keyword.dashdbshort_notm}} haben, posten Sie die Fragen in [Stack Overflow ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://stackoverflow.com/search?q=dashdb+bluemix){:new_window} und kennzeichnen Sie die Frage mit den Tags "bluemix" und "db2".
* Bei Fragen zum Service und zu den Anweisungen für den Einstieg verwenden Sie das Forum [IBM developerWorks® dW Answers ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/answers/topics/dashdb/?smartspace=bluemix){:new_window}. Geben Sie die Tags "bluemix" und "db2" an.

Weitere Details zur Nutzung der Foren finden Sie unter [Hilfe anfordern](/docs/get-support/howtogetsupport.html#using-avatar){:new_window}.

Informationen zum Öffnen eines IBM Support-Tickets oder zu den Supportebenen und den Prioritätsstufen von Tickets finden Sie unter: [Ein Support-Ticket öffnen](/docs/get-support/howtogetsupport.html#open-ticket){:new_window}.



