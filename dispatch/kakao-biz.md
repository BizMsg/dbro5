# 카카오톡 비즈메시지

### AT 발송

알림톡은 사전에 발급된 **발신 프로필 키**와 미리 등록된 **템플릿 코드**를 통하여, 알림톡 발송이 가능합니다.\
실제 발송할 메시지 유형으로 등록된 **템플릿** 형식에 맞춰 메시지를 입력하여야 합니다.

```sql
INSERT INTO EM_TRAN_KKO(SENDER_KEY, TEMPLATE_CODE, NATION_CODE, MESSAGE)
VALUES ({발신 프로필 키}, {템플릿 코드}, '82', 'AT 테스트입니다'); 

INSERT INTO EM_TRAN(TRAN_PHONE, TRAN_CALLBACK, 
TRAN_STATUS, TRAN_DATE, TRAN_TYPE, TRAN_ETC4) 
VALUES ('01000000000', '01000000000', '1', NOW(), 7, {EM_TRAN_KKO 의 KKO_SEQ 값});
```

### FT 발송

친구톡은 **발신 프로필 키**를 사용하여 발송되며, 카카오톡 사용자이고 발신프로필(카카오톡 채널)과 **친구일 경우** 발송 가능합니다.

```sql
INSERT INTO EM_TRAN_KKO (SENDER_KEY, NATION_CODE, MESSAGE)
VALUES ({발신 프로필 키}, '82', 'FT 테스트입니다'); 

INSERT INTO EM_TRAN
(TRAN_PHONE, TRAN_CALLBACK, TRAN_STATUS, TRAN_DATE, TRAN_TYPE, TRAN_ETC4) 
VALUES ('01000000000', '01000000000', '1', NOW(), 8, {EM_TRAN_KKO 의 KKO_SEQ 값});
```

### AT/FT + ATTACHMENT 발송

알림톡/친구톡은 링크 버튼을 첨부하거나 추가 파라미터를 포함하여 발송할 수 있습니다.\
JSON 형식 파일을 생성 후 파일 경로를 입력합니다.

> 버튼 및 추가 파라미터가 등록된 템플릿코드만 사용가능합니다

**AT + ATTACHMENT**

```sql
INSERT INTO EM_TRAN_KKO(
SENDER_KEY, TEMPLATE_CODE, NATION_CODE, MESSAGE, ATTACHED_FILE_1)
VALUES (
{발신 프로필 키}, {템플릿 코드}, '82', 'AT 테스트입니다', ‘D:/spool/add_info.json’);

INSERT INTO EM_TRAN(
TRAN_PHONE, TRAN_CALLBACK, TRAN_STATUS, TRAN_DATE, TRAN_TYPE, TRAN_ETC4)
VALUES (
'01000000000', '01000000000', '1', NOW(), 7, {EM_TRAN_KKO 의 KKO_SEQ 값});
```

**FT + ATTACHMENT**

```sql
INSERT INTO EM_TRAN_KKO(
SENDER_KEY, NATION_CODE, MESSAGE, ATTACHED_FILE_1)
VALUES (
{발신 프로필 키}, '82', 'AT 테스트입니다', ‘D:/spool/add_info.json’); 

INSERT INTO EM_TRAN( 
TRAN_PHONE, TRAN_CALLBACK, TRAN_STATUS, TRAN_DATE, TRAN_TYPE, TRAN_ETC4)
VALUES (
'01000000000', '01000000000', '1', NOW(), 8, {EM_TRAN_KKO 의 KKO_SEQ 값});
```

### ATTACHMENT FIELDS

![](<../.gitbook/assets/image (18) (1).png>)

