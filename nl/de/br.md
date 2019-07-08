---

copyright:
  years: 2014, 2019
lastupdated: "2019-05-21"

keywords:

subcollection: Db2whc

---

<!-- Attribute definitions --> 
{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}

# Sicherung und Wiederherstellung
{: #br}

Eine verschlüsselte Sicherung für die vollständige {{site.data.keyword.dashdbshort_notm}}-Datenbank wird einmal pro Tag ausgeführt.
{: shortdesc}

| Plan              | Häufigkeit der Sicherung | Anzahl der aufbewahrten Sicherungen | Sicherungsaufbewahrungszeitraum   | Self-Service |
|-------------------|------------------|----------------------------|---------------------------|--------------|
| MPP               | 1 / Tag          | 2                          | 2 Tage; FIFO* Rollover   | Nein           |
| Flex              | 1 / Tag          | bis zu 7                   | 7 Tage; FIFO* Rollover   | Ja          |
| Flex Performance  | 1 / Tag          | bis zu 7                   | 7 Tage; FIFO* Rollover   | Ja          |
{: caption="Tabelle 1. Häufigkeit der Sicherung und Aufbewahrung" caption-side="top"}

*First in, First out

## SMP- und MPP-Pläne
{: #smp_mpp}

Es werden die letzten 2 täglichen Sicherungen aufbewahrt.

Es werden die aufbewahrten Sicherungen ausschließlich von IBM verwendet, um im Falle einer Katastrophe oder eines Systemausfalls eine Systemwiederherstellung durchzuführen. Eine Anforderung zur Wiederherstellung Ihrer Datenbank wird nicht unterstützt. Sie können die Daten mithilfe von Db2-Tools wie IBM Data Studio oder mit dem Befehl **db2 export** exportieren. 

## Flex- und Flex Performance-Pläne
{: #flex}

Es werden bis zu 7 der letzten täglichen Sicherungsmomentaufnahmen aufbewahrt. Die Anzahl der bis zu einem Maximum von 7 aufbewahrten Momentaufnahmen hängt von der Größe der einzelnen Momentaufnahmen ab (ebenso von der Menge an Daten, die zwischen den einzelnen Momentaufnahmen nach der ersten Momentaufnahme geändert wurden) und von der Speicherkapazität für aufbewahrte Sicherungen. 

Mit der {{site.data.keyword.dashdbshort_notm}}-Konsole können Sie die Sicherungen so terminieren, dass sie zu dem am besten geeigneten Zeitpunkt ausgeführt werden, und Sie können die Datenbank auf der Basis jeder beliebigen aufbewahrten Sicherungsmomentaufnahme zu jedem beliebigen Zeitpunkt wiederherstellen. Das System ist während des Wiederherstellungszeitraums inaktiv. Sie erhalten eine Benachrichtigungs-E-Mail, wenn die Wiederherstellungsoperation abgeschlossen ist.

![Ansicht der Webkonsolenseite für Sicherung und Wiederherstellung](images/br.png)

