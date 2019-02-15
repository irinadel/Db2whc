---

copyright:
  years: 2014, 2019
lastupdated: "2018-05-10"

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

# Copia de seguridad y restauración
{: #br}

Una vez al día se realiza una copia de seguridad cifrada en la base de datos de {{site.data.keyword.dashdbshort_notm}}.
{: shortdesc}

| Plan              | Frecuencia de copia de seguridad | Número de copias de seguridad retenidas | Periodo de retención de copia de seguridad   | Autoservicio |
|-------------------|------------------|----------------------------|---------------------------|--------------|
| MPP               | 1 / día          | 2                          | 2 días; renovación de FIFO*   | No           |
| Flex Performance  | 1 / día          | 7                          | 7 días; renovación de FIFO*   | Sí          |
{: caption="Tabla 1. Frecuencia y retención de copia de seguridad" caption-side="top"}

*Primero en entrar, primero en salir

## Planes de SMP y MPP
{: #smp_mpp}

Se retienen las 2 últimas copias de seguridad diarias.

IBM utiliza las copias de seguridad retenidas exclusivamente para fines de recuperación en el caso de desastre o de pérdidas en el sistema. No se admiten las solicitudes para restaurar bases de datos a partir de una copia de seguridad. Puede exportar sus datos mediante herramientas Db2 como IBM Data Studio o el mandato **db2 export**. 

## Plan Flex Performance
{: #flex}

Se retienen las 7 últimas instantáneas de copia de seguridad.

Desde la consola de {{site.data.keyword.dashdbshort_notm}}, puede programar que sus copias de seguridad se ejecuten cuando sea más conveniente y puede restaurar la base de datos desde cualquier instancia de copia de seguridad retenida en el momento que quiera. El sistema cae durante el periodo de restauración. Se enviará un correo electrónico para notificar que se ha completado la operación de restauración.

![Vista de la copia de seguridad de la consola web y de la página de restauración](images/br.png)

