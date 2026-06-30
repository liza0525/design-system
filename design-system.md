# Lizzie Design System

> AI에게 디자인 작업을 요청할 때 컨텍스트로 제공하는 문서입니다.
> 새 프로젝트를 시작할 때 이 파일을 함께 첨부해 일관된 톤을 유지하세요.

---

## 브랜드 철학

**키워드: 정밀한 사람**

- 화려하지 않고, 근거가 있고, 군더더기가 없는
- 개발자의 논리적 사고방식이 디자인과 기획에도 묻어나는 느낌
- 색보다 구조와 타이포그래피 위계로 말하는 디자인
- 장식 없이 정보 자체가 말하는 구조

---

## 컬러 팔레트

### 라이트 모드

```
--bg:       #f6f2eb   /* 크림 배경 */
--surface:  #edeae2   /* 카드/서피스 */
--border:   #e4ddd0   /* 구분선 */
--muted:    #9a9590   /* 보조 텍스트 */
--text:     #282420   /* 본문 (완전 검정 아닌 오프블랙) */
--accent:   #3d5a80   /* 슬레이트블루 — 강조/핵심 */
--accent2:  #b85c38   /* 테라코타 — 카테고리 레이블 / 인라인 강조 */
```

### 다크 모드

```
--bg:       #0d1117
--surface:  #161b22
--border:   #21262d
--muted:    #555e6a
--text:     #e8e0d0
--accent:   #4a7fa5
--accent2:  #c9b48a
```

### 컬러 사용 원칙

- 포인트 컬러는 최소한으로, 쓸 때는 이유 있게
- `--accent` (블루): 강조, 핵심 레이블, 링크, 탐색 활성 표시
- `--accent2` (테라코타): 코어 카테고리 레이블, 인라인 코드 강조 — 빈도 높은 곳에 쓰되 *탐색 상태 표시*에는 쓰지 않는다 (선택 상태는 밑줄/굵기로 처리)
- 카드에 border-top/border-left 포인트 컬러 사용 금지 — 템플릿처럼 보임

---

## 타이포그래피

### 폰트 페어링

| 역할     | 폰트       | 용도                                       |
| -------- | ---------- | ------------------------------------------ |
| 산세리프 | Pretendard | 제목, 레이블, 표제성 텍스트, 버튼, eyebrow |
| 세리프   | Hahmlet    | 본문 문장, 설명 텍스트, 부연               |

### 폰트 불러오기

```html
<link
  rel="stylesheet"
  href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.css"
/>
<link
  href="https://fonts.googleapis.com/css2?family=Hahmlet:wght@400;600;900&display=swap"
  rel="stylesheet"
/>
```

### 타입 스케일 (발표자료 기준)

```
eyebrow:     0.94rem  — Pretendard, uppercase, letter-spacing 0.22em
section h2:  clamp(2rem, 5vw, 3.6rem)  — Pretendard, weight 900
card-label:  0.7~1.2rem  — Pretendard, uppercase
card-title:  1rem  — Pretendard, weight 600~700
card-desc:   0.78~0.82rem  — Hahmlet, serif
slide-note:  0.96rem  — Hahmlet, muted color
```

### 타이포그래피 원칙

- 제목/레이블/버튼 → Pretendard (산세리프)
- 본문/설명/부연 → Hahmlet (세리프)
- 본문 텍스트는 완전 검정(`#000`) 대신 오프블랙(`#282420`) 사용
- 타이포 크기 위계가 곧 정보 위계 — 색보다 크기로 먼저 말할 것

---

## 컴포넌트 원칙

### 카드

```
- border-radius: 0  (각진 모서리, 라운드 없음)
- background: var(--surface)
- border: 1px solid var(--border)
- border-top/left 포인트 컬러 금지
- 카드 그룹은 gap 없이 붙이고 내부 구분선으로 처리
```

### 버튼 (랜딩페이지)

```
- border-radius: 999px  (pill 모양, 세로축 반원)
- background: var(--accent)
- font-family: Pretendard
```

### 버튼 (발표자료)

