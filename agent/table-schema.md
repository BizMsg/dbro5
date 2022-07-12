# Table Schema

### DBRO 테이블 구조

DBRO에서 사용하는 테이블의 목록은 다음과 같습니다.

> 메시지 테이블 : **EM\_TRAN**
>
> * 메시지 발송을 위한 데이터가 입력되며, 발송결과 업데이트가 이루어지기까지 데이터가 존재하는 테이블

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

![](<../.gitbook/assets/image (14).png>)

### EM\_TRAN\_MMS

![](<../.gitbook/assets/image (17) (1).png>)

### EM\_TRAN\_KKO

![](<../.gitbook/assets/image (3).png>)

### EM\_TRAN\_RCS

![](<../.gitbook/assets/image (6).png>)
