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

# Soporte para la capa de sockets seguros (SSL)
{: #ssl_support}

La base de datos de {{site.data.keyword.dashdbshort_notm}} utiliza un certificado para conexiones SSL que emite una entidad emisora de certificados digitales de terceros. 
{: shortdesc}

El certificado de CA forma parte del paquete de controlador Db2. Si la aplicación se conecta con un controlador desde el paquete del controlador Db2, no será necesario que descargue el certificado por separado. Puede descargar el paquete de controlador Db2 desde la consola web.

Sin embargo, si la aplicación tiene su propio controlador, es posible que tenga que descargar el certificado por separado. Puede descargar el certificado desde la consola web.

La capa de sockets seguros (SSL) es un
protocolo de seguridad que proporciona privacidad de las comunicaciones. SSL
permite que las aplicaciones de cliente y de servidor se comuniquen
de modo que haya protección contra escuchas, manipulación y
falsificación de mensajes. Las aplicaciones de cliente con SSL habilitado utilizan técnicas de cifrado estándar para ayudar a garantizar una comunicación segura.

La configuración de las aplicaciones para conectarse a su base de datos de {{site.data.keyword.dashdbshort_notm}} con SSL depende de la política de compañía. Ambos protocolos, el estándar y SSL, que puede utilizar para conectarse a la base de datos transmiten los nombres de usuario y las contraseñas como datos cifrados. Si desea garantizar una seguridad integral completa, transmita toda la información de base de datos, incluyendo datos y metadatos sensibles, a través de una conexión SSL. Los administradores pueden hacer que las conexiones SSL sean obligatorias modificando un valor en la consola web.


