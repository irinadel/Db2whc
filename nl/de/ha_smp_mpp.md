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

# Hochverfügbarkeit (High Availability, HA): MPP-Plan
{: #ha_smp_mpp}

Der Cluster im Rahmen des {{site.data.keyword.dashdblong}} MPP-Plans wird mit Hochverfügbarkeit bereitgestellt.  
{: shortdesc}

Wenn bei der Verwendung eines MPP-Plans ein Knoten ausfällt, startet die Hochverfügbarkeitskomponente die Datenbankpartitionen mit den übrigen funktionsfähigen Knoten. Während dieser Phase kommt es zu einer kurzen Ausfallzeit. 

Sobald der Knoten wieder zum Cluster hinzugefügt wird, muss die Datenbankengine neu gestartet werden, damit sie mit der vollen Kapazität ausgeführt werden kann. 

