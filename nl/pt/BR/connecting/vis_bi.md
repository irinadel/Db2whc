---

copyright:
  years: 2014, 2019
lastupdated: "2018-10-24"

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

# Visualização de dados / BI
{: #data_vis_bi}

Também é possível conectar ferramentas e aplicativos externos ao {{site.data.keyword.dashdbshort_notm}} e utilizá-los para gerenciar ou analisar ainda mais os dados. 
{: shortdesc}

## Cognos Analytics
{: #cognos}

É possível executar relatórios do IBM Cognos® com relação a dados na nuvem, em vez dos dados em um banco de dados local. Depois de carregar seus dados em um banco de dados {{site.data.keyword.dashdbshort_notm}}, você configurará o driver JDBC e, em seguida, usará as ferramentas de administração do Cognos para criar a conexão com o banco de dados. <!--These instructions explain how to connect to the database from Cognos version 10.2.1.-->
{: shortdesc}

Assista a este vídeo para ver como criar uma conexão.

<iframe class="embed-responsive-item" id="youtubeplayer" title="Criando uma conexão por meio do Cognos Analytics" type="text/html" width="640" height="390" src="//www.youtube.com/embed/TRUEPVHGi0s?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

Para obter mais informações, consulte [Conectando o Cognos Analytics ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/en/SSEP7J_11.0.0/com.ibm.swg.ba.cognos.ug_cra.doc/c_create_ds.html#create_ds){:new_window}

## Looker
{: #looker}

É possível conectar o Looker a um banco de dados {{site.data.keyword.dashdbshort_notm}}. Looker é um app de inteligência de negócios e uma plataforma de análise de Big Data com a qual é possível explorar, analisar e compartilhar business analytics em tempo real.
{: shortdesc}

[Conectando o Looker ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.looker.com/setup-and-management/connecting-to-db){:new_window}

## Tableau
{: #tableau}

Estas instruções explicam como conectar o Tableau a um banco de dados {{site.data.keyword.dashdbshort_notm}} e se aplicam à Área de trabalho do Tableau<!--version 8.x-->, mas é possível usar etapas semelhantes para outras ferramentas do Tableau.
{: shortdesc}

### Pré-requisitos
{: #prereq8}

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) necessários.

### Procedimento
{: #proc8}

1. Na Área de trabalho do Tableau, abra a janela ou a página na ferramenta usada para definir uma conexão com o banco de dados.
2. Na página inicial, clique em **Conectar aos dados**.
3. Na lista **Origens de dados**, selecione a origem de dados ou o driver a ser usado para a conexão com o banco de dados. Na seção **Em um servidor** da lista, selecione **IBM Db2**.
4. Na janela **Conexão do IBM DB2**, insira as informações de conexão usando a tabela a seguir.

| Campo Tableau | Campo de informações de conexões do Db2 |
|---------------|-----------------------------------|
| Etapa 1: Digitar um nome de servidor | Nome do host |
| Etapa 2: Porta | Número da porta |
| Etapa 3: Inserir um banco de dados no servidor | Nome do banco de dados |
| Nome do usuário | ID do Usuário |
| Senha | Senha |
{: caption="Tabela 1. Campos no Tableau para informações de conexão" caption-side="top"}

5. Clique em  ** Conectar **  para estabelecer a conexão. O Tableau oferece várias opções para conexão com seus dados. Para fazer uso completo do banco de dados {{site.data.keyword.dashdbshort_notm}}, escolha a opção **Conectar em tempo real**.

## Microsoft Excel
{: #excel}

Estas instruções explicam como conectar o Microsoft Excel <!--2010-->a um banco de dados {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

### Pré-requisitos
{: #prereq9}

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) necessários.

Deve-se ter o pacote de drivers do Db2 ou o IBM® Data Server Driver Package instalado no computador local. 

**Restrição**: conexões entre o Excel e o {{site.data.keyword.dashdbshort_notm}} são suportadas apenas no sistema operacional Windows.

### Procedimento
{: #proc9}

1. No console da web, acesse a página **Executar SQL**.
    
2. Digite uma ou mais instruções SELECT na caixa de texto do editor.

3. Clique em uma das opções Executar.

4. Clique em  ** Arquivo ODC do Excel **.

5. Faça download e abra o arquivo `BLUExcel.odc` no Excel. Se for exibido um aviso de segurança, clique em **Ativar**.

6. Clique em **Abrir** para se conectar ao banco de dados {{site.data.keyword.dashdbshort_notm}}. A caixa de diálogo **Conectar-se ao banco de dados DB2** é aberta.

7. Digite o ID de usuário e a senha usados para efetuar login no {{site.data.keyword.dashdbshort_notm}}. Para obter o ID de usuário e a senha, clique em **Conectar** no console da web ou em **Conectar > Informações de conexão** no console da web.

8. Assegure-se de que o modo de conexão seja `Share` e, em seguida, clique em **OK**.

### Resultados
{: #results2}

Os resultados da consulta são exibidos em uma planilha do Excel. Esses são os mesmos resultados exibidos no visualizador Resultados. Agora é possível gerar gráficos e relatórios e analisar seus dados usando o Excel. Para obter mais informações sobre como fazer isso e como executar consultas SQL em seus dados por meio do console da web, consulte: 
- [Tutorial: Gerando gráficos e relatórios usando o Excel ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/explore_excel_reports.html){:new_window}
- [Analisando com o Excel ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.analytics.doc/doc/exploreexcel.html){:new_window}

## Esri ArcGIS para Desktop
{: #esri_arcgis}

É possível conectar o Esri ArcGIS for Desktop <!--version 10.3.1 -->a um banco de dados {{site.data.keyword.dashdbshort_notm}} e, em seguida, usá-lo para analisar e visualizar dados geoespaciais.
{: shortdesc}

### Pré-requisitos
{: #prereq10}

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](/docs/services/Db2whc/connecting?topic=Db2whc-connect_ov#prereqs) necessários.

Deve-se ter o pacote de drivers do Db2 ou o IBM® Data Server Driver Package instalado no computador.

### Procedimento
{: #proc10}

1. Determine seus dados de DSN do ODBC por meio das [informações de conexão](/docs/services/Db2whc/connecting?topic=Db2whc-db_details_cxn_creds#db_details_cxn_creds) coletadas antecipadamente.

2. Crie uma nova conexão:
      
   a. Na árvore Catálogo do ArcCatalog, abra o nó Conexões com o banco de dados e clique em **Incluir conexão com o banco de dados**.
        
   b. No assistente Conexões com o Banco de Dados:
   - Selecione **DB2** na lista suspensa Plataforma de banco de dados.
   - Insira a sequência a seguir no campo **Origem de dados**:
     ```
     HostName=<hostname>;Port=<port>;Database=<database>;
     CLIENTBUFFERSUNBOUNDLOBS=1;LOBCACHESIZE=50000000;
     FET_BUF_SIZE=256K  
     ```

     em que `<hostname>`, `<port>` e `<database>` são marcadores que representam o nome do host, o número da porta e o nome do banco de dados que você observou anteriormente.
            
   - Selecione **Autenticação do banco de dados** como o tipo de autenticação.
            
   - Especifique seu nome de usuário e senha (o ID de usuário e a senha observados anteriormente) nos campos correspondentes.
            
   - Pressione  ** OK **.
        
     ![Database Connections wizard](images/2_gs_conn.jpg)

### Resultados
{: #results3}

O componente ArcCatalog do Esri ArcGIS for Desktop está agora conectado ao banco de dados {{site.data.keyword.dashdbshort_notm}}. 


