---

copyright:
  years: 2014, 2018
lastupdated: "2018-05-08"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Migración de datos a {{site.data.keyword.Bluemix_notm}}
{: #migration}

Puede cargar datos desde un archivo de datos en un formato delimitado (CSV o TXT) ubicados en una red local o en un almacén de objetos (Amazon S3 o {{site.data.keyword.Bluemix_notm}} Object Storage) a {{site.data.keyword.dashdblong}}. Puede incluso migrar los datos desde un sistema local.
{: shortdesc}

## Carga de datos desde el almacén de objetos
{: #cos}

Para cargar datos de Amazon S3, seleccione uno de los métodos siguientes:
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

**Nota:** Para {{site.data.keyword.Bluemix_notm}} Storage, para crear las credenciales de HMAC al crear las nuevas credenciales de servicio, especifique {"HMAC:true"} en el campo *Añadir parámetros de configuración en línea*.

Para obtener una demostración guiada acerca de cómo cargar datos desde {{site.data.keyword.Bluemix_notm}} Object Storage, consulte [Demostración guiada de {{site.data.keyword.dashdblong}}: Explorar la carga de datos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud){:new_window}

## Migración de datos desde un sistema local
{: #onprem}

Para migrar los datos desde un sistema local, seleccione uno de los métodos siguientes dependiendo del tamaño del conjunto de datos:
* Menos de 25 TB de datos: [IBM Lift](#lift)
* 25 TB de datos y superior: [{{site.data.keyword.Bluemix_notm}}Mass Data Migration Service](#mdms)

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

Para descargar e instalar Lift, consulte: [Descargar Lift ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://lift.ng.bluemix.net/#download){:new_window}.

Para obtener instrucciones paso a paso sobre la migración de los datos al {{site.data.keyword.Bluemix_notm}} utilizando Lift, consulte: [Migrar datos a {{site.data.keyword.dashdblong}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://lift.ng.bluemix.net/#docs){:new_window}.

### {{site.data.keyword.Bluemix_notm}} Mass Data Migration Service
{: #mdms}

El servicio de migración de datos masiva (MDMS) de {{site.data.keyword.Bluemix_notm}} puede utilizarse para migrar datos desde bases de datos de IBM PureData Systems for Analytics (Netezza) grandes (de 25 TB y superiores) a una base de datos de {{site.data.keyword.dashdblong}} completamente gestionada en {{site.data.keyword.Bluemix_notm}}.

MDMS ofrece una forma rápida, sencilla y segura para transferir físicamente de terabytes a petabytes de datos a {{site.data.keyword.Bluemix_notm}}. MDMS es un dispositivo de almacenamiento móvil con una capacidad de almacenamiento utilizable de 120 TB. Este dispositivo le permite superar, con un solo servicio, desafíos comunes, como altos costes de transferencia, tiempos de transferencia largos y problemas de seguridad.

![Vista del dispositivo del servicio de migración de datos masiva](images/mdms.svg)

Para obtener más información sobre el dispositivo MDMS, consulte: 
- [Iniciación a {{site.data.keyword.Bluemix_notm}} Mass Data Migration](/docs/infrastructure/mass-data-migration/index.html#getting-started-with-ibm-cloud-mass-data-migration){:new_window}.

Para obtener información sobre cómo migrar datos desde una base de datos de IBM PureData System for Analytics (Netezza) a una base de datos de {{site.data.keyword.dashdblong}} mediante el dispositivo MDMS, consulte: 
- [Migración desde IBM PureData System for Analytics (Netezza)](/docs/services/Db2whc/pda_db2whc_mdms.html){:new_window}.

## Guía de aprendizaje: Migración de datos desde bases de datos relacionales locales
{: #tutorial}

En esta guía de aprendizaje se muestra cómo migrar datos desde bases de datos relacionales locales a {{site.data.keyword.dashdbshort_notm}} para aplicaciones de análisis empresarial. 

[Depósito de datos híbrido con {{site.data.keyword.dashdbshort_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/cloud/garage/tutorials/ibm-db2-warehouse-on-cloud/hybrid-data-warehousing-with-db-2-warehouse-on-cloud){:new_window}

