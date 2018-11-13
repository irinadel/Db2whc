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

# Instalación del paquete de controlador en Windows

Puede instalar el paquete de controlador de {{site.data.keyword.dashdbshort_notm}} en Windows utilizando el instalador. 
{: shortdesc}

## Requisitos previos

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](connecting.html#prereqs) necesarios.

<!-- Download the driver package for your operating system from the web console and install it. -->

## Procedimiento

1. Ejecute el archivo ejecutable descargado como administrador.

   La vía de acceso de instalación predeterminada del paquete del controlador es: `Program Files\IBM\IBM DATA SERVER DRIVER`
2. [*Opcional*] Añada el subdirectorio `bin` del directorio de instalación del paquete de controlador a la variable de entorno `%PATH%` (para poder ejecutar el mandato **db2cli** sin especificar la vía de acceso completa al ejecutable del mandato).

## Qué hacer a continuación

Para poder conectar aplicaciones locales o herramientas de cliente a la base de datos de {{site.data.keyword.dashdbshort_notm}}, [configure el entorno local](driver_pkg_cfg.html).
