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

# Instalando o Pacote do Driver no Windows

É possível instalar o pacote de drivers do {{site.data.keyword.dashdbshort_notm}} no Windows usando o instalador.
{: shortdesc}

## Pré-requisitos

Antes de tentar se conectar ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, verifique se você tem os [pré-requisitos](connecting.html#prereqs) necessários.

<!-- Download the driver package for your operating system from the web console and install it. -->

## Procedimento

1. Execute o arquivo executável transferido por download como um administrador.

   O caminho da instalação padrão do pacote de drivers é: `Program Files\IBM\IBM DATA SERVER DRIVER`
2. [*Opcional*] Inclua o subdiretório `bin` do diretório de instalação do pacote de drivers na variável de ambiente `%PATH%` (para que seja possível executar o comando **db2cli** sem especificar o caminho completo para o executável do comando.)

## Qual o próximo?

Para poder conectar os seus aplicativos locais ou as ferramentas do cliente ao seu banco de dados do {{site.data.keyword.dashdbshort_notm}}, [configure o seu ambiente local](driver_pkg_cfg.html).
