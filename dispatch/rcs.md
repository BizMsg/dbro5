# RCS

RCS는 사용 가능한 챗봇ID와 메시지베이스ID를 사용하여 발송되며 RCS 지원기기 사용자인 경우 발송 가능합니다.

메시지베이스 ID 는 이통사에서 제공하는 **메시지 포맷**을 사용하거나 **\*\[RCS 비즈센터]**을 통해 **템플릿**을 등록하여 사용가능합니다.

```sql
INSERT INTO EM_TRAN_RCS(
CHATBOT_ID, HEADER, MESSAGEBASE_ID, RCS_BODY)
VALUES ({챗봇 ID}, 0, 'SS000000', '{"description":"안녕하세요"}');

INSERT INTO EM_TRAN(
TRAN_PHONE, TRAN_CALLBACK, TRAN_STATUS, TRAN_DATE, TRAN_TYPE, TRAN_ETC4) 
VALUES ('01000000000', '01000000000', '1', NOW(), 11, {EM_TRAN_RCS 의 RCS_SEQ 값});
```

### RCS 공통포맷 (MESSAGEBASE\_ID)

![](<../.gitbook/assets/image (10).png>)

### RCS BODY

**BODY**

**key : title, media, description**

리치카드 개수 및 순서에 따라 넘버링 (ex. title1, title2, ...)

```sql
#1개
{
    "title" : "카드",
    "media" : "등록된 이미지 URL", 
    "description": "안녕하세요!"
}
```

```sql
#2개 이상
{
    "title1" : "카드",
    "media1" : "등록된 이미지 URL", 
    "description1": "안녕하세요!", 
    "title2" : "카드 2",
    "media2" : "등록된 이미지 URL", 
    "description2" : "안녕하세요!",
            .
            .
            .
}
```

**media 종류**

**1. 이미지**

* 비즈뿌리오 사이트 \[메시지관리] - \[RCS 관리] - \[RCS 이미지 관리] 에서 이미지를 등록하여 사용합니다.

