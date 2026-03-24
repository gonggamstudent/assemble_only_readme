# UI Builder Pro

**Unity 스타일 비주얼 UI 에디터** - 코딩 없이 웹페이지를 만들고 HTML/CSS/React/Vue 코드로 변환하는 프로페셔널 툴

Unity 엔진처럼 직관적으로 UI를 디자인하고, 실제 동작하는 코드로 자동 변환합니다.

---

## 주요 기능

### 핵심 기능
- **드래그 앤 드롭 인터페이스**: 마우스로 요소를 배치하고 크기 조정
- **8방향 리사이즈 핸들**: 요소 선택 시 마우스로 직관적인 크기 조정
- **스냅/그리드 시스템**: 20px 단위 자동 정렬 + 요소끼리 자동 스냅
- **이미지 드래그 앤 드롭**: 컴퓨터에서 이미지 파일을 직접 드래그하여 추가
- **계층형 레이어 패널**: Unity Hierarchy처럼 부모-자식 구조 표시
- **다중 선택 및 그룹화**: Ctrl+클릭으로 다중 선택, 그룹으로 관리
- **Undo/Redo**: 최대 50단계 히스토리 (Ctrl+Z / Ctrl+Y)
- **복사/붙여넣기**: Ctrl+C / Ctrl+V 지원
- **프로젝트 저장/불러오기**: JSON 파일로 저장 및 불러오기 (그룹 정보 유지)
- **실시간 미리보기**: 새 창에서 실제 페이지 미리보기
- **반응형 모드**: 데스크톱(1200px), 태블릿(768px), 모바일(375px)
- **다크모드**: 라이트/다크 테마 전환

### Unity 스타일 기능
- **부모-자식 계층 구조**: 요소를 다른 요소의 자식으로 설정, 부모 이동 시 자식도 함께 이동
- **Anchor/Pivot 시스템**: Unity Rect Transform과 동일한 앵커 프리셋 9개
- **Scene View 도구**: Rect Tool(Q), Move Tool(W), Scale Tool(E) 전환
- **Inspector 패널**: Unity Inspector처럼 카테고리별 섹션 (Transform, Rect Transform, Hierarchy, Content, Appearance)
- **컴포넌트 설정 다이얼로그**: 네비바/사이드바/푸터 삽입 시 상세 설정 가능

### 🎨 컴포넌트
- **기본**: 텍스트, 제목, 버튼, 이미지, 입력창, 박스
- **고급**: 카드, 네비게이션 바, 푸터, 사이드바

### 📤 Export 옵션
- **HTML 단일 파일**: 모든 코드가 포함된 하나의 HTML 파일
- **HTML + CSS 분리**: HTML과 CSS를 별도 파일로 다운로드
- **React 컴포넌트**: JSX 코드로 변환
- **Vue 컴포넌트**: Vue SFC 코드로 변환
- **ZIP 프로젝트**: 전체 프로젝트를 ZIP으로 압축

---

## 📁 파일 구조

```
todeogi/
├── visual-editor-pro.html    # 메인 HTML 파일
├── visual-editor-pro.css     # 스타일시트 (라이트/다크 모드)
├── visual-editor-pro.js      # 전체 기능 구현 JavaScript
├── README.md                 # 이 파일
│
├── visual-editor.html        # 구버전 (베이직)
├── visual-editor.js          # 구버전 JavaScript
│
├── index.html                # 토더기 챗봇 (별도 프로젝트)
├── app.js                    # 토더기 챗봇 로직
│
└── 대화내역_공공기관_챗봇_구현.md  # 프로젝트 문서
```

### 주요 파일 설명

#### `visual-editor-pro.html`
- 메인 UI 구조
- 상단 메뉴바, 왼쪽 팔레트, 중앙 캔버스, 오른쪽 속성 패널
- Export 모달, 코드 미리보기 모달

#### `visual-editor-pro.css`
- CSS 변수 기반 테마 시스템 (`:root`, `[data-theme="dark"]`)
- 반응형 레이아웃
- 애니메이션 및 트랜지션
- 커스텀 스크롤바

#### `visual-editor-pro.js`
- 전역 변수 관리 (`elements`, `selectedElement`, `history` 등)
- 드래그 앤 드롭 시스템
- 리사이즈 핸들 구현
- 요소 생성 및 관리
- 속성 편집 시스템
- Undo/Redo 히스토리
- Export 기능 (HTML, CSS, React, Vue, ZIP)
- 프로젝트 저장/불러오기

