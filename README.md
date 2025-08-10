# n-won-challenge-backend
# README — N간히 써(엔간히 써) 🏋️💸

서로 **“N원 이하 소비 챌린지”**에 참여하며 *재미있게* 소비 습관을 개선하는 게이미피케이션 서비스입니다. 매일 06:00 자동 생성되는 챌린지 방에서 목표 금액 안에 버티면 포인트를 받고, 포인트로 기프티콘을 사 보세요!

***

## 프로젝트 개요
- **문제의식**  
  이제 막 경제생활을 시작한 대학생·사회초년생은 충동 소비를 하더라도 이를 제어할 *동기*가 부족합니다.  
- **해결책**  
  1) *경쟁*·*보상* 요소가 있는 N원 챌린지로 지출을 게임처럼 관리  
  2) 성공 포인트를 **상품권·기프티콘** 구매에 사용해 즉각적인 보상 제공  
- **핵심 기능**  
  - 매일 06:00 목표 금액별 챌린지 방 자동 생성  
  - 계좌 잔액 & 지출 데이터 연동 → 목표 초과 시 즉시 탈락  
  - 성공자에게 포인트 차등 지급, 포인트로 상점 상품 구매  
  - 랭킹·캐릭터 커스터마이징으로 장기 참여 유도  

***

## 기술 스택 & 아키텍처
- **Front-End**: React 18, TypeScript, Vite  
- **Back-End**: Spring Boot 3 (Java 17)  
- **DB/ORM**: MySQL 8 + JPA (Hibernate)  
- **CI/CD**: GitHub Actions → Docker → AWS ECS  
- **외부 API**: 신한 Open API (인증, 계좌·잔액 조회)  

```
[Client] ── HTTPS ──> [API Gateway] ──> [Spring Boot App]
                                          │  │  │
                              ┌───────────┴──┴──┴───────────┐
                              ▼           ▼          ▼      ▼
                       인증도메인   지출·계좌도메인   챌린지도메인   포인트·상점
                              └────────── MySQL (RDS) ───────┘
```

***

## 디렉터리 구조 (백엔드)

```
backend/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/nspend/nspend/
│   │   │       ├── Application.java        # SpringBoot 메인
│   │   │       ├── controller/             # REST API
│   │   │       ├── service/                # 비즈니스 로직
│   │   │       ├── repository/             # JPA, QueryDSL
│   │   │       ├── domain/                 # entity, dto, vo
│   │   │       ├── config/                 # Security, Swagger
│   │   │       ├── exception/              # 글로벌 예외
│   │   │       └── utils/                  # 공통 유틸
│   │   ├── resources/
│   │   │   ├── application.yml
│   │   │   ├── static/
│   │   │   └── templates/
│   │   └── config/                         # logback 등
│   └── test/
│       ├── java/
│       └── resources/
├── build.gradle
├── Dockerfile
├── .env
└── README.md
```


## API 요약

| 메서드 | 엔드포인트 | 설명 |
| --- | --- | --- |
| POST | /auth/login | 신한 OAuth 토큰 발급 |
| GET | /challenges/today | 오늘 생성된 챌린지 목록 |
| POST | /challenges/{id}/join | 챌린지 참여 신청 |
| GET | /expenses | 당일 지출 내역 조회 |
| POST | /rewards/{itemId}/purchase | 포인트로 상품 구매 |

***



## 팀 / 연락처

| 역할 | 이름 | 이메일 |
| --- | --- | --- |
| 팀장·FE | 안지원 | anjiwon@example.com |
| BE(지출·계좌) | 박지원 | parkjw@example.com |
| BE(인증·사용자·뱃지) | 이은지 | leeyj@example.com |
| BE(공통 인프라·API) | 조문희 | jomunhee@example.com |
| BE(챌린지·참여) | 진광환 | jingh@example.com |
