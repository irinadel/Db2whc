---

copyright:
  years: 2014, 2019
lastupdated: "2018-07-18"

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

# Virtualización de datos (federación)
{: #data_virt_fed}

La virtualización de datos de Db2 (también denominada federación) recibe soporte de {{site.data.keyword.dashdbshort_notm}}. La virtualización de datos le ofrece acceso mediante una sola consulta a todos sus datos ubicados en diversas bases de datos distribuidas en cualquier punto de la organización. Puede acceder a los datos ubicados en cualquiera de los orígenes de datos Db2 o Informix, tanto en la nube como locales. 
{: shortdesc}

Esta función está admitida en todas las versiones de {{site.data.keyword.dashdbshort_notm}}, excepto en el plan de entrada. Sin embargo, puede utilizar el plan de entrada como destino desde el que extraer datos.

## Casos de uso
{: #use_cases}

### Consolidar orígenes de datos

Mediante la federación de sus orígenes de datos ubicadas tanto en la nube como de forma local en cualquier lugar de la organización, parece que los datos virtualizados se recuperan desde un solo origen de datos. La virtualización de datos elimina el molesto y costoso proceso de migración de datos y le ofrece la posibilidad de analizar todos los datos de forma eficiente y asequible.

<!-- A company may have started their operations with an on-premises Db2 server. As cloud technology becomes more widespread and companies start to operate on cloud in a cost-effective fashion, there will be continued Cloud growth. However, the organization’s data on both sources remain as a critical component to their decision-making processes. By way of example, a client operating in retail industry needs to be able to access all data, say customer information, to run further analysis on their customers’ consumption behaviors. They need to be able to identify customers, match their records on cloud with already existing ones from an on-premises database and compose them as if the data is being retrieved from a single source. Federation capability here prevents the burdensome data migration process and allows the user to access the data without moving the data.

located in the cloud and on-premises -->

### Adjuntar a Db2 on Cloud

Los usuarios de productos de la familia Db2 pueden federar datos procedentes de bases de datos {{site.data.keyword.Db2_on_Cloud_short}} y {{site.data.keyword.dashdbshort_notm}}. Desde una interfaz común para acceder a los datos, puede añadir, consultar y analizar fácilmente sus datos sin tener que utilizar completos procesos ETL y sin código adicional.

<!-- Db2 family users would now be able to federate data between Db2 on Cloud and Db2 Warehouse on Cloud. By being provided a common interface for accessing the data, a user can now easily add or query data from or to the Warehouse without complex ETL processes or any additional code. -->

<!-- ### Sharded data across multiple servers

At times, you might choose to partition (shard) your data. With federation capabilities, sharded data can be queried with a unified interface. Federation gives you the ability to better balance your workloads, scale specific parts of an app, and create microservices that work together. -->

<!-- At times, users may choose to partition (shard). With federation capabilities, data can be queried with a unified interface and this lets the user better balance the workload, scale specific parts of an app or create microservices that work together. -->

### Aumentar la capacidad de la base de datos por encima de los límites fijados

La federación le ofrece la posibilidad de aumentar la capacidad de una base de datos local, mediante la federación con una base de datos en la nube. En este caso, la virtualización de datos constituye una excelente opción si la base de datos local se queda sin almacenamiento. El hecho de aumentar la capacidad de una base de datos mediante federación resulta útil para nuevos desarrollos ya que los desarrolladores no tienen que modificar una base de datos que ya esté en producción. También puede federar dos bases de datos {{site.data.keyword.dashdbshort_notm}} para aumentar la capacidad de las bases de datos por encima de los límites actuales del plan Flex.

<!-- By using federation, users can increase capacity of an on premises database by federating to or from the cloud. This is a great option if your on premises database is running out of storage. Increased capacity will also be useful for new development as our users no longer need to change a database in production. You can also use this feature to federate between two Db2 on Cloud databases to increase the capacity beyond the current limits of the Flex plan. -->

## Cómo empezar
{: #gtng_strtd}

En los pasos siguientes se muestra un ejemplo del proceso de federar orígenes de datos dispares para que parezca que los datos se recuperan de un solo origen. En el siguiente ejemplo se muestra la federación de dos bases de datos {{site.data.keyword.dashdbshort_notm}}:

### En la máquina de destino de Db2 Warehouse on Cloud
{: #targ}

Nombre de host: targetdotcom

1. Cree una tabla `testdata` en el esquema `admin2`.

2. En la consola de {{site.data.keyword.dashdbshort_notm}}, cargue la tabla `testdata` con los datos como usuario `admin2` con la contraseña `YYYY`.

### En una máquina de Db2 Warehouse on Cloud utilizada como origen de federación
{: #fed_src}

Desde la consola de {{site.data.keyword.dashdbshort_notm}}:

<!-- 1. Catalog the target machine:<br/>
   `db2 catalog tcpip node <node_name> remote <host_name> server 50000`<br/>

   For example:<br/>
   `db2 catalog tcpip node fedS remote targetdotcom server 50000`

2. Catalog the database on fedS:<br/>
   `db2 catalog db bludb as <db_name> at node <node_name>`

   For example:<br/>
   `db2 catalog db bludb as srcdb at node fedS`

3. Connect to the database on fedS:<br/>
   `db2 connect to <catalog_db_name> user <admin_user> using '<admin_password>'`

   For example:<br/>
   `db2 connect to srcdb user 'admin1' with password 'XXXX'`

4. Create a wrapper on fedS:<br/>
   `db2 "create wrapper drda"` -->

1. Cree un servidor para comunicar con la máquina de destino:<br/>
   `create server <server_name> type dashdb version 11 wrapper drda authorization "<admin_user_on_target>" password "<admin_password_on_target>" options (host '<target_host_name>', port '50000', dbname 'bludb')`

   Por ejemplo:<br/>
   `create server db2server type dashdb version 11 wrapper drda authorization "admin2" password "YYYY" options (host 'targetdotcom', port '50000', dbname 'bludb')`

2. Cree una correlación de usuario para admin2:<br/>
   `create user mapping for <admin_user> server db2server options (remote_authid '<admin_user_on_target>', remote_password '<admin_password_on_target>')`

   Por ejemplo:<br/>
   `create user mapping for admin1 server db2server options (remote_authid 'admin2', remote_password 'YYYY')`

3. Cree un apodo para la base de datos:<br/>
   `create nickname <nickname> for <server_name>.<schema_name>.<table_name>`

   Por ejemplo:<br/>
   `create nickname ntest1 for db2server.admin2.testdata`

4. Pruebe que puede extraer datos del servidor de destino:<br/>
   `select * from <nickname>`

   Por ejemplo:<br/>
   `select * from ntest1`

## Información adicional

Para obtener más información sobre la virtualización de datos (federación), consulte: [Federación](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/fcontainer.html){:external}.

Para obtener información sobre los orígenes de datos que reciben soporte de la federación, consulte: [Orígenes de datos admitidos por la federación](https://www.ibm.com/support/docview.wss?uid=swg27050561){:external}.
