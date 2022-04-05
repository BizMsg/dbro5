# 카카오 비즈 메시지

### AT 발송&#x20;

알림톡은 사전에 발급된 **발신 프로필 키**와 미리 등록된 **템플릿 코드**를 통하여, 알림톡 발송이 가능합니다. \
실제 발송할 메시지 유형으로 등록된 **템플릿** 형식에 맞춰 메시지를 입력하여야 합니다.

```sql
INSERT INTO EM_TRAN_KKO(SENDER_KEY, TEMPLATE_CODE, NATION_CODE, MESSAGE)
VALUES ({발신 프로필 키}, {템플릿 코드}, ‘82’, ‘AT 테스트입니다’); 

INSERT INTO EM_TRAN(TRAN_PHONE, TRAN_CALLBACK, 
TRAN_STATUS, TRAN_DATE, TRAN_TYPE, TRAN_ETC4) 
VALUES (‘01000000000’, ‘01000000000’, ‘1’, NOW(), 7, {EM_TRAN_KKO 의 KKO_SEQ 값});
```



### FT 발송

친구톡은 **발신 프로필 키**를 사용하여 발송되며, 카카오톡 사용자이고 발신프로필(옐로아이디 또는 플러스친구)과 **친구일 경우** 발송 가능합니다.

```sql
INSERT INTO EM_TRAN_KKO (SENDER_KEY, NATION_CODE, MESSAGE)
VALUES ({발신 프로필 키}, ‘82’, ‘FT 테스트입니다’); 

INSERT INTO EM_TRAN
(TRAN_PHONE, TRAN_CALLBACK, TRAN_STATUS, TRAN_DATE, TRAN_TYPE, TRAN_ETC4) 
VALUES (‘01000000000’, ‘01000000000’, ‘1’, NOW(), 8, {EM_TRAN_KKO 의 KKO_SEQ 값});
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
SENDER_KEY, TEMPLATE_CODE, NATION_CODE, MESSAGE, ATTACHED_FILE_1)
VALUES (
{발신 프로필 키}, {템플릿 코드}, '82', 'AT 테스트입니다', ‘D:/spool/add_info.json’); 

INSERT INTO EM_TRAN( 
TRAN_PHONE, TRAN_CALLBACK, TRAN_STATUS, TRAN_DATE, TRAN_TYPE, TRAN_ETC4)
VALUES (
'01000000000', '01000000000', '1', NOW(), 8, {EM_TRAN_KKO 의 KKO_SEQ 값});
```



### ATTACHMENT FIELDS

|   |   |   |
| - | - | - |
|   |   |   |
|   |   |   |
|   |   |   |

