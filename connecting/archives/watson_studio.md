---

copyright:
  years: 2014, 2018
lastupdated: "2018-09-25"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Connecting Watson Studio

After you create a project in IBM Watson Studio (formerly Data Science Experience), you add data assets to it so that you can work with data. All the collaborators in the project are automatically authorized to access the data in the project.
{: shortdesc}

How you add data and from where you can add data differs between legacy and IBM Watson projects. IBM Watson projects use {{site.data.keyword.Bluemix_notm}} Object Storage. The project is a legacy project if it uses Object Storage OpenStack Swift. 

## To create a new connection in an IBM Watson project:

1. Click **Add to project > Connection**.
    
2. Choose a data source.
    
3. Enter the connection information required for your data source. Typically, you need to provide information like the host, port number, user name, and password.
    
4. You can discover assets from connections to {{site.data.keyword.dashdbshort_notm}}, which gives you the ability to add all tables from the connection as data assets to a project. Select **Discover data assets** and choose a project.
    
5. Click **Create**. The connection appears on the **Assets** page.

Watch this video to see how to create a connection and add connected data to a project.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Create a connection and add connected data to a project" type="text/html" width="640" height="390" src="//www.youtube.com/embed/U7-gCbo4QtM?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

## To create a new connection in a legacy project:

1. From your project's **Assets** page, click the **Find and add data** icon.
    
2. On the **Connections** pane, click **Create Connection**.

3. Enter a name and description and choose a Service Category:

   **Data Service** = {{site.data.keyword.Bluemix_notm}} data service

   When you choose **Data Service**, your existing {{site.data.keyword.Bluemix_notm}} data services appear in the **Service Instance** list.

4. Choose the service or database server from the list.

5. Enter the connection information:

   When you choose **Data Service**, your existing {{site.data.keyword.Bluemix_notm}} data services appear in the **Service Instance** list.
    
6. Click **Create**. The connection is available to all legacy projects.
    
7. On the **Connections** pane, select the connection and click **Apply**.

To add an existing connection to a legacy project:

1. From your project's **Assets** page, click the **Find and add data** icon.
    
2. On the **Connections** pane, select the connection and click **Apply**.

