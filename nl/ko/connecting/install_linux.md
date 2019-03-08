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

# Linux 또는 PowerLinux에서 드라이버 패키지 설치
{: #install_dr_pkg_linux}

`installDSDriver`를 사용하여 Linux 또는 PowerLinux에서 {{site.data.keyword.dashdbshort_notm}} 드라이버 패키지를 설치할 수 있습니다. 
{: shortdesc}

## 전제조건
{: #prereq31}

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](/docs/services/Db2whc/connecting/connecting.html#prereqs)이 있는지 확인하십시오.

<!-- Download the Db2 driver package for your operating system from the web console and install it. -->

**PowerLinux의 경우에만** 다음 단계를 완료하여 XL C/C++ 컴파일러 런타임 패키지를 설치하십시오.

1. FTP 사이트에서 XL C/C++ 컴파일러 런타임 패키지를 다운로드하십시오. 예를 들어, **wget** 도구를 사용하여 Linux 리틀 엔디언 Ubuntu 14용 런타임 패키지를 다운로드하려면 다음 명령을 실행하십시오. 

   `wget ftp://public.dhe.ibm.com/software/server/POWER/Linux/rte/xlcpp/le/ubuntu/dists/trusty/main/binary-ppc64el/*`
2. 다음 명령을 실행하여 런타임 패키지를 설치하십시오.

   `sudo dpkg -iG *.deb` 

## 프로시저
{: #proc31}

1. 이전에 다운로드한 압축 드라이버 패키지 파일의 압축을 푸십시오.

   예: 

   `gunzip file_name.tar.gz`

   `tar -xvf file_name.tar`

    `dsdriver` 서브디렉토리가 압축 풀기 명령을 실행한 디렉토리에 작성됩니다.
2. Java 및 ODBC/CLI 드라이버의 압축을 푸십시오.

   a. `dsdriver` 서브디렉토리에서 **installDSDriver** 명령을 실행하십시오.
   
   **installDSDriver** 명령은 `dsdriver` 디렉토리에 `db2profile` 및 `db2cshrc` 스크립트 파일을 작성합니다.

   b. 쉘 환경에 따라 다음 스크립트 파일 중 하나를 실행하십시오.

   - **Bash 또는 Korn 쉘**: `source db2profile`
   - **C 쉘**: `source db2cshrc`

## 다음에 수행할 작업
{: #wn}

로컬 애플리케이션 또는 클라이언트 도구를 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하려면 [로컬 환경을 구성](/docs/services/Db2whc/connecting/driver_pkg_cfg.html)하십시오.   




