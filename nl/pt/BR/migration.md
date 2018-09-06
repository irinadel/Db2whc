---

copyright:
  years: 2014, 2018
lastupdated: "2018-05-08"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Migrando dados para o IBM Cloud
{: #migration}

É possível carregar dados de um arquivo de dados em um formato delimitado (CSV ou TXT) localizado em uma rede local ou em um armazenamento de objeto (Amazon S3 ou IBM Cloud Object Storage) para o {{site.data.keyword.dashdblong}}. É possível até mesmo migrar seus dados de um sistema no local.
{: shortdesc}

## Carregando dados do armazenamento de objeto
{: #cos}

Para carregar dados do Amazon S3, selecione um dos métodos a seguir:
  * Console da web do {{site.data.keyword.dashdbshort_notm}}. **Carregar > Amazon S3**. 
  * Tabelas externas diretamente. Esta é uma instrução SQL de exemplo:

    ```
    INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
        (CCSID 1208 s3('s3.amazonaws.com',
        '<S3-access-key-ID>',
        '<S3-secret-access-key>',
        '<my_bucket>'
           )
      )      
    ```

Para carregar dados do IBM Cloud Object Storage usando tabelas externas diretamente, o trecho a seguir é uma instrução SQL de exemplo:

```
INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net',
  '<S3-access-key-ID>',
  '<S3-secret-access-key>',
  '<my_bucket>'
     )
  )      
```

**Nota:** para o IBM Cloud Object Storage, para criar credenciais HMAC ao criar novas credenciais de serviço, especifique {"HMAC:true"} no campo *Incluir parâmetros de configuração sequenciais*.

## Migrando dados do sistema no local
{: #onprem}

Para migrar seus dados de um sistema no local, escolha um dos métodos a seguir, dependendo do tamanho do seu conjunto de dados:
* Menos de 25 TB de dados: [IBM Lift](#lift)
* 25 TB de dados e superiores: [IBM Cloud Mass Data Migration Service](#mdms)

### Lift
{: #lift}

O Lift é um aplicativo que pode ser usado sem encargos para migrar os seus dados para o {{site.data.keyword.Bluemix_notm}} de várias origens de dados listadas na Tabela 1. 

| Banco de dados de destino no IBM Cloud | Fonte de dados |
|------------------------------|-------------|
| IBM Db2 Warehouse on Cloud   | IBM Db2 |
|                              | IBM Db2 Warehouse |
|                              | IBM Integrated Analytics System |
|                              | IBM PureData System for Analytics |
|                              | Oracle Database |
|                              | Microsoft SQL Server |
|                              | Formato de arquivo CSV |
{: caption="Tabela 1. Origens de dados de migração" caption-side="top"}

Para fazer download e instalar o Lift, veja: [Fazer download do Lift ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://lift.ng.bluemix.net/#download){:new_window}.

Para obter instruções passo a passo sobre a migração dos seus dados para o {{site.data.keyword.Bluemix_notm}} usando o Lift, consulte: [Migrar dados para o {{site.data.keyword.dashdblong}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://lift.ng.bluemix.net/#docs){:new_window}.

### IBM Cloud Mass Data Migration Service
{: #mdms}

O IBM Cloud Mass Data Migration Service (MDMS) pode ser usado para migrar dados de grandes bancos de dados IBM PureData Systems for Analytics (Netezza) de cerca de 25 TB e superiores para um banco de dados {{site.data.keyword.dashdblong}} totalmente gerenciado no {{site.data.keyword.Bluemix_notm}}.

O MDMS oferece uma maneira rápida, simples e segura para transferir fisicamente de terabytes até petabytes de dados para o {{site.data.keyword.Bluemix_notm}}. O MDMS é um dispositivo de armazenamento móvel com 120 TB de capacidade de armazenamento utilizável. Esse dispositivo fornece a capacidade de superar desafios comuns de transferência, tais como altos custos, longos tempos de transferência e preocupações de segurança - tudo em um único serviço.

![Visualização do dispositivo Mass Data Migration Service](images/mdms.svg)

Para obter mais informações sobre o dispositivo MDMS, veja: [Introdução ao IBM Cloud Mass Data Migration](/docs/infrastructure/mass-data-migration/index.html#getting-started-with-ibm-cloud-mass-data-migration){:new_window}.

Para obter mais informações sobre como migrar seus dados de um banco de dados IBM PureData System for Analytics (Netezza) para um banco de dados {{site.data.keyword.dashdblong}} usando o dispositivo MDMS, veja: [Migrando do IBM PureData System for Analytics (Netezza)](/docs/services/Db2whc/pda_db2whc_mdms.html).

