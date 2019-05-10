---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# Instalación del paquete de controlador en Windows
{: #install_dr_pkg_windows}

Puede instalar el paquete de controlador de {{site.data.keyword.dashdbshort_notm}} en Windows utilizando el instalador. 
{: shortdesc}

## Requisitos previos
{: #prereq51}

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) necesarios.

<!-- Download the driver package for your operating system from the web console and install it. -->

## Procedimiento
{: #proc51}

1. Ejecute el archivo ejecutable descargado como administrador.

   La vía de acceso de instalación predeterminada del paquete del controlador es: `Program Files\IBM\IBM DATA SERVER DRIVER`
2. [*Opcional*] Añada el subdirectorio `bin` del directorio de instalación del paquete de controlador a la variable de entorno `%PATH%` (para poder ejecutar el mandato **db2cli** sin especificar la vía de acceso completa al ejecutable del mandato).

## Qué hacer a continuación
{: #wn51}

Para poder conectar aplicaciones locales o herramientas de cliente a la base de datos de {{site.data.keyword.dashdbshort_notm}}, [configure el entorno local](/docs/services/Db2whc?topic=Db2whc-cfg_loc_env#cfg_loc_env).
