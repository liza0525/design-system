# 블로그 적용 가이드 & 내역 — lizzie-blog

> Next.js 블로그에 디자인 시스템을 적용한 가이드와 실제 적용 내역.
> 토큰(색·폰트)은 `tokens.css` 및 `design-system.md`를 따른다.

---

## 색 사용 원칙 (블로그 맥락)

- `--accent` (슬레이트블루): 상시 사용 가능한 톤. 링크, 목차 활성 항목, 일반 태그 배지,
  탐색 선택 상태(필터 바 밑줄), 코드블록 키워드 등 "늘 보이는 강조"에 자유롭게 사용
- `--accent2` (테라코타): **레이블로 쓰되, 탐색 상태에는 쓰지 않는다.**
  코어 카테고리 배지(백엔드/인프라 등 최상위 분류), 인라인 코드, 콜아웃 박스처럼
  "이 정보는 다른 정보와 계층이 다르다"는 신호에 사용.
  필터 바 활성 버튼처럼 선택/탐색 상태를 나타낼 때는 쓰지 않는다
  (색이 "코어 카테고리"인지 "선택됨"인지 의미가 겹치기 때문).

---

## 글 목록 페이지

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

## 글 본문 페이지

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

## 태그

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

## 태그 필터 바

```
위치:    글 목록 상단 수평 배치 (햄버거 사이드바 없음)
노출:    글 있는 코어 태그만 기본 표시 → "+N 더 보기"로 나머지 펼침
         활성 태그가 비코어 태그일 경우 자동 전체 펼침
활성:    border-bottom 2px solid --accent, text-ink, font-semibold
비활성:  text-muted, hover: text-ink
```

색이 아닌 밑줄로 선택 상태 표현 → 태그 배지의 accent2(코어 분류)와 의미 충돌 없음.

## 콜아웃 박스 (테라코타)

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

## 실제 적용 내역 (2026.06)

### 다크모드

dark 팔레트(`#0d1117` 계열) 채택해 유지. `globals.css`의 `.dark {}` 블록에 정의.

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

### 콜아웃 색상 (9가지, 크림 배경 재조정)

`border-left: 4px solid` 방식 유지. 값은 `tokens.css` 참고.

### 글 목록 레이아웃

카드 3-column 그리드 → 텍스트 리스트 (border-bottom 구분).
썸네일은 `coverImage`가 있는 글에만 우측 96×72px로 표시 (picsum.photos fallback 제거).

### 태그 필터 바

햄버거 버튼 → 사이드바 방식 완전 제거. 글 목록 상단 수평 배치로 교체.
코어 태그(CORE_TAGS)만 기본 노출, "+N 더 보기"로 나머지 펼침.
활성 상태를 `bg-accent` 채워진 배지 대신 `border-b-2 border-accent` 밑줄로 변경
— 카드의 accent2 코어 카테고리 배지와 의미 혼선을 방지.

### 코드블록 인라인 코드

`--accent2` 색상으로 텍스트만 표시 (배경 없음). 블록 배경은 `--surface`, `border-border`, radius 0.