```json5
{   
    "button": {  
    /* array *//* 버튼 목록 */
        "name": {},                     
        /* text(14) *//* 버튼 제목  ‘AC’ 타입인 경우 ‘채널 추가’로 고정*/                     
        "type": {},   
        /* text(2) *//* 버튼 타입(아래 타입 별 속성 표 참조) */
        "url_pc": {},                   
        /* text *//* pc 환경에서 버튼 클릭 시 이동할 */                  
        "url_mobile": {},               
        /* text *//* Mobile 환경에서 버튼 클릭 시 이동할 URL */
        "scheme_ios": {},               
        /* text *//* Mobile iOS 환경에서 버튼 클릭 시 실행할 Application Custom Scheme */
        "scheme_android": {},           
        /* text *//* Mobile Android 환경에서 버튼 클릭 시 실행할 Application Custom Scheme */
        "chat_extra": {},               
        /* text(50) *//* 상담톡/봇 전환 시 전달할 메타정보 */
        "chat_event": {}, 
        /* text(50) *//* 봇 전환 시 연결할 봇 이벤트명 */  
        "plugin_id": {},                
        /* text(50) *//* 플러그인 ID */              
        "relay_id": {},                 
        /* text *//* 플러그인 실행시 X-Kakao-Plugin-Relay-Id 헤더를 통해 전달 받을 값 */
        "oneclick_id": {},              
        /* text *//* 원클릭 결제 플러그인에서 사용하는 결제 정보 */
        "product_id": {}                
        /* text *//* 원클릭 결제 플러그인에서 사용하는 결제 정보 */
    },
    "image": {                        
        /* JSON *//* 친구톡 이미지 */
        "Img_url": {},                  
        /* text *//* 노출할 이미지 친구톡 이미지(와이드) 발송 시 필수입력 */
        "Img_link": {}                  
        /* text *//* 이미지 클릭시 이동할 url - 미설정시 카카오톡 내 이미지 뷰어 사용*/
    },
    "item_highlight": {               
        /* JSON *//* 아이템 하이라이트 */
        "title": {},                    
        /* text(30) *//* 타이틀 (이미지가 있는 경우 최대 21자) */
        "description": {}               
        /* text(19) *//* 부가정보 (이미지가 있는 경우 최대 14자) */
    },
    "item": {                         
        /* JSON *//* 아이템 리스트와 아이템 요약정보 */
        "list": {                       
          /* array *//* 아이템리스트 */
          "title": {},                  
          /* text(6) *//* 타이틀 */
          "description": {}             
          /* text(23) *//* 부가정보 */
      },
      "summary": {                    
          /* JSON *//* 아이템 요약정보 */
          "title": {},                  
          /* text(6) *//* 타이틀 */
          "description": {}             
          /* text(14) *//* 가격정보
           * 허용되는 문자: 통화기호(유니코드 통화기호, 元, 円, 원), 
                         통화코드(ISO 4217), 숫자, 콤마, 소수점, 공백
          * 소수점 2자리까지 허용 */
      }
    },
    "expansion": {                    
        /* JSON *//* 추가 기능 */
        "msg_type": {},                 
        /* text *//* 카카오 발송 유형 -  알림톡 이미지 발송 시 필수입력 */
        "title": {},                   
        /* text(50) *//* 템플릿 내용 중 강조 표기할 핵심 정보 */
        "supplement": {                 
          /* json *//* 메시지에 첨부할 바로연결 */
          "quick_reply": {
              "name": {},             
              /* text(14) *//* 바로연결 제목 */
              "type": {},             
              /* text(2) *//* 바로연결 타입 */
              "scheme_android": {},   
              /* text *//* mobile android 환경에서 바로연결 클릭 시 실행할 application custom scheme */
              "scheme_ios": {},       
              /* text *//* mobile ios 환경에서 바로연결 클릭 시 실행할 application custom scheme */
              "url_mobile": {},       
              /* text *//* mobile 환경에서 바로연결 클릭 시 이동할 url */
              "url_pc": {},           
              /* text *//* pc 환경에서 버튼 클릭 시 이동할 url */
              "chat_extra": {},       
              /* text(50) *//* 상담톡/봇 전환 시 전달할 메타정보 */
              "chat_event": {}        
              /* text(50) *//* 봇 전환 시 연결할 봇 이벤트명 */
            }
        },
        "price": {},                    
        /* number *//* 모먼트 광고 전환 최적화 전용 */
        "currency_type": {}, 
        /* text(6) *//* 모먼트 광고 전환 최적화 전용
        메시지 내 포함된 가격/금액/결제금액의 통화단위
        KRW, USD, EUR 등 국제 통화 코드 사용 */
        "header": {}                    
        /* text(6) *//* 메시지 상단에 표기할 제목 */
    }
}
```

**Supplement**

![](<../.gitbook/assets/image (9) (1).png>)

### AT/FT + BUTTON

알림톡/친구톡은 링크 버튼을 첨부하여 발송할 수 있으며, 버튼 타입은 아래와 같습니다.

{% hint style="info" %}
버튼은 최대 5개 등록 가능하나 바로연결과 함께 사용 시 2개로 제한됩니다.
{% endhint %}

![](<../.gitbook/assets/image (2).png>)

### **AT/FT + BUTTON**

**알림톡/친구톡은** 링크 버튼을 **첨부하여 발송할 수 있으며, 버튼 타입은 아래와 같습니다.**

(버튼은 최대 5개 등록 가능하나 바로연결과 함께 사용 시 2개로 제한됩니다.)

**버튼 타입**

![](<../.gitbook/assets/image (7) (1).png>)

**버튼 타입 별 속성**

![](<../.gitbook/assets/image (13).png>)

### **AT + 바로연결**

알림톡 바로연결이란?

