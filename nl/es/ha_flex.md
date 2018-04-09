---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-15"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Alta disponibilidad (HA): plan Flex Performance
{: #ha_flex}

Si se produce un error inesperado del nodo, su clúster Flex Performance MPP vuelve a la capacidad completa después de un tiempo de inactividad breve debido al uso de IBM Container Service (basado en Kubernetes). Los nodos de una agrupación se utilizan para mover las entidades del nodo que han fallado. 
{: shortdesc}

## Calcular HA
{: #compute_ha}

El servicio de contenedor detecta los errores de nodo inmediatamente. Los contenedores y pods que se han ejecutado en el nodo erróneo se programan para un nuevo nodo de una agrupación de nodos. El sistema vuelve al funcionamiento 100% normal después de un tiempo de inactividad breve.

## Almacenamiento de HA
{: #storage_ha}

Su almacenamiento se configura con una implementación de paridad dual RAID6 que proporciona protección contra fallos de disco doble en el mismo grupo de RAID para un alto rendimiento y un almacenamiento de alta disponibilidad en su sistema.

## Red HA
{: #net_ha}

Las conexiones de red se hacen altamente disponibles al suministrar su servicio con una tarjeta de interfaz de red (NIC) redundante. 

Si el servicio del contenedor detecta un problema de red, los pods y contenedores pueden reiniciarse automáticamente después de un tiempo de inactividad breve.
