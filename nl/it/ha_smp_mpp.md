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

# Elevata disponibilità (HA): piano MPP
{: #ha_smp_mpp}

Il cluster del piano {{site.data.keyword.dashdblong}} MPP viene fornito con l'elevata disponibilità.  
{: shortdesc}

Quando un nodo si arresta per un piano MPP, il componente HA riavvia le tue partizioni del database in altri nodi integri rimanenti. Si verifica un breve tempo di inattività durante questa fase. 

Dopo che il nodo è stato aggiunto al cluster, il motore del database deve essere riavviato per essere eseguito alla sua capacità completa. 

