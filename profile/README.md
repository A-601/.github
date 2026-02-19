# 🌌 Project A601

> "서기 2324년, 중앙 AI가 지배하는 우주선에 오신 것을 환영합니다."

AI 판사 기반 몰입형 SF 서바이벌 마피아 게임 프로젝트입니다.

### 플랫폼 : 웹
### 개발 기간 : 2026.01.06 ~ 2026.02.13
### 개발 인원 : 4명

<img src="./docs/app.png" alt = "logo" width= "800">


## 팀원 구성

<img src="./docs/team.png" alt = "team" width= "800">


## 🚀 Getting Started

### 1. 사전 준비 (Prerequisites)
- Docker & Docker Compose
- Node.js 20+ (로컬 IDE용)
- Java 17 (로컬 IDE용)

### 2. 실행 방법 (Local Development)

```bash
# 1. 프로젝트 초기화 (최초 1회)
chmod +x ./scripts/*.sh # 리눅스일시
./scripts/init.sh

# 2. .env 파일 수정
# 생성된 .env 파일에 환경 변수 등을 입력하세요.

# 3. 개발 시작
# 3-a. 인프라만 실행 (AI, MySQL, Redis, LiveKit)
docker-compose up -d

# 3-b. 각 서비스 실행 (개별 터미널 사용 권장)
# Backend
cd backend && ./gradlew bootrun

# Frontend
cd frontend && npm run dev

```

### 3. 접속 정보 (로컬 기준)
| 서비스 | URL | 비고 |
|---|---|---|
| Frontend | http://localhost:5173 | React 개발 서버 |
| Backend | http://localhost:8080/swagger-ui/index.html | API 문서 |
| AI Server | http://localhost:8000/docs | AI API 문서 |
| LiveKit | http://localhost:7880 | WebRTC Media Server |
| Dozzle| https://localhost:8888 | 전체 컨테이너 Log 및 사용률 확인 |
| redis-commander | http://localhost:8081 | redis 관리 |

## ⚠️ 환경 변수 및 인프라 가이드
### 환경 변수 관리
- 모든 Secret Key는 `.env` 파일에서 관리하며 Git에 업로드하지 않습니다.
- 운영 배포 시 Jenkins 파이프라인을 통해 환경 변수가 주입됩니다.


## 🛠 Tech Stack

| Layer | Technologies |
|---|---|
| **Frontend** | React 18, Vite, React Vits, TailwindCSS, StompJS, Antd, Axios, Livekit-client, Zustand, React-OAuth |
| **Backend** | Spring Boot 3.5.9, Java 17, JPA, Redis, MySQL, WebSocket, Security, livekit, JWT, Swagger, Email SMTP, OAuth2 |
| **AI** | Python 3.11, FastAPI, OpenAI API, Uvicorn |
| **Infra** | Docker Compose, Nginx, Dozzle, RedisCommander |


## 시스템 아키텍처
<img src="./docs/architecture.png" alt = "team" width= "800">

## 기능 구성

### 로그인

<img src="./docs/login.png" alt = "team" width= "800">

### 마이페이지

<img src="./docs/mypage.png" alt = "team" width= "800">

### 메인 로비

<img src="./docs/main.png" alt = "team" width= "800">

### 게임 대기방

<img src="./docs/lobby.png" alt = "team" width= "800">

### 인게임 화면

#### 직업 배정

<img src="./docs/role.gif" alt = "team" width= "800">

#### 낮 화면

<img src="./docs/day.gif" alt = "team" width= "800">

#### 밤 화면

<img src="./docs/night.gif" alt = "team" width= "800">

#### AI 변론 화면

<img src="./docs/pleading.gif" alt = "team" width= "800">

<img src="./docs/judgment.gif" alt = "team" width= "800">

### 능력 사용

#### 시스템 엔지니어
<img src="./docs/sys.gif" alt = "team" width= "800">

#### 외계인
<img src="./docs/alien.gif" alt = "team" width= "800">

#### 영상 엔지니어
<img src="./docs/cam.gif" alt = "team" width= "800">

#### 밀항자
<img src="./docs/milhangza.gif" alt = "team" width= "800">

## 디렉토리 구조

