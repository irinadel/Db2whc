---

copyright:
  years: 2014, 2019
lastupdated: "2019-04-01"

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

- [Detalles de base de datos y credenciales de conexión](/docs/services/Db2whc/connecting?topic=Db2whc-db_details_cxn_creds#db_details_cxn_creds)

### Descarga e instalación del paquete de controlador
{: #dl_install}

- [Descarga del paquete de instalación](/docs/services/Db2whc/connecting?topic=Db2whc-dr_pkg#dr_pkg)
- [Instalación en Linux o PowerLinux](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_linux#install_dr_pkg_linux)
- [Instalación en Mac OS X](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_mac#install_dr_pkg_mac)
- [Instalación en Windows](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_windows#install_dr_pkg_windows)

### Configuración del entorno
{: #cfg_env}

- [Configuración del entorno](/docs/services/Db2whc/connecting?topic=Db2whc-cfg_loc_env#cfg_loc_env)
- [Soporte para la capa de sockets seguros (SSL)](/docs/services/Db2whc/connecting?topic=Db2whc-ssl_support#ssl_support)

## Opciones de conectividad
{: #connect_opts}

{{site.data.keyword.dashdbshort_notm}} ofrece diversas opciones de conectividad segura que dependen de los requisitos de conexión de la aplicación.  
{: shortdesc}

Consulte [Opciones de conectividad](/docs/services/Db2whc/connecting?topic=Db2whc-connect_options#connect_options).

## Conexión mediante programas
{: #conx_prgrm}

Puede utilizar lenguajes de programación comunes para crear aplicaciones que conectan a una base de datos de {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

- [JDBC](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_jdbc#con_prog_jdbc)
- [ODBC o CLI de Microsoft Windows](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_odbc_cli#con_prog_odbc_cli)
- [.NET](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_net#con_prog_net)
- [Administrador de orígenes de datos ODBC](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_odbc_dsa#con_prog_odbc_dsa)
- [PHP](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_php#con_prog_php)
- [API REST](/docs/services/Db2whc/connecting?topic=Db2whc-con_rest_api#con_rest_api)
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
- [DataStage](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#datastage)
- [Informatica](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#informatica)
- [Lift](https://www.lift-cli.cloud.ibm.com/#docs){:external}
- [InfoSphere Data Replication](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#idr)
- [Segment](https://segment.com/docs/destinations/db2/){:external}
- [Data Studio](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#data_studio)
- [Data Server Manager](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#dsm)
- [CLPPLUS](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#clpplus)
- [Conecte Aginity Workbench para migrar modelos de datos y datos de Netezza® a {{site.data.keyword.dashdbshort_notm}}](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#aginity_wb)
- [InfoSphere Data Architect para diseñar y desplegar el esquema de base de datos](/docs/services/Db2whc/connecting?topic=Db2whc-data_int#ida)

### Visualización de datos/BI
{: #dvis_bi}

- [Cognos Analytics para ejecutar informes de inteligencia empresarial en sus datos](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#cognos)
- [Looker](https://docs.looker.com/setup-and-management/connecting-to-db){:external}
- [Tableau](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#tableau)
- [Microsoft Excel](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#excel)
- [Esri ArcGIS for Desktop para realizar análisis geoespaciales y publicar mapas con sus datos](/docs/services/Db2whc/connecting?topic=Db2whc-data_vis_bi#esri_arcgis)

### Ciencia de datos
{: #dsci}

- [Watson Studio (anteriormente IBM Data Science Experience)](/docs/services/Db2whc/connecting?topic=Db2whc-ds#watson_studio)
- [SPSS Statistics](/docs/services/Db2whc/connecting?topic=Db2whc-ds#spss_stats)
- [SAS](/docs/services/Db2whc/connecting?topic=Db2whc-ds#sas)
- [Entorno de desarrollo R local](/docs/services/Db2whc/connecting?topic=Db2whc-ds#r_dev_env)

## Conexión a otra base de datos Db2
{: #fed}

La virtualización de datos de Db2 (también denominada federación) recibe soporte de {{site.data.keyword.dashdbshort_notm}}. La virtualización de datos le ofrece acceso mediante una sola consulta a todos sus datos ubicados en diversas bases de datos distribuidas en cualquier punto de la organización. Puede acceder a los datos ubicados en cualquiera de los orígenes de datos Db2 o Informix, tanto en la nube como locales. 

Esta función está admitida en todas las versiones de {{site.data.keyword.dashdbshort_notm}}, excepto en el plan de entrada. Sin embargo, puede utilizar el plan de entrada como destino desde el que extraer datos.

- [Virtualización de datos (federación)](/docs/services/Db2whc?topic=Db2whc-data_virt_fed#data_virt_fed)