{% hint style="info" %}
**URL 예시 ( maapfile://{fileId} )**

"media":"maapfile://BR.i6dOpSm8N8.20200302150000.001"
{% endhint %}

#### 2. 동영상 스트리밍

* 3가지 형태의 YouTube URL 주소 지원 (정확한 형식을 준수해야 하며, 일부만 일치하는 경우 실패)
*   동영상 썸네일은 등록된 이미지만 사용 가능하며 YouTube URL 뒤에 콤마(,)와 함께 입력

    (콤마(,) 외 공백을 포함하는 경우 실패)
* 동영상 발송 시 Footer에 '동영상 재생 시 데이터 요금제가 적용됩니다.'라는 문구 자동 삽입

{% hint style="info" %}
**URL 예시 ( https://youtu.be/\[VideoId],maapfile://{썸네일용 fileId} )**

"media1":"https://www.youtube.com/watch?v=\[videoId],maapfile://BR.i6dOpSm8N8.20200302150000.001"

"media2":"https://youtu.be/\[VideoId],maapfile://BR.i6dOpSm8N8.20200302150000.001"

"media3":"https://m.youtube.com/watch?v=\[videoId],maapfile://BR.i6dOpSm8N8.20200302150000.001"
{% endhint %}

> RCS MMS 슬라이드형(Carousel Medium, Small)은 1,300 자까지 발송 가능하나\
> 실제 단말에서 수신 가능한 글자 수가 적어 메시지 내용이 잘려 발송될 수 있습니다.\
> 포토여부/타이틀 글자 수/버튼 개수에 따라 입력 가능한 본문 글자 수가 상이할 수 있습니다.

{% hint style="info" %}
글자 수 및 라인 수 정의

글자 수 : 1 줄 당 정상적으로 표현가능한 글자 수, 한글 '가' 기준 측정 줄

(라인) 수 : expand 없이 메시지 버블 최대크기에서 표현 가능한 description 줄 수
{% endhint %}

**LMS (Standalone No Media)**

글자 수

![](<../.gitbook/assets/image (17).png>)

줄 수 (접혀있는 경우)

![](<../.gitbook/assets/image (4).png>)

**MMS (Carousel Medium - 슬라이드 형)**

글자 수

![](<../.gitbook/assets/image (15).png>)

줄 수 (Media 없는 경우, RCS A2P 단말 기준)

![](<../.gitbook/assets/image (11).png>)

줄 수 (Media Medium 경우, RCS A2P 단말 기준)

![](<../.gitbook/assets/image (8).png>)

**MMS (Carousel Medium - 슬라이드 형)**

글자 수

![](<../.gitbook/assets/image (19).png>)

줄 수 (Media Short 인 경우, RCS A2P 단말 기준)

![](<../.gitbook/assets/image (12).png>)

### RCS + BUTTONS

RCS 에 버튼 링크를 추가하고자 할 경우 아래와 같은 JSON 형식에 맞춰 RCS 테이블(BIZ\_RCS)의 **BUTTONS** 필드에 입력합니다.

```sql
INSERT INTO EM_TRAN_RCS(
CHATBOT_ID, HEADER, MESSAGEBASE_ID, RCS_BODY, BUTTONS)
VALUES ({챗봇 ID}, 0, 'SS000000', '{"description":"안녕하세요"}', '{버튼 예시 참조}');

INSERT INTO EM_TRAN(
TRAN_PHONE, TRAN_CALLBACK, TRAN_STATUS, TRAN_DATE, TRAN_TYPE, TRAN_ETC4) 
VALUES ('01000000000', '01000000000', '1', NOW(), 11, {EM_TRAN_RCS 의 RCS_SEQ 값});
```

### RCS + 1차 대체 발송

RCS 는 발송결과에 대해 실패가 발생할 경우, 대체발송이 가능합니다.

단, 해당 서비스 아이디에 대해 대체발송 가능여부와 주체에 대한 설정이 되어있어야 합니다.\
대체발송의 경우, EM\_TRAN 테이블에 해당 레코드가 추가로 생성되며 SMS 의 TRAN\_TYPE 은 1 이고 MMS 의 TRAN\_TYPE 은 2 이며, TRAN\_ETC4 에 입력된 값이 실제 원본데이터의 TRAN\_PR 입니다.

#### **RCS+SMS**

```sql
INSERT INTO EM_TRAN_RCS(
CHATBOT_ID, HEADER, MESSAGEBASE_ID, RCS_BODY, RE_TYPE, RE_BODY)
VALUES (
{챗봇 ID}, 0, 'SS000000', '{"description":"RCS+SMS 대체발송"}' 'SMS', '대체발송');

INSERT INTO EM_TRAN(
TRAN_PHONE, TRAN_CALLBACK, TRAN_STATUS, TRAN_DATE, TRAN_TYPE, TRAN_ETC4) 
VALUES (
'01000000000', '01000000000', '1', now(), 11, {EM_TRAN_RCS 의 RCS_SEQ});
```

**RCS + MMS**

```sql
INSERT INTO EM_TRAN_KKO(
CHATBOT_ID, HEADER, MESSAGEBASE_ID, RCS_BODY, RE_TYPE, RE_BODY) 
VALUES (
{챗봇 ID}, 0, 'SS000000', '{"description":"RCS+MMS 대체발송"}',
'MMS', '대체발송', 'D:/spool/mms.jpg'); 

INSERT INTO EM_TRAN(
TRAN_PHONE, TRAN_CALLBACK, TRAN_STATUS, TRAN_DATE, TRAN_TYPE, TRAN_ETC4) 
VALUES ('01000000000', '01000000000', '1', now(), 11, {EM_TRAN_RCS 의 RCS_SEQ});
```

### RCS + 1차 + 2차 대체발송

RCS 는 발송결과에 대해 실패가 발생할 경우, 최대 2 차 대체발송이 가능합니다. - 대체발송의 경우, EM\_TRAN 테이블에 해당 레코드가 추가로 됩니다.

* 발송에 사용되는 RCS\_SEQ 값과 KKO\_SEQ 값은 동일해야 합니다.
* 2 차 대체(SMS/MMS)의 정보는 KKO 테이블에 입력해야 정상적으로 발송됩니다.

**RCS + AT + SMS**

```sql
INSERT INTO EM_TRAN_RCS(
RCS_SEQ, CHATBOT_ID, HEADER, MESSAGEBASE_ID, RCS_BODY, RE_TYPE) 
VALUES ({RCS_SEQ}, {챗봇 ID}, 0, 'SS000000', '{"description":"RCS 메시지"}', 'K');

INSERT INTO EM_TRAN_KKO(
KKO_SEQ, SENDER_KEY, TEMPLATE_CODE, NATION_CODE, MESSAGE, RE_TYPE, RE_BODY) 
VALUES ({RCS_SEQ 동일}, {발신 프로필 키}, {템플릿 코드}, '82', 'RCS+AT+SMS 대체발송',
'SMS', 'SMS 2 차 대체발송 메시지'); 

INSERT INTO EM_TRAN(
TRAN_PHONE, TRAN_CALLBACK, TRAN_STATUS, TRAN_DATE, TRAN_TYPE, TRAN_ETC4) 
VALUES ('01000000000', '01000000000', '1', now(), 11, {EM_TRAN_RCS 의 RCS_SEQ});
```

**RCS + AT + MMS**

```sql
INSERT INTO EM_TRAN_RCS(
RCS_SEQ, CHATBOT_ID, HEADER, MESSAGEBASE_ID, RCS_BODY, RE_TYPE) 
VALUES ({RCS_SEQ}, {챗봇 ID}, 0, 'SS000000', '{"description":"RCS 메시지"}', 'K');

INSERT INTO EM_TRAN_KKO(
KKO_SEQ, SENDER_KEY, TEMPLATE_CODE, NATION_CODE, MESSAGE, RE_TYPE, RE_BODY) 
VALUES ({RCS_SEQ 동일}, {발신 프로필 키}, {템플릿 코드}, '82', 'RCS+AT+MMS 대체발송',
'MMS', 'MMS 2 차 대체발송 메시지'); 

INSERT INTO EM_TRAN(
TRAN_PHONE, TRAN_CALLBACK, TRAN_STATUS, TRAN_DATE, TRAN_TYPE, TRAN_ETC4)
VALUES ('01000000000', '01000000000', '1', now(), 11, {EM_TRAN_RCS 의 RCS_SEQ});
```