```
- border: none, background: transparent
- 네비게이션 버튼은 장식 최소화
```

### 레이아웃

- 카드 그룹: `display: grid`, gap 없이 붙인 후 `border-right`로 구분
- 최대 너비: `max-width: 900px` (카드 그룹), `max-width: 820px` (차트/타임라인)
- 정렬: 발표자료는 가운데 정렬, 랜딩페이지는 좌측 정렬

### 타임라인

```
- 가로형 사용
- 점(dot) + 연결선(::before) 구조
- 강조 지점: dot을 accent 색으로 채움
- border로 카드 구분 금지, dot으로만 구분
```

---

## AI 냄새 나는 패턴 (사용 금지)

- 카드 `border-top: 2px solid accent` 스타일
- `border-radius: 8~12px` 중간 라운드
- 배경색 없이 그림자만 있는 카드 (`box-shadow`)
- 파란색/주황색 조합의 기본 포인트 컬러
- 세 컬럼 카드에 아이콘 + 제목 + 설명 반복 구조
- Noto Sans KR / Noto Serif KR 조합 (너무 흔함)

---

## 발표자료 특이사항

- fade-in/out 전환 애니메이션 (0.4s ease)
- 상단 progress bar로 진행도 표시
- 키보드 ← → 및 화면 클릭 좌/우로 슬라이드 전환
- 슬라이드 번호는 우측 상단에 표시

---

## 사용 맥락

- 개인 브랜드: 백엔드 기반이지만 기획·데이터·콘텐츠까지 엮을 줄 아는 사람
- 타겟: 소규모 대면 발표, 1:1 공유, 개인 포트폴리오
- 톤: 차분하고 단단한, 과하지 않은

---

## 블로그 적용 가이드 (lizzie-shelf)

> 2026.06 블로그 레이아웃 작업에서 합의된 내용. 위 발표자료 기준 시스템을
> 블로그 컴포넌트 단위로 구체화한 것이며, 토큰(색·폰트)은 동일하게 따른다.

### 색 사용 원칙 (블로그 맥락)

- `--accent` (슬레이트블루): 상시 사용 가능한 톤. 링크, 목차 활성 항목, 일반 태그 배지,
  탐색 선택 상태(필터 바 밑줄), 코드블록 키워드 등 "늘 보이는 강조"에 자유롭게 사용
- `--accent2` (테라코타): **레이블로 쓰되, 탐색 상태에는 쓰지 않는다.**
  코어 카테고리 배지(백엔드/인프라 등 최상위 분류), 인라인 코드, 콜아웃 박스처럼
  "이 정보는 다른 정보와 계층이 다르다"는 신호에 사용.
  필터 바 활성 버튼처럼 선택/탐색 상태를 나타낼 때는 쓰지 않는다
  (색이 "코어 카테고리"인지 "선택됨"인지 의미가 겹치기 때문).

### 글 목록 페이지

```
구조:  날짜 | 제목 + 요약 + 태그           [이미지]
       (이미지는 cover 필드가 있을 때만 우측에 추가, 없으면 텍스트만)

날짜:    Pretendard 11px, weight 600, letter-spacing 0.08em, --muted
제목:    Pretendard 18px, weight 600, --text
요약:    Hahmlet 15px, line-height 1.7, --text (opacity 0.75)
태그:    아래 "태그" 항목 참고
구분:    각 항목 사이 border-bottom 1px solid --border (gap 없이 붙임)
썸네일:  96x72px, radius 0, border 1px solid --border, object-fit: cover
```

### 글 본문 페이지

```
제목:    Pretendard 26px, weight 700
메타:    날짜 + 태그, 제목 하단
본문:    Hahmlet 16px, line-height 1.85, --text
목차:    우측 고정(sticky) 사이드바, 너비 140px
         - 활성 섹션: Pretendard 13px weight 600, --accent
         - 비활성 섹션: Pretendard 13px, --muted
         - 컬러 보더로 표시하지 않음 (카드 left-border 금지 원칙과 동일하게 적용)
코드블록: 배경 --surface, border 1px solid --border, radius 0
         - 키워드(const, await 등): --accent
         - 주석: --muted
이미지:   캡션은 이미지 하단, Pretendard 12px, --muted, 중앙 정렬
```

