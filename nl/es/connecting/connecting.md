---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-15"

keywords:

subcollection: Db2whc

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}

# Visión general de la conexión
{: #connect_ov}

Puede conectar interfaces de línea de mandatos, aplicaciones y herramientas de IBM® o terceros, o apps que crea a su base de datos de {{site.data.keyword.dashdbshort_notm}}. 
{: shortdesc}

## Requisitos previos
{: #prereqs}

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los requisitos previos necesarios. 

- Recopile detalles y credenciales de la base de datos

   Para conectarse a la base de datos, necesita detalles de base de datos (como el nombre de host), así como credenciales (como ID de usuario y contraseña). Puede recopilar la información de conexión de la consola web de {{site.data.keyword.dashdbshort_notm}}.

- Verifique que está instalado un controlador soportado

   - Si su aplicación o herramienta contiene IBM Data Server Driver Package de Db2 v11.1, la aplicación o herramienta podrán conectarse a la base de datos de {{site.data.keyword.dashdbshort_notm}} utilizando el controlador.
   - De lo contrario, instale el paquete de controladores de Db2, que puede descargar desde la consola web de {{site.data.keyword.dashdbshort_notm}}.

- Configure el entorno

  - Añada entradas al archivo de configuración del controlador, `db2dsdriver.cfg`, para la base de datos.
  - Capa de sockets seguros (SSL)

    Puede elegir conectarse con o sin SSL. Los detalles de conexión como, por ejemplo, qué puerto utiliza y la serie de conexión, dependen de si utiliza o no conexiones SSL.

    Para utilizar conexiones SSL, necesita un certificado CA:
    - Si utiliza el último paquete de controladores de {{site.data.keyword.dashdbshort_notm}}, el archivo de certificado se incorporará en el paquete y se utilizará para las conexiones.
    - Si utiliza IBM Data Server Driver Package, puede descargar el certificado SSL de la consola web de {{site.data.keyword.dashdbshort_notm}}.

- Confirme que los puertos están disponibles

   Si la red se encuentra detrás de un cortafuegos, confirme que las comunicaciones están permitidas en el número de puerto `50000` para protocolos estándar o el número de puerto `50001` para conexiones SSL.

<!-- Before you can connect to your {{site.data.keyword.dashdbshort_notm}} database, verify that you completed downloading and installing the necessary components on the prerequisites checklist: 

- [Prerequisites checklist](prereqs.html) -->

### Recopilación de información de conexión
{: #collect_info}

- [Detalles de base de datos y credenciales de conexión](/docs/services/Db2whc/connecting/credentials.html)

### Descarga e instalación del paquete de controlador
{: #dl_install}

- [Descarga del paquete de instalación](/docs/services/Db2whc/connecting/driver_pkg.html)
- [Instalación en Linux o PowerLinux](/docs/services/Db2whc/connecting/install_linux.html)
- [Instalación en Mac OS X](/docs/services/Db2whc/connecting/install_mac.html)
- [Instalación en Windows](/docs/services/Db2whc/connecting/install_win.html)

### Configuración del entorno
{: #cfg_env}

- [Configuración del entorno](/docs/services/Db2whc/connecting/driver_pkg_cfg.html)
- [Soporte para la capa de sockets seguros (SSL)](/docs/services/Db2whc/connecting/ssl.html)

## Conexión mediante programas
{: #conx_prgrm}

Puede utilizar lenguajes de programación comunes para crear aplicaciones que conectan a una base de datos de {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

- [JDBC](/docs/services/Db2whc/connecting/jdbc.html)
- [ODBC o CLI de Microsoft Windows](odbc_cli.html)
- [.NET](/docs/services/Db2whc/connecting/net_apps.html)
- [Administrador de orígenes de datos ODBC](/docs/services/Db2whc/connecting/odbc_data_source_admin.html)
- [PHP](/docs/services/Db2whc/connecting/php.html)
- [API REST](/docs/services/Db2whc/connecting/rest_api.html)
<!-- - [C++]() -->
<!-- - [Java]() -->
<!-- - [Node.js]() -->
<!-- - [Perl]() -->
<!-- - [Python]() -->

## Integración de apps y herramientas
{: #conx_apps_tools}

También puede conectar aplicaciones externas a {{site.data.keyword.dashdbshort_notm}} y utilizarlas para gestionar o analizar todavía más sus datos. Por ejemplo:

### Integración de datos
{: #di}

- Conecte sus aplicaciones {{site.data.keyword.Bluemix_short}} que necesitan una base de datos de análisis.
- [DataStage](/docs/services/Db2whc/connecting/data.html#datastage)
- [Informatica](/docs/services/Db2whc/connecting/data.html#informatica)
- [Lift ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://lift.ng.bluemix.net/#docs){:new_window}
- [InfoSphere Data Replication](/docs/services/Db2whc/connecting/data.html#idr)
- [Segment ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://segment.com/docs/destinations/db2/){:new_window}
- [Data Studio](/docs/services/Db2whc/connecting/data.html#data_studio)
- [Data Server Manager](/docs/services/Db2whc/connecting/data.html#dsm)
- [CLPPLUS](/docs/services/Db2whc/connecting/data.html#clpplus)
- [Conecte Aginity Workbench para migrar modelos de datos y datos de Netezza® a {{site.data.keyword.dashdbshort_notm}}](/docs/services/Db2whc/connecting/data.html#aginity_wb)
- [InfoSphere Data Architect para diseñar y desplegar el esquema de base de datos](/docs/services/Db2whc/connecting/data.html#ida)

### Visualización de datos/BI
{: #dvis_bi}

- [Cognos Analytics para ejecutar informes de inteligencia empresarial en sus datos](/docs/services/Db2whc/connecting/vis_bi.html#cognos)
- [Looker ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.looker.com/setup-and-management/connecting-to-db){:new_window}
- [Tableau](/docs/services/Db2whc/connecting/vis_bi.html#tableau)
- [Microsoft Excel](/docs/services/Db2whc/connecting/vis_bi.html#excel)
- [Esri ArcGIS for Desktop para realizar análisis geoespaciales y publicar mapas con sus datos](/docs/services/Db2whc/connecting/vis_bi.html#esri_arcgis)

### Ciencia de datos
{: #dsci}

- [Watson Studio (anteriormente IBM Data Science Experience)](/docs/services/Db2whc/connecting/data_sci.html#watson_studio)
- [SPSS Statistics](/docs/services/Db2whc/connecting/data_sci.html#spss_stats)
- [SAS](/docs/services/Db2whc/connecting/data_sci.html#sas)
- [Entorno de desarrollo R local](/docs/services/Db2whc/connecting/data_sci.html#r_dev_env)

## Conexión a otra base de datos Db2
{: #fed}

La virtualización de datos de Db2 (también denominada federación) recibe soporte de {{site.data.keyword.dashdbshort_notm}}. La virtualización de datos le ofrece acceso mediante una sola consulta a todos sus datos ubicados en diversas bases de datos distribuidas en cualquier punto de la organización. Puede acceder a los datos ubicados en cualquiera de los orígenes de datos Db2 o Informix, tanto en la nube como locales. 

Esta función está admitida en todas las versiones de {{site.data.keyword.dashdbshort_notm}}, excepto en el plan de entrada. Sin embargo, puede utilizar el plan de entrada como destino desde el que extraer datos.

- [Virtualización de datos (federación)](/docs/services/Db2whc/federation.html)