### Backend
```
.
|-- backend/                                # Spring Boot backend (REST API, WebSocket, Auth)
|   |-- build.gradle                        # Gradle 빌드 스크립트
|   |-- Dockerfile                          # 컨테이너 이미지를 위한 Dockerfile
|   |-- gradlew / gradlew.bat               # 로컬 빌드/실행 래퍼
|   |-- src/
|   |   |-- main/
|   |   |   |-- java/
|   |   |   |   |-- com/
|   |   |   |   |   |-- project/
|   |   |   |   |   |   |-- controller/     # HTTP 요청을 처리하는 컨트롤러
|   |   |   |   |   |   |-- service/        # 비즈니스 로직
|   |   |   |   |   |   |-- repository/     # JPA 리포지토리 (데이터 접근)
|   |   |   |   |   |   |-- domain/         # 엔티티 / 도메인 모델
|   |   |   |   |   |   |-- dto/            # 요청/응답용 DTO
|   |   |   |   |   |   |-- config/         # Spring 설정 클래스
|   |   |   |   |   |   |-- security/       # 인증/인가 관련 (JWT, OAuth2)
|   |   |   |   |   |   |-- websocket/      # WebSocket 핸들러/구성
|   |   |   |-- resources/
|   |   |   |   |-- application.properties   # 애플리케이션 설정
|   |   |   |   |-- static/                  # 정적 파일 (필요 시)
|   |   |   |   |-- templates/               # 서버템플릿 (Thymeleaf 등, 필요 시)
|   |   |-- test/                            # 단위/통합 테스트
|   |-- init.sql                             # DB 초기 스크립트
|   |-- scripts/                             # 배포/운영/편의 스크립트
```

### Frontend
```
|-- frontend/                                # React + Vite 프론트엔드
|   |-- package.json                         # npm/패키지 설정
|   |-- vite.config.js                       # Vite 설정
|   |-- tailwind.config.js                   # Tailwind 설정
|   |-- src/
|   |   |-- main.jsx                         # 엔트리 포인트
|   |   |-- index.css                         # 전역 스타일
|   |   |-- api/                              # 서버 호출 로직 (Axios instance, endpoints)
|   |   |-- components/                       # 재사용 컴포넌트
|   |   |-- pages/                            # 페이지 컴포넌트
|   |   |-- router/                           # 라우팅 설정
|   |   |-- store/                            # Zustand 또는 Redux 상태 관리
|   |   |-- assets/                           # 이미지, 폰트 등 정적 자산
|   |-- public/                               # 정적 퍼블릭 파일
```

### AI
```
|-- ai/                                      # AI 서비스 (FastAPI, 모델 로직)
|   |-- Dockerfile                           # AI 컨테이너 이미지
|   |-- requirements.txt                     # Python 의존성
|   |-- app/
|   |   |-- main.py                          # FastAPI 엔트리
|   |   |-- core/
|   |   |   |-- config.py                     # 설정 관리
|   |   |   |-- preprocess.py                 # 데이터 전처리 유틸
|   |   |-- models/                           # 모델 정의/로딩 코드
|   |   |-- routers/                          # API 라우터 모듈
|   |   |-- services/                         # 모델 추론 및 유틸 서비스
```

### Infra
```
|-- root/                                   # 인프라/배포 관련 설정
|-- docker-compose.yml                    # 로컬 개발용 Compose
|-- docker-compose.prod.yml               # 프로덕션용 Compose
|-- livekit.yaml                          # LiveKit 설정
|-- Jenkinsfile                           # CI/CD 파이프라인
|-- scripts/                              # 인프라 관련 스크립트
|-- docs/                                    # 문서 및 이미지
|-- README.md                                # 프로젝트 문서
```


## 프로젝트 산출물

### ERD 

<img src="./docs/erd.png" alt = "team" width= "800">

### Swagger API Docs 

<img src="./docs/swagger_1.png" alt = "team" width= "800">


<img src="./docs/swagger_2.png" alt = "team" width= "800">


<img src="./docs/swagger_3.png" alt = "team" width= "800">


<img src="./docs/swagger_4.png" alt = "team" width= "800">


<img src="./docs/swagger_5.png" alt = "team" width= "800">


### <a href="https://drive.google.com/file/d/1U3-hgDkIL4uVr8fKiIEmFyrDxVgn_6zn/view?usp=drive_link">영상 포트폴리오</a>

### <a href="https://wind-oval-efe.notion.site/2e6eb24de535818cb00ed97ea1a1d208?pvs=73">기능 명세서</a>

### <a href="https://wind-oval-efe.notion.site/API-2e2eb24de53581e4b3e4c9d9eee76863?pvs=74">API 명세서 </a>

### <a href="https://docs.google.com/spreadsheets/d/1QTYnJbTTe41X3c6OtbqZKlY-3x4Qjuwpz5bJQpaAs_4/edit?usp=drive_link">간트차트</a>
