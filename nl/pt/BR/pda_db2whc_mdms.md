---

copyright:
  years: 2014, 2018
lastupdated: "2018-06-15"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Migrando do IBM PureData System for Analytics (Netezza)
{: #pda}

O {{site.data.keyword.Bluemix_notm}} Mass Data Migration Service (MDMS) pode ser usado para migrar dados de grandes bancos de dados IBM PureData Systems for Analytics (Netezza) de cerca de 25 TB e superiores para um banco de dados {{site.data.keyword.dashdblong}} totalmente gerenciado no {{site.data.keyword.Bluemix_notm}}.

O MDMS oferece uma maneira rápida, simples e segura para transferir fisicamente de terabytes até petabytes de dados para o {{site.data.keyword.Bluemix_notm}}. O MDMS é um dispositivo de armazenamento móvel com 120 TB de capacidade de armazenamento utilizável. Esse dispositivo fornece a capacidade de superar desafios comuns de transferência, tais como altos custos, longos tempos de transferência e preocupações de segurança - tudo em um único serviço.
{: shortdesc}

![Visualização do dispositivo Mass Data Migration Service](images/mdms.svg)

## Do que você precisará ao solicitar um dispositivo
{: #prereq}

1. Configurações de rede para o dispositivo de armazenamento
   - Endereço IP estático
   - Máscara de rede para ativação da transferência de dados
2. Configurações de rede para computador remoto
   - Endereço IP estático
   - Máscara de rede 
   - Gateway padrão para acessar a interface com o usuário (IU)
3. Destino de download do Cloud Object Storage <br/>
   **Importante**: é necessário ter pelo menos uma conta do {{site.data.keyword.cos_full}} e um depósito em um local para Várias regiões dos EUA ou Sul dos EUA para concluir o formulário de solicitação. Se você ainda não tiver uma conta do {{site.data.keyword.cos_full_notm}}}, crie uma antes de solicitar o dispositivo MDMS. Para obter mais informações, veja: [Sobre o {{site.data.keyword.cos_full}}](/docs/services/cloud-object-storage/about-cos.html){:new_window}.

## Etapa 1: Criando uma solicitação
{: #create-req}

1. Efetue login no [{{site.data.keyword.slportal}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/){:new_window} usando suas credenciais exclusivas.
2. Selecione **Armazenamento > Migração de dados > Mass Data Migration** na barra de navegação para acessar a página inicial do MDMS.
3. Clique em **Solicitar dispositivo** para abrir o formulário do pedido.
4. Preencha cada campo no formulário do pedido **Mass Data Migration**.
   - **Endereço de entrega**: esse formulário não é previamente preenchido e cada campo é editável. Forneça o nome da pessoa que aceitará a entrega do dispositivo no campo Atenção. Ao escolher o local de entrega, considere o peso do dispositivo (30 kg (66 lb.) com sua embalagem) e a acessibilidade. <br/> (**Nota**: o dispositivo é equipado com rodas e com uma alça suspensa para manobras).
   - **Contatos de migração de chave**: esse formulário não é previamente preenchido. Cada campo é editável. Mais de uma pessoa pode ser incluída.
   - **Configuração de rede do data center**: forneça detalhes de configuração de rede para o provisionamento prévio da porta Eth3 no dispositivo MDMS antes da remessa.
   - **Destino de transferência de dados**: selecione a conta de destino existente na lista.
   - **Nome da solicitação**: insira um nome para ajudá-lo a rastrear seu pedido.
5. Selecione a caixa de seleção **Eu li e concordo com os termos completos do Contrato do Mass Data Migration** após ler cada contrato de prestação de serviços que é fornecido.
6. Clique em **Fazer solicitação** para enviar a solicitação. Clique em **Cancelar** para abandonar completamente o formulário e retornar para a página inicial do MDMS.

## Etapa 2: Preparação e remessa
{: #prep-ship}

Após enviar a solicitação, o status para o chamado da solicitação aparecerá como *Processando a solicitação*. Quando sua solicitação tiver sido processada, o {{site.data.keyword.IBM}} iniciará a pré-configuração do próximo dispositivo disponível e o status na grade [Solicitações ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/storage/mdms){:new_window} mostrará *Preparando o dispositivo* seguido por *Aguardando remessa*. Após sua solicitação entrar no status *Aguardando remessa*, ela não poderá mais ser cancelada. 

O dispositivo é retirado pela transportadora para ser enviado para o seu local. Nesse momento, o status da solicitação será atualizado para *Dispositivo enviado*. O número de rastreamento será compartilhado com você na seção **Detalhes do pedido** da grade [Solicitações ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/storage/mdms){:new_window}.

## Etapa 3: Recebimento e conexão
{: #rec-con}

<!-- **[Editor's note: What to keep from this section immediately below?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
1. The device arrives pre-configured for you. Basic [powering/connectivity instructions](docs/infrastructure/mass-data-migration/user-instructions.html) are included.  **[Editor's note: Are the instructions included in the MDMS package? If so, are they different from the instructions found with the "powering/connectivity" link?]**<br/>
  **Note**: User name and storage pool password is provided separately. Check the **Request Details** in your [Requests ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/storage/mdms){:new_window} grid for the credentials.
2. Point your browser to the static IP address that you provided in the order form. **[Editor's note: Is this done on PDA? What system is the static IP address for?]**
3. Log in. Enter password to unlock the empty storage pool. **[Editor's note: How is this done?]**<br/>
   **Note**: See the **Request Details** of your [Requests ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/storage/mdms){:new_window} grid for the password.
4. Mount the NFS share on your server. **[Editor's note: How is this done?]**
5. Rerun your DataShuttle inventory to ensure any new files are captured. **[Editor's note: Is "DataShuttle inventory" a command that is run on PDA?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& -->

### Visão geral

O dispositivo {{site.data.keyword.cloud}} Mass Data Migration é um dispositivo de armazenamento móvel capaz de apresentar compartilhamentos Network File System (NFS) ou FileNet Content Federations (CF) montáveis e é gerenciado por meio de uma interface de navegador da web. O dispositivo é enviado para o seu data center, carregado com dados no local, retornado para um data center {{site.data.keyword.BluSoftlayer_full}} e seus dados são carregados em sua conta do {{site.data.keyword.cos_full}}.

### Energia

O dispositivo inclui com um cabo de energia C13-US ([IEC 60320 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://en.wikipedia.org/wiki/IEC_60320){:new_window}). Se o dispositivo for usado fora dos Estados Unidos, um adaptador de energia poderá ser necessário.

O dispositivo MDMS aceita todas as faixas de energia padrão. ![Faixa de energia](/images/PowerRating.png)

### Conectividade Ethernet

Há duas conexões Ethernet a serem feitas. Uma para gerenciamento de dispositivo por meio de um navegador e outra para a movimentação de dados na mesma sub-rede na qual os dados de origem residem.

Ambas as portas se originam do dispositivo como RJ45 e os cabos CAT6A são fornecidos. Adaptadores SFP+ de cobre são fornecidos para converter de RJ45. Os adaptadores funcionam com todos os fabricantes de comutador. Esses adaptadores estão localizados em um depósito na parte de baixo da tampa de remessa.

- Eth1 (1 GbE-B) é usada para o gerenciamento de dispositivos, e como tal, deve ter um gateway especificado na configuração de endereço IP. Isso pode ser visualizado na tela LCD após o dispositivo ser ligado (veja a seção [Configuração do endereço IP](#ip_cfg)).

- Eth3 (10 GbE-B) é usada para a transferência de dados. Essa conexão deve estar na mesma sub-rede que os dados de origem ou pode ser diretamente conectada ao servidor, se necessário.

Caso um fator de forma diferente de conexão Ethernet seja necessário, deve-se fornecer o conversor.

### Instruções passo a passo do usuário

1. O dispositivo MDMS chega pré-configurado com seu endereço IP, nome do usuário, conjunto de armazenamentos bloqueado e compartilhamento NFS. A senha de usuário e a senha do conjunto de armazenamentos são comunicadas por meio de um e-mail separado.

2. Determine o local mais apropriado para o dispositivo ser colocado; no qual ele atingirá ambas as conexões de energia e de sua Ethernet (1 GbE e 10 GbE) e terá tráfego mínimo de pedestres nas proximidades.

3. Posicione o dispositivo a ser conectado. Ele pode permanecer na embalagem de transporte durante o uso. Assegure-se de que o dispositivo esteja em temperatura ambiente e que não haja condensação nele. Conecte à energia usando o cabo de alimentação fornecido embaixo da tampa da embalagem. Ligue o dispositivo.<br/>
    **Nota**: há dois comutadores de energia.
![Comutadores de energia](/images/MDMSPowerSwitch.png)
    **Nota**: o dispositivo não precisa ser removido da caixa móvel.

4. Remova o cabo CAT6A da tampa da embalagem e conecte-a à porta Eth3 (10 GbE-B) que é mostrada na figura.
    ![Local das portas Eth1 e Eth3](/images/MDMSNewEth1and3.png)

5. Conecte o adaptador CAT6A para SFP+ fornecido e conecte seu comutador 10 Gb.

6. Se o endereço IP configurado para a Eth3 puder ser acessado por meio de um navegador `https://<your_Eth3_IP_Address>`, continue com a próxima etapa. 

   Caso contrário, conecte-se à porta Eth1 (1 GbE-B). Abra seu navegador e insira `https://<your_Eth1_IP_Address>`. Insira o endereço IP Eth1 apropriado para sua configuração de rede. Aceite a exceção de certificado.<br/>
   **Nota**: se você precisar alterar quaisquer configurações IP para Eth3 ou Eth1, veja a seção [Configuração do endereço IP](#ip_cfg).

7. Use o nome do usuário e a senha fornecidos para efetuar login.<br/>
    ![Página de login](/images/Login.png)

8. O assistente de fluxo de trabalho apresenta acesso aos itens específicos geralmente usados em ordem da esquerda para a direita.<br/>
    ![Ícones de fluxo de trabalho](/images/workflow.png) <br/>
    **NOTA**: o fluxo de pode ser reaberto usando o **Workflow Manager** no canto superior esquerdo da GUI.

9. Ative o conjunto de armazenamentos pré-configurado:
    - Clique em **Desbloquear e iniciar o conjunto de armazenamentos**.
    - Insira sua passphrase do conjunto de armazenamentos e clique em **OK**.
    ![Ativar conjunto de armazenamentos](/images/UnlockPool.png)

10. Por padrão, o compartilhamento tem os protocolos NFS e SMB que estão ativados sem restrições de acesso que são colocadas no compartilhamento. Para restringir o acesso a esse compartilhamento (para NFS ou SMB), clique com o botão direito no nome do compartilhamento e selecione o item de menu apropriado.<br/>
    ![Restringir acesso de compartilhamento](/images/ShareControls.png)

11. Quando o conjunto de armazenamentos é ativado, o compartilhamento do NFS se torna disponível para montagem. No fluxo de trabalho, clique em **Visualizar compartilhamentos de rede** para
abrira a visualização de compartilhamentos de rede. Feche o fluxo de trabalho, clique com o botão direito no compartilhamento e selecione **Visualizar comando de montagem** para ver o nome do compartilhamento e as informações de montagem. Monte o compartilhamento em seu servidor de origem. Assegure-se de especificar o endereço IP do link de 10 GB ao montar o compartilhamento.
    ![Montando o compartilhamento](/images/MountCommand.png)

## Etapa 4: Copiando dados e enviando
{: #copy-ship}

<!-- &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&

1. Run the DataShuttle copy to move the data. **[Editor's note: What is "DataShuttle"? Is "DataShuttle copy" a command that is run on PDA?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& -->

1. Copie seus dados para o compartilhamento do NFS. Escolha um dos métodos a seguir para extrair seus dados do seu banco de dados Netezza:
    1. Execute o exemplo a seguir do utilitário **nz_backup**:

       `/nz/support/contrib/bin/nz_backup –db <db_name> –d <target_directory>  ascii threads 4`

       **Nota**: o `<target_directory>` é o compartilhamento do NFS no dispositivo MDMS que é montado em seu servidor Netezza.
   
    2. Execute o exemplo a seguir de uma instrução CREATE EXTERNAL TABLE:

       `CREATE EXTERNAL TABLE '<path_to_mdms_device>/<file_name>' SELECT * FROM <table name>`

       **Nota:** se você usou as opções da cláusula `USING` para exportação de dados, lembre-se ou salve as opções da cláusula. A cláusula será reutilizada posteriormente durante o processo de carregamento de tabela externa do IBM Cloud Object Storage.

       Para obter mais informações sobre a instrução SQL, veja: [Instrução CREATE EXTERNAL TABLE ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.sql.ref.doc/doc/r_create_ext_table.html){:new_window}. 

<!--       - Provide the {{site.data.keyword.Bluemix_notm}} team with the "USING" clause that was used for data export. The clause is reused during the load process on {{site.data.keyword.Bluemix_notm}}.
       - Select FORMAT = "Text"
-->

2. No fluxo de trabalho, clique em **Visualizar atividade de rede** para mostrar a carga Ethernet de entrada na GUI conforme os dados são transferidos para o dispositivo no link de 10 Gb/s.
    ![Visualizar atividade](/images/UserGuide13.png)

3. No fluxo de trabalho, clique em **Visualizar conjuntos de armazenamentos** para monitorar o uso de armazenamento e o IOPS no dispositivo.
    ![Visualizar conjunto de armazenamentos](/images/UserGuide14.png)

4. Quando a cópia estiver pronta, desligue o sistema normalmente. Desligar o dispositivo também bloqueia o conjunto de armazenamentos. No fluxo de trabalho, clique em **Encerrar dispositivo...**.  
    ![Localização do botão da UI de encerramento do dispositivo](/images/Shutdown.png)

5. Desconecte o dispositivo. Retorne o cabo de energia, o cabo Ethernet e o adaptador SFP+ em seus respectivos locais de armazenamento sob a tampa.

6. Anexe a etiqueta de remessa fornecida no dispositivo. Notifique a transportadora e retorne o dispositivo para o {{site.data.keyword.BluSoftlayer_full}} Data Center. Após a chegada no data center, seus dados serão então carregados em seu depósito do {{site.data.keyword.cos_full_notm}}.

Após o dispositivo ser retornado para a equipe do {{site.data.keyword.BluSoftlayer}}, o status da solicitação mudará para *Dispositivo recebido*.

## Etapa 5: Transferência e acesso
{: #offload}

Durante o processo de transferência de dados, o status da solicitação é exibido como *Transferência de dados*. O status mudará novamente quando a migração para o depósito do {{site.data.keyword.objectstorageshort}} for concluída (*Transferência concluída*). Os seus dados estarão acessíveis imediatamente quando a transferência de alta velocidade em seu depósito do Cloud Object Storage for concluída. 

Quando a migração de seus dados no depósito do Cloud Object Storage for concluída, será possível continuar em [importar seus dados em seu banco de dados {{site.data.keyword.dashdbshort_notm}}](#import).

## Etapa 6: Importando dados do IBM Cloud Object Storage
{: #import}

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

**Notas:** 
* Certifique-se de usar as mesmas opções da cláusula `USING` que você usou para extrair os dados do seu banco de dados PureData System for Analytics (Netezza) usando a instrução CREATE EXTERNAL TABLE.
* Para o IBM Cloud Object Storage, para criar credenciais HMAC ao criar novas credenciais de serviço, especifique {"HMAC:true"} no campo *Incluir parâmetros de configuração sequenciais*.

Para obter um tutorial guiado sobre a importação de dados do IBM Cloud Object Storage, veja: [Demo guiada do IBM Db2 Warehouse on Cloud: Explorar carregamento de dados ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud/){:new_window}.

## Etapa 7: Apagando o dispositivo MDMS
{: #erase}

O {{site.data.keyword.IBM}} implementa a limpeza de dados no nível dos requisitos do Departamento de Defesa dos EUA para apagar permanentemente seus dados do dispositivo MDMS. Quando concluído, o status da solicitação será exibido como *Apagamento concluído*.

## Notas adicionais
{: #notes}

### Exclusividade no depósito

Para assegurar que os nomes de objetos sejam exclusivos quando eles forem copiados no depósito, o caminho de arquivo será incluído como um prefixo no nome do objeto. Por exemplo, o arquivo config.ini na pasta `/root/user/` será renomeado para "root/user/config.ini" quando copiado no depósito.

### Depósitos

Se o depósito de destino não existir, ele será criado. Se ele existir, deverá estar vazio, caso contrário, a cópia não poderá continuar.

### Sistemas de arquivos

Symlinks e links físicos são ignorados durante o processo de varredura.

### Configuração do endereço IP
{: #ip_cfg}

O monitor LCD no dispositivo pode ser usado para configurar os endereços IP para as portas Ethernet. É possível navegar no monitor LCD usando os botões de **seta para cima**, **seta para baixo**, **Esc** e **Enter**. O botão **Enter** o leva a um menu e **Esc** o leva para fora do menu.

![Monitor LCD](/images/MDMSLCD.png)

Ao editar um endereço IP ou uma máscara de sub-rede, o botão **Enter** o faz avançar um caractere por vez; **Esc** o faz retroceder um caractere por vez. Os botões **seta para cima** e **seta para baixo** alternam pelos números para o local selecionado.

Use **Esc** para voltar para o menu anterior.  

Acesse o item de menu **Atualizar...** e pressione **Enter** para salvar as configurações.
