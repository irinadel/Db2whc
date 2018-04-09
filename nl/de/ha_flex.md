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

# Hochverfügbarkeit (High Availability, HA): Flex Performance-Plan
{: #ha_flex}

Tritt ein nicht erwarteter Knotenfehler auf, wird die vollständige Kapazität des Flex Performance-MPP-Clusters nach einer kurzen Ausfallzeit wiederhergestellt, indem IBM Container Service (auf der Basis von Kubernetes) eingesetzt wird. Es werden Knoten aus einem Pool verwendet, um die fehlgeschlagenen Knotenentitäten zu verlagern.
{: shortdesc}

## Hochverfügbarkeit für Prozessorresourcen
{: #compute_ha}

Knotenfehler werden sofort vom Container-Service festgestellt. Die Container und Pods, die auf dem fehlgeschlagenen Knoten ausgeführt wurden, werden auf einem anderen Knoten terminiert, der aus einem Knotenpool zugeordnet wird. Das System erreicht nach einer kurzen Ausfallzeit wieder 100 % seiner normalen Betriebsleistung. 

## Hochverfügbarkeit für den Speicher
{: #storage_ha}

Der Speicher ist mit einer Dual-Parity-RAID6-Implementierung konfiguriert, die Schutz bei doppelten Datenträgerausfällen in derselben RAID-Gruppe und damit hohe Leistung und hohe Speicherverfügbarkeit für das System bietet.


## Hochverfügbarkeit für das Netz
{: #net_ha}

Die Hochverfügbarkeit von Netzverbindungen wird ermöglicht, indem der Service mit einer redundanten NIC (Network Interface Card, Netzschnittstellenkarte) ausgestattet wird. 

Wenn der Container-Service ein Netzproblem feststellt, können Pods und Container nach einer kurzen Ausfallzeit automatisch erneut gestartet werden.
