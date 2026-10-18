# Lizzie Design System

> AI에게 디자인 작업을 요청할 때 컨텍스트로 제공하는 문서입니다.
> 실제 값은 `tokens.css`가 원본이고, 이 문서는 그 값을 **언제, 왜** 쓰는지를 설명합니다.

---

## 브랜드 철학

**키워드: 정밀한 사람**

- 화려하지 않고, 근거가 있고, 군더더기가 없는
- 개발자의 논리적 사고방식이 디자인과 기획에도 묻어나는 느낌
- 색보다 구조와 타이포그래피 위계로 말하는 디자인
- **무드: 현대적이고 깔끔한.** 장식 대신 정렬, 간격, 숫자 정렬의 정확함으로 인상을 만든다

### 브랜드를 지탱하는 세 가지

깔끔한 시스템은 쉽게 흔해진다. 아래 세 가지는 어떤 프로젝트에서도 빼지 않는다.

1. **장문의 Maru Buri** — 오래 읽는 글에서만 세리프가 등장해서, 읽는 순간이 다르게 느껴진다
2. **슬레이트블루 한 색** — 포인트 색은 이것 하나. 다른 색은 의미(주의)가 있을 때만
3. **정확한 정렬** — 숫자는 `tabular-nums`, 간격은 토큰 단위, 선은 1px로 겹치지 않게

---

## 컬러

### 원시값

웜 그레이 11단계(`--gray-50` ~ `--gray-950`)와 슬레이트블루(`--blue-*`), 테라코타(`--terra-*`).
라이트와 다크가 **같은 웜 그레이 단계**에서 나오기 때문에 두 모드가 같은 브랜드로 읽힌다.
프로젝트 코드에서 원시값을 직접 쓰지 않는다.

### 역할 토큰 (이것만 쓴다)

| 토큰 | 용도 | 라이트 | 다크 |
| --- | --- | --- | --- |
| `--bg` | 페이지 배경 | gray-50 | gray-950 |
| `--surface` | 카드·코드블록·입력창 면 | gray-100 | gray-900 |
| `--border` | 장식용 구분선 | gray-200 | gray-800 |
| `--input-border` | 입력창·보조 버튼 테두리 (3:1 이상) | gray-500 | gray-500 |
| `--text` | 본문 | gray-900 | gray-100 |
| `--muted` | 보조 텍스트 (설명, 리드) | gray-700 | gray-400 |
| `--subtle` | 메타 정보 (날짜, 플레이스홀더) | gray-600 | gray-500 |
| `--accent` | 링크, 주요 버튼, 활성 표시 | blue-600 | blue-400 |
| `--accent-soft` | 코어 태그, 정보 콜아웃 면 | blue-100 | blue-900 |
| `--on-accent` / `--on-accent-soft` | 위 두 면 위의 글자 | white / blue-700 | gray-950 / blue-300 |
| `--warning` / `--warning-soft` | 주의 레이블 / 주의 콜아웃 면 | terra-600 / terra-100 | terra-400 / terra-900 |

### 컬러 사용 원칙

- **포인트 색은 `--accent` 하나.** 링크, 주요 버튼, 탐색 활성 표시, 코어 분류 태그에 쓴다
- **테라코타는 `--warning`이라는 의미 색이다.** 막혔던 지점, 주의사항에만 쓰고 장식이나 분류 표시에는 쓰지 않는다
- 선택·탐색 상태는 색 면이 아니라 **밑줄 2px(accent) + semibold**로 표시한다
- 위계는 회색 단계(`--text` → `--muted` → `--subtle`)로 먼저 나누고, 그래도 부족할 때만 accent를 쓴다
- 카드에 border-top/border-left 포인트 색 금지

### 대비 기준

모든 글자 조합은 WCAG AA를 통과한다(작은 글씨 4.5:1, UI 테두리 3:1). 새 색 조합을 만들면 대비를 먼저 확인한다.
`--border`는 장식용이라 대비가 낮다. 입력창처럼 **경계가 기능인 곳에는 `--input-border`**를 쓴다.

---

## 타이포그래피

### 폰트

