# DBRO Configuration

### 모듈 디렉터리 구성

* bat : Windows 용 실행 스크립트 위치
  * Java Windows Service Wrapper 파일 위치
* blk : 블랙리스트 파일 위치
* rep : 리포트 임시보관 위치
* config : 설정파일 위치
  * Data : 지원 DB별 SQL문 위치
* lib : 모듈에서 사용하는 라이브러리(JAR) 위치
* log : 로그 위치
* script : Linux/Unix용 실행 스크립트 위치

{% hint style="info" %}
blk, req, log 경로 (기본 상대경로 위치 사용 시)

* Windows: bat/wrapper 하위 경로에 위치
* Linux/Unix: config 와 동일 레벨에 위
{% endhint %}

### 환경설정 파일

DBRO의 설정파일(dbro.conf)은 config 폴더에 존재하며, 설정에 따라 동작됩니다.

{% hint style="info" %}
최초 설정 후 클라이언트 실행 시 dbro.conf -> **dbro.confx** 로 파일명이 변경됨

\[비밀번호 설정 값 수정 방법]

* dbro.confx -> <mark style="color:purple;">**dbro**</mark><mark style="color:purple;">.</mark><mark style="color:purple;">**conf**</mark>로 변경
* dbro.conf 파일 내 암호 관련 옵션 (<mark style="color:purple;">**GW\_AUTH\_PW, DB\_PASS**</mark>) 모두 수정
{% endhint %}

### 모듈 버전 업그레이드

최신 모듈을 사용하려는 기존 모듈 사용자가 환경설정을 유지하고자 할 때 참고해야 할 사항을 표기합니다.

모듈(dbro5.jar) 교체는 공통

|  버전 명 |     추가 기능    |                                                                       설명                                                                      |
| :---: | :----------: | :-------------------------------------------------------------------------------------------------------------------------------------------: |
| 5.6.3 | RCS 발송 기능 추가 | <p>1. Config/Data/*.cfg 파일 교체 필요<br>2. 설정파일 옵션 변경/추가 (dbro.conf)</p><p>- 접속 Port 변경 : 4005 -> 4006<br>- RCS 테이블 명 추가 : RCS_CONTENTS_TABLE</p> |



### 추가 옵션 구성

**추가 기능 사용 여부에 따라 설정할 수 있는 옵션에 대한 안내입니다.**

1\) 최초 발신사업자 식별코드(RESELLER\_CODE) 설정 (v5.8.0 이상)

RESELLER\_CODE 는 특부가사업자 등록번호(9 자리 숫자로 구성)를 의미합니다.&#x20;

1. USE\_RESELLERCODE (Y/N) 옵션 설정\
   메시지 발송시 식별코드를 포함하여 전송합니다.\
   \- config/dbro.conf 파일 내에 다음과 같이 설정하여 사용합니다.\
   "USE\_RESELLERCODE = Y" - 기본값(DEFAULT): N
2. 메시지/로그 테이블 RESELLER\_CODE VARCHAR(10) 컬럼 추가\
   \- 신규 설치시 위 옵션을 설정 후 구동하면 자동으로 추가됩니다.\
   \- 기존 테이블(EM\_TRAN/EM\_LOG)이 존재한다면 테이블 삭제 후 모듈을 재구동하거나 해당 컬럼을 추가하여 발송 가능합니다.

### Configuration 작성

```tsconfig
######################################################################################
# DBRO v5 Config File - 2021.06.07
######################################################################################

######################################################################################
# G/W CONNECT INFO
# SSL Port     : 4006
# Not Supported NON-SSL Port
######################################################################################
GW_CONNECT_IP =
GW_CONNECT_PORT = 4006
GW_AUTH_ID =
GW_AUTH_PW =
USE_SSL = Y
######################################################################################

######################################################################################
# DBMS CONNECT INFO
# DBTYPE
#	MSSQL, MYSQL, ORACLE, INFORMIX, DB2, TIBERO
# DBURL
#   MSSQL           
#	 jdbc:microsoft:sqlserver://<host>:<port,1433>;DatabaseName=<db>
#   MYSQL           
#	 jdbc:mysql://<host>:<port,3306>/<db>?useUnicode=true&characterEncoding=euc-kr
#   ORACLE          
#	 jdbc:oracle:thin:@<host>:<port,1521>:<db>
#   INFORMIX
#	 jdbc:informix-sqli://<host>:<port>/<db>:informixserver=<server>
#   DB2
#        jdbc:db2://<host>:<port,50000>/<db>
#   TIBERO
#       jdbc:tibero:thin:@<host>:<port,8629>:<db>
######################################################################################
DB_TYPE =
DB_URL  =
DB_USER =
DB_PASS =
MSG_TABLE = EM_TRAN
BACKUP_TABLE = EM_LOG
MMS_CONTENTS_TABLE = EM_TRAN_MMS
KKO_CONTENTS_TABLE = EM_TRAN_KKO
RCS_CONTENTS_TABLE = EM_TRAN_RCS

USE_ORACLE_PREPARED_STATEMENT = Y
######################################################################################

######################################################################################
# FILE PATH INFO
LOG_PATH = ./log
BLACKLIST_PATH = ./blk
REPORT_PATH = ./rep
######################################################################################

######################################################################################
# LOG LEVEL
######################################################################################
MAIN_LOG_LEVEL = INFO
FETCH_LOG_LEVEL = INFO
SEND_LOG_LEVEL = INFO
RECV_LOG_LEVEL = INFO
REPORT_LOG_LEVEL = INFO
REORDER_LOG_LEVEL = INFO
BACKUP_LOG_LEVEL = INFO

```
