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

# Alta disponibilidade (HA): plano MPP
{: #ha_smp_mpp}

O cluster do plano MPP do {{site.data.keyword.dashdblong}} é provisionado com alta
disponibilidade.  
{: shortdesc}

Quando um nó ficar inativo para um plano MPP, o componente de HA reiniciará suas partições de banco de dados nos nós
em funcionamento restantes. Um curto tempo de inatividade ocorre durante essa fase. 

Após o nó ser incluído de volta no cluster, o mecanismo do banco de dados deve ser reiniciado para ser executado em capacidade
total. 

