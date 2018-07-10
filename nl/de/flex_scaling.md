---

copyright:
  years: 2014, 2018
lastupdated: "2018-05-01"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Flexible Skalierung
{: #scale}

Der Flex Performance-Plan bietet eine unabhängige Skalierung von Speicher und Prozessorkernen.
{: shortdesc}

Passen Sie vor der Bereitstellung des Flex Performance-Systems die voraussichtlich benötigten Speicherkapazitäten und Prozessorkerne an und übergeben Sie dann Ihre Auswahl.


Wenn sich nach der Bereitstellung des Systems die Anforderungen ändern, können Sie die Prozessorkerne skalieren und die Speicherkapazität erhöhen, indem Sie **Instanz skalieren** auf der Service-Seite **Verwalten** den Schieberegler verwenden.

![Ansicht der Seite mit den Prozessorkernen der Webkonsole](images/launch.png)

![Ansicht der Seite mit den Prozessorkernen der Webkonsole](images/scaling_full.png)


## Prozessorkerne
{: #cores}

Sie können Ihre Prozessorkerne nach oben oder unten skalieren. Eine Änderung bei den Prozessorkernen bewirkt eine kurze Systemausfallzeit von bis zu 45 Minuten. Sie können die Ausfallzeit so terminieren, dass sie in einen geeigneteren Zeitraum fällt, oder die Änderung der Prozessorkerne sofort starten.

![Ansicht der Seite mit den Prozessorkernen der Webkonsole](images/cores.png)

## Speicher
{: #storage}

Sie können Ihre Speicherkapazität erhöhen. Bei Speicheränderungen treten keine Ausfallzeiten auf.

![Ansicht der Seite mit der Speicherkapazität für die Webkonsole](images/storage.png)

## Hauptspeicher
{: #ram}

RAM wird mit einem festen Quotienten proportional zugeordnet, wenn die Anzahl der Prozessorkerne geändert wird.