---

## 🚀 사용 방법

### 1. 실행

```bash
# 브라우저에서 파일 열기
visual-editor-pro.html
```

또는 파일을 더블클릭하여 기본 브라우저로 실행

### 2. 기본 워크플로우

```
1. 왼쪽 팔레트에서 컴포넌트 선택
   ↓
2. 중앙 캔버스로 드래그 앤 드롭
   ↓
3. 요소 선택 → 리사이즈 핸들로 크기 조정
   ↓
4. 오른쪽 패널에서 속성 편집 (색상, 텍스트 등)
   ↓
5. 완성 후 Export 버튼 클릭
   ↓
6. 원하는 형식으로 코드 다운로드
```

### 3. 이미지 추가

**방법 1**: 이미지 컴포넌트 드래그 후 속성에서 URL 입력
**방법 2**: 컴퓨터에서 이미지 파일을 직접 캔버스로 드래그 앤 드롭

### 4. 프로젝트 저장

```
상단 메뉴 → 💾 저장
→ JSON 파일 다운로드 (ui-builder-project.json)
```

### 5. 프로젝트 불러오기

```
상단 메뉴 → 불러오기
→ JSON 파일 선택
```

### 6. Unity 스타일 기능 사용

#### 부모-자식 계층 구조
```
방법 1 (Inspector):
1. 자식으로 만들 요소 선택
2. 오른쪽 Inspector → Hierarchy 섹션
3. 부모 드롭다운에서 부모 요소 선택

부모 이동 시 자식도 함께 이동됩니다.
```

#### 그룹 만들기
```
1. Ctrl+클릭으로 여러 요소 선택
2. 레이어 패널 상단의 "그룹 만들기" 버튼 클릭
   또는 Inspector 패널의 "그룹 만들기" 버튼 클릭
3. 그룹 이름 편집 가능
```

#### Anchor/Pivot 설정
```
1. 요소 선택
2. Inspector → Rect Transform 섹션
3. Anchor Preset 버튼 클릭 (9가지 프리셋)
   - Top Left, Top Center, Top Right
   - Middle Left, Center, Middle Right
   - Bottom Left, Bottom Center, Bottom Right
4. Pivot X, Y 값 조정 (0~1)
```

#### Scene View 도구 전환
```
Q: Rect Tool - 이동 + 크기 조절 (기본)
W: Move Tool - 이동만 (리사이즈 핸들 숨김)
E: Scale Tool - 크기 조절 전용

툴바에서 버튼 클릭으로도 전환 가능
```

#### 컴포넌트 설정 다이얼로그
```
네비바, 사이드바, 푸터를 드래그 앤 드롭하면
자동으로 설정 다이얼로그가 표시됩니다:

- 메뉴 항목/섹션 개수
- 스타일 (다크, 라이트 등)
- 크기 (너비, 높이)
```

---

## 키보드 단축키

### Scene View 도구
| 단축키 | 기능 |
|--------|------|
| `Q` | Rect Tool (이동 + 크기 조절) |
| `W` | Move Tool (이동만) |
| `E` | Scale Tool (크기 조절만) |

### 편집
| 단축키 | 기능 |
|--------|------|
| `Ctrl + Z` | 실행 취소 (Undo) |
| `Ctrl + Y` | 다시 실행 (Redo) |
| `Ctrl + C` | 요소 복사 |
| `Ctrl + V` | 요소 붙여넣기 |
| `Delete` | 선택한 요소 삭제 |
| `Ctrl + Click` | 레이어/캔버스에서 다중 선택 |

---

## 🎯 Export 가이드

### 1. HTML 단일 파일
```
Export → 📄 HTML 단일 파일
→ page.html 다운로드
→ 브라우저로 바로 실행 가능
```

### 2. HTML + CSS 분리
```
Export → 📁 HTML + CSS + JS 분리
→ index.html, styles.css 다운로드
→ 같은 폴더에 두고 실행
```

### 3. React 컴포넌트
```
Export → ⚛️ React 컴포넌트
→ JSX 코드 복사
→ React 프로젝트에 붙여넣기
```

예시:
```jsx
import React from "react";

const Page = () => {
  return (
    <div className="container">
      <div id="element-1" style={{ ... }}>
        <p>Hello World</p>
      </div>
    </div>
  );
};

export default Page;
```

