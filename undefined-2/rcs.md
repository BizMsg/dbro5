# RCS

RCS는 사용 가능한 챗봇ID와 메시지베이스ID를 사용하여 발송되며 RCS 지원기기 사용자인 경우 발송 가능합니다.&#x20;

메시지베이스 ID 는 이통사에서 제공하는 **메시지 포맷**을 사용하거나 **\[RCS 비즈센터]**을 통해 **템플릿**을 등록하여 사용가능합니다.

```sql
INSERT INTO EM_TRAN_RCS(
CHATBOT_ID, HEADER, MESSAGEBASE_ID, RCS_BODY)
VALUES ({챗봇 ID}, 0, ‘SS000000’, ‘{“description”:”안녕하세요”}’);

INSERT INTO EM_TRAN(
TRAN_PHONE, TRAN_CALLBACK, TRAN_STATUS, TRAN_DATE, TRAN_TYPE, TRAN_ETC4) 
VALUES (‘01000000000’, ‘01000000000’, ‘1’, NOW(), 11, {EM_TRAN_RCS 의 RCS_SEQ 값});
```



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

URL 예시 – maapfile://BR.i6dOpSm8N8.20200302150000.001





### RCS 공통포맷 (MESSAGEBASE\_ID)

| MESSAGEBASE\_ID |  상품 |         메시지 타입        | 카드 장 수 | 최대 버튼 수 | 메시지 최대 본문 길이 (글자수) |
| :-------------: | :-: | :-------------------: | :----: | :-----: | :----------------: |
|     SS000000    | SMS |       Standalone      |    1   |    1    |         100        |
|     SL000000    | LMS |       Standalone      |    1   |    3    |        1300        |
|     SMwThT00    | MMS |  Standalone Media Top |    1   |    2    |        1300        |
|     SMwThM00    | MMS |  Standalone Media Top |    1   |    2    |        1300        |
|     SMwLhX00    | MMS | Standalone Horizontal |    1   |    2    |        1300        |
|     SMwRHX00    | MMS | Standalone Horizontal |    1   |    2    |        1300        |
|    CMwMhM0300   | MMS |    Carousel Medium    |    3   |    2    |     1300 (총 합)     |
|    CMwMhM0400   | MMS |    Carousel Medium    |    4   |    2    |     1300 (총 합)     |
|    CMwMhM0500   | MMS |    Carousel Medium    |    5   |    2    |     1300 (총 합)     |
|    CMwMhM0600   | MMS |    Carousel Medium    |    6   |    2    |     1300 (총 합)     |
|    CMwShS0300   | MMS |     Carousel Small    |    3   |    2    |     1300 (총 합)     |
|    CMwShS0400   | MMS |     Carousel Small    |    4   |    2    |     1300 (총 합)     |
|    CMwShS0500   | MMS |     Carousel Small    |    5   |    2    |     1300 (총 합)     |
|    CMwShS0600   | MMS |     Carousel Small    |    6   |    2    |     1300 (총 합)     |

> RCS MMS 슬라이드형(Carousel Medium, Small)은 1,300 자까지 발송 가능하나 \
> 실제 단말에서 수신 가능한 글자 수가 적어 메시지 내용이 잘려 발송될 가능성이 존재합니다.

> 포토여부/타이틀 글자 수/버튼 개수에 따라 입력 가능한 본문 글자 수가 상이할 수 있습니다.

{% hint style="info" %}
글자 수 및 라인 수 정의

글자 수 : 1 줄 당 정상적으로 표현가능한 글자 수, 한글 '가' 기준 측정 줄

(라인) 수 : expand 없이 메시지 버블 최대크기에서 표현 가능한 description 줄 수
{% endhint %}



**LMS (Standalone No Media)**

글자 수

| title | description | button name |
| :---: | :---------: | :---------: |
|   16  |      18     |      17     |

줄 수 (접혀있는 경)

