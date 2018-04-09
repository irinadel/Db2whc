---

copyright:
  years: 2014, 2018
lastupdated: "2018-03-16"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Copia de seguridad y restauración
{: #br}

Una vez al día se realiza una copia de seguridad cifrada en la base de datos de {{site.data.keyword.dashdbshort_notm}}. Para el plan
de Flex Performance, se retienen las 7 últimas instantáneas de las copias de seguridad diarias. Para los planes de SMP y MPP, se retienen las 2 últimas copias de seguridad diarias.
{: shortdesc}

En el plan de Flex Performance, puede programar que sus copias de seguridad se ejecuten cuando sea más conveniente y puede restaurar la base de datos desde cualquier instancia de copia de seguridad retenida en el momento que quiera. El sistema cae durante el periodo de restauración. Se enviará un correo electrónico para notificar que se ha completado la operación de restauración.

En el caso de los planes de SMP y MPP, IBM utiliza las copias de seguridad retenidas exclusivamente para fines de recuperación en el caso de desastre o de pérdidas en el sistema. No se admiten las solicitudes para restaurar bases de datos a partir de una copia de seguridad. Puede exportar sus datos mediante herramientas Db2 como IBM Data Studio o el mandato **db2 export**. 
