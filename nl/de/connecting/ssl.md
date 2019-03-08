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

# SSL-Unterstützung
{: #ssl_support}

Die {{site.data.keyword.dashdbshort_notm}}-Datenbank verwendet ein Zertifikat für SSL-Verbindungen (SSL = Secure Sockets Layer), das von einer Drittanbieter-Zertifizierungsstelle ausgegeben wurde. 
{: shortdesc}

Das CA-Zertifikat ist Bestandteil des Db2-Treiberpakets. Stellt Ihre Anwendung die Verbindung über einen Treiber des Db2-Treiberpakets her, ist ein separates Herunterladen des Zertifikats nicht erforderlich. Das Db2-Treiberpaket können Sie über die Webkonsole herunterladen.

Verfügt Ihre Anwendung jedoch über einen eigenen Treiber, müssen Sie das Zertifikat möglicherweise separat herunterladen. Das Zertifikat können Sie über die Webkonsole herunterladen.

Bei SSL (Secure Sockets Layer) handelt es sich um ein Sicherheitsprotokoll für den Datenschutz bei der Kommunikation. SSL ermöglicht einen Datenaustausch zwischen Client- und Serveranwendungen, der einen Schutz vor dem Ausspionieren, Manipulieren und Fälschen von Nachrichten bietet. SSL-fähige Clientanwendungen unterstützen eine sichere Kommunikation mithilfe von Standardverschlüsselungsverfahren.

Die Konfiguration Ihrer Anwendung für SSL-Verbindungen zur {{site.data.keyword.dashdbshort_notm}}-Datenbank richtet sich nach Ihrer Unternehmensrichtlinie. Sowohl bei den Standardprotokollen als auch bei den SSL-Protokollen, die Sie für die Verbindung zur Datenbank verwenden können, werden Benutzernamen und Kennwörter als verschlüsselte Daten übertragen. Wenn Sie eine vollständige End-to-End-Sicherheit sicherstellen möchten, müssen alle Datenbankinformationen, sensible Daten und Metadaten eingeschlossen, über eine SSL-Verbindung übertragen werden. Administratoren können SSL-Verbindungen durch die Änderung einer Webkonsoleneinstellung vorschreiben.


