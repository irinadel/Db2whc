---

copyright:
  years: 2014, 2019
lastupdated: "2018-12-07"

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

Vea todos los planes de {{site.data.keyword.dashdbshort_notm}} disponibles en el [catálogo de {{site.data.keyword.Bluemix}}](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window}.
<!--   * Plans configured for data warehouse and online analytical processing (OLAP) workloads: [{{site.data.keyword.dashdbshort_notm}}](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window} -->
<!--   * Plans configured for high-speed, transactional processing (OLTP): [{{site.data.keyword.dashdbshort_notm}} for Transactions](https://console.ng.bluemix.net/catalog/services/dashdb-for-transactions-sql-database){:new_window} -->

Vea este vídeo para ver una introducción al plan Flex Performance de {{site.data.keyword.dashdbshort_notm}}.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Creación de una conexión desde Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

Puede solicitar que se despliegue su servicio de {{site.data.keyword.dashdbshort_notm}} en un entorno con aislamiento de red en {{site.data.keyword.Bluemix}}. Póngase en contacto con [Ventas de {{site.data.keyword.IBM_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window}.

Si no ve una configuración en el catálogo que necesita, [póngase en contacto con el representante de ventas de {{site.data.keyword.IBM_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window} para hablar sobre otras opciones.

## Disponibilidad de planes en centros de datos
{: #availability}

En la tabla siguiente se proporciona información sobre la disponibilidad de los distintos planes {{site.data.keyword.dashdbshort_notm}} por centros de datos ubicados en regiones geográficas:


| planes {{site.data.keyword.dashdbshort_notm}} | Asia/Pacífico | Europa    | América del Norte/Centroamérica     | América del Sur |
|------------------------------|--------------|-----------|-----------------------    |---------------|
| Flex                         | *NA          | Frankfurt | Washington D.C. (us-east) | *NA           |
|                              |              |           | Dallas (us-south)         |               |  
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
{: caption="Tabla 1. Centros de datos que admiten los planes de servicio de Db2 Warehouse on Cloud" caption-side="top"}

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
| Características y funciones | Federación | No soportada |
|  | Compatibilidad con Oracle | No soportada |
|  | Extensiones definidas por el usuario (UDF) | No soportadas |
|  | Gestión de usuarios | Al usuario no se le da autoridad administrativa |
|  | Control de acceso a filas y columnas (RCAC) | No soportado |
|  | IBM InfoSphere Data Replication para uso en la carga de datos | No soportado |
|  |  |
| Entorno de red | IBM Cloud Integrated Analytics | No soportado |
|  | IBM Cloud Dedicated | No soportado |
|  |  |
| Conformidades de seguridad | Health Insurance Portability and Accountability Act de 1996 (HIPAA) | No soportada. Consulte la descripción de servicio. |
|  | Reglamento general de protección de datos de la Unión Europea (GDPR) | No se aplican restricciones específicas |
|  |  |
| Gestión de la cuenta | Reactivación | No hay requisitos de reactivación |
{: caption="Tabla 1. {{site.data.keyword.dashdbshort_notm}} Restricciones del plan de Entrada" caption-side="top"}
