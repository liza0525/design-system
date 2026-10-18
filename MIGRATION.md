# Migration

버전을 올릴 때 프로젝트 코드에서 고칠 곳과 고치는 방법.
구간마다 섹션이 하나씩 있고, 각 섹션은 **0단계(적용 방식 확인) → 1단계(고칠 곳 찾기) → 2단계(고치기)** 순서로 되어 있다.

CSS는 없어진 변수나 클래스를 써도 에러 없이 조용히 무시한다. 눈으로 확인하지 말고 반드시 1단계의 검색 명령어로 찾는다.

---

## 0.0.1 → 0.0.2

0.0.2는 무드를 "따뜻한 에디토리얼"에서 "현대적이고 깔끔한"으로 바꾼 리뉴얼이다.
0.0.1 태그 이후의 미태그 커밋(`ad8c96b`까지: base.css, components.css, 다크모드, 간격 토큰)에 고정된 프로젝트도 이 섹션을 따른다.

### 0단계: 적용 방식 확인

프로젝트 `CLAUDE.md`의 Design System 섹션에 적힌 적용 방식을 확인한다. 없으면 프로젝트 CSS를 보고 판단한다.

| 방식 | 판단 기준 | 이 업그레이드에서 할 일 |
| --- | --- | --- |
| **import** | 프로젝트 CSS에 `@import "…/design-system/tokens.css"`가 있다 | submodule을 0.0.2로 올리면 토큰 값은 자동으로 바뀐다. 1·2단계로 삭제된 이름만 고친다 |
| **copy** | `--bg: #f6f2eb` 같은 토큰 값이 프로젝트 CSS에 직접 적혀 있다 | submodule을 올려도 화면은 그대로다. 아래 "copy 방식 전환"을 먼저 하고 1·2단계로 간다 |

#### copy 방식 전환 (권장: import로 바꾸기)

0.0.2부터 `tokens.css`는 Tailwind v4 프로젝트에 그대로 import해도 충돌하지 않는다(`@theme inline` 매핑 포함, Tailwind 4.2.2로 컴파일 검증).
그래서 복사본을 새 값으로 다시 맞추기보다 **import로 바꾸는 것을 권장**한다. 그래야 다음 버전부터는 값이 자동으로 따라온다.

1. 프로젝트 CSS에서 복사해 둔 토큰 블록(`:root { --bg … }`, `.dark { … }`)을 삭제한다
2. 프로젝트 CSS의 `@theme inline`에서 색·폰트 매핑(`--color-bg` … `--color-accent2`, `--font-sans`, `--font-serif`)을 삭제한다. 프로젝트 고유의 매핑은 남긴다
3. Tailwind import 바로 다음 줄에 추가한다:
   ```css
   @import "tailwindcss";
   @import "../design-system/tokens.css";   /* 프로젝트 CSS 위치 기준 상대 경로 */
   ```
4. (선택) 재사용 클래스가 필요하면 `@import "…/design-system/components.css" layer(components);` — `layer(components)`로 넣어야 Tailwind 유틸리티가 이긴다
5. `base.css`는 Tailwind Preflight와 역할이 겹치므로 Tailwind 프로젝트에서는 넣지 않는다. 대신 다음 세 가지가 프로젝트 CSS에 있는지 확인하고 없으면 추가한다: `html { word-break: keep-all; }`, 제목의 `letter-spacing: var(--letter-tight)`, `:focus-visible` 아웃라인
6. 다크모드 토글이 `<html>`에 `.dark` 클래스를 붙이는 방식이면 그대로 동작한다. OS가 다크일 때 라이트로 고정하려면 라이트 선택 시 `.light` 클래스를 붙이도록 바꾼다

copy 방식을 유지해야 하는 이유가 있다면, 복사본을 0.0.2 `tokens.css`의 역할 토큰·원시값 전체로 교체하고 `CLAUDE.md`에 그 이유를 적어 둔다.

### 1단계: 고칠 곳 찾기

프로젝트 루트에서 실행한다. **결과가 0건이 될 때까지** 2단계 대응표대로 고친다.

