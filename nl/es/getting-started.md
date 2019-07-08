---

copyright:
  years: 2014, 2019
lastupdated: "2019-05-21"

keywords:

subcollection: Db2whc

---

<!-- Attribute definitions --> 
{:javascript: #javascript .ph data-hd-programlang='javascript'}
{:java: #java .ph data-hd-programlang='java'}
{:ruby: #ruby .ph data-hd-programlang='ruby'}
{:php: #php .ph data-hd-programlang='php'}
{:python: #python .ph data-hd-programlang='python'}
{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}

# Guía de aprendizaje de iniciación
{: #getting-started}

El servicio gestionado de {{site.data.keyword.dashdblong}} es una base de datos SQL suministrada para usted en la nube. Puede utilizar Db2 Warehouse como utilizaría cualquier software de base de datos, pero sin la sobrecarga ni el gasto de la configuración de hardware o la instalación y el mantenimiento de software. 
{: shortdesc}

<!-- New tutorial submitted by Olaf Depper of DTE on 5-May-2019. Working on edits of Word doc. -->
<!--To get started on accessing and working with {{site.data.keyword.dashdbshort_notm}}, go through the [Getting started tutorial](https://cloudcontent.mybluemix.net/cloud/garage/dte/tutorial/test-db2-warehouse-cloud-post-sales){:external}. -->

## Prueba gratuita
{: #freetrial}

Puede probar el plan {{site.data.keyword.dashdbshort_notm}} Entry con hasta 1 GB de almacenamiento sin coste. [Prueba gratuita](https://cloud.ibm.com/catalog/services/db2-warehouse){:external}

## Interfaces
{: #interfaces}

Puede trabajar con la base de datos de Db2 Warehouse de los siguientes modos:
{: shortdesc}

   * Desde la consola web
   * API REST
   * Conecte aplicaciones o herramientas preferidas desde el sistema local
   * Utilice {{site.data.keyword.dashdbshort_notm}} como origen de datos para apps o servicios de {{site.data.keyword.Bluemix_notm}}

### Consola web
{: #web_console}

La consola web proporciona una interfaz gráfica para todo lo que puede utilizar su base de datos, incluyendo: recursos de cargas, un editor SQL, descargas de controladores, etc.
{: shortdesc}

![Vista de la página del panel de control de la consola web](images/uc.png "Se abre la consola web en la página del panel de control")

<!-- Click the link to take a tour of the {{site.data.keyword.dashdbshort_notm}} for Analytics web console: [General tour](http://ibm.biz/dashdb-general-quick-tour){:external}. -->

Puede acceder a la consola web de los siguientes modos:
   * Desde el panel de control de {{site.data.keyword.Bluemix_notm}} - Puede abrir la consola web desde la página Detalles de servicio para el servicio de {{site.data.keyword.dashdbshort_notm}}.
   * URL directo - Puede marcar como favorito el URL de la consola web para el servicio de {{site.data.keyword.dashdbshort_notm}}.

### API REST
{: #api}

Con los planes de servicio de {{site.data.keyword.dashdbshort_notm}} puede realizar tareas relacionadas con la gestión de archivos y carga de datos utilizando la [API REST de {{site.data.keyword.dashdbshort_notm}}](http://ibm.biz/db2whc_api){:external}.
{: shortdesc}

### Conecte aplicaciones o herramientas preferidas desde el sistema local
{: #connect_apps}

Configure el entorno local para conectar la base de datos de {{site.data.keyword.dashdbshort_notm}} siguiendo estos pasos:
{: shortdesc}

1. Descargue el [paquete de controlador](/docs/services/Db2whc/connecting?topic=Db2whc-dr_pkg#dr_pkg) desde la consola web de {{site.data.keyword.dashdbshort_notm}}.
2. Instale el paquete de controlador en el sistema en el que se ejecutan sus apps o herramientas:
   - [Instalación en Linux o PowerLinux](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_linux#install_dr_pkg_linux)
   - [Instalación en Mac OS X](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_mac#install_dr_pkg_mac)
   - [Instalación en Windows](/docs/services/Db2whc/connecting?topic=Db2whc-install_dr_pkg_windows#install_dr_pkg_windows)
3. [Configure los archivos de controlador](/docs/services/Db2whc/connecting?topic=Db2whc-cfg_loc_env#cfg_loc_env) para la base de datos de {{site.data.keyword.dashdbshort_notm}}.

### Utilice Db2 Warehouse on Cloud como origen de datos para apps o servicios de {{site.data.keyword.Bluemix_notm}}
{: #data_src}

Las apps alojadas en {{site.data.keyword.Bluemix_notm}} pueden conectarse a la base de datos de {{site.data.keyword.dashdbshort_notm}} del mismo modo que se conectan las aplicaciones locales a la base de datos de {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

Cuando las apps utilizan la plataforma de {{site.data.keyword.Bluemix_notm}}, puede sacar partido de la variable de entorno `VCAP _SERVICES` para simplificar la tarea de especificar detalles y credenciales de bases de datos:
1. En el panel de control de {{site.data.keyword.Bluemix_notm}}, en el separador **Conexiones** de la página Detalles del servicio para el servicio de {{site.data.keyword.dashdbshort_notm}}, pulse el botón **Crear conexión**.
2. Seleccione la app de {{site.data.keyword.cloud_notm}} para utilizarla con la base de datos de {{site.data.keyword.dashdbshort_notm}} como origen de datos y luego pulse el botón **Conectar**.
3. Actualice el código de aplicación para recuperar detalles y credenciales de la base de datos desde la variable de entorno `VCAP_SERVICES`:

    **Ejemplo sin `VCAP_SERVICES`**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    $database    = "BLUDB";         # Obtenga los detalles de la base de datos desde
    $hostname    = "<Host-name>";   # la página Conectar de dashDB
    $port        = 50000;           # consola web.
    $user        = "<User-ID >";    #
    $password    = "<Password>";    #
    $dsn         = "DATABASE=$database;" .
                   "HOSTNAME=$hostname;" .
                   "PORT=$port;" .
                   "PROTOCOL=TCPIP;" .
                   "UID=$user;" .
                   "PWD=$password;";

    $conn_string = $driver . $dsn;

    $conn        = db2_connect( $conn_string, "", "" );
    ?>
    ```

    **Ejemplo con `VCAP_SERVICES`**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    $vcap        = json_decode( getenv( "VCAP_SERVICES" ), true );
    $dsn         = $vcap[ "dashDB" ][0][ "credentials" ][ "dsn" ];

    $conn_string = $driver . $dsn;
                                   
    $conn        = db2_connect( $conn_string, "", "" );
    ?>
    ```

## Ejemplos
{: #samples}

A continuación, se muestran los enlaces a ejemplos que demuestran cómo conectarse mediante programas a la base de datos de {{site.data.keyword.dashdbshort_notm}} desde aplicaciones en distintos idiomas:
{: shortdesc}

- [JDBC](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_jdbc#con_prog_jdbc)
- [ODBC o CLI de Microsoft Windows](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_odbc_cli#con_prog_odbc_cli)
- [.NET](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_net#con_prog_net)
- [Administrador de orígenes de datos ODBC](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_odbc_dsa#con_prog_odbc_dsa)
- [PHP](/docs/services/Db2whc/connecting?topic=Db2whc-con_prog_php#con_prog_php)
- [API REST](/docs/services/Db2whc/connecting?topic=Db2whc-con_rest_api#con_rest_api)

## Vídeo: Introducción de Db2 Warehouse on Cloud
{: #intro_vid}

Vea el vídeo para ver una introducción a {{site.data.keyword.dashdbshort_notm}}.

<iframe class="embed-responsive-item" id="youtubeplayer1" title="Introducción a {{site.data.keyword.dashdbshort_notm}}" type="text/html" width="640" height="390" src="//www.youtube.com/embed/0NO9OTFWzKs?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

## Vídeo: Introducción al plan Flex Performance
{: #intro_vid_flex}

Vea este vídeo para ver una introducción al plan Flex Performance de {{site.data.keyword.dashdbshort_notm}}.

<iframe class="embed-responsive-item" id="youtubeplayer2" title="Creación de una conexión desde Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

## Vídeo: Conexión a una aplicación de análisis
{: #cognos_vid}

Vea este vídeo para saber cómo crear una conexión desde Cognos Analytics.

<iframe class="embed-responsive-item" id="youtubeplayer3" title="Creación de una conexión desde Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TRUEPVHGi0s?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

