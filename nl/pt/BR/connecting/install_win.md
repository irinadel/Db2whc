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

# Instalando o Pacote do Driver no Windows
{: #install_dr_pkg_windows}

É possível instalar o pacote de drivers do {{site.data.keyword.dashdbshort_notm}} no Windows usando o instalador. 
{: shortdesc}

## Pré-requisitos
{: #prereq51}

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](/docs/services/Db2whc/connecting/connecting.html#prereqs) necessários.

<!-- Download the driver package for your operating system from the web console and install it. -->

## Procedimento
{: #proc51}

1. Execute o arquivo executável transferido por download como um administrador.

   O caminho da instalação padrão do pacote de drivers é: `Program Files\IBM\IBM DATA SERVER DRIVER`
2. [*Opcional*] Inclua o subdiretório `bin` do diretório de instalação do pacote de drivers na variável de ambiente `%PATH%` (para que seja possível executar o comando **db2cli** sem especificar o caminho completo para o executável do comando.)

## Qual o próximo?
{: #wn51}

Para poder conectar os seus aplicativos locais ou as ferramentas do cliente ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, [configure o seu ambiente local](/docs/services/Db2whc/connecting/driver_pkg_cfg.html).
