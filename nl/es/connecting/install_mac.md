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

# Instalación de paquete de controlador en Mac OS X

Puede instalar el paquete de controlador de {{site.data.keyword.dashdbshort_notm}} en Mac OS X utilizando el script `installDSDriver.sh`. 
{: shortdesc}

## Requisitos previos

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](connecting.html#prereqs) necesarios.

<!-- Download the Db2 driver package for your operating system from the web console and install it. -->

## Procedimiento

- **Para una nueva instalación**

  1. Monte la imagen de disco pulsando dos veces en el archivo `macos_dsdriver.dmg`.
   
     Se abre una nueva ventana **Buscador** con el contenido de la imagen de disco.

     Si la ventana **Buscador** no se abre, pulse dos veces en el icono `macos_dsdriver` del escritorio.
  2. En la ventana **Buscador**, efectúe una doble pulsación en el archivo `installDSDriver.sh`.

     El paquete de controlador se instala en la ubicación predeterminada: `/Applications/dsdriver`.

- **Para las actualizaciones de la instalación del paquete de controlador existente**

  1. Haga una copia de seguridad de los archivos de configuración actuales:

     a. Vaya a la carpeta `Applications/dsdriver/cfg`.

     b. Copie los archivos siguientes en una carpeta diferente: 
    
        `db2cli.ini`

        `db2dsdriver.cfg`
  2. Elimine el paquete de controlador que tiene instalado pulsando con el botón derecho en la carpeta `dsdriver` y seleccionando **Mover a la papelera**.
  3. Instale el nuevo paquete de controlador como se describe en la sección anterior **Para una nueva instalación**:
     
     a. Monte la imagen de disco pulsando dos veces en el archivo `macos_dsdriver.dmg`.
     b. En la ventana **Buscador**, efectúe una doble pulsación en el archivo `installDSDriver.sh`.
  4. Restaure los archivos de configuración:

     Copie los archivos `db2cli.ini` y `db2dsdriver.cfg` que ha guardado del paso 1 en la carpeta `/Applications/dsdriver/cfg`.

## Qué hacer a continuación

Para poder conectar aplicaciones locales o herramientas de cliente a la base de datos de {{site.data.keyword.dashdbshort_notm}}, [configure el entorno local](driver_pkg_cfg.html).
