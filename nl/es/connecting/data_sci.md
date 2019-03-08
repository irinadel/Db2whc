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

# Ciencia de datos
{: #ds}

También puede conectar aplicaciones externas a {{site.data.keyword.dashdbshort_notm}} y utilizarlas para gestionar o analizar todavía más sus datos. 
{: shortdesc}

## Watson Studio
{: #watson_studio}

Después de crear un proyecto en IBM Watson Studio (anteriormente Data Science Experience), añada activos de datos para poder trabajar con los datos. Todos los colaboradores del proyecto obtienen una autorización automática para acceder a los datos del proyecto.
{: shortdesc}

La forma en la que se añaden datos y el sitio desde el que se pueden añadir difiere en proyectos existentes y proyectos de IBM Watson. Los proyectos de IBM Watson utilizan {{site.data.keyword.Bluemix_notm}} Object Storage. Hablamos de un proyecto heredado si este utiliza Object Storage OpenStack Swift. 

### Para crear una nueva conexión en un proyecto de IBM Watson:

1. Pulse **Añadir a proyecto > Conexión**.
    
2. Seleccione un origen de datos.
    
3. Especifique la información de conexión necesaria para el origen de datos. Normalmente, debe proporcionar información como el host, el número de puerto, el nombre de usuario y la contraseña.
    
4. Puede descubrir activos de las conexiones a {{site.data.keyword.dashdbshort_notm}}, lo que le proporciona la capacidad de añadir todas las tablas de la conexión como activos de datos a un proyecto. Seleccione **Descubrir activos de datos** y seleccione un proyecto.
    
5. Pulse **Crear**. Aparece la conexión en la página **Activos**.

Vea este vídeo para saber cómo crear una conexión y añadir datos conectados a un proyecto.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Crear una conexión y agregar datos conectados a un proyecto" type="text/html" width="640" height="390" src="//www.youtube.com/embed/U7-gCbo4QtM?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

### Para crear una nueva conexión en un proyecto existente:

1. En la página **Activos** del proyecto, pulse el icono **Buscar y añadir datos**.
    
2. En el panel **Conexiones**, pulse **Crear conexión**.

3. Especifique un nombre y una descripción y seleccione una categoría de servicio:

   **Servicio de datos** = Servicio de datos de {{site.data.keyword.Bluemix_notm}}

   Al seleccionar **Servicio de datos**, los servicios de datos existentes de {{site.data.keyword.Bluemix_notm}} aparecerán en la lista **Instancia de servicio**.

4. Seleccione el servicio o servidor de base de datos de la lista.

5. Especifique la información de conexión:

   Al seleccionar **Servicio de datos**, los servicios de datos existentes de {{site.data.keyword.Bluemix_notm}} aparecerán en la lista **Instancia de servicio**.
    
6. Pulse **Crear**. La conexión está disponible para todos los proyectos existentes.
    
7. En el panel **Conexiones**, seleccione la conexión y pulse **Aplicar**.

Para añadir una conexión existente a un proyecto existente:

1. En la página **Activos** del proyecto, pulse el icono **Buscar y añadir datos**.
    
2. En el panel **Conexiones**, seleccione la conexión y pulse **Aplicar**.

## SPSS Statistics
{: #spss_stats}

En estas instrucciones se explica cómo crear una conexión desde IBM® SPSS® Statistics a una base de datos de {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Requisitos previos
{: #prereq11}

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](/docs/services/Db2whc/connecting/connecting.html#prereqs) necesarios.

### Procedimiento
{: #proc11}

1. En SPSS Statistics, pulse **Archivo > Abrir base de datos > Nueva consulta**.
    
2. En el asistente Base de datos, pulse **Añadir origen de datos ODBC**.
    
3. Utilice la ventana Administrador de orígenes de datos ODBC para agregar un nombre de origen de datos (DSN) de ODBC en la base de datos de {{site.data.keyword.dashdbshort_notm}}:
        
   a. En el separador **DSN de usuario**, pulse **Añadir**.

   b. En la ventana Crear nuevo origen de datos, seleccione el controlador denominado **IBM DB2 ODBC DRIVER** y pulse **Finalizar**.

   Asegúrese de que el controlador que seleccione no es un controlador con un nombre similar como, por ejemplo, `IBM DB2® ODBC DRIVER - DB2COPY`. Si el controlador no aparece en la lista, salga de SPSS Statistics y, a continuación, descargue e instale el controlador. Consulte [Paquete de controlador Db2](/docs/services/Db2whc/connecting/driver_pkg.html).
        
   c. En la ventana Controlador ODBC IBM - Añadir, especifique un nombre de origen de datos (normalmente el nombre de la base de datos a la que se está conectando) y pulse **Añadir**.
        
   d. En la ventana Configuración de CLI/ODBC, en el separador **Origen de datos**, especifique el ID de usuario y la contraseña de la [información de conexión](/docs/services/Db2whc/connecting/credentials.html) que ha recopilado antes.
        
   e. En la página Configuración avanzada, para cada uno de los parámetros siguientes, pulse **Añadir** para abrir la ventana Añadir parámetro CLI e iniciar el paso y pulse **Aceptar** para volver a la página Configuración avanzada:
            
   - Seleccione el parámetro `Database` y, a continuación, pulse **Aceptar** para abrir la ventana Valores de CLI/ODBC. En el campo **Valor pendiente**, especifique el nombre de base de datos de la información de conexión que ha recopilado antes.

   - Seleccione el parámetro `Hostname` y, a continuación, pulse **Aceptar** para abrir la ventana Valores de CLI/ODBC. En el campo **Valor pendiente**, especifique el nombre de host de la información de conexión que ha recopilado antes.

   - Seleccione el parámetro `Port` y pulse **Aceptar** para abrir la ventana Valores de ODBC/CLI. En el campo **Valor pendiente**, especifique el número de puerto de la información de conexión que ha recopilado antes.
            
   - Seleccione el parámetro `Protocol` y pulse **Aceptar** para abrir la ventana Valores de ODBC/CLI. Seleccione **TCP/IP**.
        
   f. Pulse **Aceptar** para volver a la ventana Administrador de orígenes de datos ODBC.
        
   g. En el separador **DSN de usuario**, seleccione el nombre de origen de datos y, después, pulse **Configurar**.
        
   h. En la ventana Valores de ODBC/CLI, pulse **Conectar** para probar la conexión.
            
   - Si la conexión se ha realizado correctamente, pulse **Aceptar** para volver a la ventana Administrador de orígenes de datos ODBC y pulse **Aceptar** para salir de la ventana.
            
   - Si la conexión no se ha realizado correctamente, observe y corrija los errores antes de volver a probar la conexión.

## SAS
{: #sas}

En estas instrucciones se explica cómo crear una conexión desde SAS a una base de datos de {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Requisitos previos
{: #prereq12}

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](/docs/services/Db2whc/connecting/connecting.html#prereqs) necesarios.

### Procedimiento
{: #proc12}

Para obtener los pasos sobre cómo conectarse desde SAS a una base de datos de {{site.data.keyword.dashdbshort_notm}}, consulte la documentación de SAS:
- [Interfaz SAS/ACCESS a DB2 en hosts UNIX y PC ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://documentation.sas.com/?docsetId=acreldb&docsetTarget=p1dzq4zjg1iycgn16l4xj9nnvibt.htm&docsetVersion=9.4&locale=en){:new_window}

## Entorno de desarrollo R
{: #r_dev_env}

En lugar de utilizar un entorno RStudio® que esté integrado con IBM Watson Studio, es posible que prefiera utilizar su propio entorno de desarrollo R instalado localmente. Por ejemplo, puede tener su propia instalación de RStudio o puede que prefiera utilizar alguna otra herramienta de desarrollo como Rcmdr o Rattle. En estas instrucciones se explica cómo conectar un entorno de desarrollo R a una base de datos de {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Requisitos previos
{: #prereq13}

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](/docs/services/Db2whc/connecting/connecting.html#prereqs) necesarios.

### Procedimiento
{: #proc13}

1. En su entorno R local, instale el paquete `ibmdbR` especificando el mandato siguiente:

   `install.packages("ibmdbR")`

   El entorno R local accede a la red CRAN (Comprehensive R Archive Network) y descarga e instala automáticamente el paquete `ibmdbR` y cualquier paquete de requisito previo que todavía no esté instalado.
    
2. Cree una conexión de controlador ODBC entre el entorno de desarrollo R y la base de datos de {{site.data.keyword.dashdbshort_notm}}:
        
   a. [Configure la base de datos como origen de datos ODBC ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_cli_and_odbc_applications.html){:new_window}.
        
   b. Abra el entorno de desarrollo R instalado localmente.
        
   c. En el indicador R, entre las sentencias siguientes para crear la conexión. Sustituya los marcadores con la [información de conexión](/docs/services/Db2whc/connecting/credentials.html) que ha recopilado antes.

   - Si el entorno de desarrollo R instalado localmente se ejecuta en la base de datos {{site.data.keyword.dashdbshort_notm}}:

     ```
     library(ibmdbR)
     host.name <- "placeholderForYourHostName"
     port <-"placeholderForPortNumber" # 50000 if not using SSL or 50001 if using SSL
     user.name <-"placeholderForYourUserName"
     pwd <- "placeholderForYourPassword"
     con.text <- paste("placeholderForYourDSNName;DRIVER=BLUDB",
                       ";Database=BLUDB",
                       ";Hostname=",host.name,
                       ";Port=",port,
                       ";PROTOCOL=TCPIP",
                       ";UID=", user.name,
                       ";PWD=",pwd,sep="")
     # Conéctese para utilizar una serie de conexión del controlador odbc a una base de datos remota
     con <- idaConnect(con.text)
     ```

   - Si el entorno de desarrollo R instalado localmente no se ejecuta en la base de datos {{site.data.keyword.dashdbshort_notm}}:

     ```
     library(ibmdbR)
     driver.name <- "{placeholderForYourDriverName}"
     db.name <- "placeholderForYourDatabaseName"
     host.name <- "placeholderForYourHostName"
     port <-"placeholderForYourPort"
     user.name <-"placeholderForYourUserName"
     pwd <- "placeholderForYourPassword"
     con.text <- paste("placeholderForYourDSNName;DRIVER=",driver.name,
                       ";Database=",db.name,
                       ";Hostname=",host.name,
                       ";Port=",port,
                       ";PROTOCOL=TCPIP",
                       ";UID=", user.name,
                       ";PWD=",pwd,sep="")
     # Conéctese para utilizar una serie de conexión del controlador odbc a una base de datos remota
     con <- idaConnect(con.text)
     ```

     **Nota**: La sentencia que se utiliza para crear el objeto de conexión emplea el método `idaConnect()`, en lugar de los métodos `odbcConnect()` u `odbcDriverConnect()`.
        
   d. Inicialice el paquete de análisis emitiendo el mandato R siguiente:

   `idaInit(con)`

   e. Para probar si la conexión funciona, emita el mandato R siguiente:

   `idaShowTables()`

   La consola muestra una lista de todas las tablas y vistas en el esquema actual.