### 4. Vue 컴포넌트
```
Export → 🟢 Vue 컴포넌트
→ Vue SFC 코드 복사
→ Vue 프로젝트에 붙여넣기
```

### 5. ZIP 프로젝트
```
Export → 🗜️ ZIP 프로젝트
→ ui-builder-project.zip 다운로드
→ index.html, styles.css, README.md 포함
```

---

## 🔧 기술 스택

- **HTML5**: 시맨틱 마크업
- **CSS3**: CSS 변수, Flexbox, Grid
- **Vanilla JavaScript**: ES6+
- **외부 라이브러리**:
  - [JSZip](https://stuk.github.io/jszip/) (3.10.1) - ZIP 파일 생성
  - [FileSaver.js](https://github.com/eligrey/FileSaver.js/) (2.0.5) - 파일 다운로드

---

## 🏗️ 아키텍처

### 데이터 구조

```javascript
// 요소 데이터 구조
{
  id: "element-1",           // 고유 ID
  type: "button",            // 컴포넌트 타입
  name: "버튼",              // 레이어 패널에 표시되는 이름
  x: 100,                    // X 좌표
  y: 200,                    // Y 좌표
  width: 120,                // 너비
  height: 40,                // 높이
  text: "버튼",              // 텍스트 내용
  backgroundColor: "#0d6efd", // 배경색
  color: "#ffffff",          // 글자색
  fontSize: 16,              // 글자 크기
  borderRadius: 6,           // 테두리 둥글기
  border: "none",            // 테두리
  zIndex: 1,                 // Z-인덱스

  // 계층 구조
  parentId: null,            // 부모 요소 ID
  children: [],              // 자식 요소 ID 배열

  // Unity Rect Transform
  anchor: {                  // 앵커 (0~1)
    min: { x: 0.5, y: 0.5 },
    max: { x: 0.5, y: 0.5 }
  },
  pivot: { x: 0.5, y: 0.5 }, // 피벗 (0~1)

  // 그룹
  groupId: "group-1"         // 그룹 ID (옵션)
}

// 그룹 데이터 구조
{
  id: "group-1",
  name: "Group 1",
  elementIds: ["element-1", "element-2"]
}
```

### 상태 관리

- `elements[]`: 모든 캔버스 요소 배열
- `selectedElement`: 현재 선택된 요소
- `selectedElements[]`: 다중 선택된 요소 배열
- `groups[]`: 그룹 배열
- `history[]`: Undo/Redo 히스토리 (최대 50개)
- `historyIndex`: 현재 히스토리 위치
- `copiedElement`: 복사된 요소
- `currentTool`: 현재 Scene View 도구 ('rect', 'move', 'scale')

### 주요 함수

| 함수명 | 설명 |
|--------|------|
| `createElement(type, x, y, options)` | 새 요소 생성 |
| `selectElement(element, data, addToSelection)` | 요소 선택 (다중 선택 지원) |
| `updateProperty(property, value)` | 속성 업데이트 |
| `setParent(childId, parentId)` | 부모-자식 관계 설정 |
| `unparent(childId)` | 부모 관계 해제 |
| `createGroup()` | 선택된 요소들로 그룹 생성 |
| `ungroupElements(groupId)` | 그룹 해제 |
| `setAnchorPreset(elementId, preset)` | 앵커 프리셋 설정 |
| `setTool(tool)` | Scene View 도구 전환 |
| `saveState()` | 현재 상태를 히스토리에 저장 |
| `undo()` / `redo()` | 실행 취소/다시 실행 |
| `generateHTMLCode()` | HTML 코드 생성 |
| `exportHTML()` | HTML 파일 다운로드 |

---

## 🛠️ 배포 옵션

### 옵션 1: HTML 파일 그대로 (가장 간단)

```bash
# 3개 파일을 압축
visual-editor-pro.html
visual-editor-pro.css
visual-editor-pro.js

# 압축 파일 공유
# 받는 사람: 압축 풀고 HTML 파일 더블클릭
```

**장점**: 빌드 불필요, 즉시 사용 가능

---

### 옵션 2: Electron 데스크톱 앱

#### 설치
```bash
npm init -y
npm install electron electron-builder
```

#### package.json 생성
```json
{
  "name": "ui-builder-pro",
  "version": "1.0.0",
  "main": "main.js",
  "scripts": {
    "start": "electron .",
    "build:win": "electron-builder --win",
    "build:mac": "electron-builder --mac"
  },
  "devDependencies": {
    "electron": "^28.0.0",
    "electron-builder": "^24.0.0"
  },
  "build": {
    "appId": "com.uibuilder.pro",
    "productName": "UI Builder Pro",
    "directories": {
      "output": "dist"
    },
    "win": {
      "target": "nsis",
      "icon": "icon.ico"
    },
    "mac": {
      "target": "dmg",
      "icon": "icon.icns"
    }
  }
}
```

#### main.js 생성
```javascript
const { app, BrowserWindow } = require('electron');
const path = require('path');

function createWindow() {
  const win = new BrowserWindow({
    width: 1400,
    height: 900,
    webPreferences: {
      nodeIntegration: true
    }
  });

  win.loadFile('visual-editor-pro.html');
}

app.whenReady().then(createWindow);

app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') {
    app.quit();
  }
});
```

#### 빌드
```bash
# Windows용 .exe 생성
npm run build:win

# Mac용 .dmg 생성
npm run build:mac

# dist/ 폴더에 실행 파일 생성됨
```

---

### 옵션 3: 웹 배포 (Netlify/Vercel)

#### Netlify (가장 쉬움)
```bash
1. https://netlify.com 접속
2. "Add new site" → "Deploy manually"
3. 파일 3개를 드래그 앤 드롭
4. 자동으로 URL 생성 (예: https://your-site.netlify.app)
```

#### Vercel
```bash
1. https://vercel.com 접속
2. "New Project" → "Import"
3. 파일 업로드
4. 자동 배포
```

#### GitHub Pages
```bash
1. GitHub 저장소 생성
2. 파일 3개 업로드
3. Settings → Pages → Enable
4. https://username.github.io/project 접근
```

---

### 옵션 4: PWA (앱처럼 설치 가능)

#### manifest.json 생성
```json
{
  "name": "UI Builder Pro",
  "short_name": "UI Builder",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#0d6efd",
  "icons": [
    {
      "src": "icon-192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "icon-512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
```

#### service-worker.js 생성
```javascript
self.addEventListener('install', (e) => {
  e.waitUntil(
    caches.open('ui-builder-v1').then((cache) => {
      return cache.addAll([
        '/',
        '/visual-editor-pro.html',
        '/visual-editor-pro.css',
        '/visual-editor-pro.js'
      ]);
    })
  );
});

self.addEventListener('fetch', (e) => {
  e.respondWith(
    caches.match(e.request).then((response) => {
      return response || fetch(e.request);
    })
  );
});
```

#### HTML에 추가
```html
<link rel="manifest" href="manifest.json">
<script>
  if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('/service-worker.js');
  }
</script>
```

---

## 🐛 알려진 이슈 및 제한사항

1. **이미지 저장**: Base64로 인코딩되어 파일 크기가 커질 수 있음
2. **브라우저 호환성**: 최신 Chrome, Firefox, Edge, Safari 권장
3. **모바일 지원**: 터치 이벤트 미지원 (데스크톱 전용)

---

## 향후 개선 사항 (추가 개발 아이디어)

### 우선순위 높음
- [ ] **정렬 도구**: 요소를 자동으로 정렬 (왼쪽, 중앙, 오른쪽, 위, 아래, 균등 분산)
- [ ] **Ctrl+D 빠른 복제**: Unity처럼 선택한 요소 즉시 복제
- [ ] **레이어 드래그로 부모 설정**: 레이어 패널에서 드래그 앤 드롭으로 부모-자식 관계 설정
- [ ] **프리팹/템플릿 시스템**: 자주 사용하는 UI 패턴을 저장하고 재사용
- [ ] **캔버스 줌 인/아웃**: 전체 레이아웃을 한눈에 보기 위한 줌 기능

### 우선순위 중간
- [ ] **Horizontal/Vertical Layout**: Unity처럼 자식 요소를 자동으로 가로/세로 배치
- [ ] **Grid Layout**: 자식 요소를 격자 형태로 자동 배치
- [ ] **텍스트 에디터**: 리치 텍스트 편집 (볼드, 이탤릭, 폰트 패밀리 등)
- [ ] **애니메이션 추가**: 요소에 CSS 애니메이션 효과 적용
- [ ] **Flexbox/Grid 레이아웃**: CSS Flexbox/Grid 기반 레이아웃 시스템
- [ ] **컴포넌트 마켓플레이스**: 커뮤니티 공유 컴포넌트

### 우선순위 낮음
- [ ] **협업 기능**: 여러 사람이 동시에 편집 (WebSocket 기반)
- [ ] **버전 관리**: Git처럼 프로젝트 히스토리 저장 및 브랜치
- [ ] **Figma 파일 임포트**: Figma API 연동
- [ ] **AI 디자인 제안**: AI가 디자인 개선사항 제안
- [ ] **반응형 레이아웃 자동 생성**: 다양한 화면 크기에 맞는 레이아웃 자동 생성

---

## 📝 추가 개발 시 주의사항

### 새 컴포넌트 추가 방법

1. **HTML에 팔레트 아이템 추가**:
```html
<div class="component-item" draggable="true" data-type="newtype">
    <div class="icon">🎯</div>
    <div class="name">새 컴포넌트</div>
</div>
```

2. **JS의 `createElementData()` 함수에 설정 추가**:
```javascript
const configs = {
    // ... 기존 코드
    newtype: {
        width: 200,
        height: 100,
        text: '새 컴포넌트',
        backgroundColor: '#ffffff'
    }
};
```

3. **`createElementContent()` 함수에 렌더링 로직 추가**:
```javascript
case 'newtype':
    content.innerHTML = '<div>새 컴포넌트 내용</div>';
    break;
```

### 스타일 수정 시
- CSS 변수(`--bg-primary` 등)를 활용하면 테마 일관성 유지
- 다크모드 지원을 위해 `[data-theme="dark"]`에도 스타일 추가

### 성능 최적화
- `elements` 배열이 커지면 성능 저하 가능 → Virtual DOM 고려
- 리사이즈/드래그 중에는 `requestAnimationFrame` 사용 고려

---

## 📄 라이선스

이 프로젝트는 개인 및 상업적 사용이 가능합니다.
단, 재배포 시 출처를 명시해주세요.

---

## FAQ

### Q: 생성된 코드를 실제 웹사이트에 사용할 수 있나요?
**A**: 네! Export된 HTML/CSS는 즉시 사용 가능합니다. 필요에 따라 JavaScript 기능을 추가하세요.

### Q: Unity와 완전히 똑같이 작동하나요?
**A**: Unity UI 시스템의 핵심 기능들(Hierarchy, Inspector, Rect Transform, Anchor/Pivot)을 구현했습니다. Layout 컴포넌트 등 일부 기능은 향후 추가 예정입니다.

### Q: 부모-자식 관계가 Export된 코드에도 반영되나요?
**A**: 현재는 절대 위치로 Export됩니다. 향후 실제 HTML 부모-자식 구조로 Export하는 옵션을 추가할 예정입니다.

### Q: React/Vue 코드가 제대로 작동하나요?
**A**: 기본 구조는 작동하지만, 이벤트 핸들러나 상태 관리는 수동으로 추가해야 합니다.

### Q: 모바일에서도 사용할 수 있나요?
**A**: 현재는 데스크톱 전용입니다. 터치 이벤트 지원은 향후 추가 예정입니다.

### Q: 그룹과 부모-자식의 차이는 무엇인가요?
**A**:
- **그룹**: 여러 요소를 논리적으로 묶어서 관리 (함께 이동)
- **부모-자식**: 실제 계층 구조를 형성하며, 부모 이동 시 자식도 함께 이동

### Q: Anchor 시스템이 실제로 작동하나요?
**A**: 현재는 Anchor 값이 데이터로만 저장됩니다. 실제 반응형 레이아웃에 적용하는 기능은 향후 추가 예정입니다.

---

## 🤝 기여

버그 리포트, 기능 제안, 개선 사항은 언제든 환영합니다!

---

**만든이**: todeogi 프로젝트
**버전**: 2.0.0 (Unity Edition)
**최종 업데이트**: 2025년 1월 6일

### 변경 이력

- 부모-자식 계층 구조 시스템
- Anchor/Pivot 시스템 (Rect Transform)
- Scene View 도구 분리 (Q/W/E)
- Inspector 패널 카테고리별 섹션
- 다중 선택 및 그룹화 (Ctrl+클릭)
- 컴포넌트 설정 다이얼로그
- 그룹 정보 저장/로드 유지

#### v1.0.0 (2025-11-05)
- 초기 릴리스
- 기본 드래그 앤 드롭 UI
- Export 기능

---

즐거운 디자인 되세요!
