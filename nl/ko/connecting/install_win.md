---

copyright:
  years: 2014, 2019
lastupdated: "2018-09-25"

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

# Windows에서 드라이버 패키지 설치
{: #install_dr_pkg_windows}

설치 프로그램을 사용하여 Windows에서 {{site.data.keyword.dashdbshort_notm}} 드라이버 패키지를 설치할 수 있습니다. 
{: shortdesc}

## 전제조건

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](connecting.html#prereqs)이 있는지 확인하십시오.

<!-- Download the driver package for your operating system from the web console and install it. -->

## 프로시저

1. 관리자로서 다운로드한 실행 파일을 실행하십시오.

   드라이버 패키지의 기본 설치 경로는 다음과 같습니다. `Program Files\IBM\IBM DATA SERVER DRIVER`
2. [*선택사항*] 드라이버 패키지 설치 디렉토리의 `bin` 서브디렉토리를 `%PATH%` 환경 변수에 추가하십시오(명령 실행 파일의 전체 경로를 지정하지 않고 **db2cli** 명령을 실행할 수 있음).

## 다음에 수행할 작업

로컬 애플리케이션 또는 클라이언트 도구를 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하려면 [로컬 환경을 구성](driver_pkg_cfg.html)하십시오.
