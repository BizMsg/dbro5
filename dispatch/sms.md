---
description: 발송쿼리
---

# SMS

### SMS (텍스트 90byte 이하의 단문 메시지)

```sql
INSERT INTO EM_TRAN
(TRAN_PHONE, TRAN_CALLBACK, TRAN_STATUS, TRAN_DATE, TRAN_MSG, TRAN_TYPE)
VALUES ('01000000000', '01000000000', '1', NOW(), 'Test Message 입니다', 4)
```
