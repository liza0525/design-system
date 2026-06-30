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
| 세리프   | Maru Buri  | 본문 문장, 설명 텍스트, 부연               |

### 폰트 불러오기

```html
<link
  rel="stylesheet"
  href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.css"
/>
<link
  rel="stylesheet"
  href="https://cdn.jsdelivr.net/gh/fonts-archive/MaruBuri/MaruBuri.css"
/>
```

### CSS 파일 로드 순서

```html
<link rel="stylesheet" href="tokens.css" />
<link rel="stylesheet" href="base.css" />
<link rel="stylesheet" href="components.css" />
```

`tokens.css` — CSS 변수 정의 (색, 폰트, 타입 스케일, 레이아웃, 애니메이션)  
`base.css` — 토큰을 전역에 적용 (reset, body, heading, link 기본값)  
`components.css` — 재사용 클래스 (.card, .btn-pill, .callout, .eyebrow, .timeline...)

### 타입 스케일 (발표자료 기준)

```
eyebrow:     0.94rem  — Pretendard, uppercase, letter-spacing 0.22em
section h2:  clamp(2rem, 5vw, 3.6rem)  — Pretendard, weight 900
card-label:  0.7~1.2rem  — Pretendard, uppercase
card-title:  1rem  — Pretendard, weight 600~700
card-desc:   0.78~0.82rem  — Maru Buri, serif
slide-note:  0.96rem  — Maru Buri, muted color
```

### 타이포그래피 원칙

- 제목/레이블/버튼 → Pretendard (산세리프)
- 본문/설명/부연 → Maru Buri (세리프)
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