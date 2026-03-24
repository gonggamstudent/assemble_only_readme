# 🚀 Electron Host - AI 에이전트 간 통신 플랫폼

<div align="center">

![Version](https://img.shields.io/badge/version-0.1.0-blue.svg)
![Electron](https://img.shields.io/badge/Electron-13.0.0-47848f.svg)
![Vue.js](https://img.shields.io/badge/Vue.js-3.2.13-4fc08d.svg)
![Node.js](https://img.shields.io/badge/Node.js-Latest-339933.svg)
![Docker](https://img.shields.io/badge/Docker-Ready-2496ED.svg)

**A2A 프로토콜을 지원하는 강력한 Electron 기반 AI 에이전트 오케스트레이션 플랫폼**

[기능](#-기능) • [빠른 시작](#-빠른-시작) • [아키텍처](#-아키텍처) • [클라이언트](#-클라이언트-통합) • [배포](#-배포)

</div>

---

## 🌟 기능

### 🤖 **멀티 에이전트 시스템**
- **채팅 에이전트** - Google Gemini & Anthropic Claude 기반 대화형 AI
- **이미지 에이전트** - AI 기반 이미지 생성 및 처리
- **음악 에이전트** - 오디오 콘텐츠 생성 및 조작
- **스토리 에이전트** - 창작 글쓰기 및 내러티브 생성
- **코드 에이전트** - 프로그래밍 지원 및 코드 생성
- **DeepSick 에이전트** - 전문 도메인 에이전트

### 🔗 **A2A 프로토콜 통합**
- 완전한 Agent2Agent 프로토콜 준수
- 실시간 에이전트 간 통신
- 작업 오케스트레이션 및 위임
- 컨텍스트 보존을 위한 세션 관리
- **WebSocket 기반 스트리밍 통신** (HTTP SSE에서 업그레이드)

### 🏗️ **엔터프라이즈급 아키텍처**
- **Thin Client 패턴** - 클라이언트는 UI만 담당, 모든 로직은 서버에서 처리
- **Vue.js 프론트엔드**를 가진 **Electron 데스크톱 애플리케이션**
- **SQLite 데이터베이스**를 가진 **Express.js 백엔드**
- **Docker 기반 프로덕션 배포**
- **WebSocket 프록시** - 클라이언트와 서버 간 안전한 통신 중계
- **JWT 인증 & 권한 부여**
- **속도 제한 & 사용량 분석**
- **파일 업로드 & 처리 서비스**

### 🛡️ **보안 & 관리**
- 사용자 인증 및 역할 기반 액세스 제어
- API 키 및 서버 정보 완전 은닉 (클라이언트에서 접근 불가)
- 요청 속도 제한 및 사용량 모니터링
- 안전한 파일 업로드 및 처리
- 실시간 클라이언트 모니터링 및 제어
- 포괄적인 감사 로깅

---

## 🏗️ 아키텍처

### 전체 시스템 구조
```
┌─────────────────────────────────────────────────────────┐
│                Unity EditorWindow                       │
│                   (Thin Client)                         │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │
│  │     UI      │  │  WebSocket  │  │   Payload   │     │
│  │   로직만    │  │    통신     │  │   파싱      │     │
│  └─────────────┘  └─────────────┘  └─────────────┘     │
└─────────────────────────────────────────────────────────┘
                             │ ws://host:8282
                             ▼
┌─────────────────────────────────────────────────────────┐
│                 Electron 호스트 앱                       │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │
│  │  WebSocket  │  │ 클라이언트  │  │   관리      │     │
│  │   서버      │  │ 모니터링    │  │  대시보드   │     │
│  └─────────────┘  └─────────────┘  └─────────────┘     │
└─────────────────────────────────────────────────────────┘
                             │ HTTP Proxy
                             ▼
┌─────────────────────────────────────────────────────────┐
│                   Express.js 서버                       │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │
│  │    인증     │  │   라우트    │  │  미들웨어   │     │
│  │   서비스    │  │   핸들러    │  │    계층     │     │
│  └─────────────┘  └─────────────┘  └─────────────┘     │
└─────────────────────────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────┐
│                  A2A 호스트 에이전트                      │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │
│  │ 태스크 저장 │  │   세션      │  │   의도      │     │
│  │   관리자    │  │   관리자    │  │  분류기     │     │
│  └─────────────┘  └─────────────┘  └─────────────┘     │
└─────────────────────────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────┐
│                  전문 에이전트들                          │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │
│  │    채팅     │  │   이미지    │  │    음악     │     │
│  │   에이전트  │  │   에이전트  │  │   에이전트  │     │
│  └─────────────┘  └─────────────┘  └─────────────┘     │
│  ┌─────────────┐  ┌─────────────┐                       │
│  │   스토리    │  │    코드     │                       │
│  │   에이전트  │  │   에이전트  │                       │
│  └─────────────┘  └─────────────┘                       │
└─────────────────────────────────────────────────────────┘
```

### 보안 설계 원칙
- **완전한 정보 은닉**: 클라이언트는 API 키, 서버 주소, 내부 로직을 전혀 알 수 없음
- **중앙 집중 제어**: 모든 요청이 호스트를 거쳐 검증 및 로깅
- **실시간 모니터링**: 클라이언트 상태 및 사용 패턴 실시간 추적
- **Zero-Maintenance Client**: 클라이언트 업데이트 없이 서버 측 기능 확장 가능

---

## 🚀 빠른 시작

### 필수 요구사항

```bash
node >= 16.0.0
npm >= 8.0.0
docker >= 20.10.0 (프로덕션 배포용)
```

### 로컬 개발환경 설치

```bash
# 저장소 클론
git clone <repository-url>
cd electron-host

# 의존성 설치
npm install

# 환경 변수 설정
cp .env.example .env
# API 키와 설정으로 .env 파일 편집
```

### 개발 환경 실행

```bash
# Express.js 서버 시작 (포트 8282)
npm run server

# A2A 호스트 에이전트 시작
npm run host:start

# 개별 에이전트들 시작
npm run chatagent:start
npm run imageagent:start
npm run musicagent:start
npm run storyagent:start
npm run codeagent:start

# Electron 호스트 앱 시작 (WebSocket 서버 포트 8282)
npm run electron:serve

# Vue.js 개발 서버 시작 (관리 대시보드)
npm run serve
```

---

## 🤖 에이전트

### 🗣️ 채팅 에이전트
**포트: 10001**
- 멀티 프로바이더 지원 대화형 AI (Gemini, Claude)
- 컨텍스트 인식 대화 관리
- 실시간 스트리밍 응답

### 🎨 이미지 에이전트  
**포트: 10002**
- AI 이미지 생성 및 처리
- 아티팩트 기반 파일 관리 (raw data / downloadURL)
- 다중 포맷 지원 (PNG, JPG, WebP)

### 🎵 음악 에이전트
**포트: 10003**
- 오디오 콘텐츠 생성
- 음악 작곡 지원
- 사운드 이펙트 제작

### 📚 스토리 에이전트
**포트: 10004**
- 창작 글쓰기 지원
- 내러티브 구조 생성
- 캐릭터 및 플롯 개발

### 💻 코드 에이전트
**포트: 10005**
- 프로그래밍 지원
- 코드 생성 및 리팩토링
- 다중 언어 지원

---

## 🎮 클라이언트 통합

### Unity EditorWindow 클라이언트
**WebSocket 연결**: `ws://host:8282`

```csharp
// Unity 클라이언트 연결 예시
using UnityEngine;
using System;
using WebSocketSharp;

public class HostConnector : MonoBehaviour 
{
    private WebSocket ws;
    
    void Start() 
    {
        // 호스트 앱에만 연결 (서버 정보 불필요)
        ws = new WebSocket("ws://localhost:8282");
        ws.OnMessage += OnMessageReceived;
        ws.Connect();
    }
    
    void OnMessageReceived(object sender, MessageEventArgs e) 
    {
        // 응답 처리 및 UI 업데이트
        ProcessResponse(e.Data);
    }
}
```

### 클라이언트 특징
- **Thin Client**: UI 로직과 통신 로직만 포함
- **Zero Configuration**: API 키나 서버 설정 불필요
- **Real-time**: WebSocket 기반 실시간 양방향 통신
- **Private Distribution**: DLL 형태로 보안 배포 가능

---

## 📁 프로젝트 구조

```
electron-host/
  ├── src/                                    # Vue.js 프론트엔드 소스
  │   ├── App.vue                            # 메인 Vue 앱 컴포넌트   
  │   ├── APP_backup.vue                     # 앱 백업 파일
  │   ├── ClientsView.vue                    # 클라이언트 뷰
  │   ├── clientspanel_backup.vue            # 클라이언트 패널 백업   
  │   ├── main.js                            # Vue 앱 진입점
  │   ├── background.js                      # Electron 메인 프로세스
  │   ├── preload.js                         # Electron 프리로드 스크립트
  │   ├── index.css                          # 글로벌 CSS
  │   ├── 레거시백업.vue                      # 레거시 백업 파일
  │   ├── 뭐백업인갑지.vue                    # 추가 백업 파일
  │   ├── components/                        # 재사용 가능한 Vue 컴포넌트
  │   │   ├── HelloWorld.vue                 # 헬로월드 컴포넌트
  │   │   ├── NotificationContainer.vue      # 알림 컨테이너
  │   │   └── modals/                        # 모달 컴포넌트들
  │   │       ├── ConfirmModal.vue           # 확인 모달
  │   │       ├── LimitSettingsModal.vue     # 제한 설정 모달
  │   │       ├── LogDetailsModal.vue        # 로그 상세 모달
  │   │       ├── PasswordChangeModal.vue    # 비밀번호 변경 모달
  │   │       ├── ProfileModal.vue           # 프로필 모달
  │   │       ├── RegisterModal.vue          # 등록 모달
  │   │       ├── RejectReasonModal.vue      # 거부 사유 모달
  │   │       ├── RequestDetailsModal.vue    # 요청 상세 모달
  │   │       ├── RoleChangeModal.vue        # 역할 변경 모달
  │   │       ├── SettingsModal.vue          # 설정 모달
  │   │       └── ToggleSwitch.vue           # 토글 스위치
  │   ├── views/                             # 페이지 뷰 컴포넌트
  │   │   ├── AIPanel.vue                    # AI 패널
  │   │   ├── AnalyticsPanel.vue             # 분석 패널
  │   │   ├── ClientsPanel.vue               # 클라이언트 패널
  │   │   ├── ExtensionsPanel.vue            # 확장 패널
  │   │   ├── IdRequestsPanel.vue            # ID 요청 패널
  │   │   ├── LoginPanel.vue                 # 로그인 패널
  │   │   ├── OverviewPanel.vue              # 개요 패널
  │   │   ├── SettingsPanel.vue              # 설정 패널
  │   │   ├── log.vue                        # 로그 뷰
  │   │   ├── test.vue                       # 테스트 뷰 1
  │   │   └── test2.vue                      # 테스트 뷰 2
  │   ├── services/                          # 클라이언트 서비스 레이어
  │   │   ├── a2aService.js                  # A2A 프로토콜 서비스
  │   │   ├── aiProxyService.js              # AI 프록시 서비스
  │   │   ├── apiService.js                  # API 통신 서비스
  │   │   ├── authService.js                 # 인증 서비스
  │   │   ├── mcpService.js                  # MCP 서비스
  │   │   ├── notificationService.js         # 알림 서비스
  │   │   ├── ragService.js                  # RAG 서비스
  │   │   └── websocketService.js            # WebSocket 서비스
  │   ├── utils/                             # 유틸리티 함수
  │   │   ├── a2a-client.js                  # A2A 클라이언트 유틸
  │   │   └── eventutil.js                   # 이벤트 유틸리티
  │   ├── config/                            # 설정 파일
  │   │   └── index.js                       # 메인 설정
  │   ├── plugins/                           # Vue 플러그인
  │   │   ├── vuetify.js                     # Vuetify 설정
  │   │   └── webfontloader.js               # 웹폰트 로더
  │   ├── router/                            # Vue 라우터
  │   │   └── index.js                       # 라우터 설정
  │   └── assets/                            # 정적 자산
  │       ├── logo.png                       # 로고 PNG
  │       └── logo.svg                       # 로고 SVG
  ├── server/                                # Express.js 백엔드 서버
  │   ├── index.js                           # 서버 진입점
  │   ├── main.js                            # 메인 서버 파일
  │   ├── server_context_backup.js           # 서버 컨텍스트 백업
  │   ├── aitool_host_data.sqlite            # 메인 데이터베이스
  │   ├── 컨텍스트수정중aitool_host_data.sqlite # 수정 중인 DB
  │   ├── ______________aitool_host_data.sqlite # DB 백업들
  │   ├── ___________aitool_host_data.sqlite
  │   ├── _________aitool_host_data.sqlite
  │   ├── _______aitool_host_data.sqlite
  │   ├── ______aitool_host_data.sqlite
  │   ├── _____aitool_host_data.sqlite
  │   ├── ____aitool_host_data.sqlite
  │   ├── __aitool_host_data.sqlite
  │   ├── _aitool_host_data.sqlite
  │   ├── a2a/                               # A2A 프로토콜 구현
  │   │   ├── client.js                      # A2A 클라이언트
  │   │   ├── error.js                       # 에러 핸들링
  │   │   ├── schema.js                      # 데이터 스키마
  │   │   ├── store.js                       # 데이터 스토어
  │   │   ├── streaming.js                   # 스트리밍 처리
  │   │   ├── utils.js                       # A2A 유틸리티
  │   │   ├── start-bridge.js                # 브릿지 시작 스크립트
  │   │   ├── agents/                        # AI 에이전트들
  │   │   │   ├── chat-agent/                # 채팅 에이전트
  │   │   │   │   └── server.js
  │   │   │   ├── code-agent/                # 코드 에이전트
  │   │   │   │   └── server.js
  │   │   │   ├── deepsick-agent/            # 딥식 에이전트
  │   │   │   │   └── server.js
  │   │   │   ├── image-agent/               # 이미지 에이전트
  │   │   │   │   └── server.js
  │   │   │   ├── music-agent/               # 음악 에이전트
  │   │   │   │   └── server.js
  │   │   │   └── story-agent/               # 스토리 에이전트
  │   │   │       └── server.js
  │   │   ├── host/                          # 호스트 관리
  │   │   │   ├── agentRegistry.js           # 에이전트 레지스트리
  │   │   │   ├── host server..js            # 호스트 서버
  │   │   │   ├── hostAgent.js               # 호스트 에이전트
  │   │   │   └── intentClassifier.js        # 의도 분류기
  │   │   ├── services/                      # A2A 서비스들
  │   │   │   ├── artifactProcessingService.js # 아티팩트 처리
  │   │   │   ├── fileUploadService.js       # 파일 업로드
  │   │   │   ├── permissionManager.js       # 권한 관리
  │   │   │   ├── ragService.js              # RAG 서비스
  │   │   │   ├── realtimeNotificationService.js # 실시간 알림
  │   │   │   └── usageLimiterService.js     # 사용량 제한
  │   │   ├── config/                        # A2A 설정
  │   │   │   ├── agent.json                 # 에이전트 설정
  │   │   │   └── system.json                # 시스템 설정
  │   │   ├── utils/                         # A2A 유틸리티
  │   │   │   ├── errorHandler.js            # 에러 핸들러
  │   │   │   └── logger.js                  # 로거
  │   │   └── websocket/                     # WebSocket 구현
  │   │       ├── a2a-bridge.js              # A2A 브릿지
  │   │       └── server.js                  # WebSocket 서버
  │   ├── routes/                            # Express 라우트
  │   │   ├── a2a.js                         # A2A 라우트
  │   │   ├── ai.js                          # AI 라우트
  │   │   ├── analytics.js                   # 분석 라우트
  │   │   ├── chat.js                        # 채팅 라우트
  │   │   ├── unityClient.js                 # Unity 클라이언트 라우트
  │   │   └── unitybridge.js                 # Unity 브릿지 라우트
  │   ├── middleware/                        # Express 미들웨어
  │   │   └── auth.js                        # 인증 미들웨어
  │   ├── services/                          # 백엔드 서비스
  │   │   ├── chatservice.js                 # 채팅 서비스
  │   │   ├── fileservice.js                 # 파일 서비스
  │   │   └── limiterservice.js              # 제한 서비스
  │   ├── database/                          # 데이터베이스
  │   │   └── authSchema.js                  # 인증 스키마
  │   ├── uploads/                           # 업로드된 파일
  │   └── generated_image_folder/            # 이미지 생성 폴더
  ├── data/                                  # 데이터 저장소
  │   ├── a2a.db                             # A2A 데이터베이스
  │   ├── auth.db                            # 인증 데이터베이스
  │   └── rag.db                             # RAG 데이터베이스
  ├── public/                                # 정적 파일
  ├── dist_electron/                         # Electron 빌드 결과
  │   ├── aitool.zip                         # 압축된 앱
  │   ├── builder-debug.yml                  # 빌더 디버그 설정
  │   ├── builder-effective-config.yaml      # 빌더 효과적 설정
  │   ├── index.js                           # 빌드된 메인 파일
  │   ├── package.json                       # 빌드된 패키지 설정
  │   ├── electron-host Setup 0.1.0.exe      # Windows 설치 파일
  │   ├── electron-host Setup 0.1.0.exe.blockmap # 블록맵
  │   ├── bundled/                           # 번들된 웹 자산
  │   └── win-unpacked/                      # Windows 언패킹된 앱
  ├── node_modules/                          # NPM 의존성
  ├── package.json                           # 프로젝트 설정
  ├── package-lock.json                      # 의존성 잠금 파일
  ├── vue.config.js                          # Vue CLI 설정
  ├── babel.config.js                        # Babel 설정
  ├── jsconfig.json                          # JavaScript 설정
  ├── postcss.config.js                     # PostCSS 설정
  ├── tailwind.config.js                    # Tailwind CSS 설정
  ├── Dockerfile                             # Docker 이미지 설정
  ├── unity_client.cs                        # Unity 클라이언트 코드
  ├── a2a_standard_server.js                 # A2A 표준 서버
  ├── filelist.txt                          # 파일 목록
  ├── README.md                              # 프로젝트 문서
  ├── 에이전트 시작.txt                       # 에이전트 시작 가이드
  └── 할거.txt                               # 할 일 목록
```

---

## 🔧 설정

### 환경 변수

```bash
# API 키
GOOGLE_API_KEY=your_google_api_key
ANTHROPIC_API_KEY=your_anthropic_api_key
OPENAI_API_KEY=your_openai_api_key

# 서버 설정
PORT=8282                      # Express.js 서버 포트
WEBSOCKET_PORT=8282           # WebSocket 서버 포트
HOST_AGENT_PORT=10000         # A2A 호스트 에이전트

# 데이터베이스
DB_PATH=./data/aitool_host_data.sqlite

# 보안
JWT_SECRET=your_jwt_secret
BCRYPT_ROUNDS=12

# 업로드 설정
UPLOAD_MAX_SIZE=50MB
UPLOAD_ALLOWED_TYPES=image/*,audio/*,text/*
UPLOAD_PATH=./uploads

# 프로덕션 설정
NODE_ENV=production
SERVER_HOST=your_server_ip
BASE_URL=http://your_server_ip:8282
```

---

## 🐳 배포

### Docker를 이용한 프로덕션 배포

#### 1. Docker 이미지 빌드
```bash
# 전체 서비스 빌드
docker-compose build

# 개별 서비스 빌드
docker build -t electron-host .
```

#### 2. 환경별 배포
```bash
# 개발 환경
docker-compose -f docker-compose.dev.yml up -d

# 프로덕션 환경
docker-compose -f docker-compose.prod.yml up -d
```

#### 3. 서비스 관리
```bash
# 모든 서비스 시작
docker-compose up -d

# 특정 서비스 재시작
docker-compose restart host-app
docker-compose restart express-server

# 로그 확인
docker-compose logs -f

# 서비스 중지
docker-compose stop
```

### Docker Compose 설정 예시
```yaml
version: '3.8'

services:
  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf
    
  host-app:
    build: .
    ports:
      - "8282:8282"
    environment:
      - NODE_ENV=production
      - WEBSOCKET_PORT=8282
    volumes:
      - ./uploads:/app/uploads
      - ./data:/app/data
    
  express-server:
    build: .
    command: npm run server
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - PORT=3000
    
  # A2A 에이전트들
  host-agent:
    build: .
    command: npm run host:start
    ports:
      - "10000:10000"
      
  chat-agent:
    build: .
    command: npm run chatagent:start
    ports:
      - "10001:10001"
```

### 전통적인 PM2 배포
```bash
# 프로덕션 빌드
npm run build
npm run electron:build

# PM2로 모든 서비스 시작
npm run agent:start

# 서비스 상태 확인
pm2 status
pm2 logs

# 서비스 중지
npm run agent:stop
```

---

## 📚 API 참고자료

### WebSocket API (클라이언트용)
```javascript
// 연결
ws://host:8282

// 메시지 형식
{
  "type": "chat",
  "payload": {
    "message": "Hello AI",
    "sessionId": "unique-session-id"
  }
}

// 응답 형식
{
  "type": "response",
  "data": {
    "content": "AI response",
    "artifacts": [...],
    "sessionId": "unique-session-id"
  }
}
```

### HTTP API (내부 통신용)
```javascript
POST /a2a/task          # 새 작업 생성
GET /a2a/task/:id       # 작업 상태 조회
DELETE /a2a/task/:id    # 작업 취소

POST /api/upload        # 파일 업로드
GET /api/download/:id   # 아티팩트 다운로드
```

---

## 🛠️ 개발

### 새 에이전트 추가하기

1. **에이전트 디렉토리 생성**: `server/a2a/agents/your-agent/`
2. **A2A 프로토콜 준수 구현**
3. **에이전트 레지스트리에 추가**: `server/a2a/host/agentRegistry.js`
4. **설정 업데이트**: `server/a2a/config/agent.json`
5. **Docker 서비스 추가**: `docker-compose.yml`
6. **npm 스크립트 추가**: `"youragent:start": "nodemon server/a2a/agents/your-agent/server.js"`

### 클라이언트 SDK 개발
Unity 클라이언트를 위한 SDK는 별도 리포지토리에서 관리되며, DLL 형태로 배포됩니다.

### 테스트 및 디버깅
```bash
# 린팅 실행
npm run lint

# 서비스별 로그 확인
docker-compose logs host-app
docker-compose logs express-server

# 개발 모드 실행
npm run dev
```

---

**Vue.js, Electron, Docker 그리고 최신 AI 기술로 ❤️를 담아 제작되었습니다**