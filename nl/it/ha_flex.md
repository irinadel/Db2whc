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

# Elevata disponibilità (HA): piano Flex Performance
{: #ha_flex}

Se si verifica un malfunzionamento non previsto con il nodo, il tuo cluster Flex Performance MPP viene riportato alla capacità completa dopo un breve tempo di inattività dovuto all'utilizzo del servizio IBM Container (basato su Kubernetes). I nodi da un pool sono utilizzati per spostare le entità del nodo in errore.
{: shortdesc}

## Calcolo HA
{: #compute_ha}

Qualsiasi errore del nodo viene immediatamente individuato dal servizio del contenitore. I contenitori e i pod che sono in esecuzione nel nodo in errore vengono pianificati in un nuovo nodo da un pool di nodi. Il sistema torna all'operatività normale del 100% dopo un breve tempo di inattività.

## Archiviazione HA
{: #storage_ha}

La tua archiviazione viene configurata con un'implementazione RAID6 a doppia parità che fornisce protezione contro doppi errori disco nello stesso gruppo di RAID per elevate prestazioni e l'archiviazione altamente disponibile del tuo sistema.

## Rete HA
{: #net_ha}

Le connessioni di rete sono rese altamente disponibili fornendo al tuo servizio una NIC (network interface card) ridondante. 

Se il servizio contenitore rileva un problema di rete, i pod e i contenitori possono riavviarsi automaticamente dopo un breve tempo di inattività. 
