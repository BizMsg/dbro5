# Table Schema

### DBRO 테이블 구조

DBRO에서 사용하는 테이블의 목록은 다음과 같습니다.



> 메시지 테이블 : **EM\_TRAN**
>
> * 메시지 발송을 위한 데이터가 입력되며, 발송결과 업데이트가 이루어지기까지 데이터가 존재하는 테이

> 로그 테이블 : **EM\_LOG\_YYYYMM**
>
> * 메시지 테이블에서 발송결과업데이트가 완료된 데이터가 이동되는 테이블

> MMS 콘텐츠 테이블 : **EM\_TRAN\_MMS**
>
> * MMS 전송 시, 필요한 정보들이 입력되는 테이블

> KKO 콘텐츠 테이블 – **EM\_TRAN\_KKO**
>
> * AT/FT 전송 시, 필요한 정보들이 입력되는 테이블

> RCS 콘텐츠 테이블 - **EM\_TRAN**_**\_**_**RCS**
>
> * RCS 전송 시, 필요한 정보들이 입력되는 테이블

테이블 생성 권한이 있다면, 자동으로 위의 테이블을 생성합니다.



### EM\_TRAN

|       컬럼 명       |  데이터 타입  |  길이 | 입력 필수 |  PK | NOT NULL |                                                        비고                                                        |   |
| :--------------: | :------: | :-: | :---: | :-: | :------: | :--------------------------------------------------------------------------------------------------------------: | - |
|     TRAN\_PR     |  INTEGER |     |   O   |  O  |     O    |                                              메시지 키 (AUTO INCREMENT)                                              |   |
|   TRAN\_REFKEY   |  VARCHAR |  40 |       |     |          |                                                        참조용                                                       |   |
|     TRAN\_ID     |  VARCHAR |  20 |       |     |          |                                                        참조용                                                       |   |
|    TRAN\_PHONE   |  VARCHAR |  15 |   O   |     |     O    |                                                     수신자 전화번호                                                     |   |
|  TRAN\_CALLBACK  |  VARCHAR |  15 |       |     |          |                                                     송신자 전화번호                                                     |   |
|   TRAN\_STATUS   |   CHAR   |  1  |   O   |     |          |                            <p>메시지 상태 <br>(1:접수, 0:발송진행중, <br>2:발송 후 대기, 3:리포트수신완료)</p>                           |   |
|    TRAN\_DATE    | DATETIME |     |   O   |     |     O    |                                                메시지 접수시간 (전송 요청 시간)                                               |   |
|  TRAN\_RSLTDATE  | DATETIME |     |       |     |          |                                           실제 단말기에 전달된 시간 (통신사에서 전달한 시간)                                          |   |
| TRAN\_REPORTDATE | DATETIME |     |       |     |          |                                                    전송결과 수신 시간                                                    |   |
|    TRAN\_RSLT    |   CHAR   |  1  |       |     |          |                                                      전송결과코드                                                      |   |
|     TRAN\_NET    |  VARCHAR |  3  |       |     |          |                                              통신사 정보 (SKT/KT/LGT/KKO)                                             |   |
|     TRAN\_MSG    |  VARCHAR | 255 |   O   |     |          |                                                      전송 메시지                                                      |   |
|    TRAN\_ETC1    |  VARCHAR |  64 |       |     |          |                                               사용자가 임의로 사용할 수 있는 필드                                               |   |
|    TRAN\_ETC2    |  VARCHAR |  16 |       |     |          |                                               사용자가 임의로 사용할 수 있는 필드                                               |   |
|    TRAN\_ETC3    |  VARCHAR |  16 |       |     |          |                                               사용자가 임의로 사용할 수 있는 필드                                               |   |
|    TRAN\_ETC4    |  INTEGER |     |       |     |          |                                          (MMS/AT/FT/RCS) 콘텐츠 테이블 매칭키 정보                                          |   |
|    TRAN\_TYPE    |  INTEGER |     |   O   |     |          | <p>메시지 타입<br>(4:SMS, 6:MMS, 7:AT, 8:FT, 11:RCS) <br>대체발송이 이루진 경우<br>(1:SMS / 2:MMS / 23:AT / 24:FT / 27:RCS)</p> |   |





### EM\_TRAN\_MMS

