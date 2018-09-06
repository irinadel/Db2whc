---

copyright:
  years: 2014, 2018
lastupdated: "2018-06-15"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# IBM PureData System for Analytics(Netezza)에서 마이그레이션
{: #pda}

{{site.data.keyword.Bluemix_notm}} 대량 데이터 마이그레이션 서비스(MDMS)는 25TB 이상의 대형 IBM PureData Systems for Analytics(Netezza) 데이터베이스에서 {{site.data.keyword.Bluemix_notm}}의 완전히 관리되는 {{site.data.keyword.dashdblong}} 데이터베이스로 데이터를 마이그레이션하는 데 사용될 수 있습니다.

MDMS는 테라바이트에서 페타바이트까지의 데이터를 {{site.data.keyword.Bluemix_notm}}에 물리적으로 전송하는 빠르고 단순하고 안전한 방법을 제공합니다. MDMS는 120TB의 사용 가능한 스토리지 용량이 있는 모바일 스토리지 디바이스입니다. 이 디바이스를 사용하면 높은 비용, 긴 전송 시간 및 보안 문제와 같은 일반적인 전송의 어려움을 단일 서비스 내에서 모두 해결할 수 있습니다.
{: shortdesc}

![대량 데이터 마이그레이션 서비스 디바이스의 보기](images/mdms.svg)

## 디바이스를 요청할 때 필요한 사항
{: #prereq}

1. 스토리지 디바이스에 대한 네트워크 설정
   - 정적 IP 주소
   - 데이터 전송을 위한 넷마스크
2. 원격 컴퓨터에 대한 네트워크 설정
   - 정적 IP 주소
   - 넷마스크 
   - 사용자 인터페이스(UI)에 액세스하기 위한 기본 게이트웨이
3. Cloud Object Storage 다운로드 대상 <br/>
   **중요**: 요청 양식을 완료하려면 US Cross Region 또는 US South 위치에 하나 이상의 {{site.data.keyword.cos_full}} 계정 및 하나의 버킷이 있어야 합니다. 아직 {{site.data.keyword.cos_full_notm}}} 계정이 없는 경우, MDMS 디바이스를 요청하기 전에 먼저 계정을 작성하십시오. 자세한 정보는 [{{site.data.keyword.cos_full}} 정보](/docs/services/cloud-object-storage/about-cos.html){:new_window}를 참조하십시오.

## 1단계: 요청 작성
{: #create-req}

1. 고유 신임 정보를 사용하여 [{{site.data.keyword.slportal}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/){:new_window}에 로그인하십시오.
2. 탐색줄에서 **스토리지 > 데이터 마이그레이션 > 대량 데이터 마이그레이션**을 선택하여 MDMS 랜딩 페이지에 액세스하십시오.
3. **디바이스 요청**을 클릭하여 주문 양식을 여십시오.
4. **대량 데이터 마이그레이션** 주문 양식에서 각 필드를 완료하십시오.
   - **발송 주소**: 이 양식은 미리 채워져 있지 않으며 각 필드는 편집 가능합니다. 주의 필드에 디바이스를 전달받을 사람의 이름을 입력하십시오. 전달 위치를 선택할 때 디바이스의 중량(케이스를 포함하여 30kg(66lb)) 및 접근성을 고려하십시오. <br/> (**참고**: 디바이스에는 이동에 필요한 바퀴 및 팝업 핸들이 있습니다.)
   - **핵심 마이그레이션 담당자**: 이 양식은 미리 채워져 있지 않습니다. 각 필드는 편집 가능합니다. 두 명 이상의 사람만 추가될 수 있습니다.
   - **데이터 센터 네트워크 구성**: 발송 전에 MDMS 디바이스에서 Eth3 포트를 사전프로비저닝할 수 있도록 네트워크 구성 세부사항을 입력하십시오.
   - **데이터 오프로드 대상**: 목록에서 기존 대상 계정을 선택하십시오.
   - **요청 이름**: 주문을 추적하는 데 도움이 될 이름을 입력하십시오.
5. 제공되는 각 서비스 계약을 읽은 후에 **대량 데이터 마이그레이션 계약의 전체 이용 약관을 읽고 이에 동의합니다.** 선택란을 선택하십시오.
6. **요청하기**를 클릭하여 요청을 제출하십시오. 양식을 완전히 버리고 MDMS 랜딩 페이지로 돌아가려면 **취소**를 클릭하십시오.

## 2단계: 준비 및 발송
{: #prep-ship}

요청을 제출한 후에 요청 티켓의 상태는 *요청 처리 중*으로 표시됩니다. 요청이 처리되면 {{site.data.keyword.IBM}}에서 다음으로 사용 가능한 디바이스의 사전 구성을 시작하고 [요청 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/storage/mdms){:new_window} 그리드의 상태는 *디바이스 준비 중*을 표시하고 그 뒤에 *발송 대기 중*을 표시합니다. 요청이 *발송 대기 중* 상태가 되면 더 이상 취소할 수 없습니다. 

디바이스는 운송 업체에서 가져가서 사용자의 위치로 발송됩니다. 이 시점에서 요청 상태는 *디바이스가 발송됨*으로 업데이트됩니다. 추적 번호는 [요청 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/storage/mdms){:new_window} 그리드의 **주문 세부사항** 섹션에서 사용자와 공유됩니다.

## 3단계: 수령 및 연결
{: #rec-con}

<!-- **[Editor's note: What to keep from this section immediately below?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
1. The device arrives pre-configured for you. Basic [powering/connectivity instructions](docs/infrastructure/mass-data-migration/user-instructions.html) are included.  **[Editor's note: Are the instructions included in the MDMS package? If so, are they different from the instructions found with the "powering/connectivity" link?]**<br/>
  **Note**: User name and storage pool password is provided separately. Check the **Request Details** in your [Requests ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/storage/mdms){:new_window} grid for the credentials.
2. Point your browser to the static IP address that you provided in the order form. **[Editor's note: Is this done on PDA? What system is the static IP address for?]**
3. Log in. Enter password to unlock the empty storage pool. **[Editor's note: How is this done?]**<br/>
   **Note**: See the **Request Details** of your [Requests ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/storage/mdms){:new_window} grid for the password.
4. Mount the NFS share on your server. **[Editor's note: How is this done?]**
5. Rerun your DataShuttle inventory to ensure any new files are captured. **[Editor's note: Is "DataShuttle inventory" a command that is run on PDA?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& -->

### 개요

{{site.data.keyword.cloud}} 대량 데이터 마이그레이션 디바이스는 마운트할 수 있는 네트워크 파일 시스템(NFS) 또는 FileNet Content Federations Services(CFS) 공유를 나타낼 수 있는 휴대용 스토리지 디바이스이며 웹 브라우저 인터페이스를 통해 관리됩니다. 디바이스는 사용자의 데이터 센터로 발송되고 온사이트 데이터가 로드되어 {{site.data.keyword.BluSoftlayer_full}} 데이터 센터로 리턴되며 사용자의 데이터가 사용자의 {{site.data.keyword.cos_full}} 계정에 로드됩니다.

### 전원

디바이스에는 C13-US 전원 코드([IEC 60320 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://en.wikipedia.org/wiki/IEC_60320){:new_window})가 포함되어 있습니다. 디바이스가 미국 외부에서 사용되는 경우, 전원 어댑터가 필요할 수 있습니다.

MDMS 디바이스는 모든 표준 전원 범위를 허용합니다.
![전원 범위](/images/PowerRating.png)

### 이더넷 연결

두 가지의 이더넷 연결이 작성됩니다. 브라우저를 통해 디바이스를 관리하기 위해 하나가 작성되고 소스 데이터가 상주하는 서브넷과 동일한 서브넷에서 데이터를 이동하기 위해 하나가 작성됩니다.

RJ45 및 CAT6A 케이블이 제공되므로 두 포트 모두 디바이스에서 시작됩니다. RJ45에서 변환될 수 있도록 구리선 SFP+ 어댑터가 제공됩니다. 어댑터는 모든 스위치 제조업체와 호환됩니다. 이 어댑터는 화물 덮개 아래쪽 포켓에 있습니다.

- Eth1(1GbE-B)은 디바이스 관리에 사용되므로 IP 주소 구성에서 지정된 게이트웨이가 있어야 합니다. 이는 디바이스에 전원을 공급한 후에 LCD 화면에서 볼 수 있습니다([IP 주소 구성](#ip_cfg) 섹션을 참조하십시오).

- Eth3(10GbE-B)은 데이터 전송에 사용됩니다. 이 연결은 소스 데이터와 동일한 서브넷에 있거나 필요한 경우 서버에 직접 연결될 수 있습니다.

다른 폼 팩터의 이더넷 연결이 필요한 경우, 변환기를 제공해야 합니다.

### 단계별 사용자 지시사항

1. MDMS 디바이스는 사용자의 IP 주소, 사용자 이름, 잠긴 스토리지 풀 및 NFS 공유로 사전 구성되어 도착합니다. 사용자 비밀번호 및 스토리지 풀 비밀번호는 별도의 이메일을 통해 전달됩니다.

2. 디바이스를 배치할 가장 적절한 위치를 결정하십시오. 해당 위치는 전원 및 이더넷(1GbE 및 10GbE) 둘 다에 연결되어야 하며 최소한의 도보 범위여야 합니다.

3. 디바이스를 연결할 위치를 지정하십시오. 사용 중에는 운송 케이스에 둘 수 있습니다. 디바이스는 상온에 두어야 하며 표면에 응결이 없어야 합니다. 케이스 덮개 아래에서 제공되는 전원 케이블을 사용하여 전원에 연결하십시오. 디바이스 전원을 켜십시오.<br/>
    **참고**: 두 개의 전원 스위치가 있습니다.
    ![전원 스위치](/images/MDMSPowerSwitch.png)
    **참고**: 디바이스를 휴대용 케이스에서 제거할 필요는 없습니다.

4. 케이스 덮개에서 CAT6A 케이블을 제거하고 그림에 표시된 Eth3(10GbE-B) 포트로 연결하십시오.
    ![Eth1 및 Eth3 포트 위치](/images/MDMSNewEth1and3.png)

5. 제공된 CAT6A를 SFP+ 어댑터에 연결하고 사용자의 10Gb 스위치에 연결하십시오.

6. Eth3에 대해 구성된 IP 주소에 `https://<your_Eth3_IP_Address>` 브라우저를 통해 도달할 수 있는 경우, 다음 단계로 계속 진행하십시오. 

   그렇지 않으면 Eth1(1GbE-B) 포트에 연결하십시오. 브라우저를 열고 `https://<your_Eth1_IP_Address>`를 입력하십시오. 네트워크 구성에 적합한 Eth1 IP 주소를 입력하십시오. 인증서 예외를 허용하십시오.<br/>
   **참고**: Eth3 또는 Eth1에 대한 IP 설정을 변경해야 하는 경우, [IP 주소 구성](#ip_cfg) 섹션을 참조하십시오.

7. 제공된 사용자 이름 및 비밀번호를 사용하여 로그인하십시오.<br/>
    ![로그인 페이지](/images/Login.png)

8. 워크플로우 마법사는 일반적으로 왼쪽에서 오른쪽으로 사용되는 특정 항목에 대한 액세스를 표시합니다.<br/>
    ![워크플로우 아이콘](/images/workflow.png) <br/>
    **참고**: 워크플로우는 GUI의 왼쪽 상단에 있는 **워크플로우 관리자**를 사용하여 다시 열 수 있습니다.

9. 사전 구성된 스토리지 풀 활성화:
    - **스토리지 풀 잠금 해제 및 시작**을 클릭하십시오.
    - 스토리지 풀 비밀번호 문구를 입력하고 **확인**을 클릭하십시오.
    ![스토리지 풀 활성화](/images/UnlockPool.png)

10. 기본적으로 공유에는 공유에 부과된 액세스 제한사항 없이 사용 가능한 NFS 및 SMB 프로토콜이 둘 다 있습니다. NFS 또는 SMB의 경우, 이 공유에 대한 액세스를 제한하려면 마우스 오른쪽 단추로 공유 이름을 클릭하고 적절한 메뉴 항목을 선택하십시오.<br/>
    ![공유 액세스 제한](/images/ShareControls.png)

11. 스토리지 풀을 사용할 수 있는 경우, NFS 공유를 사용하여 마운트할 수 있습니다. 워크플로우에서 **네트워크 공유 보기**를 클릭하여 네트워크 공유 보기를 보십시오. 워크플로우를 닫고 마우스 오른쪽 단추로 공유를 클릭한 다음 **마운트 명령 보기**를 선택하여 공유 이름 및 마운트 정보를 보십시오. 공유를 소스 서버에 마운트하십시오. 공유를 마운트할 때 10GB 링크의 IP 주소를 지정해야 합니다.
    ![공유 마운트](/images/MountCommand.png)

## 4단계: 데이터 복사 및 발송
{: #copy-ship}

<!-- &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&

1. Run the DataShuttle copy to move the data. **[Editor's note: What is "DataShuttle"? Is "DataShuttle copy" a command that is run on PDA?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& -->

1. 데이터를 NFS 공유에 복사하십시오. 다음 방법 중 하나를 선택하여 Netezza 데이터베이스에서 데이터를 추출하십시오.
    1. **nz_backup** 유틸리티의 다음 예제 실행:

       `/nz/support/contrib/bin/nz_backup –db <db_name> –d <target_directory>  ascii threads 4`

       **참고**: `<target_directory>`는 사용자의 Netezza 서버에 마운트된 MDMS 디바이스의 NFS 공유입니다.
   
    2. CREATE EXTERNAL TABLE문의 다음 예제 실행:

       `CREATE EXTERNAL TABLE '<path_to_mdms_device>/<file_name>' SELECT * FROM <table name>`

       **참고:** 데이터를 내보내기 위해 `USING` 절 옵션을 사용한 경우, 이 절 옵션을 기억해 두거나 저장하십시오. 나중에 IBM Cloud Object Storage에서 외부 테이블을 로드하는 프로세스 동안 이 절이 재사용됩니다.

       SQL문에 대한 자세한 정보는 [CREATE EXTERNAL TABLE문 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.sql.ref.doc/doc/r_create_ext_table.html){:new_window}을 참조하십시오. 

<!--       - Provide the {{site.data.keyword.Bluemix_notm}} team with the "USING" clause that was used for data export. The clause is reused during the load process on {{site.data.keyword.Bluemix_notm}}.
       - Select FORMAT = "Text"
-->

2. 워크플로우에서 **네트워크 활동 보기**를 클릭하여 데이터가 10Gb/초 링크의 디바이스로 전송될 때 GUI에 인바운드 이더넷 로드를 표시하십시오.
    ![활동 보기](/images/UserGuide13.png)

3. 워크플로우에서 **스토리지 풀 보기**를 클릭하여 디바이스에서의 스토리지 사용량 및 IOPS를 모니터하십시오.
    ![스토리지 풀 보기](/images/UserGuide14.png)

4. 복사가 완료되면 조심스럽게 시스템의 전원을 끄십시오. 디바이스의 전원을 끄면 스토리지 풀도 잠깁니다. 워크플로우에서 **어플라이언스 시스템 종료...**를 클릭하십시오.  
    ![어플라이언스 시스템 종료 UI 단추 위치](/images/Shutdown.png)

5. 디바이스의 연결을 끊으십시오. 전원 케이블, 이더넷 케이블 및 SFP+ 어댑터를 각각 덮개 아래의 저장 위치로 돌려놓으십시오.

6. 제공되는 발송 레이블을 디바이스에 부착하십시오. 발송자에게 알리고 디바이스를 {{site.data.keyword.BluSoftlayer_full}} 데이터 센터로 반환하십시오. 데이터 센터에 도달한 후에 데이터가 {{site.data.keyword.cos_full_notm}} 버킷에 로드됩니다.

디바이스가 {{site.data.keyword.BluSoftlayer}} 팀에 반환된 후에 요청 상태는 *디바이스를 수신함*으로 변경됩니다.

## 5단계: 오프로드 및 액세스
{: #offload}

데이터 전송 프로세스 동안 요청 상태는 *데이터 오프로드 중*으로 표시됩니다. {{site.data.keyword.objectstorageshort}} 버킷으로의 마이그레이션이 완료되면 상태가 다시 변경됩니다(*오프로드 완료*). Cloud Object Storage 버킷으로의 고속 오프로드가 완료되면 즉각적으로 데이터에 액세스할 수 있습니다. 

데이터를 Cloud Object Storage 버킷에 마이그레이션하는 작업이 완료되면 [데이터를 {{site.data.keyword.dashdbshort_notm}} 데이터베이스로 가져오기](#import)로 진행할 수 있습니다.

## 6단계: IBM Cloud Object Storage에서 데이터 가져오기
{: #import}

외부 테이블을 직접 사용하여 IBM Cloud Object Storage에서 데이터를 로드하는 경우, 예제 SQL문은 다음과 같습니다.

```
INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net',
  '<S3-access-key-ID>',
  '<S3-secret-access-key>',
  '<my_bucket>'
     )
  )      
```

**참고:** 
* CREATE EXTERNAL TABLE문을 사용하여 PureData System for Analytics(Netezza) 데이터베이스에서 데이터를 추출할 때 사용한 절과 동일한 `USING` 절을 사용해야 합니다.
* IBM Cloud Object Storage의 경우, 새 서비스 신임 정보를 작성할 때 HMAC 신임 정보를 작성하려면 *인라인 구성 매개변수* 필드에서 {"HMAC:true"}를 지정하십시오.

IBM Cloud Object Storage에서 데이터를 가져오는 방법에 대한 안내 튜토리얼을 보려면 [IBM Db2 Warehouse on Cloud 안내 데모: 데이터 로드 탐색 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud/){:new_window}을 참조하십시오.

## 7단계: MDMS 디바이스 삭제
{: #erase}

{{site.data.keyword.IBM}}은 MDMS 디바이스에서 데이터를 영구적으로 삭제하기 위해 미국방부 요구사항 수준의 데이터 삭제를 구현합니다. 완료되면 요청 상태가 *삭제 완료*로 표시됩니다.

## 추가 참고
{: #notes}

### 버킷에서의 고유성

오브젝트 이름을 버킷으로 복사할 때 오브젝트 이름의 고유성을 유지하기 위해 파일 경로가 접두부로 오브젝트 이름에 포함됩니다. 예를 들어, `/root/user/` 폴더 내의 config.ini 파일 이름은 버킷에 복사될 때 "root/user/config.ini"가 됩니다.

### 버킷

대상 버킷이 없으면 작성됩니다. 있는 경우, 비어 있어야 하며 그렇지 않으면 복사가 진행되지 않습니다.

### 파일 시스템

스캔 프로세스 동안 기호 링크 및 하드 링크는 건너뜁니다.

### IP 주소 구성
{: #ip_cfg}

디바이스의 LCD 디스플레이는 이더넷 포트에 대한 IP 주소를 구성하는 데 사용될 수 있습니다. **위로 화살표**, **아래로 화살표**, **Esc** 및 **Enter** 단추를 사용하여 LCD 디스플레이로 이동합니다. **Enter** 단추를 누르면 메뉴가 표시되고 **Esc** 단추를 누르면 메뉴에서 나갑니다.

![LCD 디스플레이](/images/MDMSLCD.png)

IP 주소 또는 서브넷 마스크를 편집할 때 **Enter**를 사용하면 한 번에 한 문자씩 앞으로 이동합니다. **Esc**를 사용하면 한 번에 한 문자씩 뒤로 이동합니다. **위로 화살표** 및 **아래로 화살표**는 선택한 위치에 대한 수 사이를 토글합니다.

이전 메뉴로 되돌아가려면 **Esc**를 사용하십시오.  

설정을 저장하려면 **업데이트...** 메뉴 항목으로 이동하여 **Enter**를 누르십시오.
