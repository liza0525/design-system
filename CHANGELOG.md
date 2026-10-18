# Changelog

버전 규칙은 README의 "버전 규칙"을 따른다. 아직 0.0.x 단계라 **어느 태그든 깨지는 변경이 있을 수 있다.**
버전을 올릴 때는 현재 버전 다음부터 대상 버전까지의 항목을 모두 읽고, `MIGRATION.md`의 해당 구간 절차를 따른다.

CSS는 없어진 변수나 클래스를 써도 에러를 내지 않고 조용히 무시한다.
그래서 **Removed** 항목은 반드시 `MIGRATION.md`의 검색 명령어로 사용처를 찾아서 고친다.

## 0.0.2 — 2026.10

무드를 "따뜻한 에디토리얼"에서 "현대적이고 깔끔한"으로 바꾼 리뉴얼.
0.0.1 태그 이후의 미태그 커밋(`ad8c96b`까지)을 기준으로 비교한다.

### Removed (깨지는 변경)

- `--accent2` — 포인트 색을 하나로 줄임. 용도별로 나뉨: 코어 태그 → `.tag-accent`, 인라인 코드 → `--text` + `--surface`, 주의 → `--warning`
- `--callout-{gray|brown|orange|yellow|green|blue|purple|pink|red}-{bg|border}` 와 `.callout-{9색}` — 3톤(`.callout`, `.callout-accent`, `.callout-warning`)으로 통합
- `--font-sans`, `--font-serif` (원시 변수) — `--family-sans`, `--family-serif`로 이름 변경. Tailwind `font-sans`/`font-serif` 클래스는 그대로
- `--text-eyebrow`, `--text-h2`, `--text-card-label`, `--text-card-title`, `--text-card-desc`, `--text-note` — `--size-xs` … `--size-display` 단계로 교체
- `--tracking-eyebrow`, `--weight-black` — 넓은 자간과 900 굵기를 쓰지 않음
- `--radius-card`, `--radius-pill` — `--corner`(4px)로 통일
- `--max-w-card`, `--max-w-chart` — `--max-w-wide`로 통합
- `--transition-slide` — `--motion-base` + `--motion-ease`
- `.btn-pill` → `.btn .btn-primary`
- `.slide-note` → `.lead`

### Changed

- 기본 폰트가 Pretendard로 바뀜. Maru Buri는 `.prose`(장문 본문) 안에서만
- 회색이 크림 3단계에서 웜 그레이 50–950 + 역할 토큰으로 바뀜. `--bg`, `--surface`, `--border`, `--text`, `--muted`, `--accent`는 이름은 같고 값이 바뀜
- 제목 900 → 700, 자간 −0.022em. 아이브로우의 대문자 변환과 넓은 자간 제거
- 모서리 전부 4px
- 다크모드: GitHub 다크 값을 버리고 웜 그레이에서 파생. `light-dark()`로 정의해서 `.light`로 라이트 고정도 가능
- `.card-group`: 바깥 테두리 + 1px 구분선 구조로 바뀜. 열 수는 `data-cols`로 지정
- 최소 글씨 크기 13px

### Added

- 토큰: `--gray-50` … `--gray-950`, `--input-border`, `--subtle`, `--accent-soft`, `--on-accent`, `--on-accent-soft`, `--warning`, `--warning-soft`, `--size-*`, `--line-*`, `--letter-*`, `--corner`, `--corner-round`, `--max-w-prose`, `--motion-*`
- 클래스: `.btn-primary`, `.btn-secondary`, `.tag`, `.tag-accent`, `.input`, `.callout-accent`, `.callout-warning`, `.prose`, `.divided-list`, `.display`, `.lead`, `.meta`
- Tailwind v4 매핑이 실제로 동작함 (0.0.1은 색만 동작): `font-*`, `text-xs` … `text-display`, `tracking-tight`, `leading-*`, `rounded-box`, `max-w-reading`, `max-w-wide`
- `showcase/index.html`, `guides/slides.md`, `guides/project-claude-md.md`(프로젝트 CLAUDE.md 표준 섹션), `CHANGELOG.md`, `MIGRATION.md`

### Fixed

- `.card-group` 카드 사이 선이 2px로 겹치고 마지막 카드 오른쪽 선이 없던 문제
- OS가 다크일 때 수동으로 라이트로 돌아갈 수 없던 문제
- `--muted` 텍스트 대비 미달 (2.66:1 → 7.42:1)

### Removed (문서)

- `SKILL.md` — Claude Code가 스킬로 인식하지 않는 위치·형식이라 실제로 로드되지 않았음. 규칙은 `guides/project-claude-md.md`로 이동

## 0.0.1 — 2026.06

첫 태그. 크림 배경, Pretendard + 세리프 본문, 슬레이트블루 + 테라코타, 카드 radius 0.
