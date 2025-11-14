# yangganag523
강경아 소개용 레포지토리입니다. 


---

# [🎼 Melog — Classical Music Social Platform](https://github.com/Melog-Osunji/melog_backend2)

**Spring Boot 기반 음악 감상 기록/공유 SNS — 전체 백엔드 아키텍처를 직접 설계·구현한 개인 프로젝트**

Melog는 클래식 음악 감상을 기록하고 공유하는 모바일 SNS입니다.
사용자가 음악 취향을 자유롭게 표현하고, 일정을 관리하며, 콘텐츠를 탐색할 수 있도록
백엔드 아키텍처를 **처음부터 끝까지 설계**하고 실제 서비스 수준으로 운영했습니다.

<br>

---

# 🚀 Tech Stack

### **Backend**

* Spring Boot 3.x
* JPA(Hibernate), Query Optimization
* PostgreSQL
* Redis (Token / Session / Security)
* Elasticsearch 8.x (검색 / 피드 추천)

### **Infrastructure**

* Docker · Docker Compose
* Raspberry Pi 5 (ARM64 실서버 운영)
* Cloudflare DNS/SSL (HTTPS 구축)
* GitHub Actions (CI/CD Pipeline)

### **Auth / Security**

* JWT Access & Refresh Token
* JTI 기반 재사용 차단
* Redis TTL 기반 Sliding Refresh
* Google · Kakao OIDC Login

<br>

---

# 🧩 Architecture Overview

```
┌────────────────────────────┐
│        Mobile App          │  (React Native)
└──────────────┬─────────────┘
               │ REST API
┌──────────────▼─────────────┐
│      Spring Boot API        │
│  ─ User / Post / Feed       │
│  ─ Calendar / Alarm         │
│  ─ JWT Auth / OIDC          │
│  ─ Elasticsearch Querying   │
└───────┬───────────┬────────┘
        │           │
┌───────▼───┐   ┌───▼──────────┐
│PostgreSQL │   │    Redis      │
│ RDB Core  │   │Token/Session  │
└───────┬───┘   └───┬──────────┘
        │           │
┌───────▼───────────▼───────────┐
│     Elasticsearch Cluster      │
│ - Post Indexing / Search       │
│ - Feed Ranking Experiments     │
└────────────────────────────────┘

Infra: Docker Compose on Raspberry Pi + Cloudflare HTTPS
```

<br>

---

# 🔑 Key Features

## **1. 인증 · 보안 시스템(JWT / JTI / Redis)**

* Access/Refresh Token 직접 설계
* Refresh Token 저장 시 SHA-256 해시 처리
* Redis에 사용자별 JTI 저장 → **재사용 탐지 & 차단**
* Refresh Token Sliding Window 구조 구현
* 유저 경험 개선을 위한 Access Token 자동 재발급 흐름 설계
* Kakao/Google OIDC 연동(JWKS 검증/Clock Skew 처리 포함)

---

## **2. 게시물 · 피드 시스템**

* 미디어 포함 여부, Hidden Users 필터링, 작성자 Fetch 등
  **복합 조건을 처리하는 JPQL 기반 조회 최적화**
* N+1 문제 제거(Fetch Join / Batch Size 적용)
* readOnly 트랜잭션 전략으로 시스템 부하 감소
* Elasticsearch 기반 통합 검색·추천 구조 구축

---

## **3. 캘린더 · 알람 모듈**

* KCISA OpenAPI 연동(전시·공연 정보 수집)
* EventSchedule ↔ EventAlarm **1:N 관계 직접 모델링**
* 일정 & 알람 동시 생성/삭제 로직 구현
* “두 번 요청하면 toggle” 과 같은 실사용 패턴 처리
* calendar ensure → schedule/alarm 무결성 보장
* 중복 생성 시 DB 무결성 409 처리 설계

---

## **4. Docker 기반 인프라 운영**

* Raspberry Pi 5(ARM64) 환경에서 Docker Compose로
  PostgreSQL, Redis, Elasticsearch, Spring Boot 컨테이너 오케스트레이션
* ARM 기반 메모리 이슈 해결 & JVM 메모리 튜닝 경험
* Cloudflare SSL/TLS 구성으로 HTTPS 실서비스 구축

---

## **5. CI/CD Pipeline**

* GitHub Actions 기반 빌드/배포 자동화 구축
* Gradle 캐싱, 멀티 브랜치 전략(develop → deploy) 적용
* Docker 이미지 빌드 후 Raspberry Pi 원격 배포(예정)

<br>

---

# 📦 Directory Overview

```
melog-backend/
├── src/
│   ├── main/java/com/osunji/melog/
│   │   ├── user/
│   │   ├── post/
│   │   ├── feed/
│   │   ├── calendar/
│   │   ├── global/security/
│   │   └── ...
│   └── resources/
│       ├── application.yml
│       └── ...
├── docker/
│   ├── docker-compose.yml
│   └── elasticsearch/
└── README.md
```

<br>

---

# 📈 주요 개발 포인트

* **도메인 설계부터 인프라 운영까지 “전체 기술 스택”을 완성한 프로젝트**
* JWT/JTI 기반 보안 구조 등 **실서비스 수준의 인증 시스템** 구현
* Elasticsearch 기반 검색·추천 기능 연구 및 적용
* Docker 활용해 **개인 서버 환경을 안정적인 서비스 환경으로 전환**
* 팀 리딩 경험(프론트/디자인 협업, API 명세 공유, 구조 설계)

<br>

---

# 📮 Contact

문의 또는 피드백은 Issue/PR로 남겨주세요.
개인 연락처는 GitHub Profile 참고 부탁드립니다. 

---