| 역할 | 폰트 | 쓰는 곳 |
| --- | --- | --- |
| UI 전체 | Pretendard | 제목, 본문 UI, 레이블, 버튼, 설명, 메타 — 기본값 |
| 장문 | Maru Buri | `.prose` 안의 본문만 (블로그 글 본문, 긴 에세이) |
| 코드 | 시스템 모노 | 인라인 코드, 코드블록 |

세리프는 **`.prose` 밖에서 쓰지 않는다.** 카드 설명, 콜아웃, 리드 문장도 Pretendard다.

### 폰트 불러오기

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/pretendard@1.3.9/dist/web/variable/pretendardvariable-dynamic-subset.css" />
<!-- 장문 본문이 있는 프로젝트만 -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/fonts-archive/MaruBuri/MaruBuri.css" />
```

### CSS 파일 로드 순서

```html
<link rel="stylesheet" href="tokens.css" />
<link rel="stylesheet" href="base.css" />
<link rel="stylesheet" href="components.css" />
```

`tokens.css` — 원시값, 역할 토큰, Tailwind v4 매핑
`base.css` — reset, 전역 기본값 (폰트, 제목, 링크, focus, 선택 영역)
`components.css` — 재사용 클래스 (`.card`, `.btn`, `.tag`, `.input`, `.callout`, `.prose`, `.timeline` …)

### 타입 스케일

| 토큰 | 크기 | 용도 |
| --- | --- | --- |
| `--size-xs` | 13px | 태그, 레이블, 아이브로우 — **하한선** |
| `--size-sm` | 14px | 설명, 메타, 버튼 |
| `--size-base` | 16px | 본문 |
| `--size-lg` | 18px | 리드, 목록의 글 제목 |
| `--size-xl` | 22px | h3 |
| `--size-2xl` | 28px | h2 |
| `--size-3xl` | 36px | h1 |
| `--size-display` | 32–52px | 히어로, 표지 |

### 타이포그래피 원칙

- **13px 미만 글씨를 쓰지 않는다**
- 제목은 **700**, 자간 `--letter-tight`(−0.022em). 900은 쓰지 않는다
- **대문자 변환(`uppercase`)과 넓은 자간을 쓰지 않는다** — 한글에는 대문자가 없어서 자간만 벌어진다
- 아이브로우는 작은 크기(`--size-xs`) + `--muted` 색으로만 구분
- 한글은 `word-break: keep-all`로 어절 단위 줄바꿈 (base.css에 포함)
- 숫자가 세로로 나열되는 곳(날짜, 표, 통계)은 `font-variant-numeric: tabular-nums`
- 크기 위계가 곧 정보 위계 — 색보다 크기와 굵기로 먼저 말한다

---

## 간격 · 모서리 · 레이아웃

### 간격

`--space-1`(4px)부터 `--space-16`(64px)까지 4px 단위. 컴포넌트 안의 여백도 토큰으로만 쓴다.
Tailwind의 `p-4`, `gap-6` 등과 값이 같다.

### 모서리

- **`--corner: 4px` 하나로 통일.** 카드, 버튼, 태그, 입력창, 콜아웃, 코드블록 모두
- 예외는 `--corner-round` — 타임라인 점, 아바타처럼 **원래 둥근 것**만
- 알약 모양(pill) 버튼, 8–12px 중간 라운드는 쓰지 않는다

### 레이아웃

- 장문 본문 최대 너비 `--max-w-prose`(42rem, 약 68자)
- 카드 그룹·목록·차트 최대 너비 `--max-w-wide`(60rem)
- 정렬은 좌측 기준. 가운데 정렬은 표지·발표자료처럼 한 화면에 한 메시지일 때만

---

## 컴포넌트 원칙

### 카드 · 카드 그룹

- `background: --surface`, `border: 1px --border`, `radius: --corner`, 그림자 없음
- 여러 장이면 `.card-group`으로 묶는다: 바깥 테두리 하나 + 내부 1px 구분선, 카드 사이 gap 없음
- 아이콘 + 제목 + 설명을 3열로 반복하는 구조는 피한다. 같은 모양이 반복되면 목록(`.divided-list`)이 더 맞는지 먼저 검토

### 버튼

| 종류 | 용도 |
| --- | --- |
| `.btn-primary` | 한 화면에서 가장 중요한 행동 하나. accent 면 |
| `.btn-secondary` | 그 외 행동. `--input-border` 테두리 |
| `.btn-ghost` | 내비게이션, 아이콘 버튼 |

hover는 투명도가 아니라 면 색 변화로 표시한다. disabled는 opacity 0.45.

### 태그

- 기본 `.tag`: 선만 있는 태그, `--muted` 글자
- 코어 분류 `.tag-accent`: `--accent-soft` 면 + `--on-accent-soft` 글자
- 꽉 찬 진한 색 태그는 쓰지 않는다 (목록에서 가장 시끄러운 요소가 됨)

### 입력창

`--surface` 면 + `--input-border` 테두리. focus는 accent 테두리 + 1px 링.

### 콜아웃

- 왼쪽 굵은 바 없이 **면 색으로 구분**. 레이블(`.callout-label`)을 위에 둔다
- 톤은 세 가지뿐: 기본(`--surface`), `.callout-accent`(정보), `.callout-warning`(주의)
- warning은 막혔던 지점, 삽질, 주의사항에만. 일반 강조나 인용에는 쓰지 않는다

### 장문 본문 (`.prose`)

- Maru Buri 16px, 줄간격 1.8, 최대 42rem
- 본문 안의 제목·코드·캡션은 Pretendard / 모노
- 인용은 2px `--border` 왼쪽 선 (인용이라는 의미가 있는 선이라 허용)

### 타임라인

- 가로형, 점(dot) + 1px 연결선
- 강조 지점은 dot을 accent로 채움
- 카드 테두리로 항목을 나누지 않는다

### 접근성

- 모든 인터랙티브 요소에 `:focus-visible` 표시 (accent 2px 아웃라인, base.css에 포함)
- `prefers-reduced-motion`을 존중한다 (base.css에 포함)

---

## 다크모드

- 역할 토큰은 `light-dark()`로 한 번만 정의되어 있다. 컴포넌트에 `dark:` 분기를 쓰지 않는다
- 기본은 OS 설정을 따르고, 루트에 `.dark`/`.light` 클래스나 `data-theme="dark|light"`를 주면 그쪽으로 고정된다
- 다크는 라이트를 반전한 것이 아니라 **같은 웜 그레이 단계에서 고른 것**이다. 프레임워크 기본 다크 팔레트(GitHub 등)를 가져오지 않는다

---

## 'AI 냄새' 판단 기준

> **장식이 정보와 무관하게, 프레임워크·라이브러리 기본값 그대로 깔려 있는가?**

체크리스트:

- [ ] 이 스타일이 Tailwind UI, shadcn, Material, GitHub 등의 기본값을 그대로 가져온 것처럼 보이는가?
- [ ] 이 장식(라운드, 그림자, 보더, 색)이 콘텐츠의 의미와 무관하게 모든 자리에 기계적으로 들어가 있는가?
- [ ] 이 선택에 "왜 이렇게 했는지" 한 문장으로 답할 수 있는가?

자주 걸리는 패턴 (이유 없이 쓰면 위 기준에 걸린다):

- 카드에 `border-top`/`border-left` 포인트 색
- 8–12px 중간 라운드를 모든 요소에 일괄 적용
- 배경 없이 그림자만 있는 카드
- 아이콘 + 제목 + 설명 3열 반복
- 이모지를 섹션 표시로 사용
- 크림 배경 + 세리프 제목 + 테라코타 포인트 조합 (0.0.1에서 벗어난 이유)
- Noto Sans KR / Noto Serif KR 조합

위 기준을 통과하면 형태 자체는 문제가 되지 않는다. (예: 4px 모서리는 "중간 라운드를 피하되 각진 화면의 딱딱함도 피한 선택"이라 통과)

---

## 사용 맥락

- 개인 브랜드: 백엔드 기반이지만 기획·데이터·콘텐츠까지 엮을 줄 아는 사람
- 쓰는 곳: 블로그, 개인 포트폴리오, 소규모 발표, 1:1 공유
- 톤: 차분하고 단단한, 과하지 않은
- 발표자료 전용 규칙은 [`guides/slides.md`](guides/slides.md)
