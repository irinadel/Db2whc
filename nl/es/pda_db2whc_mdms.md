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

# Migración desde IBM PureData System for Analytics (Netezza)
{: #pda}

El servicio de migración de datos masiva (MDMS) de {{site.data.keyword.Bluemix_notm}} puede utilizarse para migrar datos desde bases de datos de IBM PureData Systems for Analytics (Netezza) grandes (de 25 TB y superiores) a una base de datos de {{site.data.keyword.dashdblong}} completamente gestionada en {{site.data.keyword.Bluemix_notm}}.

MDMS ofrece una forma rápida, sencilla y segura para transferir físicamente de terabytes a petabytes de datos a {{site.data.keyword.Bluemix_notm}}. MDMS es un dispositivo de almacenamiento móvil con una capacidad de almacenamiento utilizable de 120 TB. Este dispositivo le permite superar, con un solo servicio, desafíos comunes, como altos costes de transferencia, tiempos de transferencia largos y problemas de seguridad.
{: shortdesc}

![Vista del dispositivo del servicio de migración de datos masiva](images/mdms.svg)

## Qué necesitará al solicitar un dispositivo
{: #prereq}

1. Valores de red del dispositivo de almacenamiento
   - Dirección IP estática
   - Máscara para habilitar la transferencia de datos
2. Valores de red del sistema remoto
   - Dirección IP estática
   - Máscara de red 
   - Pasarela predeterminada para acceder a la interfaz de usuario (IU)
3. Destino de descarga de Cloud Object Storage <br/>
   **Importante**: Debe tener como mínimo una cuenta de {{site.data.keyword.cos_full}} y un grupo en varias regiones de EE. UU. o en una ubicación del sur de EE. UU. para cumplimentar el formulario de solicitud. Si todavía no dispone de una cuenta de {{site.data.keyword.cos_full_notm}}, cree una antes de solicitar el dispositivo MDMS. Para obtener más información, consulte: [Acerca de {{site.data.keyword.cos_full}}](/docs/services/cloud-object-storage/about-cos.html){:new_window}.

## Paso 1: creación de una solicitud
{: #create-req}

1. Inicie una sesión en el [{{site.data.keyword.slportal}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://control.softlayer.com/){:new_window} utilizando sus credenciales exclusivas.
2. Seleccione **Almacenamiento > Migración de datos > Migración de datos masiva** en la barra de navegación para acceder a la página de destino de MDMS.
3. Pulse **Solicitar dispositivo** para abrir el formulario de pedido.
4. Rellene todos los campos del formulario de solicitud de **migración de datos masiva**.
   - **Dirección de envío**: Este formulario no se rellena previamente y sus campos son editables. Proporcione el nombre de la persona que aceptará la entrega del dispositivo en el campo A la atención de. Al escoger la ubicación de entrega, tenga en cuenta el peso del dispositivo (30 kg con el maletín) y la accesibilidad. <br/> (**Nota**: el dispositivo está equipado con ruedas y un asa para poder moverlo).
   - **Contactos de migración clave**: Este formulario no se rellena previamente. Los campos son editables. Se puede añadir más de una persona.
   - **Configuración de red del centro de datos**: Proporciona detalles sobre la configuración de red para el suministro previo del puerto Eth3 en el dispositivo MDMS.
   - **Destino de la descarga de datos**: Seleccione la cuenta de destino de la lista.
   - **Nombre de la solicitud**: Especifique un nombre para realizar el seguimiento del pedido.
5. Marque el recuadro de selección **He leído y acepto los términos del Acuerdo de migración de datos masiva** después de leer los acuerdos de servicio proporcionados.
6. Pulse **Realizar solicitud** para enviar la solicitud. Pulse **Cancelar** para abandonar completamente el formulario y volver a la página de destino de MDMS.

## Paso 2: Preparación y envío
{: #prep-ship}

Después de enviar la solicitud, el estado de la incidencia de la solicitud aparece como *Procesando solicitud*. Una vez que se haya procesado la solicitud, {{site.data.keyword.IBM}} empieza a preconfigurar el siguiente dispositivo disponible y el estado en la cuadrícula [Solicitudes ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://control.softlayer.com/storage/mdms){:new_window} aparecerá como *Preparando dispositivo* seguido de *Esperando envío*. Después de pasar al estado *Pendiente de envío*, la solicitud ya no puede cancelarse. 

El transportista recoge el dispositivo que se debe enviar a su ubicación. En este momento, el estado de la solicitud se actualiza a *Dispositivo enviado*. Se le proporciona el número de seguimiento en el apartado **Detalles de la solicitud** de la cuadrícula [Solicitudes ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://control.softlayer.com/storage/mdms){:new_window}.

## Paso 3: Recepción y conexión
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

### Visión general

El dispositivo de migración de datos masiva de {{site.data.keyword.cloud}} es un dispositivo de almacenamiento portátil que puede presentar recursos compartidos montables NFS (Network File System) o CFS (Content Federations Services) de FileNet y que se gestiona mediante una interfaz de navegador web. El dispositivo se envía al centro de datos, cargado con datos en el sitio y se devuelve a un centro de datos de {{site.data.keyword.BluSoftlayer_full}} y sus datos se carga en la cuenta de {{site.data.keyword.cos_full}}.

### Alimentación

El dispositivo incluye un cable de alimentación C13-US ([IEC 60320 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://en.wikipedia.org/wiki/IEC_60320){:new_window}). Si se utiliza el dispositivo fuera de Estados Unidos, es posible que sea necesario un adaptador de alimentación.

El dispositivo MDMS acepta todos los rangos de alimentación estándar. ![Rango de alimentación](/images/PowerRating.png)

### Conectividad Ethernet

Deben hacerse dos conexiones Ethernet. Una para la gestión de dispositivos mediante un navegador y otra para el traslado de datos en la misma subred en la que residen los datos de origen.

Ambos puertos se originan en el mismo dispositivo que los cables RJ45, y se suministran los cables CAT6A. Se proporcionan los adaptadores de cobre SFP+ para realizar las conversiones desde RJ45. Los adaptadores funcionan con todos los fabricantes de conmutadores. Dichos adaptadores están ubicados en un bolsillo de la parte inferior de la tapa de envío.

- Eth1 (1 GbE-B) se utiliza para la gestión de dispositivos y, por lo tanto, debe tener una pasarela especificada en la configuración de direcciones IP. Esto puede verse en la pantalla LCD después de que el dispositivo se encienda (consulte la sección [Configuración de dirección IP](#ip_cfg)).

- Eth3 (10 GbE-B) se utiliza para la transferencia de datos. Dicha conexión debe estar en la misma subred que los datos de origen o puede conectarse directamente al servidor si es necesario.

Si se requiere un factor de forma diferente de conexión Ethernet, debe proporcionar el conversor.

### Instrucciones paso a paso para el usuario

1. El dispositivo MDMS llega preconfigurado con su dirección IP, nombre de usuario, agrupación de almacenamiento bloqueado y recurso compartido NFS. La contraseña de usuario y la contraseña de agrupación de almacenamiento se comunicarán en otro correo electrónico.

2. Determine el lugar más adecuado para colocar el dispositivo; donde lleguen tanto la alimentación como las conexiones Ethernet (1 GbE y 10 GbE) y donde pase el mínimo de gente cerca.

3. Coloque el dispositivo para conectarlo. Puede permanecer en el maletín de transporte durante su uso. Asegúrese de que el dispositivo esté a temperatura ambiente y de que no haya condensación en él. Conecte el dispositivo a la corriente mediante el cable de alimentación proporcionado debajo de la tapa del compartimento. Encienda el dispositivo.<br/>
    **Nota**: hay dos interruptores de alimentación. ![Interruptores de alimentación](/images/MDMSPowerSwitch.png)
    **Nota**: no es necesario que el dispositivo se extraiga del compartimento portátil.

4. Extraiga el cable CAT6A de la tapa del compartimento y conéctelo al puerto Eth3 (10 GbE-B) que se muestra en la imagen.
    ![Ubicación de los puertos Eth1 y Eth3](/images/MDMSNewEth1and3.png)

5. Conecte el adaptador de CAT6A a SFP proporcionado y conecte el conmutador de 10 Gb.

6. Si se puede llegar a la dirección IP configurada para Eth3 mediante un navegador `https://<your_Eth3_IP_Address>`, vaya al siguiente paso. 

   De lo contrario, conéctelo en el puerto Eth1 (1 GbE-B). Abra el navegador y escriba `https://<your_Eth1_IP_Address>`. Especifique la dirección IP de Eth1 adecuada para su configuración de red. Acepte la excepción de certificado.<br/>
   **Nota**: Si tiene que modificar los valores de IP para Eth3 o Eth1, consulte la sección [Configuración de dirección IP](#ip_cfg).

7. Utilice el nombre de usuario y la contraseña proporcionados para iniciar la sesión.<br/>
    ![Página de inicio de sesión](/images/Login.png)

8. El asistente de flujo presenta el acceso a los temas específicos utilizados habitualmente ordenados de izquierda a derecha.<br/>
    ![Iconos de flujo de trabajos](/images/workflow.png) <br/>
    **NOTA**: El flujo de trabajo se puede reabrir con **Gestor de trabajo** de la parte superior izquierda de la GUI.

9. Active la agrupación de almacenamiento preconfigurado:
    - Pulse **Desbloquear e iniciar agrupación de almacenamiento**.
    - Escriba la contraseña de la agrupación de almacenamiento y pulse **Aceptar**.
    ![Activar agrupación de almacenamiento](/images/UnlockPool.png)

10. De forma predeterminada, el recurso compartido tiene habilitados los protocolos NFS y SMB sin restricciones de acceso al recurso compartido. Para restringir el acceso a este recurso compartido (para NFS o SMB), pulse con el botón derecho del ratón el nombre del recurso compartido y seleccione el elemento de menú correspondiente.<br/>
    ![Restringir el acceso al recurso compartido](/images/ShareControls.png)

11. Cuando la agrupación de almacenamiento esté habilitada, el recurso compartido NFS está disponible para montar. En el flujo de trabajo, pulse **Ver recursos compartidos de red** para ver la vista de recursos compartidos de red. Cierre el flujo de trabajo, pulse con el botón derecho del ratón el recurso compartido y seleccione **Ver mandato de montaje** para ver el nombre del recurso compartido y la información de montaje. Monte el recurso compartido en el servidor. Asegúrese de especificar la dirección IP del enlace de 10 GB al montar el recurso compartido.
    ![Montaje del recurso compartido](/images/MountCommand.png)

## Paso 4: Copia de datos y envío
{: #copy-ship}

<!-- &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&

1. Run the DataShuttle copy to move the data. **[Editor's note: What is "DataShuttle"? Is "DataShuttle copy" a command that is run on PDA?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& -->

1. Copie los datos en el recurso compartido NFS. Elija uno de los métodos siguientes para extraer los datos de su base de datos Netezza:
    1. Ejecute el ejemplo siguiente de la utilidad **nz_backup**:

       `/nz/support/contrib/bin/nz_backup –db <db_name> –d <target_directory>  ascii threads 4`

       **Nota**: `<target_directory>` es el recurso compartido NFS en el dispositivo MDMS que se monta en el servidor Netezza.
   
    2. Ejecute el ejemplo siguiente de sentencia CREATE EXTERNAL TABLE:

       `CREATE EXTERNAL TABLE '<path_to_mdms_device>/<file_name>' SELECT * FROM <table name>`

       **Nota:** Si ha utilizado las opciones de la cláusula `USING` para la exportación de datos, recuerde o guarde las opciones de cláusula. La cláusula se reutilizará más tarde durante el proceso de carga de la tabla externa desde IBM Cloud Object Storage.

       Para obtener más información sobre la sentencia SQL, consulte: [Sentencia CREATE EXTERNAL TABLE ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.sql.ref.doc/doc/r_create_ext_table.html){:new_window}. 

<!--       - Provide the {{site.data.keyword.Bluemix_notm}} team with the "USING" clause that was used for data export. The clause is reused during the load process on {{site.data.keyword.Bluemix_notm}}.
       - Select FORMAT = "Text"
-->

2. En el flujo de trabajo, pulse **Ver actividad de red** para mostrar la carga de entrada de Ethernet en la GUI a medida que se transfieren datos al dispositivo en el enlace de 10 Gb/seg.
    ![Ver actividad](/images/UserGuide13.png)

3. En el flujo de trabajo, pulse **Ver agrupaciones de almacenamiento** para supervisar el uso de almacenamiento en el dispositivo.
    ![Ver agrupaciones de almacenamiento](/images/UserGuide14.png)

4. Cuando haya finalizado la copia, apague correctamente el sistema. Al apagar el sistema, también se bloquea la agrupación de almacenamiento. En el flujo de trabajo, pulse **Cerrar dispositivo...**.  
    ![Ubicación del botón de la IU de apagado del dispositivo](/images/Shutdown.png)

5. Desconecte el dispositivo. Devuelva el cable de alimentación, el cable Ethernet y el adaptador de SFP+ en sus respectivas ubicaciones de almacenamiento debajo de la tapa.

6. Adjunte la etiqueta de envío al dispositivo. Avise al expedidor y devuelva el dispositivo al centro de datos de {{site.data.keyword.BluSoftlayer_full}}. Al llegar al centro de datos, los datos se cargan en su grupo de {{site.data.keyword.cos_full_notm}}.

Una vez que se devuelve el dispositivo al equipo de {{site.data.keyword.BluSoftlayer}}, el estado de la solicitud cambia a *Dispositivo recibido*.

## Paso 5: Descarga y acceso
{: #offload}

Durante el proceso de transferencia de datos, el estado de la solicitud se muestra como *Descargando datos*. El estado cambia de nuevo cuando finaliza la migración al grupo de {{site.data.keyword.objectstorageshort}} (*Descarga completada*). Se podrá acceder a los datos inmediatamente cuando se haya completado la descarga de alta velocidad al grupo de Cloud Object Storage. 

Cuando la migración de los datos en el grupo de Cloud Object Storage se haya completado, puede continuar para [importar los datos en la base de datos de {{site.data.keyword.dashdbshort_notm}}](#import).

## Paso 6: Importación de datos desde IBM Cloud Object Storage
{: #import}

Para cargar datos desde IBM Cloud Object Storage utilizando Tablas externas directamente, a continuación se muestra una sentencia SQL de ejemplo:

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
* Asegúrese de utilizar las mismas opciones de cláusula `USING` que ha utilizado para extraer los datos desde la base de datos de PureData System for Analytics (Netezza) utilizando la sentencia CREATE EXTERNAL TABLE.
* Para IBM Cloud Object Storage, para crear las credenciales de HMAC al crear las nuevas credenciales de servicio, especifique {"HMAC:true"} en el campo *Añadir parámetros de configuración en línea*.

Para obtener una guía de aprendizaje guiada sobre la importación de datos desde IBM Cloud Object Storage, consulte: [Demostración guiada de IBM Db2 Warehouse on Cloud: Explorar datos cargando ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud/){:new_window}.

## Paso 7: Borrado del dispositivo MDMS
{: #erase}

{{site.data.keyword.IBM}} implementa una limpieza de datos que cumple los requisitos del Departamento de Defensa de EE.UU. para borrar de forma permanente los datos del dispositivo MDMS. Cuando haya terminado, el estado de la solicitud es *Borrado completo*.

## Notas adicionales
{: #notes}

### Exclusividad en el grupo

Para garantizar que los nombres de objetos son únicos cuando se copian en el grupo, la vía de acceso de archivo se incluye como prefijo del nombre de objeto. Por ejemplo, el archivo config.ini de la carpeta `/root/user/` se renombra a "root/user/config.ini" cuando se copia en el grupo.

### Grupos

Si el grupo de destino no existe, se crea. Si existe, debe estar vacío; de lo contrario la copia no puede continuar.

### Sistemas de archivos

Los enlaces simbólicos y los enlaces fijos se omiten durante el proceso de exploración.

### Configuración de dirección IP
{: #ip_cfg}

La pantalla LCD del dispositivo se puede utilizar para configurar las direcciones IP de los puertos Ethernet. Puede navegar por la pantalla LCD utilizando los botones de **flecha arriba**, **flecha abajo**, **esc** y **entrar**. Con el botón **entrar** se accede a un menú y con el botón **esc**, se sale del menú.

![Pantalla LCD](/images/MDMSLCD.png)

Al editar una dirección IP o máscara de subred, el botón **entrar** hace avanzar un carácter cada vez; el botón **esc** hace retroceder un paso cada vez. Los botones de **flecha arriba** y **flecha abajo** permiten desplazarse por los números de la ubicación seleccionada.

Utilice **esc** para volver al menú anterior.  

Vaya al elemento de menú **Actualizar...** y pulse **entrar** para guardar los valores.
