# Lizzie Design System — Claude Code Rules

## 이 파일을 로드하는 조건 (디자인 키워드 감지)

다음 키워드가 요청에 포함될 때 `design-system.md`와 `tokens.css`를 읽고 적용한다:

**한국어:** 디자인, 스타일, 컬러, 색상, 색, 폰트, 서체, 레이아웃, 컴포넌트, 카드, 버튼,
태그, 배경, 테마, 타이포그래피, 여백, 간격, 모서리, 라운드, 보더, 그림자, UI, 시각, 배지

**영어:** design, style, color, colour, font, layout, component, card, button, tag,
background, theme, typography, spacing, border, radius, shadow, UI, visual, badge

**맥락 단서:** "어떻게 생겼어야 해", "어울리는 색", "CSS 짜줘", "스타일 수정", "Tailwind 클래스"

## 적용 방법

1. `design-system.md` 읽기 — 브랜드 철학, 컬러 사용 원칙, 타이포그래피, 컴포넌트 원칙
2. `tokens.css` 읽기 — 실제 CSS 변수 값과 Tailwind 클래스명 확인
3. 시스템에 없는 색, 폰트, 컴포넌트 패턴을 임의로 추가하지 않는다

## 빠른 참조 (읽기 전 체크)

| 항목 | 규칙 |
|------|------|
| 색 | `--bg`, `--surface`, `--border`, `--muted`, `--text`, `--accent`, `--accent2` 7개만 |
| 폰트 | Pretendard (제목/레이블), Hahmlet (본문/설명) |
| 카드 | `border-radius: 0`, `background: var(--surface)`, `border: 1px solid var(--border)` |
| 금지 | 카드 `border-top/left` 포인트 컬러, `box-shadow`만 있는 카드, `border-radius: 8–12px` |
| accent | 링크·활성 탐색·일반 강조 — 자유롭게 사용 가능 |
| accent2 | 코어 카테고리 레이블, 인라인 코드 — **선택/탐색 상태에는 사용 금지** |
