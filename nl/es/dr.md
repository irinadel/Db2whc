---

copyright:
  years: 2014, 2019
lastupdated: "2019-04-16"

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

# Recuperación tras desastre (DR)
{: #dr}

<!-- If your data warehouse instance is deployed in a data center that suffers a significant data center outage with an expected downtime of more than 8 hours, you will be sent a request to allow service operators to fail over your instance to another data center before disaster recovery actions can begin.
{: shortdesc}

A Db2 backup of your database is done every day, except for the Flex plan where a Db2 backup is done every 7 days and a snapshot backup is done daily. Daily backups are stored in the IBM Cloud Object Storage service from which it is replicated to multiple availability zones. If something should happen to your primary data center, our service operators will work with you to stand up your recovered database in a secondary data center. -->

La estrategia de recuperación tras desastre depende del tipo de plan y de la generación de depósito de datos que ejecute.
{: shortdesc}

Para planes de tipo SMP pequeño, mediano, grande y MPP pequeño de primera generación, se realiza una copia de seguridad una vez al día y se despliega en el servicio {{site.data.keyword.Bluemix_notm}} Object Storage. Desde ahí, la copia de seguridad se duplica en varias zonas de disponibilidad. Si se produce un suceso desastroso en el centro de datos principal, nuestros operadores de servicio trabajarán con usted para generar un nuevo depósito de datos en otro centro de datos. Utilizaremos la copia de seguridad diaria que reside en el servicio {{site.data.keyword.Bluemix_notm}} Object Storage.

En el caso de los planes Flex de segunda generación de {{site.data.keyword.Bluemix_notm}}, se realiza una copia de seguridad una vez por semana y se despliega en el servicio {{site.data.keyword.Bluemix_notm}} Object Storage. Desde ahí, la copia de seguridad se duplica en varias zonas de disponibilidad. Si se produce un suceso desastroso en el centro de datos principal, nuestros operadores de servicio trabajarán con usted para generar un nuevo depósito de datos en otro centro de datos. Utilizaremos la copia de seguridad semanal que reside en el servicio {{site.data.keyword.Bluemix_notm}} Object Storage.

En el caso de planes Flex de segunda generación en Amazon Web Services, se descarga automáticamente una copia de seguridad diaria de autoservicio en AWS S3. Si está en S3, la copia de seguridad se duplica en varias regiones. Si se produce un suceso desastroso, se utiliza la copia de seguridad más reciente para restaurar el clúster en un centro de datos secundario.

## **Brasil: Regla complementaria 14** (se aplica a sistema suministrado para el gobierno federal brasileño)
{: #rule_14}

En este momento, la opción de recuperación tras desastre (DR) para las ofertas de {{site.data.keyword.dashdbshort_notm}} no está disponible en Brasil para el gobierno federal debido a la regla complementaria 14.

