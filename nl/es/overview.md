---

copyright:
  years: 2014, 2018
lastupdated: "2018-02-27"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Acerca de Db2 Warehouse on Cloud
{: #overview}

En los planes de servicio de {{site.data.keyword.dashdblong}}, utilice el almacén de datos para guardar datos relacionales, incluidos tipos especiales. Analice sus propios datos, o los datos cargados desde otros servicios de nube, utilizando las herramientas de análisis incluidas o conectando sus propias apps. Puede aprovecharse del alto rendimiento, tecnología de base de datos en memoria con tablas con columnas para cargas de trabajo de análisis. La consola web de {{site.data.keyword.dashdbshort_notm}} puede trabajar con tareas de gestión de datos comunes, como cargar datos, y con tareas de análisis, como ejecutar consultas y scripts R.
{: shortdesc}

También puede conectar aplicaciones externas a {{site.data.keyword.dashdbshort_notm}} y utilizarlas para gestionar o analizar todavía más sus datos. Por ejemplo:
   * Conecte {{site.data.keyword.IBM_notm}} InfoSphere® Data Architect para diseñar y desplegar su esquema de base de datos.
<!--   * Connect Esri ArcGIS to perform geospatial analytics and map publishing with your data. -->
   * Conecte un servidor {{site.data.keyword.IBM_notm}} Cognos® para ejecutar informes de Cognos de sus datos.
   * Conecte herramientas basadas en SQL, como Tableau, Microstrategy o Microsoft Excel para manipular o analizar sus datos.
   * Conecte sus aplicaciones {{site.data.keyword.Bluemix_short}} que necesitan una base de datos de análisis.
   * Conecte Aginity Workbench para migrar modelos de datos y datos de Netezza® a {{site.data.keyword.dashdbshort_notm}}.

## Servicio gestionado de Db2 Warehouse on Cloud
{: #managed_service}

El servicio completamente gestionado de {{site.data.keyword.dashdbshort_notm}} maneja todas las actualizaciones de software, actualizaciones de sistema operativo y mantenimiento de hardware. El servicio incluye supervisión de estado de tipo 24x7 de la base de datos y de la infraestructura. En el caso de que se produzca un error de hardware o de software, el servicio se reinicia automáticamente.
{: shortdesc}

## Planes y configuraciones
{: #plans_cfgs}

Puede elegir un plan {{site.data.keyword.dashdbshort_notm}} que está configurado y optimizado para el trabajo que necesita realizar:
{: shortdesc}

   * Un plan de entrada para realizar pruebas
   * Un plan de Flex Performance para poder escalar el almacenamiento y calcular recursos de forma independiente
   * Planes pequeños, medianos y grandes para producción
   * Configuraciones MPP para procesamientos paralelos
   * Planes configurados para Alta disponibilidad o para compatibilidad con Oracle
   * Y más...

Vea los planes disponibles en el catálogo {{site.data.keyword.Bluemix}}:
   * Planes configurados para almacenes de datos y cargas de trabajo analíticas (OLAP): [{{site.data.keyword.dashdbshort_notm}}](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window}
<!--   * Plans configured for high-speed, transactional processing (OLTP): [{{site.data.keyword.dashdbshort_notm}} for Transactions](https://console.ng.bluemix.net/catalog/services/dashdb-for-transactions-sql-database){:new_window} -->

Si no ve una configuración en el catálogo que necesita, [póngase en contacto con ventas de {{site.data.keyword.IBM_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window} para hablar sobre otras opciones.

## Suministro de Db2 Warehouse on Cloud
{: #whse_provision}

La base de datos de {{site.data.keyword.dashdbshort_notm}} puede suministrarse en {{site.data.keyword.BluSoftlayer_full}} y para AWS.
{: shortdesc}

Si desea que se suministre el almacén de datos para AWS, seleccione el plan **MPP Small for AWS**.

<!-- If you want to have the data warehouse provisioned for AWS, select the **{{site.data.keyword.IBM_notm}} {{site.data.keyword.dashdbshort_notm}} for Analytics MPP Small for AWS** plan. -->

<!-- ##dashDB for Transactions
{: #dashDB_tr}

In the {{site.data.keyword.dashdbshort_notm}} for Transactions plans, use the {{site.data.keyword.dashdbshort_notm}} relational database for online transaction processing. You can connect new or existing applications, and you can begin processing transactions and storing your data. With DB2® and Oracle compatibility, you can connect small or large applications and benefit from a managed enterprise-class database system. You can leverage the {{site.data.keyword.dashdbshort_notm}} for Transactions web console to manage users, load data, and get connection information.
{: shortdesc} -->

<!-- ##dashDB web console overview
{: #console_overview}

You can manage your {{site.data.keyword.dashdbshort_notm}} database, analyze your data, and monitor sensitive data with the {{site.data.keyword.dashdbshort_notm}} web console accessible from {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Open the web console by clicking the service tile on your application overview page, and then click **Open**.

Single sign-on authentication connects you directly to the web console. You can access connection information from the web console, and the **Downloads** page includes links to client drivers for accessing {{site.data.keyword.dashdbshort_notm}} from remote applications. You can also access sample data and reports.

###Sensitive data reporting

The {{site.data.keyword.dashdbshort_notm}} web console includes a sensitive data reporting feature that detects and monitors sensitive objects in the {{site.data.keyword.dashdbshort_notm}} data warehouse, such as credit card numbers and US Social Security numbers.

To run and view reports that identify columns that contain sensitive data and provide information about connections and activities that access the sensitive data, select **Monitor &gt; Sensitive Data** in the web console. -->


<!-- ##IBM Analytics Services
{: #analytics_services}

For more information about {{site.data.keyword.IBM_notm}} analytics services and finding your local services representative, see: [{{site.data.keyword.IBM_notm}} Analytics Services ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/software/data/services/).
{: shortdesc} -->