```json
{
  "button": {                       /* array *//* 버튼 목록 */
    "name": {},                     /* text(14) *//* 버튼 제목  ‘AC’ 타입인 경우 ‘채널 추가’로 고정*/
    "type": {},                     /* text(2) *//* 버튼 타입(아래타입별속성표참조) */
    "url_pc": {},                   /* text *//* pc 환경에서 버튼 클릭 시 이동할 */
    "url_mobile": {},               /* text *//* Mobile 환경에서 버튼 클릭 시 이동할 URL */
    "scheme_ios": {},               /* text *//* Mobile iOS 환경에서 버튼 클릭 시 실행할 Application Custom Scheme */
    "scheme_android": {},           /* text *//* Mobile Android 환경에서 버튼 클릭 시 실행할 Application Custom Scheme */
    "chat_extra": {},               /* text(50) *//* 상담톡/봇 전환 시 전달할 메타정보 */
    "chat_event": {},               /* text(50) *//* 상담톡/봇 전환 시 전달할 메타정보 */  
    "plugin_id": {},                /* text(50) *//* 플러그인 ID */
    "relay_id": {},                 /* text *//* 플러그인 실행시 X-Kakao-Plugin-Relay-Id 헤더를 통해 전달 받을 값 */
    "oneclick_id": {},              /* text *//* 원클릭 결제 플러그인에서 사용하는 결제 정보 */
    "product_id": {}                /* text *//* 원클릭 결제 플러그인에서 사용하는 결제 정보 */
  },
  "image": {                        /* JSON *//* 친구톡 이미지 */
    "Img_url": {},                  /* text *//* 노출할 이미지 친구톡 이미지(와이드) 발송 시 필수입력 */
    "Img_link": {}                  /* text *//* 이미지 클릭시 이동할 url - 미설정시 카카오톡 내 이미지 뷰어 사용*/
  },
  "item_highlight": {               /* JSON *//* 아이템 하이라이트 */
    "title": {},                    /* text(30) *//* 타이틀 (이미지가 있는 경우 최대 21자) */
    "description": {}               /* text(19) *//* 부가정보 (이미지가 있는 경우 최대 14자) */
  },
  "item": {                         /* JSON *//* 아이템 리스트와 아이템 요약정보 */
    "list": {                       /* array *//* 아이템리스트 */
      "title": {},                  /* text(6) *//* 타이틀 */
      "description": {}             /* text(23) *//* 부가정보 */
    },
    "summary": {                    /* JSON *//* 아이템 요약정보 */
      "title": {},                  /* text(6) *//* 타이틀 */
      "description": {}             /* text(14) *//* 가격정보
                                                   * 허용되는 문자: 통화기호(유니코드 통화기호, 元, 円, 원), 
                                                                 통화코드(ISO 4217), 숫자, 콤마, 소수점, 공백
                                                   * 소수점 2자리까지 허용 */
    }
  },
  "expansion": {                    /* JSON *//* 추가 기능 */
    "msg_type": {},                 /* text *//* 카카오 발송 유형 -  알림톡 이미지 발송 시 필수입력 */
    "title": {},                    /* text(50) *//* 템플릿 내용 중 강조 표기할 핵심 정보 */
    "supplement": {                 /* json *//* 메시지에 첨부할 바로연결 */
        "quick_reply": {
            "name": {},             /* text(14) *//* 바로연결 제목 */
            "type": {},             /* text(2) *//* 바로연결 타입 */
            "scheme_android": {},   /* text *//* mobile android 환경에서 바로연결 클릭 시 실행할 application custom scheme */
            "scheme_ios": {},       /* text *//* mobile ios 환경에서 바로연결 클릭 시 실행할 application custom scheme */
            "url_mobile": {},       /* text *//* mobile 환경에서 바로연결 클릭 시 이동할 url */
            "url_pc": {},           /* text *//* pc 환경에서 버튼 클릭 시 이동할 url */
            "chat_extra": {},       /* text(50) *//* 상담톡/봇 전환 시 전달할 메타정보 */
            "chat_event": {}        /* text(50) *//* 봇 전환 시 연결할 봇 이벤트명 */
          }
    },
    "price": {},                    /* number *//* 모먼트 광고 전환 최적화 전용 */
    "currency_type": {},            /* text(6) *//* 모먼트 광고 전환 최적화 전용
                                                    메시지 내 포함된 가격/금액/결제금액의 통화단위
                                                    KRW, USD, EUR 등 국제 통화 코드 사용 */
    "header": {}                    /* text(6) *//* 메시지 상단에 표기할 제목 */
  }
```