|                      | 버튼 0개 | 버튼 1개 | 버튼 2개 | 버튼 3개 |
| -------------------- | :---: | :---: | :---: | :---: |
| description only     |   28  |   26  |   24  |   22  |
| 타이틀 1줄 + description |   27  |   25  |   23  |   20  |
| 타이틀 2줄 + description |   26  |   23  |   21  |   19  |



**MMS (Standalone Media Top - 세로형)**

글자 수

| title | description | button name |
| :---: | :---------: | :---------: |
|   16  |      18     |      17     |



줄 수 (Media Tall 인 경우, 접혀있는 경우)

|                      | 버튼 0개 | 버튼 1개 | 버튼 2개 |
| -------------------- | :---: | :---: | :---: |
| description only     |   9   |   8   |   6   |
| 타이틀 1줄 + description |   8   |   6   |   4   |
| 타이틀 2줄 + description |   7   |   5   |   3   |



줄 수 (Media Medium 인 경우, 접혀있는 경우)

|                      | 버튼 0개 | 버튼 1개 | 버튼 2개 |
| -------------------- | :---: | :---: | :---: |
| description only     |   15  |   13  |   11  |
| 타이틀 1줄 + description |   14  |   12  |   10  |
| 타이틀 2줄 + description |   13  |   11  |   9   |



**MMS (Carousel Medium - 슬라이드 형)**

글자 수

| title | description | button name |
| :---: | :---------: | :---------: |
|   13  |      14     |      13     |



줄 수 (Media 없는 경우, RCS A2P 단말 기준)

|                      | 버튼 0개 | 버튼 1개 | 버튼 2개 |
| -------------------- | :---: | :---: | :---: |
| description only     |   28  |   26  |   23  |
| 타이틀 1줄 + description |   27  |   25  |   23  |
| 타이틀 2줄 + description |   26  |   23  |   21  |
| 타이틀 3줄 + description |   24  |   22  |   20  |



줄 수 (Media Medium  경우, RCS A2P 단말 기준)

|                      | 버튼 0개 | 버튼 1개 | 버튼 2개 |
| -------------------- | :---: | :---: | :---: |
| description only     |   17  |   15  |   13  |
| 타이틀 1줄 + description |   16  |   14  |   12  |
| 타이틀 2줄 + description |   15  |   13  |   11  |
| 타이틀 3줄 + description |   14  |   12  |   10  |



**MMS (Carousel Medium - 슬라이드 형)**

글자 수

| title | description | button name |
| :---: | :---------: | :---------: |
|   5   |      6      |      5      |



줄 수 (Media Short 인 경우, RCS A2P 단말 기준)



|                      | 버튼 0개 | 버튼 1개 | 버튼 2개 |
| -------------------- | :---: | :---: | :---: |
| description only     |   20  |   18  |   16  |
| 타이틀 1줄 + description |   19  |   17  |   15  |
| 타이틀 2줄 + description |   18  |   16  |   14  |
| 타이틀 3줄 + description |   17  |   15  |   13  |
| 타이틀 4줄 + description |   16  |   14  |   12  |
| 타이틀 5줄 + description |   15  |   13  |   11  |



### RCS + BUTTONS

RCS 에 버튼 링크를 추가하고자 할 경우 아래와 같은 JSON 형식에 맞춰 RCS 테이블(BIZ\_RCS)의 **BUTTONS** 필드에 입력합니다.

```sql
INSERT INTO EM_TRAN_RCS(
CHATBOT_ID, HEADER, MESSAGEBASE_ID, RCS_BODY, BUTTONS)
VALUES ({챗봇 ID}, 0, ‘SS000000’, ‘{“description”:”안녕하세요”}’, ‘{버튼 예시 참조}’);

INSERT INTO EM_TRAN(
TRAN_PHONE, TRAN_CALLBACK, TRAN_STATUS, TRAN_DATE, TRAN_TYPE, TRAN_ETC4) 
VALUES (‘01000000000’, ‘01000000000’, ‘1’, NOW(), 11, {EM_TRAN_RCS 의 RCS_SEQ 값});
```