* 알림톡 하단에 가로 슬라이드 형태로 표시되며 웹/앱 연결, 상담톡 전환 등을 호출하는 기능
* 상담톡 또는 챗봇을 사용하는 발신프로필만 이용 가능
* 바로연결은 최대 10개까지 사용 가능, 사용 시 버튼 개수는 2개로 제한\
  \*(챗봇, 상담톡 사용 채널에만 한해 사용 가능합니다.)

**AT + 바로연결 타입별 속성**

![](<../.gitbook/assets/image (1) (1) (2).png>)

**바로연결 첨부파일 예시**

알림톡 본문 하단에 바로연결 표기 내용을 add\_info1\~2.json 파일에 아래 내용을 추가합니다.

**add\_info1.json**

버튼이 없고, 알림톡 바로연결 (웹링크/봇키워드/메시지전달/상담톡전환)이 있는 템플릿의 경우

```json
{
  "expansion": {
    "supplement": {
      "quick_reply": [
        {
          "type": "WL",
          "name": "비즈뿌리오",
          "url_mobile": "https://www.bizppurio.com/"
        },
        {
          "type": "BK",
          "name": "봇키워드하기"
        },
        {
          "type": "MD",
          "name": "메시지전달하기"
        },
        {
          "type": "BC",
          "name": "상담톡전환"
        }
      ]
    }
  }
}
```

**add\_info2.json**

버튼이 있고, 알림톡 바로연결 (웹링크/봇키워드/메시지전달/상담톡전환)이 있는 템플릿의 경우

```json5
{
  "button": [
    {
      "type": "WL",
      "name": "비즈뿌리오 바로가기",
      "url_mobile": "https://www.bizppurio.com/"
    }
  ],
  "expansion": {
    "supplement": {
      "quick_reply": [
        {
          "type": "WL",
          "name": "비즈뿌리오",
          "url_mobile": "https://www.bizppurio.com/"
        },
        {
          "type": "BK",
          "name": "봇키워드하기"
        },
        {
          "type": "MD",
          "name": "메시지전달하기"
        },
        {
          "type": "BC",
          "name": "상담톡전환"
        }
      ]
    }
  }
}
```

### AT + 이미지, 아이템 리스트

**이미지와 구조화된 목록이 포함된 알림톡**

* 기존 텍스트 알림톡 기본형에 (이미지 / 헤더 / 아이템 하이라이트 / 아이템리스트 / 아이템 요약정보) 5가지 항목이 추가로 구성
* 이미지, 헤더, 아이템 하이라이트 영역을 필요에 따라 1 개 이상 필수 선택하여 템플릿 등록
* 템플릿 당 고정된 이미지만 사용 가능
* 아이템리스트는 최소 2개 이상 최대 10개 항목으로 구성 가능\
  (알림톡 템플릿 강조 유형이 이미지형(IMAGE) 인 경우에만 **msg\_type** 을 **ai** 로 설정해주셔야 발송 가능합니다.) (ex. 알림톡 템플릿 강조 유형이 아이템리스트형이고 이미지가 포함된경우 **msg\_type** 을 **ai** 로 설정시 발송 실패)

템플릿 강조 유형이 이미지 형인 템플릿의 경우

**add\_info1.json**

```json5
{
  "expansion": {
    "msg_type": "ai"
  }
}
```

템플릿 강조 유형이 아이템리스트 형이고 헤더, 아이템리스트, 아이템 요약정보를 포함한 템플릿의 경우

**add\_info2.json**

```json5
{
  "items": {
    "list": [
      {
        "title": "가입일자",
        "description": "2021.5.23"
      },
      {
        "title": "이름",
        "description": "김카카오"
      }
    ],
    "summary": {
      "title": "구매가격",
      "description": "18,000 원"
    },
    "expansion": {
      "header": "카카오 가입을 환영합니다."
    }
  }
}
```

### FT + 이미지

이미지 포함하여 친구톡 발송 시 카카오에 등록된 이미지의 유형(일반/와이드)에 따라 add\_info.json 파일을 생성하여 등록합니다.

일반 유형의 이미지 경우

**add\_info1.json**

```json5
{
  "image": {
    "img_url": "http://mud-kage.kakao.com/dn/bYNiOa/btqBqjiQxoK/4IDZksnFEuBdU6zk9UBRKK/img.jpg",
    "img_link": "http://www.daou.co.kr"
  }
}
```

와이드 유형의 이미지 경우

**add\_info2.json**

```json5
{
  "image": {
    "img_url": "http://mud-kage.kakao.com/dn/bYNiOa/btqBqjiQxoK/4IDZksnFEuBdU6zk9UBRKK/img.jpg",
    "img_link": "http://www.daou.co.kr"
  },
  "expansion": {
    "wide": "y"
  }
}
/
```

### AT/FT + 대체(SMS/MMS) 발송

알림톡/친구톡 발송결과에 대해 실패가 발생할 경우, **대체발송이 가능합니다.**

