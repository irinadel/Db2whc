---

copyright:
  years: 2014, 2018
lastupdated: "2018-09-25"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Mac OS X에서 드라이버 패키지 설치

`installDSDriver.sh` 스크립트를 사용하여 Mac OS X에서 {{site.data.keyword.dashdbshort_notm}} 드라이버 패키지를 설치할 수 있습니다.
{: shortdesc}

## 전제조건

{{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하기 전에 먼저 필수 [전제조건](connecting.html#prereqs)이 있는지 확인하십시오.

<!-- Download the Db2 driver package for your operating system from the web console and install it. -->

## 프로시저

- **새로 설치하는 경우**

  1. `macos_dsdriver.dmg` 파일을 두 번 클릭하여 디스크 이미지를 마운트하십시오.
   
     디스크 이미지의 컨텐츠가 있는 새 **파인더** 창이 열립니다.

     **파인더** 창이 열리지 않으면 데스크탑에 있는 `macos_dsdriver` 아이콘을 두 번 클릭하십시오.
  2. **파인더** 창에서 `installDSDriver.sh` 파일을 두 번 클릭하십시오.

     드라이버 패키지는 기본 위치에 설치됩니다. `/Applications/dsdriver`

- **기존 드라이버 패키지 설치에 대한 업데이트인 경우**

  1. 현재 구성 파일을 백업하십시오.

     a. `Applications/dsdriver/cfg` 폴더로 이동하십시오.

     b. 다음 파일을 다른 폴더에 복사하십시오. 
    
        `db2cli.ini`

        `db2dsdriver.cfg`
  2. `dsdriver` 폴더를 두 번 클릭하고 **휴지통으로 이동**을 선택하여 현재 설치된 드라이버 패키지를 제거하십시오.
  3. 앞의 **새로 설치하는 경우** 섹션에서 설명한 대로 새 드라이버 패키지를 설치하십시오.
     
     a. `macos_dsdriver.dmg` 파일을 두 번 클릭하여 디스크 이미지를 마운트하십시오.
     b. **파인더** 창에서 `installDSDriver.sh` 파일을 두 번 클릭하십시오.
  4. 구성 파일을 복원하십시오.

     1단게에서 저장한 `db2cli.ini` 및 `db2dsdriver.cfg` 파일을 `/Applications/dsdriver/cfg` 폴더에 복사하십시오.

## 다음에 수행할 작업

로컬 애플리케이션 또는 클라이언트 도구를 {{site.data.keyword.dashdbshort_notm}} 데이터베이스에 연결하려면 [로컬 환경을 구성](driver_pkg_cfg.html)하십시오.
