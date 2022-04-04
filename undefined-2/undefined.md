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
