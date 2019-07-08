---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# SSL(Secure Sockets Layer) 지원
{: #ssl_support}

{{site.data.keyword.dashdbshort_notm}} 데이터베이스는 서드파티 디지털 인증 기관(CA)에서 발행하는 SSL 연결을 위한 인증서를 사용합니다. 
{: shortdesc}

CA 인증서는 Db2 드라이버 패키지의 일부입니다. 애플리케이션이 Db2 드라이버 패키지의 드라이버와 연결되는 경우 인증서를 별도로 다운로드할 필요가 없습니다. 웹 콘솔에서 Db2 드라이버 패키지를 다운로드할 수 있습니다.

그러나 애플리케이션에 고유의 드라이버가 있는 경우 인증서를 별도로 다운로드해야 할 수 있습니다. 웹 콘솔에서 인증서를 다운로드할 수 있습니다.

SSL(Secure Sockets Layer)은 통신 개인정보 보호를 제공하는 보안 프로토콜입니다. SSL을 사용하면 클라이언트 및 서버 애플리케이션이 도청, 위조 및 메시지 조작을 방지하기 위해 설계된 방식으로 통신할 수 있습니다. SSL 사용 클라이언트 애플리케이션은 표준 암호화 기술을 사용하여 보안 통신을 수행합니다.

SSL을 사용하여 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하도록 애플리케이션을 구성하는 것은 회사 정책에 따라 다릅니다. 데이터베이스에 연결하는 데 사용할 수 있는 표준 및 SSL 프로토콜 모두 사용자 이름 및 비밀번호를 암호화된 데이터로 전송합니다. 완전한 엔드-투-엔드 보안을 보장하려면 민감한 데이터 및 메타데이터를 포함하여 모든 데이터베이스 정보를 SSL 연결을 통해 전송하십시오. 관리자는 웹 콘솔에서 설정을 변경하여 SSL 연결을 필수로 설정할 수 있습니다.