```bash
grep -rnE "accent2|--callout-|--font-(sans|serif)\b|--text-(eyebrow|h2|card-|note)|--tracking-eyebrow|--weight-black|--radius-(card|pill)|--max-w-(card|chart)|--transition-slide|btn-pill|slide-note|callout-(gray|brown|orange|yellow|green|blue|purple|pink|red)\b" --include=*.css --include=*.ts --include=*.tsx --include=*.js --include=*.jsx --include=*.html --include=*.mdx --exclude-dir=node_modules --exclude-dir=design-system --exclude-dir=.next .
```

- `--callout-`처럼 프로젝트가 자체적으로 같은 이름을 정의해 쓰는 경우도 걸린다. 그런 곳도 3톤 콜아웃으로 옮기는 대상이다
- 이 명령어는 **이름이 사라진 것**만 찾는다. 값만 바뀐 것(크기, 굵기, 모서리)은 아래 "검색에 안 걸리는 변경"을 따로 확인한다

### 2단계: 고치기

#### 바뀐 결정

| 항목 | 0.0.1 | 0.0.2 |
| --- | --- | --- |
| 기본 폰트 | 본문·설명 세리프 (Hahmlet → Maru Buri) | Pretendard. 세리프는 `.prose` 장문 본문만 |
| 회색 | 크림 기반 3단계 | 웜 그레이 50–950 + 역할 토큰 |
| 포인트 색 | `--accent` + `--accent2` | `--accent` 하나. 테라코타는 `--warning` |
| 제목 | 900, uppercase 아이브로우 0.22em | 700, −0.022em, 대문자·넓은 자간 없음 |
| 모서리 | 카드 0 / 버튼 999px / 태그 2px | 전부 4px (`--corner`) |
| 다크모드 | GitHub 다크 값, `.dark`만 지원 | 웜 그레이에서 파생, `light-dark()`로 양방향 |
| 최소 글씨 | 정의 없음 (11px, 12.8px 사용) | 13px |

#### 토큰 대응표

| 0.0.1 | 0.0.2 | 비고 |
| --- | --- | --- |
| `--bg` `--surface` `--border` `--text` `--accent` | 같은 이름 | 값만 바뀜 |
| `--muted` | `--muted` 또는 `--subtle` | 설명·리드는 `--muted`, 날짜·플레이스홀더는 `--subtle` |
| `--accent2` (코어 태그) | `.tag-accent` (`--accent-soft` + `--on-accent-soft`) | |
| `--accent2` (인라인 코드) | `--text` + `--surface` 면 | `.prose` 안에서는 자동 |
| `--accent2` (콜아웃·주의) | `--warning`, `--warning-soft` | |
| `--callout-{9색}-bg/border` | 삭제 → 3톤 (아래 표) | |
| `--font-sans` `--font-serif` | `--family-sans` `--family-serif` | Tailwind 쪽 `font-sans`/`font-serif`는 그대로 |
| `--text-eyebrow` `--text-h2` `--text-card-*` `--text-note` | `--size-xs` … `--size-display` | 용도별 이름 → 크기 단계 |
| `--tracking-eyebrow` | 삭제 | 넓은 자간을 쓰지 않음 |
| `--weight-black` | 삭제 | 제목은 `--weight-bold`(700) |
| `--radius-card` `--radius-pill` | `--corner` (`--corner-round`는 점·아바타 전용) | |
| `--max-w-card` `--max-w-chart` | `--max-w-wide` | 장문은 `--max-w-prose` |
| `--transition-slide` | `--motion-base` + `--motion-ease` | |

#### 클래스 대응표

| 0.0.1 | 0.0.2 |
| --- | --- |
| `.btn-pill` | `.btn .btn-primary` |
| `.btn-ghost` | `.btn .btn-ghost` (그대로) / 테두리 있는 보조 버튼은 `.btn .btn-secondary` |
| `.callout-{9색}` | `.callout` / `.callout-accent` / `.callout-warning` |
| `.slide-note` | `.lead` |
| `.card-group` + `.card` | 그대로. 열 수는 `data-cols="2|3|4"`로 지정 |

#### Tailwind 클래스 대응표

| 0.0.1 | 0.0.2 |
| --- | --- |
| `bg-accent2` (코어 태그) | `bg-accent-soft text-on-accent-soft` |
| `text-accent2` (인라인 코드) | `text-ink bg-surface` |
| `bg-accent` (일반 태그, 진한 면) | `border border-border text-muted` |

