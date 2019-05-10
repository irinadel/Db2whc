---

copyright:
  years: 2014, 2019
lastupdated: "2019-03-15"

keywords:

subcollection: Db2whc

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

# Planos e configurações
{: #plans_cfgs}

É possível escolher um plano {{site.data.keyword.dashdbshort_notm}} que esteja configurado e otimizado para o trabalho que você precise fazer:
{: shortdesc}

   * Um plano de entrada para experimentar as coisas. É uma avaliação grátis com até 1 GB de armazenamento. Consulte: [Restrições de plano de entrada](#ep_restrictions)
   * Planos Flex nos quais é possível escalar de forma independente os recursos de armazenamento e de cálculo
   * Os planos SMP de vários tamanhos para produção: pequeno, médio e grande consistem em um único nó e uma única instância
   * Configurações de cluster com múltiplos nós MPP para processamento paralelo e alto desempenho
   * Planos configurados para Alta Disponibilidade
   * Compatibilidade do Oracle

Visualize todos os planos do {{site.data.keyword.dashdbshort_notm}} no [Catálogo do {{site.data.keyword.Bluemix}}](https://cloud.ibm.com/catalog/services/db2-warehouse){:new_window}.
<!--   * Plans configured for data warehouse and online analytical processing (OLAP) workloads: [{{site.data.keyword.dashdbshort_notm}}](https://console.bluemix.net/catalog/services/db2-warehouse){:new_window} -->
<!--   * Plans configured for high-speed, transactional processing (OLTP): [{{site.data.keyword.dashdbshort_notm}} for Transactions](https://console.ng.bluemix.net/catalog/services/dashdb-for-transactions-sql-database){:new_window} -->

Assista a este vídeo para ver uma introdução ao plano de Desempenho do {{site.data.keyword.dashdbshort_notm}} Flex.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Criando uma conexão por meio do Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/59PKSnzNQAg?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

É possível solicitar que o serviço do {{site.data.keyword.dashdbshort_notm}} seja implementado em um ambiente isolado por
rede no {{site.data.keyword.Bluemix}}. Entre em contato com o [{{site.data.keyword.IBM_notm}} Sales ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window}.

Caso você não veja no catálogo uma configuração da qual precisa, entre em contato com [Vendas do {{site.data.keyword.IBM_notm}}![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window} para discutir outras opções.

## Disponibilidade de Planos em Datacenters
{: #availability}

A tabela a seguir fornece informações sobre a disponibilidade dos vários planos do {{site.data.keyword.dashdbshort_notm}} pelos data centers localizados nas regiões geográficas:

| Planos do {{site.data.keyword.dashdbshort_notm}} | Ásia / Pacífico | Europa    | América do Norte / Central     | América do Sul |
|------------------------------|--------------|-----------|---------------------------|---------------|
| Flex                         | Tokyo        | Frankfurt | Washington D.C. (us-leste) | *NA           |
|                              |              |           | Dallas (us-sul)         |               |  
|      |||||
| SMP                          | Hong Kong    | Amsterdã | Washington D.C. (us-leste) | São Paulo     |
|                              | Seoul        | Frankfurt | Dallas (us-sul)         |               | 
|                              | Cingapura    | Londres    | Montréal                  |               | 
|                              | Sydney       | Milão     | Querétaro                 |               | 
|                              | Tokyo        | Oslo.      | Toronto                   |               | 
|                              |              | Paris     |                           |               |
|      |||||
| MPP                          | Hong Kong    | Amsterdã | Washington D.C. (us-leste) | São Paulo     |
|                              | Seoul        | Frankfurt | Dallas (us-sul)         |               | 
|                              | Cingapura    | Londres    | Montréal                  |               | 
|                              | Sydney       | Milão     | Querétaro                 |               | 
|                              | Tokyo        | Oslo.      | Toronto                   |               | 
|                              |              | Paris     |                           |               |
{: caption="Tabela 1. Data centers que suportam planos de serviço do Db2 Warehouse on Cloud" caption-side="top"}

*NA = Não disponível neste momento

## Restrições do plano de entrada
{: #ep_restrictions}

É altamente recomendável usar um plano de serviço de nível corporativo em vez de um plano de serviço de entrada para cargas de trabalho essenciais e sensíveis ao desempenho. 
{: important}

A seguir está uma tabela de {{site.data.keyword.dashdbshort_notm}} Restrições de plano de entrada:

| Categoria | Item | Restrição | 
|----------|------|-------------|
| Recursos | Storage | 20 GB de armazenamento por usuário. O plano é grátis somente se menos de 1 GB de armazenamento é usado. |
|  | Conexões | 50 conexões por usuário. Esse limite pode ser ajustado dinamicamente para manter a integridade do sistema da instância. |
|  | Desempenho | O desempenho pode flutuar devido a cargas de trabalho executadas por outros usuários no sistema de diversos locatários |
|  |  |
| Recursos e funções | Federação | Não suportado |
|  | Compatibilidade do Oracle | Não suportado |
|  | Extensões definidas pelo usuário (UDFs) | Não suportado |
|  | Gerenciamento de usuários | Usuário que não tem autoridade administrativa |
|  | Row and Column Access Control (RCAC) | Não suportado |
|  | IBM InfoSphere Data Replication para uso no carregamento de dados | Não suportado |
|  |  |
| Ambiente de rede | IBM Cloud Integrated Analytics | Não suportado |
|  | IBM Cloud Dedicado | Não suportado |
|  |  |
| Conformidades de segurança | Health Information Portability and Accountability Act de 1996 (HIPAA) | Não suportada. Consulte a descrição do serviço. |
|  | Regulamento Geral sobre a Proteção de Dados (GDPR) da UE | Nenhuma restrição específica se aplica |
|  |  |
| Gerenciamento de conta | Reativação | Nenhum requisito de reativação |
{: caption="Tabela 1. {{site.data.keyword.dashdbshort_notm}} Restrições de plano de entrada" caption-side="top"}
