---
description: UFIT DBRO란?
---

# Agent 소개

### 개요

고객사 시스템 환경에 설치하여 비즈뿌리오 서비스와 연동하는 모듈로, 이동통신사 기반의 메시지(SMS/LMS/MMS), RCS, 카카오톡 비즈메시지(AT/FT)를 발송할 수 있게 연계합니다.

### 발송 선결 조건

1. 발송 서비스 계정 생성 및 서비스 사용 승인요청
2. 카카오 비즈 메시지를 사용하려면?\
   \-> 카카오톡 발신 프로필 및 알림톡 메시지 내용(템플릿) 승인요청

### 연동 방식

DBRO는 고객사의 데이터베이스 연동을 통하여 메시지를 발송하는 모듈입니다.\
고객사의 데이터베이스에 테이블을 생성한 후 발송에 필요한 데이터를 입력하면, DBRO는 이를 체크하여 메시지를 발송하는 방식입니다.