```json5
{   /* array *//* 버튼 목록 */
    "button": {  
      /* text(14) *//* 버튼 제목  ‘AC’ 타입인 경우 ‘채널 추가’로 고정*/                     
      "name": {},                     
      /* text(2) *//* 버튼 타입(아래 타입 별 속성 표 참조) */
      "type": {},   
      /* text *//* pc 환경에서 버튼 클릭 시 이동할 */                  
      "url_pc": {},                   
      /* text *//* Mobile 환경에서 버튼 클릭 시 이동할 URL */
      "url_mobile": {},               
      /* text *//* Mobile iOS 환경에서 버튼 클릭 시 실행할 Application Custom Scheme */
      "scheme_ios": {},               
      /* text *//* Mobile Android 환경에서 버튼 클릭 시 실행할 Application Custom Scheme */
      "scheme_android": {},           
      /* text(50) *//* 상담톡/봇 전환 시 전달할 메타정보 */
      "chat_extra": {},               
      /* text(50) *//* 봇 전환 시 연결할 봇 이벤트명 */  
      "chat_event": {}, 
      /* text(50) *//* 플러그인 ID */              
      "plugin_id": {},                
      /* text *//* 플러그인 실행시 X-Kakao-Plugin-Relay-Id 헤더를 통해 전달 받을 값 */
      "relay_id": {},                 
      /* text *//* 원클릭 결제 플러그인에서 사용하는 결제 정보 */
      "oneclick_id": {},              
      /* text *//* 원클릭 결제 플러그인에서 사용하는 결제 정보 */
      "product_id": {}                
    },
    /* JSON *//* 친구톡 이미지 */
    "image": {                        
      /* text *//* 노출할 이미지 친구톡 이미지(와이드) 발송 시 필수입력 */
      "Img_url": {},                  
      /* text *//* 이미지 클릭시 이동할 url - 미설정시 카카오톡 내 이미지 뷰어 사용*/
      "Img_link": {}                  
    },
    /* JSON *//* 아이템 하이라이트 */
    "item_highlight": {               
      /* text(30) *//* 타이틀 (이미지가 있는 경우 최대 21자) */
      "title": {},                    
      /* text(19) *//* 부가정보 (이미지가 있는 경우 최대 14자) */
      "description": {}               
    },
    /* JSON *//* 아이템 리스트와 아이템 요약정보 */
    "item": {                         
        /* array *//* 아이템리스트 */
      "list": {                       
        /* text(6) *//* 타이틀 */
        "title": {},                  
        /* text(23) *//* 부가정보 */
        "description": {}             
      },
      /* JSON *//* 아이템 요약정보 */
      "summary": {                    
        /* text(6) *//* 타이틀 */
        "title": {},                  
        /* text(14) *//* 가격정보
         * 허용되는 문자: 통화기호(유니코드 통화기호, 元, 円, 원), 
                       통화코드(ISO 4217), 숫자, 콤마, 소수점, 공백
        * 소수점 2자리까지 허용 */
        "description": {}             
      }
    },
    /* JSON *//* 추가 기능 */
    "expansion": {                    
      /* text *//* 카카오 발송 유형 -  알림톡 이미지 발송 시 필수입력 */
      "msg_type": {},                 
      /* text(50) *//* 템플릿 내용 중 강조 표기할 핵심 정보 */
      "title": {},                   
      /* json *//* 메시지에 첨부할 바로연결 */
      "supplement": {                 
          "quick_reply": {
              /* text(14) *//* 바로연결 제목 */
              "name": {},             
              /* text(2) *//* 바로연결 타입 */
              "type": {},             
              /* text *//* mobile android 환경에서 바로연결 클릭 시 실행할 application custom scheme */
              "scheme_android": {},   
              /* text *//* mobile ios 환경에서 바로연결 클릭 시 실행할 application custom scheme */
              "scheme_ios": {},       
              /* text *//* mobile 환경에서 바로연결 클릭 시 이동할 url */
              "url_mobile": {},       
              /* text *//* pc 환경에서 버튼 클릭 시 이동할 url */
              "url_pc": {},           
              /* text(50) *//* 상담톡/봇 전환 시 전달할 메타정보 */
              "chat_extra": {},       
              /* text(50) *//* 봇 전환 시 연결할 봇 이벤트명 */
              "chat_event": {}        
            }
      },
      /* number *//* 모먼트 광고 전환 최적화 전용 */
      "price": {},                    
      /* text(6) *//* 모먼트 광고 전환 최적화 전용
        메시지 내 포함된 가격/금액/결제금액의 통화단위
        KRW, USD, EUR 등 국제 통화 코드 사용 */
      "currency_type": {}, 
      /* text(6) *//* 메시지 상단에 표기할 제목 */
      "header": {}                    
  }
  
```
