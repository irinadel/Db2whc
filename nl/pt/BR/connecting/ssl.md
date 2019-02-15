---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# Suporte ao Secure Sockets Layer (SSL)
{: #ssl_support}

O banco de dados {{site.data.keyword.dashdbshort_notm}} usa um certificado para conexões SSL que é emitido por uma autoridade de certificação digital (CA) de terceiros. 
{: shortdesc}

O certificado de autoridade de certificação faz parte do pacote de drivers do Db2. Se o seu aplicativo se conectar a um driver por meio do pacote de drivers do Db2, não será necessário fazer download do certificado separadamente. É possível fazer download do pacote de drivers do Db2 por meio do console da web.

No entanto, se o seu aplicativo tiver seu próprio driver, talvez seja necessário fazer download do certificado separadamente. É possível fazer download do certificado por meio do console da web.

Secure Sockets Layer (SSL) é um protocolo de segurança que fornece privacidade de comunicação. O SSL permite que aplicativos do cliente e servidor comuniquem-se de uma forma que é projetada para evitar intrusões, violação e falsificação de mensagens. Os aplicativos clientes ativados para SSL usam técnicas de criptografia padrão para ajudar a garantir a comunicação segura.

A configuração de aplicativos para se conectar ao banco de dados {{site.data.keyword.dashdbshort_notm}} com SSL depende da política de sua empresa. Os protocolos padrão e SSL que podem ser usados para se conectar ao banco de dados transmitem nomes de usuário e senhas como dados criptografados. Se desejar garantir segurança completa de ponta a ponta, transmita todas as informações do banco de dados, incluindo dados e metadados sensíveis, por meio de uma conexão SSL. Os administradores podem tornar as conexões SSL obrigatórias, mudando uma configuração no console da web.


