---

copyright:
  years: 2014, 2018
lastupdated: "2017-07-27"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Sobre o Db2 Warehouse on Cloud
{: #overview}

Nos planos de serviço do {{site.data.keyword.dashdblong}}, use o data warehouse para armazenar dados relacionais, incluindo tipos especiais. Analise seus próprios dados ou os dados carregados de outros serviços de nuvem, usando nossa analítica integrada ou ao conectar seus próprios aplicativos. É possível alavancar a tecnologia de banco de dados na memória de alto desempenho com tabelas com colunas para cargas de trabalho analíticas. O console da web do {{site.data.keyword.dashdbshort_notm}} manipula tarefas de gerenciamento de dados comuns, como carregamento de dados e tarefas de análise, como execução de consultas e scripts R.
{: shortdesc}

Também é possível conectar ferramentas e aplicativos externos ao {{site.data.keyword.dashdbshort_notm}} e utilizá-los para gerenciar ou analisar ainda mais os dados. Por exemplo:
   * Conecte o {{site.data.keyword.IBM_notm}} InfoSphere® Data Architect para projetar e implementar seu esquema do banco de dados.
<!--   * Connect Esri ArcGIS to perform geospatial analytics and map publishing with your data. -->
   * Conecte um servidor {{site.data.keyword.IBM_notm}} Cognos® para executar relatórios do Cognos em relação aos seus dados.
   * Conecte ferramentas baseadas em SQL, como Tableau, Microstrategy ou Microsoft Excel, para manipular ou analisar seus dados.
   * Conecte seus aplicativos {{site.data.keyword.Bluemix_short}} que precisam de um banco de dados de análise.
   * Conecte o Aginity Workbench para migrar dados e modelos de dados do Netezza® para o {{site.data.keyword.dashdbshort_notm}}.

## Serviço gerenciado do Db2 Warehouse on Cloud
{: #managed_service}

O serviço totalmente gerenciado do {{site.data.keyword.dashdbshort_notm}} manipula de todos os upgrades de software, atualizações de sistema operacional e manutenção de hardware. O serviço inclui monitoramento de funcionamento 24x7 do banco de dados e da infraestrutura. No caso de falha de hardware ou software, o serviço é reiniciado automaticamente.
{: shortdesc}

Para obter mais informações sobre os aspectos de serviço gerenciado do {{site.data.keyword.dashdbshort_notm}}, veja: [Serviço gerenciado do {{site.data.keyword.dashdbshort_notm}}![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/managed_service.html).

## Planos e configurações
{: #plans_cfgs}

É possível escolher um plano {{site.data.keyword.dashdbshort_notm}} que esteja configurado e otimizado para o trabalho que você precise fazer:
{: shortdesc}

   * Um plano de entrada para teste
   * Planos pequeno, médio e grande para produção
   * Configurações de MPP para processamento paralelo
   * Planos configurados para Alta disponibilidade ou para compatibilidade de Oracle
   * E muito mais...

Visualize planos disponíveis no catálogo do {{site.data.keyword.Bluemix}}:
   * Planos configurados para cargas de trabalho de data warehouse e analítica (OLAP): [{{site.data.keyword.dashdbshort_notm}}](https://console.bluemix.net/catalog/services/db2-warehouse-on-cloud?env_id=ibm:yp:us-south){:new_window}
<!--   * Plans configured for high-speed, transactional processing (OLTP): [{{site.data.keyword.dashdbshort_notm}} for Transactions](https://console.ng.bluemix.net/catalog/services/dashdb-for-transactions-sql-database){:new_window} -->

Caso você não veja no catálogo uma configuração da qual precisa, entre em contato com [Vendas do {{site.data.keyword.IBM_notm}}![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window} para discutir outras opções.

## Fornecimento do Db2 Warehouse on Cloud
{: #whse_provision}

O banco de dados {{site.data.keyword.dashdbshort_notm}} pode ser provisionado no {{site.data.keyword.BluSoftlayer_full}} e para AWS.
{: shortdesc}

Se você desejar que o data warehouse seja provisionado para o AWS, selecione o plano **MPP Small for AWS**.

<!-- If you want to have the data warehouse provisioned for AWS, select the **{{site.data.keyword.IBM_notm}} {{site.data.keyword.dashdbshort_notm}} for Analytics MPP Small for AWS** plan. -->

<!-- ##dashDB for Transactions
{: #dashDB_tr}

In the {{site.data.keyword.dashdbshort_notm}} for Transactions plans, use the {{site.data.keyword.dashdbshort_notm}} relational database for online transaction processing. You can connect new or existing applications, and you can begin processing transactions and storing your data. With DB2® and Oracle compatibility, you can connect small or large applications and benefit from a managed enterprise-class database system. You can leverage the {{site.data.keyword.dashdbshort_notm}} for Transactions web console to manage users, load data, and get connection information.
{: shortdesc} -->

<!-- ##dashDB web console overview
{: #console_overview}

You can manage your {{site.data.keyword.dashdbshort_notm}} database, analyze your data, and monitor sensitive data with the {{site.data.keyword.dashdbshort_notm}} web console accessible from {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Open the web console by clicking the service tile on your application overview page, and then click **Open**.

Single sign-on authentication connects you directly to the web console. You can access connection information from the web console, and the **Downloads** page includes links to client drivers for accessing {{site.data.keyword.dashdbshort_notm}} from remote applications. You can also access sample data and reports.

###Sensitive data reporting

The {{site.data.keyword.dashdbshort_notm}} web console includes a sensitive data reporting feature that detects and monitors sensitive objects in the {{site.data.keyword.dashdbshort_notm}} data warehouse, such as credit card numbers and US Social Security numbers.

To run and view reports that identify columns that contain sensitive data and provide information about connections and activities that access the sensitive data, select **Monitor &gt; Sensitive Data** in the web console. -->


<!-- ##IBM Analytics Services
{: #analytics_services}

For more information about {{site.data.keyword.IBM_notm}} analytics services and finding your local services representative, see: [{{site.data.keyword.IBM_notm}} Analytics Services ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/software/data/services/).
{: shortdesc} -->














