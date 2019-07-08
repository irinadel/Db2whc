---

copyright:
  years: 2014, 2019
lastupdated: "2019-05-08"

keywords: Db2 Warehouse on Cloud, loading data, object store, IBM Cloud Object Storage, Amazon S3, LOAD command, Mass Data Migration Service (MDMS), migration, Lift

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

# Carga de datos en {{site.data.keyword.dashdbshort_notm}}
{: #loading_data}

Puede cargar datos desde un archivo de datos en un formato delimitado (CSV o TXT) ubicados en una red local o en un almacén de objetos (Amazon S3 o {{site.data.keyword.Bluemix_notm}} Object Storage) a {{site.data.keyword.dashdblong}}. Puede incluso migrar los datos desde un sistema local.
{: shortdesc}

## Carga de datos desde un almacén de objetos
{: #cos}

Para cargar datos de Amazon S3 o {{site.data.keyword.Bluemix_notm}} Object Storage en {{site.data.keyword.dashdblong}}, seleccione uno de los métodos siguientes:
* Consola web de {{site.data.keyword.dashdbshort_notm}}. **Carga de > Amazon S3**. 
* Tablas externas directamente. El siguiente es un ejemplo de una sentencia SQL:

    ```
    INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
        (CCSID 1208 s3('s3.amazonaws.com', 
        '<S3-access-key-ID>',
        '<S3-secret-access-key>', 
        '<my_bucket>'
           )
      )      
    ```

  Para cargar datos de {{site.data.keyword.Bluemix_notm}} Object Storage mediante tablas externas directamente, a continuación se muestra una sentencia SQL de ejemplo:

  ```
  INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net', 
  '<S3-access-key-ID>',
  '<S3-secret-access-key>', 
  '<my_bucket>'
     )
    )      
  ```

  Para {{site.data.keyword.Bluemix_notm}} Object Storage, para crear las credenciales de HMAC al crear las nuevas credenciales de servicio, especifique {"HMAC:true"} en el campo *Añadir parámetros de configuración en línea*.
  {: note}

* Para mejorar el rendimiento, también se puede utilizar el mandato **LOAD** de DB2
para cargar datos desde Amazon S3:

  ```
  CALL SYSPROC.ADMIN_CMD('LOAD FROM "S3::<amazon-s3-URL>::<s3-access-key-id>::<s3-secret-access-key>:
  :<s3-bucket-name>::<path-to-data-file>" OF <filetype> <additional-load-options> INTO <table-name>)
  ```

  A continuación se muestra un uso de ejemplo del mandato **LOAD** de Db2:

  ```
  CALL SYSPROC.ADMIN_CMD('load from "S3::s3-us-west-2.amazonaws.com::<s3-access-key-id>:
  :<s3-secret-access-key>::ibm-state-store::bdidata2TB/web_site.dat" of DEL modified by codepage=1208
  coldel0x7c WARNINGCOUNT 1000 MESSAGES ON SERVER INSERT into BDINSIGHTS2.web_site ');
  ```

  Para ver las opciones de mandatos admitidas, consulte el mandato [**LOAD**](https://www.ibm.com/support/knowledgecenter/en/SSEPGG_11.1.0/com.ibm.db2.luw.admin.cmd.doc/doc/r0008305.html){:external}. 

Para ver una demo guiada sobre la carga de datos desde
{{site.data.keyword.Bluemix_notm}} Object Storage, consulte: [Demo guiada de {{site.data.keyword.dashdblong}}: Exploración de la carga de datos](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud){:external}

## Migración de datos desde un sistema local
{: #onprem}

Para migrar los datos desde un sistema local, seleccione uno de los métodos siguientes dependiendo del tamaño del conjunto de datos:
* Menos de 25 TB de datos: [IBM Lift](#lift)
* 25 TB de datos y superior: [{{site.data.keyword.Bluemix_notm}} Mass Data Migration Service](#mdms)

### Lift
{: #lift}

Lift es una aplicación que puede utilizar de forma gratuita para migrar los datos a {{site.data.keyword.Bluemix_notm}} desde los diversos orígenes de datos listados en la Tabla 1. 

| Base de datos de destino en {{site.data.keyword.Bluemix_notm}} | Origen de datos |
|------------------------------|-------------|
| IBM Db2 Warehouse on Cloud   | IBM Db2 |
|                              | IBM Db2 Warehouse |
|                              | IBM Integrated Analytics System |
|                              | IBM PureData System for Analytics |
|                              | Oracle Database |
|                              | Microsoft SQL Server |
|                              | Formato de archivo CSV |
{: caption="Tabla 1. Migración de orígenes de datos" caption-side="top"}

Para descargar e instalar Lift, consulte [Descargar Lift](https://www.lift-cli.cloud.ibm.com/#download){:external}.

Para obtener instrucciones paso a paso sobre la migración de los datos al {{site.data.keyword.Bluemix_notm}} utilizando Lift, consulte: [Migrar datos a {{site.data.keyword.dashdblong}}](https://www.lift-cli.cloud.ibm.com/#docs){:external}.

### {{site.data.keyword.Bluemix_notm}} Mass Data Migration Service
{: #mdms}

El servicio de migración de datos masiva (MDMS) de {{site.data.keyword.Bluemix_notm}} puede utilizarse para migrar datos desde bases de datos de IBM PureData Systems for Analytics (Netezza) grandes (de 25 TB y superiores) a una base de datos de {{site.data.keyword.dashdblong}} completamente gestionada en {{site.data.keyword.Bluemix_notm}}.

MDMS ofrece una forma rápida, sencilla y segura para transferir físicamente de terabytes a petabytes de datos a {{site.data.keyword.Bluemix_notm}}. MDMS es un dispositivo de almacenamiento móvil con una capacidad de almacenamiento utilizable de 120 TB. Este dispositivo le permite superar, con un solo servicio, desafíos comunes, como altos costes de transferencia, tiempos de transferencia largos y problemas de seguridad.

![Vista del dispositivo del servicio de migración de datos masiva](images/mdms.svg)

Para obtener más información sobre el dispositivo MDMS, consulte la [Guía de aprendizaje de iniciación](/docs/infrastructure/mass-data-migration?topic=mass-data-migration-getting-started-tutorial#getting-started-with-ibm-cloud-mass-data-migration){:external}.

Para obtener información sobre cómo migrar datos desde una base de datos de IBM PureData System for Analytics (Netezza) a una base de datos de {{site.data.keyword.dashdblong}} mediante el dispositivo MDMS, consulte: [Migración desde IBM PureData System for Analytics (Netezza)](/docs/services/Db2whc/connecting?topic=Db2whc-pda#pda){:external}.

## Guía de aprendizaje: Migración de datos desde bases de datos relacionales locales
{: #tutorial}

En esta guía de aprendizaje se muestra cómo migrar datos desde bases de datos relacionales locales a {{site.data.keyword.dashdbshort_notm}} para aplicaciones de análisis empresarial. 

[Depósito de datos híbrido con {{site.data.keyword.dashdbshort_notm}}](https://www.ibm.com/cloud/garage/tutorials/ibm-db2-warehouse-on-cloud/hybrid-data-warehousing-with-db-2-warehouse-on-cloud){:external}

