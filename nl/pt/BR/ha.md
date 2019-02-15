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

# Alta disponibilidade (HA) 
{: #ha}

A medida de uma solução de banco de dados bem-sucedida é a disponibilidade. O {{site.data.keyword.dashdblong}} tem planos altamente disponíveis para manter suas cargas de trabalho funcionando.
{: shortdesc}

## Plano MPP
{: #ha_mpp}

O cluster do plano MPP do {{site.data.keyword.dashdbshort_notm}} é provisionado com alta
disponibilidade.  

Quando um nó ficar inativo para um plano MPP, o componente de HA reiniciará suas partições de banco de dados nos nós
em funcionamento restantes. Um curto tempo de inatividade ocorre durante essa fase. 

Após o nó ser incluído de volta no cluster, o mecanismo do banco de dados deve ser reiniciado para ser executado em capacidade
total. 

## Plano Flex Performance
{: #ha_flex}

Se ocorrer uma falha de nó inesperada, o cluster do Flex Performance MPP será recuperado para capacidade total após um curto
tempo de inatividade devido ao uso do IBM Container Service (baseado no Kubernetes). Nós de um conjunto são usados para mover as
entidades do nó com falha. 

### HA de cálculo
{: #compute_ha}

Qualquer falha do nó é imediatamente detectada pelo serviço de contêiner. Os contêineres e os pods em execução no nó
com falha são planejados para um novo nó de um conjunto de nós. O sistema volta a 100% de operação normal após um curto
tempo de inatividade.

### HA de armazenamento
{: #storage_ha}

O armazenamento é configurado com uma implementação RAID6 de dupla paridade que fornece proteção contra falhas de
disco duplo no mesmo grupo RAID para alto desempenho e armazenamento altamente disponível para o seu sistema.

### HA de rede
{: #net_ha}

Conexões de rede são feitas altamente disponíveis provisionando seu serviço com uma placa da interface de rede redundante (NIC). 

Se o serviço de contêiner detectar um problema de rede, os pods e os contêineres poderão ser reiniciados automaticamente após um curto
tempo de inatividade.
