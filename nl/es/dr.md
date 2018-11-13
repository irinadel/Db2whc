---

copyright:
  years: 2014, 2018
lastupdated: "2018-10-22"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}

# Recuperación ante siniestro (DR)
{: #dr}

Si la instancia de depósito de datos se despliega en un centro de datos que sufre una parada significativa en el centro de datos con un tiempo de inactividad esperado de más de 8 horas, se le enviará una solicitud para permitir a los operadores de servicio migrar tras error la instancia a otro centro de datos antes de que puedan empezar las acciones de recuperación en caso de error.
{: shortdesc}

Se realiza una copia de seguridad de Db2 de la base de datos cada día. Las copias de seguridad diarias se almacenan en el servicio IBM Cloud Object Storage a partir del que se replica a varias zonas de disponibilidad. Si le ocurre algo a su centro de datos primario, nuestros operadores de servicio trabajarán con usted para que pueda configurar su base de datos recuperada en un centro de datos secundario.

## **Brasil: Regla complementaria 14** (se aplica a sistema suministrado para el gobierno federal brasileño)
{: #rule_14}

En este momento, la opción de recuperación tras desastre (DR) para las ofertas de Db2 Warehouse on Cloud no está disponible en Brasil para el gobierno federal debido a la regla complementaria 14.

