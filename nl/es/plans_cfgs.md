---

copyright:
  years: 2014, 2019
lastupdated: "2019-06-05"

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

# Planes y configuraciones
{: #plans_cfgs}

Puede elegir un plan {{site.data.keyword.dashdbshort_notm}} que está configurado y optimizado para el trabajo que necesita realizar:
{: shortdesc}

   * Un plan de entrada para realizar pruebas. Es una prueba gratuita con hasta 1 GB de almacenamiento. Consulte: [Restricciones del plan de Entrada](#ep_restrictions)
   * Planes Flex en los que puede escalar el almacenamiento y recursos de cálculo de forma independiente
   * Planes de SMP de varios tamaños para la producción: pequeño, mediano y grande constan de un único nodo y de una instancia única
   * Configuraciones de clúster de varios nodos de MPP para un proceso paralelo y un alto rendimiento
   * Planes configurados para la Alta disponibilidad
   * Compatibilidad con Oracle

Consulte todos los planes de {{site.data.keyword.dashdbshort_notm}} disponibles en el [catálogo de {{site.data.keyword.Bluemix}}](https://cloud.ibm.com/catalog/services/db2-warehouse){:external}.
<!--   * Plans configured for data warehouse and online analytical processing (OLAP) workloads: [{{site.data.keyword.dashdbshort_notm}}](https://console.bluemix.net/catalog/services/db2-warehouse){:external} -->
<!--   * Plans configured for high-speed, transactional processing (OLTP): [{{site.data.keyword.dashdbshort_notm}} for Transactions](https://console.ng.bluemix.net/catalog/services/dashdb-for-transactions-sql-database){:external} -->

Vea este vídeo para ver una introducción al plan Flex Performance de {{site.data.keyword.dashdbshort_notm}}.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Creación de una conexión desde Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

Puede solicitar que se despliegue su servicio de {{site.data.keyword.dashdbshort_notm}} en un entorno con aislamiento de red en {{site.data.keyword.Bluemix}}. Póngase en contacto con el departamento de [Ventas de {{site.data.keyword.IBM_notm}}](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:external}.

Si en el catálogo no ve la configuración que necesita, póngase en contacto con el [equipo de ventas de {{site.data.keyword.IBM_notm}}](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:external} para considerar otras opciones.

## Disponibilidad de planes en centros de datos IBM Cloud
{: #availability}

En la tabla siguiente se proporciona información sobre la disponibilidad de los distintos planes {{site.data.keyword.dashdbshort_notm}} por centros de datos IBM Cloud ubicados en regiones geográficas:

| planes {{site.data.keyword.dashdbshort_notm}} | Asia/Pacífico | Europa    | América del Norte/Centroamérica     | América del Sur |
|------------------------------|--------------|-----------|---------------------------|---------------|
| Flex / Rendimiento Flex      | Tokio        | Frankfurt | Washington D.C. (us-east) | *ND           |
|                              |              |           | Dallas (us-south)         |               |  
|      |||||
| Flex One                     | *ND          | *ND       | Dallas (us-south)         | *ND           |
|      |||||
| SMP                          | Hong Kong    | Ámsterdam | Washington D.C. (us-east) | São Paulo     |
|                              | Seúl        | Frankfurt | Dallas (us-south)         |               | 
|                              | Singapur    | Londres    | Montreal                  |               | 
|                              | Sídney       | Milán     | Querétaro                 |               | 
|                              | Tokio        | Oslo      | Toronto                   |               | 
|                              |              | París     |                           |               |
|      |||||
| MPP                          | Hong Kong    | Ámsterdam | Washington D.C. (us-east) | São Paulo     |
|                              | Seúl        | Frankfurt | Dallas (us-south)         |               | 
|                              | Singapur    | Londres    | Montreal                  |               | 
|                              | Sídney       | Milán     | Querétaro                 |               | 
|                              | Tokio        | Oslo      | Toronto                   |               | 
|                              |              | París     |                           |               |
{: caption="Tabla 1. Centros de datos IBM Cloud que admiten los planes de servicio de Db2 Warehouse on Cloud" caption-side="top"}

*NA = No disponible actualmente

## Disponibilidad de planes en centros de datos de Servicios web de Amazon
{: #availability_aws}

En la tabla siguiente se proporciona información sobre la disponibilidad de los distintos planes {{site.data.keyword.dashdbshort_notm}} por centros de datos de Servicios web de Amazon ubicados en regiones geográficas:

| planes {{site.data.keyword.dashdbshort_notm}} | Asia/Pacífico | Europa    | América del Norte/Centroamérica     | América del Sur |
|------------------------------|--------------|-----------|---------------------------|---------------|
| Flex                         | Sídney       | Frankfurt | N. Virginia | *ND           |
|                              | Singapur    | Londres    |             |               |  
|      |||||
| Flex Performance             | Sídney       | Frankfurt | N. Virginia | *ND           |
|                              | Singapur    | Londres    |             |               | 
{: caption="Tabla 2. Centros de datos de Servicios web de Amazon que admiten los planes de servicio de Db2 Warehouse on Cloud" caption-side="top"}

*NA = No disponible actualmente


## Restricciones del plan de Entrada
{: #ep_restrictions}

Se recomienda encarecidamente utilizar un plan de servicio de nivel de empresa en lugar de un plan de servicio de Entrada para cargas de trabajo de misión crítica o sensibles al rendimiento. 
{: important}

La siguiente tabla muestra las restricciones del plan de Entrada de {{site.data.keyword.dashdbshort_notm}}:

| Categoría | Elemento | Restricción | 
|----------|------|-------------|
| Recursos | Almacenamiento | 20 GB de almacenamiento por usuario. El plan es gratuito solamente si se usa menos de 1 GB de almacenamiento. |
|  | Conexiones | 50 conexiones por usuario. Es posible que este límite se ajuste dinámicamente para mantener la integridad de sistema de la instancia. |
|  | Rendimiento | Es posible que el rendimiento fluctúe debido a cargas de trabajo ejecutadas por otros usuarios del sistema multiarrendatario. |
|  |  |
| Características y funciones | Federación | No soportado |
|  | Compatibilidad con Oracle | No soportado |
|  | Extensiones definidas por el usuario (UDF) | No soportado |
|  | Gestión de usuarios | Al usuario no se le da autoridad administrativa |
|  | Control de acceso a filas y columnas (RCAC) | No soportado |
|  | IBM InfoSphere Data Replication para uso en la carga de datos | No soportado |
|  |  |
| Entorno de red | IBM Cloud Integrated Analytics | No soportado |
|  | IBM Cloud Dedicated | No soportado |
|  |  |
| Conformidad de seguridad | Health Insurance Portability and Accountability Act de 1996 (HIPAA) | No soportada. Consulte la descripción de servicio. |
|  | Reglamento general de protección de datos de la Unión Europea (GDPR) | No se aplican restricciones específicas |
|  |  |
| Gestión de la cuenta | Reactivación | No hay requisitos de reactivación |
{: caption="Tabla 3. {{site.data.keyword.dashdbshort_notm}} Restricciones del plan de Entrada" caption-side="top"}
