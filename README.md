# Lizzie Design System

개인 브랜딩 디자인 시스템. 키워드: **정밀한 사람**. 무드: **현대적이고 깔끔한**.

## 파일 구조

| 파일 | 용도 |
|------|------|
| `design-system.md` | 원칙 전문 — AI에게 컨텍스트로 제공 |
| `tokens.css` | 원시값 + 역할 토큰 + Tailwind v4 `@theme` 매핑 — 프로젝트에 직접 import |
| `base.css` | reset과 전역 기본값 (폰트, 제목, 링크, focus) |
| `components.css` | 재사용 클래스 (card, btn, tag, input, callout, prose, timeline …) |
| `showcase/index.html` | 모든 토큰과 컴포넌트를 실제 CSS로 렌더링한 확인용 페이지 |
| `guides/slides.md` | 발표자료 전용 규칙 |
| `CHANGELOG.md` | 버전별 변경 요약 (Removed / Changed / Added / Fixed) |
| `MIGRATION.md` | 메이저 버전을 올릴 때 고칠 곳 찾는 명령어와 대응표 |
| `guides/project-claude-md.md` | 이 시스템을 쓰는 프로젝트의 `CLAUDE.md`에 붙여 넣는 표준 섹션 (AI 진입점) |
| `log/index.md` | 이 시스템을 적용한 프로젝트 목록 |

## 핵심 원칙 요약

- **색**: 웜 그레이 11단계에서 고른 역할 토큰. 포인트는 `--accent`(슬레이트블루) 하나, 테라코타는 `--warning`(주의)으로만
- **폰트**: Pretendard가 기본. Maru Buri는 장문 본문(`.prose`)에서만
- **모양**: 모서리 4px 통일, 테두리 1px, 그림자 없음
- **다크모드**: `light-dark()`로 자동 전환. OS 설정을 따르고 `.dark`/`.light`로 고정 가능
- **AI 냄새 기준**: "이 스타일에 '왜'라고 답할 수 있는가? 기본값을 이유 없이 그대로 쓴 게 아닌가?"

## 확인하기

`showcase/index.html`을 브라우저로 열면 토큰과 컴포넌트를 라이트/다크로 볼 수 있어요.
값을 바꿨다면 커밋 전에 여기서 먼저 확인하세요.

## 사용법

### 단순하게 쓰기 (clone + gitignore)

혼자 쓰는 프로젝트라면 이게 더 단순해요.

```bash
# 처음 세팅
git clone <이-레포-URL> design-system
echo "design-system/" >> .gitignore

# 업데이트할 때
git -C design-system pull
```

버전을 git이 추적하지 않는다는 차이만 있고, 솔로 프로젝트에선 문제없어요.

### Git Submodule로 다른 프로젝트에서 사용하기 (태그로 버전 고정)

**1. 처음 추가하고 원하는 버전에 고정**

```bash
# 프로젝트 루트에서
git submodule add <이-레포-URL> design-system
git -C design-system checkout 0.0.2
git add design-system
git commit -m "build(design-system): add design-system 0.0.2"
```

**2. 이 레포를 포함한 프로젝트를 클론할 때**

```bash
git clone --recurse-submodules <프로젝트-URL>

# 이미 클론한 경우
git submodule update --init
```

**3. 새 버전으로 올리기**

```bash
git -C design-system fetch --tags
git -C design-system checkout 0.0.3
git add design-system
git commit -m "build(design-system): upgrade design-system to 0.0.3"
```

올리기 전에 `CHANGELOG.md`를 확인하고, `MIGRATION.md`의 해당 구간 절차(검색 명령어 → 대응표)를 따르세요.

**4. CSS import**

```css
/* globals.css */
@import "./design-system/tokens.css";
@import "./design-system/base.css";
@import "./design-system/components.css";
```

Tailwind v4 프로젝트면 `tokens.css`의 `@theme inline` 덕분에 `bg-surface`, `text-ink`, `rounded-box`,
`font-serif` 같은 유틸리티를 바로 쓸 수 있어요.

**5. Claude Code가 읽게 하기**

[`guides/project-claude-md.md`](guides/project-claude-md.md)의 `BEGIN`~`END` 사이 내용을 프로젝트 루트 `CLAUDE.md`에 붙여 넣고,
고정 버전과 적용 방식(import/copy) 두 곳만 고치세요.
Claude Code가 매 세션 확실히 읽는 건 프로젝트 루트 `CLAUDE.md`뿐이라, 이 섹션이 없으면 디자인 시스템 규칙도 업그레이드 절차도 읽히지 않아요.

### 버전 규칙

- 태그는 `0.0.1`, `0.0.2`처럼 `v` 없이 쓴다
- 아직 다듬는 단계라 0.0.x로 조금씩 올린다. **어느 태그든 깨지는 변경이 들어갈 수 있다**
- 그래서 태그를 찍을 때마다 `CHANGELOG.md`에 Removed / Changed / Added / Fixed를 적고, 이름이 사라지는 변경이 있으면 `MIGRATION.md`에 해당 구간 섹션(검색 명령어 + 대응표)을 추가한다

### 프로젝트별 적용 가이드

프로젝트 레포에 `DESIGN_LOG.md`를 두어 미정의 컴포넌트 처리 기준, 실제 적용 내역을 기록한다 (이 레포는 범용 원칙만 관리).
