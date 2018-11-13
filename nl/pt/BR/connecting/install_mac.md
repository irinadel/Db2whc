---

copyright:
  years: 2014, 2018
lastupdated: "2018-09-25"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Instalando o pacote de drivers no Mac OS X

É possível instalar o pacote de drivers do {{site.data.keyword.dashdbshort_notm}} no Mac OS X usando o script `installDSDriver.sh`.
{: shortdesc}

## Pré-requisitos

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](connecting.html#prereqs) necessários.

<!-- Download the Db2 driver package for your operating system from the web console and install it. -->

## Procedimento

- ** Para uma Nova Instalação **

  1. Monte a imagem do disco clicando duas vezes no arquivo `macos_dsdriver.dmg`.
   
     Uma nova janela **Localizador** é aberta com o conteúdo da imagem do disco.

     Se a janela **Localizador** não abrir, clique duas vezes no ícone `macos_dsdriver` na área de trabalho.
  2. Na janela **Localizador**, clique duas vezes no arquivo `installDSDriver.sh`.

     O pacote de drivers é instalado no local padrão: `/Applications/dsdriver`.

- **Para obter atualizações para a instalação do pacote de drivers existente**

  1. Fazer backup dos arquivos de configuração atuais:

     a. Vá para a pasta  ` Aplicativos / dsdriver/cfg ` .

     b. Copie os arquivos a seguir para uma pasta diferente: 
    
        ` db2cli.ini `

        `db2dsdriver.cfg`
  2. Remova o pacote de drivers instalado atualmente clicando com o botão direito na pasta `dsdriver` e selecionando **Mover para a Lixeira**.
  3. Instale o novo pacote de drivers conforme descrito na seção anterior **Para uma nova instalação**:
     
     a. Monte a imagem do disco clicando duas vezes no arquivo `macos_dsdriver.dmg`.
     b. Na janela **Localizador**, clique duas vezes no arquivo `installDSDriver.sh`.
  4. Restaure os arquivos de configuração:

     Copie os arquivos `db2cli.ini` e `db2dsdriver.cfg` salvos na Etapa 1 para a pasta `/Applications/dsdriver/cfg`.

## Qual o próximo?

Para poder conectar os seus aplicativos locais ou as ferramentas do cliente ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, [configure o seu ambiente local](driver_pkg_cfg.html).