### 태그

```
배경: --accent (#3d5a80)           — 일반 태그
배경: --accent2 (#b85c38)          — 코어 카테고리 태그 (CORE_TAGS)
텍스트: --bg (#f6f2eb)
border-radius: 2px
padding: 3px 10px
font: Pretendard 12px, weight 600
```

코어 카테고리(CORE_TAGS): 백엔드, 프론트엔드, 인프라, 데이터, AI, 디자인, 후기, 회고.
글이 달린 코어 태그만 필터 바에 노출 (글 없으면 자동 숨김).

판단 기준: 칩(배지) 형태 자체는 문제가 아니다. 문제는 "배경색 + 8~12px 라운드 +
대비색 텍스트"를 기본값 그대로 가져다 쓰는 것. radius를 2px로 의도적으로 낮춘 것이
이미 그 기본값에서 벗어난 선택이므로 시스템 원칙과 충돌하지 않는다.

### 태그 필터 바

```
위치:    글 목록 상단 수평 배치 (햄버거 사이드바 없음)
노출:    글 있는 코어 태그만 기본 표시 → "+N 더 보기"로 나머지 펼침
         활성 태그가 비코어 태그일 경우 자동 전체 펼침
활성:    border-bottom 2px solid --accent, text-ink, font-semibold
비활성:  text-muted, hover: text-ink
```

색이 아닌 밑줄로 선택 상태 표현 → 태그 배지의 accent2(코어 분류)와 의미 충돌 없음.

### 콜아웃 박스 (테라코타)

```
배경: --bg와 동일 (채우지 않음 — 채우면 "경고"가 아니라 "장식"처럼 무거워짐)
border: 1px solid --accent2
padding: 1.1rem 1.25rem
라벨: Pretendard 11px, weight 700, letter-spacing 0.08em, uppercase, --accent2
본문: Hahmlet 15px, --text
```

용도: 글 쓰다가 막혔던 지점, 삽질했던 부분, 주의사항을 표시할 때만 사용.
일반 강조나 인용에는 쓰지 않는다.

---

## 'AI 냄새' 판단 기준 (개정)

기존 금지 목록(중간 라운드, border-top 포인트 컬러, 그림자만 있는 카드 등)의 공통점을
한 줄로 정리하면:

> **장식이 정보량과 무관하게, 프레임워크/라이브러리 기본값 그대로 깔려 있는가?**

체크리스트:

- [ ] 이 스타일이 Tailwind UI, shadcn, Material Design 등의 기본 컴포넌트를
      그대로 가져온 것처럼 보이는가?
- [ ] 이 장식(라운드, 그림자, 보더, 색)이 콘텐츠의 의미와 무관하게 항상 같은 자리에
      기계적으로 들어가 있는가?
- [ ] 이 선택에 "왜 이렇게 했는지" 한 문장으로 답할 수 있는가? (답할 수 없으면 기본값을
      그대로 쓴 것일 가능성이 높음)

이 기준을 통과하면, 라운드든 칩이든 그림자든 형태 자체는 문제가 되지 않는다.
(예: 태그의 2px 라운드는 "8~12px 기본값을 의도적으로 피한 선택"이라 통과)

---

## 블로그 실제 적용 내역 (2026.06)

> Next.js 블로그에 위 시스템을 전면 적용한 결과물. 미정의 컴포넌트의 처리 기준을 함께 기록.

### 다크모드

design-system.md에는 "미채택(참고용)"으로 표시되어 있었으나, 기존 구현이 완전한 상태였으므로
dark 팔레트(`#0d1117` 계열)를 채택해 유지. `globals.css`의 `.dark {}` 블록에 정의.

### 폰트 로딩 방식

- Pretendard: `next/font` 미지원 → CDN `<link>` 직접 삽입 (`orioncactus/pretendard`)
- Hahmlet: `next/font/google`로 로드, CSS 변수 `--font-hahmlet` 주입

### Tailwind v4 통합

