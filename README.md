# 🏠 Sweet Home

> **"새로 산 노트북처럼, 언제나."**
> macOS를 위한 선언형 시스템 환경 격리 프레임워크

---

## 프로젝트 배경

새 맥북을 켜는 순간의 그 무결한 상태. 아무것도 깔리지 않았고, 아무것도 뿌려지지 않은 완전한 베이스.

그 상태를 영원히 유지하고 싶었어요.

앱을 설치하고, 쓰고, 지워도 — 지운 뒤에 진짜로 아무것도 남지 않는 환경. 시스템 데이터가 100GB를 넘어가고, 같은 앱이 세 개씩 깔리고, 뭘 지워야 할지 모르는 찌꺼기가 쌓이는 상황 없이. 맥이 항상 새것처럼 동작하는 구조가 목표예요.

그래서 **Sweet Home**을 만들었어요.

---

## 핵심 개념 — 비닐막 모델

Sweet Home의 설계 철학은 하나의 비유에서 출발해요.

```
새 집(맥북)을 받았어.
집 전체에 비닐막을 씌워.
막 살아. 더럽게 써. 뭔가 설치하고, 로그인하고, 파일도 쌓아.
비닐막을 뜯어.
더럽혀진 건 비닐막에 흡착되어 함께 사라져.
집은 처음 그대로야.
```

이 개념을 macOS 위에서 최대한 구현한 것이 Sweet Home이에요.

| 비유 | 기술 |
|------|------|
| 집 (베이스) | macOS + 무결한 시스템 상태 |
| 비닐막 (레이어) | Nix store + nix-darwin 선언형 환경 |
| 가구 (데이터) | 사용자 파일, 작업물 — 레이어와 독립적으로 유지 |
| 비닐막 뜯기 | `darwin-rebuild switch` + `onActivation.cleanup = "zap"` |

---

## 기술 스택

| 역할 | 기술 |
|------|------|
| 레이어 핵심 엔진 | **Nix (Determinate 3.17)** |
| macOS 시스템 관리 | **nix-darwin** |
| 사용자 환경 관리 | **Home Manager** |
| GUI 앱 관리 | **Homebrew (nix-darwin 모듈)** |
| ~/Library 찌꺼기 처리 | **AppCleaner** |
| 설정 버전 관리 | **Git + GitHub (Private)** |

**환경**
- 기기: MacBook Pro M5 (2026)
- OS: macOS Tahoe 26
- 아키텍처: aarch64-darwin

---

## 동작 방식

### 앱을 설치할 때

```nix
# flake.nix에 한 줄 추가
homebrew.casks = [
  "firefox"
  "visual-studio-code"
  "blender"
];
```

```bash
sudo darwin-rebuild switch --flake /etc/nix-darwin
```

Homebrew가 선언된 앱만 설치해요. 선언에 없는 앱은 존재하지 않아요.

### 앱을 제거할 때

```nix
# flake.nix에서 해당 줄 삭제
homebrew.casks = [
  "firefox"
  # "visual-studio-code"  ← 이 줄 지우면
];
```

```bash
sudo darwin-rebuild switch --flake /etc/nix-darwin
```

`onActivation.cleanup = "zap"` 옵션으로 앱 본체 + `~/Library` 찌꺼기까지 함께 제거돼요.

### 새 맥북으로 이전할 때

```bash
# 새 맥북에서 이것만 하면 끝
curl -fsSL https://install.determinate.systems/nix | sh -s -- install
git clone git@github.com:(계정)/sweet-home.git /etc/nix-darwin
sudo darwin-rebuild switch --flake /etc/nix-darwin
```

모든 앱, 설정, 환경이 그대로 복원돼요.

---

## 설치 방법

### 처음 세팅할 때 (순서대로)

**1. 초기 세팅 완료 후 스냅샷 찍기**
```bash
tmutil localsnapshot
```

**2. 컴퓨터 이름 설정**
```bash
sudo scutil --set ComputerName "MacBook Pro"
sudo scutil --set LocalHostName "MacBook-Pro"
```

**3. Determinate Nix 설치**
```bash
curl -fsSL https://install.determinate.systems/nix | sh -s -- install
```
새 터미널 열고 확인:
```bash
nix --version
```

**4. nix-darwin 설정 폴더 생성**
```bash
sudo mkdir -p /etc/nix-darwin && sudo chown $(id -nu):$(id -ng) /etc/nix-darwin
```