단, 해당 서비스 아이디에 대해 **대체발송 가능여부와 주체**에 대한 설정이 되어있어야 합니다.\
대체발송의 경우, EM\_TRAN 테이블에 해당 레코드가 추가로 생성되며 **SMS** 의 **TRAN\_TYPE** 은 **1** 이며 **MMS** 의 **TRAN\_TYPE** 은 **2** 이며, **TRAN\_ETC4** 에 **입력된 값이 실제 원본데이터의 TRAN\_PR 입니다**

**AT+SMS**

```sql
INSERT INTO EM_TRAN_KKO(
SENDER_KEY, TEMPLATE_CODE, NATION_CODE, MESSAGE, RE_TYPE, RE_BODY)
VALUES ({발신 프로필 키}, {템플릿 코드}, '82', 'AT+SMS 대체발송', 'SMS', '대체발송'); 

INSERT INTO EM_TRAN(
TRAN_PHONE, TRAN_CALLBACK, TRAN_STATUS, TRAN_DATE, TRAN_TYPE, TRAN_ETC4) 
VALUES ('01000000000', '01000000000', '1', now(), 7, {EM_TRAN_KKO 의 KKO_SEQ});
```

**AT+MMS**

```sql
INSERT INTO EM_TRAN_KKO (
SENDER_KEY, TEMPLATE_CODE, NATION_CODE, MESSAGE, RE_TYPE, RE_BODY, ATTACHED_FILE_1)
VALUES (
{발신 프로필 키}, {템플릿 코드}, '82', 'AT+MMS 대체발송', 'MMS', '대체발송', ‘D:/spool/mms.jpg’);

INSERT INTO EM_TRAN(
TRAN_PHONE, TRAN_CALLBACK, TRAN_STATUS, TRAN_DATE, TRAN_TYPE, TRAN_ETC4)
VALUES ('01000000000', '01000000000', '1', now(), 7, {EM_TRAN_KKO 의 KKO_SEQ});
```

### **AT/FT + 1 차 + 2 차 대체발송**

**AT + RCS + SMS**

```sql
INSERT INTO EM_TRAN_KKO(
KKO_SEQ, SENDER_KEY, TEMPLATE_CODE, NATION_CODE, MESSAGE, RE_TYPE) 
VALUES ({KKO_SEQ}, {발신 프로필 키}, {템플릿 코드}, '82', 'AT 메시지, 'R’);

INSERT INTO EM_TRAN_RCS(
RCS_SEQ, CHATBOT_ID, HEADER, MESSAGEBASE_ID, RCS_BODY, RE_TYPE, RE_BODY)
VALUES (
{KKO_SEQ 동일}, {챗봇 ID}, 0, 'SS000000', '{"description":"AT+RCS+SMS 대체발송"}', 
'SMS', 'SMS 2 차 대체발송 메시지');

INSERT INTO EM_TRAN
(TRAN_PHONE, TRAN_CALLBACK, TRAN_STATUS, TRAN_DATE, TRAN_TYPE, TRAN_ETC4)
VALUES ('01000000000', '01000000000', '1', now(), 7, {EM_TRAN_KKO 의 KKO_SEQ});
```

**AT + RCS + MMS**

```sql
INSERT INTO EM_TRAN_KKO(
KKO_SEQ, SENDER_KEY, TEMPLATE_CODE, NATION_CODE, MESSAGE, RE_TYPE) 
VALUES ({KKO_SEQ}, {발신 프로필 키}, {템플릿 코드}, '82', 'AT 메시지', 'R');

INSERT INTO EM_TRAN_RCS(
RCS_SEQ, CHATBOT_ID, HEADER, MESSAGEBASE_ID, RCS_BODY,
RE_TYPE, RE_BODY, ATTACHED_FILE_1)
VALUES (
{KKO_SEQ 동일}, {챗봇 ID}, 0, 'SS000000', '{“description":"AT+RCS+MMS 대체발송"}', 
'SMS', 'SMS 2 차 대체발송 메시지', 'D:/mms.jpg');

INSERT INTO EM_TRAN(
TRAN_PHONE, TRAN_CALLBACK, TRAN_STATUS, TRAN_DATE, TRAN_TYPE, TRAN_ETC4)
VALUES ('01000000000', '01000000000', '1', now(), 7, {EM_TRAN_KKO 의 KKO_SEQ});
```



### 카카오톡 이모티콘 삽입

카카오톡 기본 이모티콘 삽입을 원할 경우 이모티콘에 해당하는 명령어를 입력합니다.

예) 안녕하세요 (하하)(씨익)

<figure><img src="../.gitbook/assets/카카오톡 이모티콘 이름 (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
카카오에서 공식적으로 지원하는 기능이 아니므로 명령어에 대한 변경이 있을 수 있습니다.
{% endhint %}
