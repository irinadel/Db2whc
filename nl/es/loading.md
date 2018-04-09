---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-23"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Cargando datos
{: #load}

Puede cargar datos desde un archivo de datos en un formato delimitado como CSV o TXT ubicados en una red local, un almacén de objetos
(Amazon S3 o IBM Cloud Object Storage (anteriormente SoftLayer Swift)), o un servidor Db2®. También puede llenar una instancia de base de datos directamente con datos de una base de datos Cloudant® o realizando un proceso de carga desde una aplicación como InfoSphere® DataStage®.
{: shortdesc}

* [Carga de datos desde PureData System for Analytics (Netezza) ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://lift.ng.bluemix.net/#docs){:new_window}
* [Carga de datos desde Oracle ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://lift.ng.bluemix.net/#docs){:new_window}
* [Carga de datos desde SQL Server ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://lift.ng.bluemix.net/#docs){:new_window}
* [Carga de un archivo CSV ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://lift.ng.bluemix.net/#docs){:new_window}
<!-- * [Loading data from IBM Cloud Object Storage (formerly SoftLayer Swift) ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/learn_how/loaddata_swift.html){:new_window} -->
* Cargue datos de Amazon S3 utilizando uno de los métodos siguientes:
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

<!-- [Loading data from Amazon S3 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/learn_how/s3.html){:new_window} -->