|       컬럼 명      |  데이터 타입 |  길이  | 입력 필수 |  PK | NOT NULL |             비고            |   |
| :-------------: | :-----: | :--: | :---: | :-: | :------: | :-----------------------: | - |
|     MMS\_SEQ    | INTEGER |      |   O   |  O  |     O    |   메시지 키 (AUTO INCREMENT)  |   |
|    FILE\_CNT    | INTEGER |      |   O   |     |     O    | MMS 전송 시 첨부파일 개수 (1 개 이상) |   |
|    BUILD\_YN    |   CHAR  |   1  |       |     |          |                           |   |
|    MMS\_BODY    | VARCHAR | 2000 |       |     |          |           본문 내용           |   |
|   MMS\_SUBJECT  | VARCHAR |  40  |   O   |     |          |           메시지 제목          |   |
|   FILE\_TYPE1   | VARCHAR |   3  |       |     |          |       MMS 파일타입 생략 가능      |   |
|   FILE\_TYPE2   | VARCHAR |   3  |       |     |          |       MMS 파일타입 생략 가능      |   |
|   FILE\_TYPE3   | VARCHAR |   3  |       |     |          |       MMS 파일타입 생략 가능      |   |
|   FILE\_TYPE4   | VARCHAR |   3  |       |     |          |       MMS 파일타입 생략 가능      |   |
|   FILE\_TYPE5   | VARCHAR |   3  |       |     |          |       MMS 파일타입 생략 가능      |   |
|   FILE\_NAME1   | VARCHAR |  100 |       |     |          |   MMS 파일경로를 포함한 파일명 생략가능  |   |
|   FILE\_NAME2   | VARCHAR |  100 |       |     |          |   MMS 파일경로를 포함한 파일명 생략가능  |   |
|   FILE\_NAME3   | VARCHAR |  100 |       |     |          |   MMS 파일경로를 포함한 파일명 생략가능  |   |
|   FILE\_NAME4   | VARCHAR |  100 |       |     |          |   MMS 파일경로를 포함한 파일명 생략가능  |   |
|   FILE\_NAME5   | VARCHAR |  100 |       |     |          |   MMS 파일경로를 포함한 파일명 생략가능  |   |
|  SERVICE\_DEP1  | VARCHAR |   3  |       |     |          |     MMS 파일 서비스통신사 생략가능    |   |
|  SERVICE\_DEP2  | VARCHAR |   3  |       |     |          |     MMS 파일 서비스통신사 생략가능    |   |
|  SERVICE\_DEP3  | VARCHAR |   3  |       |     |          |     MMS 파일 서비스통신사 생략가능    |   |
|  SERVICE\_DEP4  | VARCHAR |   3  |       |     |          |     MMS 파일 서비스통신사 생략가능    |   |
|  SERVICE\_DEP5  | VARCHAR |   3  |       |     |          |     MMS 파일 서비스통신사 생략가능    |   |
| SKN\_FILE\_NAME | VARCHAR |  255 |       |     |          |                           |   |



### EM\_TRAN\_KKO

|        컬럼 명       |  데이터 타입 |  길이  | 입력 필수 |  PK | NOT NULL |                       비고                      |   |
| :---------------: | :-----: | :--: | :---: | :-: | :------: | :-------------------------------------------: | - |
|      KKO\_SEQ     | INTEGER |      |   O   |  O  |     O    |             메시지 키 (AUTO INCREMENT)            |   |
|     USER\_KEY     | VARCHAR |  30  |       |     |          |    <p>옐로아이디 봇을 이용해 받은<br>옐로아이디 사용자 식별키</p>    |   |
|      AD\_FLAG     | VARCHAR |   1  |       |     |          |   <p>광고성 메시지 필수 표기 사항을 노출 <br>(노출여부 Y/N)</p>  |   |
|    NATION\_CODE   | VARCHAR |   5  |   O   |     |          |                      국가코드                     |   |
|    SENDER\_KEY    | VARCHAR |  40  |   O   |     |          |                    발신프로필 키                    |   |
|   TEMPLATE\_CODE  | VARCHAR |  30  |   O   |     |          |                     템플릿코드                     |   |
|  RESPONSE\_METHOD | VARCHAR |   8  |       |     |          |      <p>전송결과를 응답 받는 방법 <br>(기본: push)</p>     |   |
|      TIMEOUT      | INTEGER |      |       |     |          |         메시지전송요청 시 성공여부를 결정하기 위한 시간(초)         |   |
|      MESSAGE      | VARCHAR | 2000 |   O   |     |          |                     메시지본문                     |   |
|      RE\_TYPE     | VARCHAR |   3  |       |     |          |                대체발송유형 (SMS/MMS)               |   |
|      RE\_BODY     | VARCHAR | 2000 |       |     |          |                  대체발송 메시지 내용                  |   |
|      RE\_PART     | VARCHAR |   1  |       |     |          | <p>대체발송 처리 주체<br>(C:클라이언트/S:게이트웨이/N:하지않음)</p> |   |
|    RE\_SUBJECT    | VARCHAR |  40  |       |     |          |              MMS 대체발송인 경우, 메시지제목              |   |
|    ORI\_MSGTYPE   | VARCHAR |   3  |       |     |          |      <p>원본 메시지 타입 <br>(AT:알림톡/FT:친구톡)</p>     |   |
|    ORI\_MSGKEY    | INTEGER |      |       |     |          |                    원본메시지 키                    |   |
| ATTACHED\_FILE\_1 | VARCHAR |  100 |       |     |          |                  첨부파일명(경로포함)                  |   |
| ATTACHED\_FILE\_2 | VARCHAR |  100 |       |     |          |                  첨부파일명(경로포함)                  |   |
| ATTACHED\_FILE\_3 | VARCHAR |  100 |       |     |          |                  첨부파일명(경로포함)                  |   |
| ATTACHED\_FILE\_4 | VARCHAR |  100 |       |     |          |                  첨부파일명(경로포함)                  |   |
| ATTACHED\_FILE\_5 | VARCHAR |  100 |       |     |          |                  첨부파일명(경로포함)                  |   |