0.0.1의 Tailwind 매핑에서 동작하던 건 `--color-*`뿐이었다. 0.0.2부터 `font-*`, `text-*`(크기), `tracking-tight`, `leading-*`,
`rounded-box`, `max-w-reading`, `max-w-wide`가 실제로 생성된다.

#### Notion 콜아웃 9색 → 3톤

| Notion 색 | 0.0.2 톤 |
| --- | --- |
| default, gray, brown, green, purple, pink | `.callout` (기본, `--surface`) |
| blue | `.callout-accent` |
| orange, yellow, red | `.callout-warning` |

#### 검색에 안 걸리는 변경

이름은 그대로라 1단계 검색에 안 걸리지만 새 규칙에 어긋나는 것들. 아래 검색으로 따로 확인한다.

```bash
grep -rnE "text-\[(9|10|11|12)px\]|uppercase|tracking-(wide|wider|widest|\[)|font-black|rounded-(full|lg|xl|md)|dark:" --include=*.tsx --include=*.jsx --include=*.html --include=*.mdx --exclude-dir=node_modules --exclude-dir=design-system --exclude-dir=.next .
```

| 걸린 것 | 고치는 방법 |
| --- | --- |
| `text-[10px]` `text-[11px]` `text-[12px]` | `text-xs` (13px) |
| `uppercase`, `tracking-wide*`, `tracking-[…]` | 삭제 |
| `font-black` | `font-bold` |
| `rounded-full` `rounded-lg` 등 | `rounded-box`. 점·아바타·원형 아이콘이면 `rounded-full` 유지 |
| `dark:` | 토큰 색만 바꾸는 분기면 삭제. 레이아웃이 달라지는 분기면 유지 |

### 프로젝트별 체크리스트

#### blog (copy 방식, `ad8c96b` 고정, 2026.10 코드 기준)

- [ ] copy → import 전환 (위 "copy 방식 전환" 1–6)
- [ ] `globals.css` `.prose`: `--tw-prose-code`를 `var(--text)`로, 폰트는 `var(--family-serif)`
- [ ] `globals.css` `.notion-callout`: `border-left: 4px` 제거, `border-radius: var(--corner)`, `data-color`별 9색 정의를 3톤 매핑으로 교체
- [ ] `PostGrid.tsx`, `posts/[slug]/page.tsx`: 태그의 `bg-accent2` / `bg-accent` → `.tag-accent` / `.tag` 계열
- [ ] `CodeBlock.tsx`: 인라인 코드 `text-accent2` → `text-ink bg-surface rounded-box`, 언어 레이블의 `uppercase tracking-wider` 제거
- [ ] `PostGrid.tsx`, `posts/[slug]/page.tsx`, `NoteHighlights.tsx`: 날짜·레이블의 `text-[10px]`/`text-[11px]` + `uppercase tracking-[0.08em]` → `text-xs text-subtle tabular-nums`
- [ ] `TocBottomSheet.tsx`: `rounded-full` → `rounded-box`. `shadow-lg`는 화면 위에 떠 있는 요소라 유지 가능
- [ ] `MermaidBlock.tsx`: Tailwind 기본 회색(`gray-*`, `bg-white`)과 `rounded-xl` + `dark:` 분기 → `bg-surface border-border rounded-box`. 오류 상태(`red-*`)는 `bg-warning-soft text-warning`
- [ ] `HighlightText.tsx`: 검색 하이라이트 `bg-yellow-200 dark:bg-yellow-500/40` → `bg-accent-soft`
- [ ] `admin/page.tsx`: 내부용 화면이라 선택. 바꾼다면 `gray-*` → 역할 토큰, `rounded-lg` → `rounded-box`
- [ ] `config.ts`: `CORE_TAGS` 주석의 "accent2(테라코타)" 설명 갱신
- [ ] `CLAUDE.md`: Design System 섹션을 `design-system/guides/project-claude-md.md` 표준 섹션으로 교체 (적용 방식: import)
- [ ] `DESIGN_LOG.md`: Hahmlet 언급과 0.0.1 색 설명을 0.0.2 기준으로 갱신
