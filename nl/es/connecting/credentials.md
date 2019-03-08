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

# Detalles de base de datos y credenciales de conexión
{: #db_details_cxn_creds}

Para configurar el entorno de desarrollo local y conectar aplicaciones y herramientas a la base de datos de {{site.data.keyword.dashdbshort_notm}}, debe conocer los detalles de base de datos y las credenciales de conexión.
{: shortdesc}

## Detalles de base de datos
{: #db_details}

Hay detalles de la base de datos importantes que son necesarios para conectar aplicaciones y herramientas a la base de datos:

- *Nombre de host* - El nombre de host del servidor.
- *Número de puerto* - Utilizado por el gestor de base de datos para la comunicación TCP/IP. (Tenga en cuenta que el servicio se suministra con un número de puerto para conexiones que utilizan SSL (Secure Socket Layer) y un puerto diferente para la conexión no SSL).

   Si es necesario, puede obtener la dirección IP del servidor utilizando el mandato ping o el mandato nslookup, especificando el nombre de host.
- *Nombre de base de datos* - El nombre de la base de datos Db2, normalmente BLUDB.

## Credenciales de conexión
{: #cxn_creds}

Hay tres tipos de credenciales:

- *IBMid* - Si utiliza {{site.data.keyword.Bluemix_notm}}, este es el ID que utilizará para iniciar sesión en {{site.data.keyword.Bluemix_notm}}. Este no es el que utiliza para conectar aplicaciones o herramientas a la base de datos Db2 Warehouse on Cloud.
- *Credenciales de base de datos Db2* - El servicio se suministra con un ID de usuario y una contraseña de base de datos que se pueden utilizar para conectar aplicaciones y herramientas a la base de datos.
- *Usuarios creados por el administrador* - Algunos planes de {{site.data.keyword.dashdbshort_notm}} permiten a los usuarios administrativos crear nuevos usuarios. Estos ID de usuario creados por el administrador se pueden utilizar para iniciar sesión directamente en el URL de la consola web y para conectarse a la base de datos Db2 desde aplicaciones o herramientas.

## Dónde encontrar detalles de la base de datos y credenciales de conexión
{: #location}

Puede recopilar esta información desde los siguientes lugares:

- *El administrador* - Si no es el propietario o administrador de la instancia Db2, puede obtener los detalles de la base de datos y conectar credenciales del administrador.
- *Consola web Db2* - Los detalles y credenciales de la base de datos están disponibles en la consola web.
- Si está utilizando {{site.data.keyword.Bluemix_notm}}: 
   
   - *{{site.data.keyword.Bluemix_notm}} Panel de control* - Al visualizar el servicio en el panel de control de {{site.data.keyword.Bluemix_notm}}, en el área "Credenciales de servicio", puede visualizar los detalles de la base de datos y el ID de usuario y la contraseña de la base de datos.
   - *`VCAP_SERVICES`* - `VCAP_SERVICES` es una variable de entorno en {{site.data.keyword.Bluemix_notm}} que contiene detalles y credenciales de base de datos en formato JSON. Al ver las credenciales de servicio para el servicio del panel de control {{site.data.keyword.Bluemix_notm}}, el contenido de `VCAP_SERVICES` es lo que se muestra. Al enlazar otros servicios o apps de {{site.data.keyword.Bluemix_notm}} al servicio, estos otros servicios o apps pueden acceder a detalles y credenciales de base de datos mediante programa leyendo `VCAP_SERVICES`.
