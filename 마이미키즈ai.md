<div align="center">

# 🧸 MYME Kids

### AI 유아 학습 & 창작 동반자 플랫폼

**3~7세 유아를 위한 안전한 AI 대화·동화 생성·학습 퀴즈 통합 서비스**

[![Node.js](https://img.shields.io/badge/Node.js-18+-339933?style=flat-square&logo=node.js&logoColor=white)](https://nodejs.org/)
[![React](https://img.shields.io/badge/React-19.2-61DAFB?style=flat-square&logo=react&logoColor=black)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4o_·_DALL--E_3-412991?style=flat-square&logo=openai&logoColor=white)](https://openai.com/)
[![ElevenLabs](https://img.shields.io/badge/ElevenLabs-TTS_·_Voice_Clone-FF6B35?style=flat-square)](https://elevenlabs.io/)
[![MongoDB](https://img.shields.io/badge/MongoDB-9.x-47A248?style=flat-square&logo=mongodb&logoColor=white)](https://mongodb.com/)

</div>

---

## 개요

MYME Kids는 **마이미(Mymi)**라는 AI 친구와 함께 유아가 대화·동화·퀴즈를 즐길 수 있는 교육·엔터테인먼트 플랫폼입니다. 3~7세 눈높이에 맞는 어휘와 말투로 설계된 AI 에이전트, 이중 콘텐츠 안전 필터, 부모 목소리 복제(Voice Cloning) 기반의 맞춤형 TTS가 핵심입니다.

---

## 주요 기능

### 🗣️ AI 대화 (마이미 챗)
- GPT-4o-mini 기반 유아 친화적 대화 에이전트
- 직전 6개 메시지 컨텍스트 유지로 자연스러운 연속 대화
- 음성 입력(Web Speech API) + 자동 전송(1.5초 묵음 감지)로 핸즈프리 모드 지원

### 📖 AI 동화 생성
- 주제 입력 → GPT가 5~7페이지 동화 JSON 자동 생성
- 각 페이지마다 DALL-E 3 삽화 개별 생성 (파스텔·아동 그림책 스타일)
- TTS로 전체 동화 낭독 (부모 목소리 클론 우선 적용)

### 🧩 학습 퀴즈
- 주제 기반 3지선다 퀴즈 자동 생성
- 정답 해설 포함 (유아 눈높이 설명)

### 🎙️ 부모 목소리 복제
- 부모가 짧은 오디오 파일을 업로드하면 ElevenLabs Voice Cloning API로 고유 보이스 등록
- 이후 모든 TTS(동화 낭독, 마이미 답변)에 부모 목소리 자동 적용
- 보이스 교체·삭제 지원

### 🛡️ 이중 콘텐츠 안전 필터
- **입력 검증**: 유해 키워드·주제 감지 시 친절한 거절 메시지 반환
- **출력 검증**: AI 응답 생성 후 안전성 재확인 → 부적절하면 재생성
- 무서운 내용, 폭력, 성인 주제를 두 단계로 차단

---

## 기술 스택

### Frontend
```
React 19.2 + TypeScript  │  Vite 8.0  │  Tailwind CSS 4.2
Zustand 5.0 (상태 관리)   │  React Router DOM 7.x  │  Axios 1.x
Web Speech API (음성 입력, 브라우저 네이티브)
```

### Backend
```
Node.js 18+  │  Express.js 5.2  │  MongoDB 9.x + Mongoose
Multer 2.x (메모리 스토리지, 음성 파일 업로드)
Form-data (ElevenLabs Multipart 요청)
```

### AI / External APIs
```
OpenAI GPT-4o-mini (대화·동화·퀴즈 생성)
OpenAI DALL-E 3 (동화 삽화)
OpenAI Moderation API (콘텐츠 안전 필터)
ElevenLabs TTS API (음성 합성)
ElevenLabs Voice Cloning API (부모 목소리 복제)
```

---

## 아키텍처

```
┌────────────────────────────────────────────────────────┐
│                   Client (React + TS)                  │
│  ChatPage  │  StoryPage  │  QuizPage  │  VoiceSetupPage│
│  Web Speech API (음성 입력 + 묵음 감지)                  │
└───────────────────────┬────────────────────────────────┘
                        │ REST API
┌───────────────────────▼────────────────────────────────┐
│                 Express.js Server (:10020)              │
│                                                        │
│  ┌─────────────────────────────────────────────────┐   │
│  │              KidsAgent (GPT-4o-mini)            │   │
│  │  • 유아 전용 시스템 프롬프트 (짧은 문장, 쉬운 어휘)  │   │
│  │  • 사투리 표준어 매핑 (어무이→엄마 등)             │   │
│  │  • 대화 히스토리 6개 슬라이딩 윈도우              │   │
│  └─────────────────────────────────────────────────┘   │
│                                                        │
│  ┌─────────────────────────────────────────────────┐   │
│  │          ModerationAgent (이중 안전 필터)         │   │
│  │  입력 → [OpenAI Moderation] → 생성 → [재검증]    │   │
│  └─────────────────────────────────────────────────┘   │
│                                                        │
│  ┌───────────┐  ┌──────────────┐  ┌───────────────┐   │
│  │  DALL-E3  │  │ ElevenLabs   │  │ Voice Cloning │   │
│  │  동화 삽화 │  │ TTS / MP3    │  │ 부모 보이스    │   │
│  └───────────┘  └──────────────┘  └───────────────┘   │
└────────────────────────────────────────────────────────┘
```

---

## API 엔드포인트

| 경로 | 메서드 | 설명 |
|------|--------|------|
| `/api/kids/chat` | POST | 마이미 대화 (히스토리 포함) |
| `/api/kids/story/generate` | POST | 동화 텍스트 + 삽화 프롬프트 생성 |
| `/api/kids/story/image` | POST | 동화 페이지 삽화 생성 (DALL-E 3) |
| `/api/kids/quiz` | POST | 주제별 3지선다 퀴즈 생성 |
| `/api/kids/tts` | POST | ElevenLabs TTS (MP3 스트림) |
| `/api/kids/voice/register` | POST | 부모 목소리 클론 등록 |
| `/api/kids/voice/status` | GET | 등록된 보이스 상태 확인 |
| `/api/kids/voice` | DELETE | 등록된 보이스 삭제 |

---

## AI 에이전트 설계

### KidsAgent — 유아 전용 페르소나

```
[시스템 프롬프트 핵심 규칙]
- 역할: "마이미" — 3~7세 친구 같은 AI 동반자
- 어휘: 유치원생이 이해할 수 있는 쉬운 단어만 사용
- 문장: 최대 3~4문장, 짧고 명확하게
- 어조: 긍정적, 따뜻함, 격려
- 금지: 무섭거나 슬픈 내용, 복잡한 개념
- 이모지: 적절히 사용하여 친근감 표현
- 사투리 정규화: 어무이→엄마, 아부지→아빠 등 자동 변환
```

### ModerationAgent — 이중 안전 계층

```
사용자 입력
    │
    ▼
[1차: OpenAI Moderation API]
    │ 위험 → "다른 걸 물어봐요 😊" 반환
    │ 안전 ↓
[GPT-4o-mini 응답 생성]
    │
    ▼
[2차: 출력 안전성 재검증]
    │ 부적절 → 중립 응답으로 대체
    │ 안전 ↓
최종 응답 전달
```

---

## 동화 생성 워크플로우

```
1. 주제 입력 (예: "아기 여우가 사냥을 배우는 이야기")
        │
        ▼
2. [입력 안전 검증]
        │
        ▼
3. GPT → 5~7페이지 구조화 JSON 생성
   {
     "title": "...",
     "pages": [
       { "text": "2~3문장 서술", "imagePrompt": "DALL-E 영어 프롬프트" },
       ...
     ]
   }
        │
        ▼
4. [출력 안전 검증]
        │
        ▼
5. 사용자에게 텍스트 즉시 반환 (삽화는 클릭 시 개별 생성)
        │
        ▼
6. 각 페이지 → DALL-E 3 삽화 생성
   ("cute children's book style, pastel colors, safe for kids")
```

---

## 목소리 클론 플로우

```
부모가 오디오 파일 업로드 (MP3/WAV, 최대 20MB)
        │
        ▼
기존 클론 보이스 삭제 (중복 방지)
        │
        ▼
ElevenLabs Voice Cloning API 요청
        │
        ▼
voice_id 수령 → 메모리에 등록
        │
        ▼
이후 TTS 요청 시 기본 보이스 대신 부모 voice_id 사용
```

---

## 프로젝트 구조

```
myme-kids/
├── client/                      # React + TypeScript SPA
│   └── src/
│       ├── pages/
│       │   ├── ChatPage.tsx     # 마이미 대화 화면
│       │   ├── StoryPage.tsx    # 동화 생성·열람
│       │   ├── QuizPage.tsx     # 학습 퀴즈
│       │   └── VoiceSetupPage.tsx  # 부모 목소리 등록
│       └── stores/              # Zustand 상태
└── server/                      # Express.js API
    └── src/
        ├── routes/kids.js       # 전체 API 라우팅
        └── agents/
            ├── kidsAgent.js     # 마이미 페르소나 + 대화
            └── moderationAgent.js  # 이중 안전 필터
```

---

## 실행 방법

```bash
cd myme-kids

# 의존성 설치
cd server && npm install
cd ../client && npm install

# 환경변수 설정
cp server/.env.example server/.env
# OPENAI_API_KEY, ELEVENLABS_API_KEY, MONGODB_URI 입력

# 개발 서버 실행
cd server && npm run dev     # :10020
cd client && npm run dev     # :5175
```

---

## 개발 하이라이트

- **이중 안전 필터 설계**: 단일 Moderation만으로는 GPT 출력의 안전성을 보장할 수 없어 입력·출력 양방향 검증 레이어를 구현. 유아 대상 서비스 특성을 고려한 방어적 설계
- **부모 목소리 우선 TTS**: voice_id를 메모리에 저장하고 TTS 요청 시 자동 선택하여 별도 설정 없이 개인화된 낭독 경험 제공
- **핸즈프리 음성 모드**: Web Speech API의 묵음 감지 타이머를 직접 구현, 아이가 버튼 없이 자연스럽게 대화할 수 있는 연속 대화 흐름 구현
- **TTS 파일 자동 정리**: 최근 10개만 유지하는 순환 삭제 전략으로 장기 운영 시 스토리지 증가 문제 예방
- **구조화 JSON 응답**: 동화와 퀴즈를 순수 텍스트 대신 JSON으로 생성하여 클라이언트에서 페이지별 렌더링·삽화 매핑·정답 판별 로직을 분리 구현
