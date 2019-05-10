---

copyright:
  years: 2014, 2019
lastupdated: "2019-04-16"

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

# Recuperação de desastre (DR)
{: #dr}

<!-- If your data warehouse instance is deployed in a data center that suffers a significant data center outage with an expected downtime of more than 8 hours, you will be sent a request to allow service operators to fail over your instance to another data center before disaster recovery actions can begin.
{: shortdesc}

A Db2 backup of your database is done every day, except for the Flex plan where a Db2 backup is done every 7 days and a snapshot backup is done daily. Daily backups are stored in the IBM Cloud Object Storage service from which it is replicated to multiple availability zones. If something should happen to your primary data center, our service operators will work with you to stand up your recovered database in a secondary data center. -->

A estratégia de recuperação de desastre depende do tipo de plano e da geração do data warehouse que você está executando atualmente.
{: shortdesc}

Para os planos SMP Small, Medium, Large e MPP Small de primeira geração, um backup é feito uma vez por dia e implementado no serviço {{site.data.keyword.Bluemix_notm}} Object Storage. A partir daí, o backup é replicado para várias zonas de disponibilidade. Se um evento de desastre ocorrer no data center principal, nossos operadores de serviço trabalharão com você para criar um novo data warehouse em um data center diferente. Usaremos o backup diário que reside no serviço do {{site.data.keyword.Bluemix_notm}} Object Storage.

Para os planos Flex de segunda geração no {{site.data.keyword.Bluemix_notm}}, um backup é feito uma vez por semana e implementado no serviço {{site.data.keyword.Bluemix_notm}} Object Storage. A partir daí, o backup é replicado para várias zonas de disponibilidade. Se um evento de desastre ocorrer no data center principal, nossos operadores de serviço trabalharão com você para criar um novo data warehouse em um data center diferente. Usaremos o backup semanal que reside no serviço {{site.data.keyword.Bluemix_notm}} Object Storage.

Para os planos Flex de segunda geração no Amazon Web Services, um backup de autoatendimento diário é transferido automaticamente para o AWS S3. Quando no S3, o backup é replicado para múltiplas regiões. Se ocorrer um evento de desastre, o backup mais recente será usado para restaurar seu cluster para um data center secundário.

## **Brasil: Regra complementar 14** (aplica-se a sistemas provisionados para o governo federal brasileiro)
{: #rule_14}

Neste momento, a opção de recuperação de desastre (DR) para as ofertas do {{site.data.keyword.dashdbshort_notm}} não está disponível no Brasil para o governo federal devido à Regra Complementar 14.

