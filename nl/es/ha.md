---

copyright:
  years: 2014, 2019
lastupdated: "2018-04-30"

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

# Alta disponibilidad (HA) 
{: #ha}

La medida de una solución de base de datos satisfactoria es su disponibilidad. {{site.data.keyword.dashdblong}} tiene planes altamente disponibles para hacer que sus cargas de trabajo continúen.
{: shortdesc}

## Plan MPP
{: #ha_mpp}

El clúster del plan MPP {{site.data.keyword.dashdbshort_notm}} está suministrado con alta disponibilidad.  

Cuando un nodo cae en un plan MPP, el componente HA reinicia su base de datos en los nodos en buen estado restantes. Se produce un tiempo de inactividad breve durante esta fase. 

Después de que se vuelva a añadir un nodo a un clúster, el motor de la base de datos debe reiniciarse para ejecutarlo en su capacidad total. 

## Plan Flex Performance
{: #ha_flex}

Si se produce un error inesperado del nodo, su clúster Flex Performance MPP vuelve a la capacidad completa después de un tiempo de inactividad breve debido al uso de IBM Container Service (basado en Kubernetes). Los nodos de una agrupación se utilizan para mover las entidades del nodo que han fallado. 

### Calcular HA
{: #compute_ha}

El servicio de contenedor detecta los errores de nodo inmediatamente. Los contenedores y pods que se han ejecutado en el nodo erróneo se programan para un nuevo nodo de una agrupación de nodos. El sistema vuelve al funcionamiento 100% normal después de un tiempo de inactividad breve.

### Almacenamiento de HA
{: #storage_ha}

Su almacenamiento se configura con una implementación de paridad dual RAID6 que proporciona protección contra fallos de disco doble en el mismo grupo de RAID para un alto rendimiento y un almacenamiento de alta disponibilidad en su sistema.

### Red HA
{: #net_ha}

Las conexiones de red se hacen altamente disponibles al suministrar su servicio con una tarjeta de interfaz de red (NIC) redundante. 

Si el servicio del contenedor detecta un problema de red, los pods y contenedores pueden reiniciarse automáticamente después de un tiempo de inactividad breve.
