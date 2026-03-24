# 감정 쓰레기통 (Emotional Trash Can)

창의적인 심리상담 웹 애플리케이션입니다. 사용자가 감정을 종이에 적어서 쓰레기통에 버리는 듯한 경험을 통해 AI와 심리상담을 할 수 있습니다.

## 🎨 주요 기능

- **메인 페이지**: 깔끔한 하얀 배경에 버튼들로 구성된 심플한 인터페이스
- **감정 쓰레기통**: 화면 중앙의 상호작용 가능한 쓰레기통
- **A4 용지 채팅**: 화면 하단에서 나오는 종이 형태의 채팅 인터페이스
- **구겨지는 애니메이션**: 메시지 전송 시 종이가 구겨져서 쓰레기통에 들어가는 애니메이션
- **AI 심리상담**: ChatGPT를 활용한 따뜻하고 공감적인 심리상담 응답

## 🚀 실행 방법

### 1. 의존성 설치
```bash
npm install
```

### 2. 로컬 ChatGPT 서버 설정
이 프로젝트는 로컬에서 실행되는 ChatGPT API를 사용합니다.
- LM Studio나 다른 로컬 AI 서버를 `http://localhost:1234`에서 실행해주세요
- 또는 `src/services/chatAPI.js`에서 API URL을 원하는 서버로 변경하세요

### 3. 개발 서버 실행
```bash
npm run dev
```

### 4. 브라우저에서 확인
`http://localhost:5173`에서 애플리케이션을 확인할 수 있습니다.

## 🛠️ 기술 스택

- **React 18**: 사용자 인터페이스 구축
- **Vite**: 빠른 개발 환경 및 빌드 도구
- **React Router**: 페이지 라우팅
- **CSS3**: 애니메이션 및 스타일링
- **OpenAI Compatible API**: AI 심리상담 기능

## 📁 프로젝트 구조

```
src/
├── components/
│   ├── MainPage.jsx          # 메인 페이지
│   ├── EmotionalTrash.jsx    # 감정쓰레기통 메인 컴포넌트
│   ├── TrashCan.jsx          # 쓰레기통 UI
│   ├── ChatPaper.jsx         # A4 용지 채팅창
│   └── ResponseDisplay.jsx   # AI 응답 표시
├── services/
│   └── chatAPI.js            # ChatGPT API 통신
├── styles/                   # CSS 파일들
└── App.jsx                   # 메인 앱 컴포넌트
```

## 🎯 사용법

1. 메인 페이지에서 "감정 쓰레기통" 버튼 클릭
2. 화면 하단의 종이를 클릭하여 채팅창 열기
3. 마음속 이야기를 종이에 적기
4. 전송 버튼을 눌러 종이를 쓰레기통에 던지기
5. 잠시 후 AI로부터 따뜻한 응답 받기

## ⚙️ 설정 변경

### API 서버 변경
`src/services/chatAPI.js`에서 다음 부분을 수정하세요:
```javascript
const OPENAI_API_URL = 'http://localhost:1234/v1/chat/completions'
```

### 상담 프롬프트 변경
같은 파일에서 `SYSTEM_PROMPT` 변수를 원하는 상담 스타일로 수정할 수 있습니다.

## 🎨 커스터마이징

CSS 파일들을 수정하여 애니메이션, 색상, 레이아웃을 자유롭게 변경할 수 있습니다.

---

💡 **참고**: 이 프로젝트는 감정 표현과 심리적 위로를 위한 창의적인 인터페이스를 제공합니다. 실제 심리상담이 필요한 경우에는 전문가의 도움을 받으시기 바랍니다.
