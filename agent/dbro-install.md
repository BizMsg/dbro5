---
description: 설치 및 구동 방법
---

# DBRO install



### 공통

1. Dbro\_v5를 업로드 한 뒤 압축
2. 환경 설정 파일을 수정합니다. _**`{모듈경로}/config/dbro.conf`**_
   1. 계정 설정 : \
      GW\_CONNECT\_IP __ **(사업팀 확인 후 설정 ex. ena.ufit.co.kr)**\
      __GW\_CONNECT_PORT **(SSL : 4006)**_\
      __USE\_SSL **(SSL : Y, NON-SSL 미지원)**
   2. DBMS 연결 정보 설정 : **DB\_TYPE, DB\_URL, DB\_USER, DB\_PASS**



### Linux 계열

1. dbro5를 실행합니다. _**`{모듈경로}/script/dbro-start`**_**→ **_**`./dbro-start`**_
2. dbro5 를 중지합니다. _**`{모듈경로}/script/dbro-stop`**_**→ **_**`./dbro-stop`**_



### Windows 계열

1. dbro5 를 설치/시작합니다. _**`{모듈경로}/bat`**_\
   _**``**_설치 : <mark style="color:orange;">**sevice-install.bat**</mark> 실행\
   DAOUTECH UFIT DBRO v5 등록 확인 : 제어판 → 관리도구 → 서비스 (해당 서비스를 통하여 직접 시작/종료 가능)\
   \
   시작 : <mark style="color:orange;">**sevice-start.bat**</mark> 실행 (서비스 상태가 ‘시작’으로 변경됨) 2 dbro5 의 설치 취소가 필요한 경우 (경로: {모듈경로}/bat)\

2. 모듈 제거 : <mark style="color:orange;">**sevice-uninstall.bat**</mark> <mark style="color:orange;"></mark><mark style="color:orange;"></mark> 실행

