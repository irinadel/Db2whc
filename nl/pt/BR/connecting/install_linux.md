---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# Instalando o pacote de drivers no Linux ou PowerLinux
{: #install_dr_pkg_linux}

É possível instalar o pacote de drivers do {{site.data.keyword.dashdbshort_notm}} no Linux ou PowerLinux usando o `installDSDriver`. 
{: shortdesc}

## Pré-requisitos
{: #prereq31}

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](/docs/services/Db2whc/connecting/connecting.html#prereqs) necessários.

<!-- Download the Db2 driver package for your operating system from the web console and install it. -->

**Apenas no PowerLinux**, conclua as etapas a seguir para instalar o pacote de tempo de execução do compilador XL C/C++:

1. Faça download do pacote de tempo de execução do compilador XL C/C++ por meio do site de FTP. Por exemplo, para usar a ferramenta **wget** para fazer download do pacote de tempo de execução para o little endian Ubuntu 14 do Linux, emita o comando a seguir: 

   ` wget ftp://public.dhe.ibm.com/software/server/POWER/Linux/rte/xlcpp/le/ubuntu/dists/trusty/main/binary-ppc64el / * `
2. Instale o pacote de tempo de execução emitindo o comando a seguir:

   ` sudo dpkg -iG *.deb ` 

## Procedimento
{: #proc31}

1. Descompacte o arquivo compactado de pacote de drivers transferido por download anteriormente.

   Exemplo: 

   ` gunzip file_name.tar.gz `

   `tar -xvf file_name.tar`

    Um subdiretório `dsdriver` é criado no diretório no qual você executou os comandos de descompactação.
2. Extraia os drivers Java e ODBC/CLI.

   a. No subdiretório `dsdriver`, execute o comando **installDSDriver**.
   
   O comando **installDSDriver** cria os arquivos de script `db2profile` e `db2cshrc` no diretório `dsdriver`.

   b. Execute um dos arquivos de script a seguir com base em seu ambiente de shell:

   - ** shell Bash ou Korn **:  ` source db2profile `
   - ** shell C **:  ` source db2cshrc `

## Qual o próximo?
{: #wn}

Para poder conectar os seus aplicativos locais ou as ferramentas do cliente ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, [configure o seu ambiente local](/docs/services/Db2whc/connecting/driver_pkg_cfg.html).   