### EM\_TRAN\_RCS

|        컬럼 명       |  데이터 타입 |  길이  | 입력 필수 |  PK | NOT NULL |                                 비고                                 |   |
| :---------------: | :-----: | :--: | :---: | :-: | :------: | :----------------------------------------------------------------: | - |
|      RCS\_SEQ     | INTEGER |      |   O   |  O  |     O    |                       메시지 키 (AUTO INCREMENT)                       |   |
|   COPY\_ALLOWED   | VARCHAR |   1  |       |     |          |         <p>단말기에서 사용자에게 복사/공유 메뉴 보기 여부 <br>(Y / N, 기본 N)</p>        |   |
|    CHATBOT\_ID    | VARCHAR |  40  |   O   |     |          |                       RCS 비즈센터를 통해 생성한 챗봇 ID                       |   |
|       FOOTER      | VARCHAR |  64  |       |     |          |                         메시지 하단에 수신거부 문구를 입력                        |   |
|       HEADER      | VARCHAR |   1  |   O   |     |          |            <p>메시지 상단에 식별 문구를 입력 <br>(0:Web 발신,1:광고)</p>            |   |
|  MESSAGEBASE\_ID  | VARCHAR |  40  |   O   |     |          | <p>RCS 공통 포맷 또는 템플릿 ID <br>(RCS SMS, LMS, MMS 공통포맷, 템플릿은 별도등록)</p> |   |
|      BUTTONS      | VARCHAR | 2000 |       |     |          |                      메시지에 삽입할 버튼 정보 (Json 형식)                      |   |
|     RCS\_BODY     | INTEGER | 2000 |   O   |     |          |              <p>메시지 베이스에서 치환할 파라미터 정보<br>(Json 형식)</p>             |   |
|     AGENCY\_ID    | VARCHAR |  20  |       |     |          |    <p>대행사 ID<br>(ChatbotId 에 대한 발송 권한 체크, default:daoutech)</p>    |   |
|      RE\_TYPE     | VARCHAR |   3  |       |     |          |                          대체발송유형 (SMS/MMS)                          |   |
|      RE\_BODY     | VARCHAR | 2000 |       |     |          |                             대체발송 메시지 내용                            |   |
|      RE\_PART     | VARCHAR |   1  |       |     |          |            <p>대체발송 처리 주체<br>(C:클라이언트/S:게이트웨이/N:하지않음)</p>           |   |
|    RE\_SUBJECT    | VARCHAR |  40  |       |     |          |                         MMS 대체발송인 경우, 메시지제목                        |   |
| ATTACHED\_FILE\_1 | VARCHAR |  100 |       |     |          |                             첨부파일명(경로포함)                            |   |
| ATTACHED\_FILE\_2 | VARCHAR |  100 |       |     |          |                             첨부파일명(경로포함)                            |   |
| ATTACHED\_FILE\_3 | VARCHAR |  100 |       |     |          |                             첨부파일명(경로포함)                            |   |
| ATTACHED\_FILE\_4 | VARCHAR |  100 |       |     |          |                             첨부파일명(경로포함)                            |   |
| ATTACHED\_FILE\_5 | VARCHAR |  100 |       |     |          |                             첨부파일명(경로포함)                            |   |
