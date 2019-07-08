---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# Instalación del paquete de controlador en Linux o PowerLinux
{: #install_dr_pkg_linux}

Puede instalar el paquete de controlador de {{site.data.keyword.dashdbshort_notm}} en Linux o PowerLinux utilizando `installDSDriver`. 
{: shortdesc}

## Requisitos previos
{: #prereq31}

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) necesarios.

<!-- Download the Db2 driver package for your operating system from the web console and install it. -->

**Solo en PowerLinux**, complete los pasos siguientes para instalar el paquete de tiempo de ejecución del compilador XL C/C++:

1. Descargue el paquete de tiempo de ejecución de compilador XL C/C++ desde el sitio de FTP. Por ejemplo, para utilizar la herramienta **wget** para descargar el paquete de tiempo de ejecución para Linux little endian Ubuntu 14, emita el mandato siguiente: 

   `wget ftp://public.dhe.ibm.com/software/server/POWER/Linux/rte/xlcpp/le/ubuntu/dists/trusty/main/binary-ppc64el/*`
2. Instale el paquete de tiempo de ejecución emitiendo el mandato siguiente:

   `sudo dpkg -iG *.deb` 

## Procedimiento
{: #proc31}

1. Descomprima el paquete de controlador comprimido que ha descargado antes.

   Ejemplo: 

   `gunzip file_name.tar.gz`

   `tar -xvf file_name.tar`

    Se crea un subdirectorio `dsdriver` en el directorio donde ha ejecutado los mandatos de descompresión.
2. Extraiga los controladores Java y ODBC/CLI.

   a. En el subdirectorio `dsdriver`, ejecute el mandato **installDSDriver**.
   
   El mandato **installDSDriver** crea los archivos de script `db2profile` y `db2cshrc` en el directorio `dsdriver`.

   b. Ejecute uno de los archivos de script siguientes basándose en el entorno de shell:

   - **Shell Bash o Korn**: `source db2profile`
   - **Shell C**: `source db2cshrc`

## Qué hacer a continuación
{: #wn}

Para poder conectar aplicaciones locales o herramientas de cliente a la base de datos de {{site.data.keyword.dashdbshort_notm}}, [configure el entorno local](/docs/services/Db2whc?topic=Db2whc-cfg_loc_env#cfg_loc_env).   




