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

# Conexión con Administrador de orígenes de datos ODBC

Utilice la herramienta Administrador de origen de datos ODBC para definir una conexión entre una aplicación ODBC o CLI y una base de datos de {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

## Requisitos previos

Antes de intentar realizar una conexión a su base de datos de {{site.data.keyword.dashdbshort_notm}}, verifique que dispone de los [requisitos previos](connecting.html#prereqs) necesarios.

<!-- Before you can connect to your database, you must perform the following steps:

- [Verify prerequisites](prereqs.html), including installing driver packages, configuring your local environment, and downloading SSL certificates (if needed)
- Collect [connection information](credentials.html), including database details such as host name and port numbers, and connection credentials such as user ID and password -->

## Procedimiento

1. Instale el [paquete de controlador Db2](driver_pkg.html).

2. Abra el administrador de orígenes de datos ODBC y cree un nombre de subsistema predeterminado de usuario o un nombre de subsistema predeterminado de sistema para el paquete de controlador Db2.
    
3. Pulse la **Configuración avanzada**. Especifique los parámetros de CLI con los valores para el servidor de {{site.data.keyword.dashdbshort_notm}}: **Nombre de servidor**, **Puerto** y **Base de datos**.
    
4. Para obtener una conexión SSL, especifique el parámetro de CLI **Seguridad** con el valor `SSL`.
    
5. Pulse **Aplicar**.
    
6. Para probar la conexión, vuelva a la página principal de ODBC Data Source Administrator. Pulse **Configurar** para el DSN que ha creado. Entre el ID de usuario y la contraseña para el servidor y pulse **Conectar**.

