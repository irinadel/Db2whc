---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-16"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Alta disponibilidad (HA): plan MPP
{: #ha_smp_mpp}

El clúster del plan MPP {{site.data.keyword.dashdblong}} está suministrado con alta disponibilidad.  
{: shortdesc}

Cuando un nodo cae en un plan MPP, el componente HA reinicia su base de datos en los nodos en buen estado restantes. Se produce un tiempo de inactividad breve durante esta fase. 

Después de que se vuelva a añadir un nodo a un clúster, el motor de la base de datos debe reiniciarse para ejecutarlo en su capacidad total. 

