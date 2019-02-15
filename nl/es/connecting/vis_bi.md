---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-24"

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

# Visualización de datos/BI
{: #data_vis_bi}

También puede conectar aplicaciones externas a {{site.data.keyword.dashdbshort_notm}} y utilizarlas para gestionar o analizar todavía más sus datos. 
{: shortdesc}

## Cognos Analytics
{: #cognos}

Puede ejecutar los informes de IBM Cognos® en datos de la nube en lugar de los datos de una base de datos local. Después de cargar los datos a una base de datos de {{site.data.keyword.dashdbshort_notm}}, configure el controlador JDBC y utilice las herramientas de administración de Cognos para crear la conexión de base de datos. <!--These instructions explain how to connect to the database from Cognos version 10.2.1.-->
{: shortdesc}

Vea este vídeo para saber cómo crear una conexión.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Creación de una conexión desde Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TRUEPVHGi0s?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

Para obtener más información, consulte [Conexión de Cognos Analytics ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/en/SSEP7J_11.0.0/com.ibm.swg.ba.cognos.ug_cra.doc/c_create_ds.html#create_ds){:new_window}

## Looker
{: #looker}

Puede conectar Looker a una base de datos de {{site.data.keyword.dashdbshort_notm}}. Looker es una app de inteligencia empresarial y una gran plataforma de análisis con la que puede explorar, analizar y compartir analíticas empresariales en tiempo real.
{: shortdesc}

[Conexión de Looker ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.looker.com/setup-and-management/connecting-to-db){:new_window}

## Tableau
{: #tableau}

En estas instrucciones se explica cómo conectar Tableau a una base de datos de {{site.data.keyword.dashdbshort_notm}} y aplicarla a Tableau Desktop<!--version 8.x-->, pero puede utilizar pasos similares para otras herramientas de Tableau.
{: shortdesc}

### Requisitos previos
{: #prereq1}

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](connecting.html#prereqs) necesarios.

### Procedimiento
{: #proc1}

1. En Tableau Desktop, abra la ventana o página de la herramienta que se utiliza para definir una conexión de base de datos.
2. Desde la página de inicio, pulse **Conectar a datos**.
3. Desde la lista **Orígenes de datos**, seleccione el origen de datos o el controlador para utilizar para la conexión de base de datos. En la sección **En un servidor** de la lista, seleccione **IBM Db2**.
4. Desde la ventana **Conexión de IBM DB2**, especifique la información de conexión utilizando la tabla siguiente.

| Campo Tableau | Campo de información de conexión de Db2 |
|---------------|-----------------------------------|
| Paso 1: Entrar un nombre de servidor | Nombre de host |
| Paso 2: Puerto | Número de puerto |
| Paso 3: Entrar una base de datos en el servidor | Nombre de base de datos |
| Nombre de usuario | ID de usuario |
| Contraseña | Contraseña |
{: caption="Tabla 1. Campos de Tableau para la información de conexión" caption-side="top"}

5. Pulse **Conectar** para establecer la conexión. Tableau ofrece varias opciones para conectarse a los datos. Para hacer un uso completo de la base de datos de {{site.data.keyword.dashdbshort_notm}}, seleccione la opción **Conectar en directo**.

## Microsoft Excel
{: #excel}

En estas instrucciones se explica cómo conectar Microsoft Excel <!--2010-->a una base de datos de {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Requisitos previos
{: #prereq2}

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](connecting.html#prereqs) necesarios.

Debe tener el paquete de controlador de Db2 o IBM® Data Server Driver Package instalados en el sistema local. 

**Restricción**: Solo se admiten conexiones entre Excel y {{site.data.keyword.dashdbshort_notm}} en el sistema operativo Windows.

### Procedimiento
{: #proc2}

1. En la consola web, vaya a la página **Ejecutar SQL**.
    
2. Escriba una o más sentencias SELECT en el recuadro de texto del editor.

3. Pulse en una de las opciones de ejecución.

4. Pulse **Archivo ODC Excel**.

5. Descargue y abra el archivo `BLUExcel.odc` en Excel. Si se muestra un aviso de seguridad, pulse **Habilitar**.

6. Pulse **Abrir** para conectarse a la base de datos {{site.data.keyword.dashdbshort_notm}}. Se abre el recuadro de diálogo **Conectarse a base de datos DB2**.

7. Escriba el ID de usuario y la contraseña que utiliza para iniciar sesión en {{site.data.keyword.dashdbshort_notm}}. Para obtener el ID de usuario y la contraseña, pulse **Conectar** en la consola web o **Conectar > Información de conexión** en la consola web.

8. Asegúrese de que la modalidad de conexión es `Compartir` y, después, pulse **Aceptar**.

### Resultados
{: #results2}

Los resultados de la consulta se muestran en una hoja de cálculo de Excel. Estos son los mismos resultados que los que se muestran en el visor de resultados. Ahora puede generar gráficos e informes y analizar los datos utilizando Excel. Para obtener más información sobre cómo hacerlo y cómo ejecutar consultas SQL en los datos desde la consola web, consulte: 
- [Guía de aprendizaje: Generación de gráficos e informes mediante Excel ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/explore_excel_reports.html){:new_window}
- [Análisis con Excel ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/exploreexcel.html){:new_window}

## Esri ArcGIS for Desktop
{: #esri_arcgis}

Puede conectar Esri ArcGIS for Desktop <!--version 10.3.1 -->a una base de datos de {{site.data.keyword.dashdbshort_notm}} y utilizarlo para analizar y visualizar datos geoespaciales.
{: shortdesc}

### Requisitos previos
{: #prereq3}

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](connecting.html#prereqs) necesarios.

Debe tener el paquete de controlador de Db2 o IBM® Data Server Driver Package instalados en el sistema.

### Procedimiento
{: #proc3}

1. Determine los datos ODBC DSN de la [información de conexión](credentials.html) que ha recopilado antes.

2. Cree una nueva conexión:
      
   a. En el árbol del catálogo ArcCatalog, abra el nodo Conexiones de base de datos y pulse **Añadir conexión de base de datos**.
        
   b. En el asistente Conexiones de base de datos:
   - Seleccione **DB2** en la lista desplegable Plataforma de base de datos.
   - Entre la serie siguiente en el campo **Origen de datos**:
     ```
     HostName=<hostname>;Port=<port>;Database=<database>;
     CLIENTBUFFERSUNBOUNDLOBS=1;LOBCACHESIZE=50000000;
     FET_BUF_SIZE=256K  
     ```

     donde `<hostname>`, `<port>`, y `<database>` son marcadores que representan el nombre de host, el número de puerto y el nombre de la base de datos que ha anotado anteriormente.
            
   - Seleccione **Autenticación de base de datos** como el tipo de autenticación.
            
   - Especifique el nombre de usuario y la contraseña (el ID de usuario y contraseña que ha anotado anteriormente) en los campos correspondientes.
            
   - Pulse **OK**.
        
     ![Asistente de la conexión de base de datos](images/2_gs_conn.jpg)

### Resultados
{: #results3}

El componente ArcCatalog de Esri ArcGIS for Desktop ahora está conectado a la base de datos {{site.data.keyword.dashdbshort_notm}}. 


