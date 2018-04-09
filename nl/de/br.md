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

# Sicherung und Wiederherstellung
{: #br}

Eine verschlüsselte Sicherung für die vollständige {{site.data.keyword.dashdbshort_notm}}-Datenbank wird einmal pro Tag ausgeführt. Im Rahmen des Flex Performance-Plans werden die letzten 7 täglichen Sicherungsmomentaufnahmen aufbewahrt. Im Rahmen des SMP- und des MPP-Plans werden die letzten 2 täglichen Sicherungen aufbewahrt.
{: shortdesc}

Im Rahmen des Flex Performance-Plans können Sie die Sicherungen so terminieren, dass sie zu dem am besten geeigneten Zeitpunkt ausgeführt werden, und Sie können die Datenbank auf der Basis jeder beliebigen aufbewahrten Sicherungsmomentaufnahme zu jedem beliebigen Zeitpunkt wiederherstellen. Das System ist während des Wiederherstellungszeitraums inaktiv. Sie erhalten eine Benachrichtigungs-E-Mail, wenn die Wiederherstellungsoperation abgeschlossen ist.

Im Rahmen des SMP- und des MPP-Plans werden die aufbewahrten Sicherungen ausschließlich von IBM verwendet, um im Falle einer Katastrophe oder eines Systemausfalls eine Systemwiederherstellung durchzuführen. Eine Anforderung zur Wiederherstellung Ihrer Datenbank wird nicht unterstützt. Sie können die Daten mithilfe von Db2-Tools wie IBM Data Studio oder mit dem Befehl **db2 export** exportieren. 