CSS 변수를 `@theme inline`으로 Tailwind 유틸리티에 노출. 다크모드를 CSS 변수가 자동으로 처리하므로
컴포넌트에서 `dark:` prefix 불필요.

```css
/* globals.css */
--color-bg: var(--bg);          → bg-bg, text-bg
--color-surface: var(--surface) → bg-surface
--color-border: var(--border)   → border-border
--color-muted: var(--muted)     → text-muted
--color-ink: var(--text)        → text-ink
--color-accent: var(--accent)   → bg-accent, text-accent
--color-accent2: var(--accent2) → text-accent2
```

### 미정의 컴포넌트 처리 기준

| 컴포넌트           | 적용 원칙                                                                                     |
| ------------------ | --------------------------------------------------------------------------------------------- |
| **Header**         | 배경 `--bg` (페이지와 동일 — 헤더가 떠있는 느낌 없이 일체화), 하단 `border-border`            |
| **Footer**         | `text-muted`, `max-w-[900px]`, `border-top border-border`                                     |
| **SearchInput**    | `border border-border`, radius 0, focus: `border-accent`, 배경 `--surface`                    |
| **TagFilter**      | 수평 필터 바, 활성 `border-b-2 border-accent` + `text-ink font-semibold`, 비활성 `text-muted` |
| **ThemeToggle**    | `text-muted hover:text-ink hover:bg-surface`                                                  |
| **ShareSidebar**   | `border border-border` (rounded-full 제거), 아이콘 `text-muted hover:text-ink`                |
| **GiscusComments** | 컨테이너에 `border-t border-border pt-8` 추가 (iframe 내부는 변경 불가)                       |
| **AdjacentPosts**  | 레이블 `text-muted`, 제목 `text-ink group-hover:text-accent`                                  |
| **PostLoading**    | 스켈레톤 `bg-border` (gray 계열 제거)                                                         |

### 콜아웃 색상 (9가지 유지, 크림 배경 재조정)

Notion callout의 9가지 색을 유지하되 크림 배경(`#f6f2eb`)에 맞게 채도를 낮춰 재정의.
`border-left: 4px solid` 방식 유지. 다크모드 색상 함께 정의.

| 색상   | 라이트 bg / border    | 다크 bg / border      |
| ------ | --------------------- | --------------------- |
| gray   | `#eeebe4` / `#9a9590` | `#1a1e26` / `#4a5568` |
| brown  | `#f2ece3` / `#8c6d4f` | `#1e1812` / `#6b4f30` |
| orange | `#f5ece2` / `#c46a2d` | `#1e1610` / `#8a4a1e` |
| yellow | `#f5eedc` / `#b89040` | `#1c1a0c` / `#7a6030` |
| green  | `#e8ede5` / `#5a8060` | `#0e1a14` / `#3d6050` |
| blue   | `#e5ecf2` / `#3d5a80` | `#0c1520` / `#4a7fa5` |
| purple | `#ede9f2` / `#7055a0` | `#160e20` / `#5a4080` |
| pink   | `#f2e8ee` / `#a06080` | `#1e1018` / `#784060` |
| red    | `#f2e8e5` / `#b85c38` | `#1e0e0c` / `#a04030` |

### 글 목록 레이아웃 변경

카드 3-column 그리드 → 텍스트 리스트 (border-bottom 구분).
썸네일은 `coverImage`가 있는 글에만 우측 96×72px로 표시 (picsum.photos fallback 제거).

### 태그 필터 바 변경

햄버거 버튼 → 사이드바 방식 완전 제거. 글 목록 상단 수평 배치로 교체.
코어 태그(CORE_TAGS)만 기본 노출, "+N 더 보기"로 나머지 펼침.
활성 상태를 `bg-accent` 채워진 배지 대신 `border-b-2 border-accent` 밑줄로 변경
— 카드의 accent2 코어 카테고리 배지와 의미 혼선을 방지.

### 코드블록 인라인 코드

`--accent2` 색상으로 텍스트만 표시 (배경 없음). 블록 배경은 `--surface`, `border-border`, radius 0.