**5. 이 레포지토리 클론**
```bash
cd /etc/nix-darwin && git init
git remote add origin git@github.com:(깃헙계정)/sweet-home.git
git pull origin main
```

**6. nix-darwin 초기 설치**
```bash
sudo nix run nix-darwin/master#darwin-rebuild -- switch --flake /etc/nix-darwin
```

**7. Homebrew 설치**
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**8. 이후부터는 이 한 줄로 모든 설정 적용**
```bash
sudo darwin-rebuild switch --flake /etc/nix-darwin
```

---

## 설치된 환경

### CLI 도구 (Nix)

| 패키지 | 설명 |
|--------|------|
| `vim` | 텍스트 편집기 |
| `gh` | GitHub CLI |
| `ollama` | 로컬 LLM 실행 도구 |
| `jupyter` | Jupyter Notebook |

### GUI 앱 (Homebrew Cask)

| 앱 | 설명 |
|----|------|
| `firefox` | 기본 브라우저 |
| `visual-studio-code` | 코드 에디터 |
| `android-studio` | 안드로이드 개발 IDE |
| `docker-desktop` | 컨테이너 관리 |
| `unity-hub` | 유니티 허브 |
| `blender` | 3D 모델링/렌더링 |
| `steam` | 게임 플랫폼 |
| `google-chrome` | 크롬 브라우저 |
| `logi-options+` | 로지텍 마우스/키보드 설정 |
| `parsec` | 원격 데스크탑 |
| `claude` | Claude 데스크탑 앱 |
| `naver-whale` | 네이버 웨일 브라우저 |
| `whisky` | macOS용 Wine 래퍼 |
| `appcleaner` | 앱 완전 삭제 도구 |

### App Store 전용 (수동 설치 필요)

| 앱 | 설명 |
|----|------|
| Final Cut Pro | 영상 편집 |
| Logic Pro | 음악 제작 |
| GarageBand | 음악 제작 (무료) |
| Xcode | Apple 개발 도구 |
| 머신프로파일 | 시스템 정보 |

---

## 자주 쓰는 커맨드

### 시스템 관리
```bash
# 설정 변경 후 적용
sudo darwin-rebuild switch --flake /etc/nix-darwin

# flake.nix 편집
vim /etc/nix-darwin/flake.nix

# 정크 정리
nix-collect-garbage -d
```

### 깃헙 백업
```bash
cd /etc/nix-darwin && git add . && git commit -m "(커밋메시지)" && git push
```

### 앱 확인
```bash
# 설치된 앱 목록
ls /Applications/

# 특정 앱 검색
ls /Applications/ | grep -i (앱이름)
```

### 스냅샷
```bash
# 스냅샷 찍기
tmutil localsnapshot

# 스냅샷 목록 확인
tmutil listlocalsnapshots /
```

### 시스템 정보
```bash
scutil --get ComputerName
scutil --get LocalHostName
id -un
nix --version
```

### 깃헙 CLI
```bash
gh auth login
gh repo create (레포이름) --private --source=. --push
```

### 네트워크 확인
```bash
ping -c 3 google.com
nslookup (도메인)
```

---

## 한계와 현실

macOS 구조상 완벽한 레이어 격리는 불가능해요. 알려진 한계:

- **`~/Library` 직접 쓰는 앱** (Logitech, Microsoft 등) → AppCleaner로 보완
- **App Store 전용 앱** → 수동 설치 필요
- **Homebrew cask 없는 앱** (카카오톡 등) → 수동 설치 필요
- **네트워크 레이어 격리** → macOS 커널 구조상 불가

이 한계들을 인지한 채로, 현재 macOS에서 구현 가능한 최선에 가까운 구조를 목표로 해요.

---

## 파일 구조

```
/etc/nix-darwin/
├── flake.nix      # 메인 선언 파일 — 모든 앱과 설정이 여기에
└── flake.lock     # 의존성 버전 고정
```

---

## 주의사항

- `darwin-rebuild switch` 실행 시 `sudo` 필요
- 터미널 전체 디스크 접근 권한 활성화 필요
  - 시스템 설정 → 개인정보 보호 및 보안 → 전체 디스크 접근 권한 → Terminal.app 토글 ON
- `flake.nix` 수정 후 반드시 `darwin-rebuild switch` 실행해야 적용됨
- 변경사항은 커밋 후 push하여 백업 권장

---

<div align="center">

**Sweet Home** — 항상 새것처럼.

*Nix · nix-darwin · Home Manager · Homebrew*

</div>
