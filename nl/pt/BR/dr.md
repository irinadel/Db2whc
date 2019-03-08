---

copyright:
  years: 2014, 2019
lastupdated: "2018-11-21"

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

Se a instância do data warehouse for implementada em um data center que sofrer uma indisponibilidade significativa do data center com um tempo de inatividade esperado de mais de 8 horas, será enviada uma solicitação para permitir que os operadores de serviço executem failover da sua instância em outro data center antes que as ações de recuperação de desastre possam começar.
{: shortdesc}

É feito um backup do Db2 de seu banco de dados todos os dias, exceto para o plano Flex, em que um backup do Db2 é feito a cada sete dias e um backup de captura instantânea é feito diariamente. Backups diários são armazenados no serviço IBM Cloud Object Storage por meio do qual é replicado para múltiplas zonas de disponibilidade. Se algo acontecer ao data center primário, nossos operadores de serviço trabalharão com você para colocar seu banco de dados recuperado em um data center secundário.

## **Brasil: Regra complementar 14** (aplica-se a sistemas provisionados para o governo federal brasileiro)
{: #rule_14}

Neste momento, a opção de recuperação de desastre (DR) para as ofertas do Db2 Warehouse on Cloud não está disponível no Brasil para o governo federal devido à Regra complementar 14.

