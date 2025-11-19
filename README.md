# Linkle

> 취미 기반 동호회 관리 플랫폼

## 프로젝트 소개

Linkle는 취미와 관심사를 공유하는 사람들을 연결하고, 동호회 운영을 돕는 종합 커뮤니티 플랫폼입니다.

### 주요 기능

- **동호회 검색/추천**: 카테고리, 지역, 인기도 기반 동호회 추천
- **동호회 관리**: 회원 관리, 권한 설정, 대시보드 통계
- **일정 관리**: 캘린더 기반 일정 생성 및 출석 체크
- **커뮤니티**: 게시판, 댓글, 좋아요, 갤러리
- **AI 챗봇**: OpenAI GPT 기반 동호회 추천 챗봇
- **알림**: 실시간 알림 시스템

## 기술 스택

### Backend

- Java 17
- Spring Boot 3.5.5
- Spring Security + JWT
- MyBatis
- Oracle 21c
- WebSocket (STOMP)
- AWS S3
- OpenAI API

### Frontend

- React 19
- Vite 7
- Tailwind CSS 4
- Zustand
- React Router DOM
- Axios
- FullCalendar
- Chart.js
- Quill Editor

### Infrastructure

- Docker
- GitHub Actions (CI/CD)
- AWS EC2
- Nginx

## 설치 및 실행

### 사전 요구사항

- Java 17
- Node.js 20.19.0 이상
- Oracle 21c
- Docker

## API 문서

Swagger UI: `http://localhost:8080/swagger-ui.html`

## 데이터베이스 스키마

주요 테이블:

- MEMBER: 회원 정보
- CLUB: 동호회 정보
- SCHEDULE: 일정 정보
- POST: 게시글
- NOTIFICATION: 알림

## 프로젝트 구조
```
linkle/
├── back/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/ggamakun/linkle/
│   │   │   │   ├── domain/
│   │   │   │   ├── global/
│   │   │   │   └── LinkkleApplication.java
│   │   │   └── resources/
│   │   │       ├── mapper/
│   │   │       └── application.yml
│   │   └── test/
│   └── build.gradle
└── front/
    ├── src/
    │   ├── components/
    │   ├── pages/
    │   ├── services/
    │   ├── store/
    │   └── utils/
    ├── package.json
    └── vite.config.js
```

## 주요 기능 구현

### 인증/인가

- JWT 기반 인증
- 이메일 인증

### 동호회 관리

- 역할 기반 권한 (LEADER, MANAGER, MEMBER)
- 회원 가입 승인 시스템
- 대시보드 통계 (출석률, 연령 분포, 성비, 분기별 가입)

### 실시간 기능

- 실시간 알림
