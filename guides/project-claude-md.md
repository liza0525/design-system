# 프로젝트 CLAUDE.md 표준 섹션

이 디자인 시스템을 쓰는 프로젝트의 **루트 `CLAUDE.md`**에 아래 `BEGIN`~`END` 사이 내용을 그대로 붙여 넣는다.
Claude Code가 매 세션 확실히 읽는 곳은 프로젝트 루트의 `CLAUDE.md`뿐이라, 디자인 시스템으로 들어오는 진입점은 여기 하나로 둔다.

붙여 넣은 뒤 `<…>`로 표시된 두 곳(고정 버전, 적용 방식)만 프로젝트에 맞게 고친다.
이미 Design System 섹션이 있으면 통째로 이 내용으로 교체한다.

<!-- BEGIN lizzie-design-system -->
## Design System

이 프로젝트는 `design-system/`(git submodule)의 Lizzie Design System을 따른다.

- **고정 버전**: `<0.0.2>` — 실제 값 확인: `git -C design-system describe --tags`
- **적용 방식**: `<import 또는 copy 중 하나만 남긴다>`
  - **import** — 프로젝트 CSS에서 `design-system/tokens.css`(필요하면 `components.css`도)를 `@import`해서 쓴다
  - **copy** — 토큰 값을 `<복사해 둔 파일 경로>`에 복사해서 쓴다. design-system이 바뀌어도 이 프로젝트에는 자동 반영되지 않는다

### UI 작업 전에

UI, 스타일, 컴포넌트를 만들거나 고치기 전에 `design-system/design-system.md`를 읽는다.
실제 값은 `design-system/tokens.css`가 원본이고, 재사용 클래스는 `design-system/components.css`에 있다.
시스템에 없는 색·폰트·컴포넌트 패턴은 임의로 만들지 말고 사용자에게 먼저 제안한다.

### 항상 지킬 규칙

- 색은 역할 토큰만 쓴다: `--bg` `--surface` `--border` `--input-border` `--text` `--muted` `--subtle` `--accent` `--accent-soft` `--on-accent` `--on-accent-soft` `--warning` `--warning-soft`. hex 값이나 `--gray-*` 원시값을 직접 쓰지 않는다
- 포인트 색은 `--accent` 하나. `--warning`은 주의 표시에만
- 폰트는 Pretendard가 기본. Maru Buri(세리프)는 장문 본문(`.prose`) 안에서만
- 13px 미만 글씨 금지. 제목은 700 + `--letter-tight`. `uppercase`와 넓은 자간 금지
- 모서리는 전부 `--corner`(4px). 점·아바타만 `--corner-round`. pill 버튼 금지
- 카드: `--surface` 면 + 1px `--border` + 4px, 그림자 없음. 카드에 `border-top/left` 포인트 색 금지
- 선택·탐색 상태는 색 면이 아니라 밑줄 2px(`--accent`) + semibold
- 다크모드는 토큰이 `light-dark()`로 자동 전환한다. 컴포넌트에 `dark:` 분기를 쓰지 않는다

### 디자인 시스템 버전을 올릴 때

"디자인 시스템 올려줘", "design-system 업데이트" 같은 요청을 받으면 아래 순서를 따른다.
**`git pull`이나 submodule 포인터만 바꾸고 끝내지 않는다.** 아직 0.0.x 단계라 어느 태그든 깨지는 변경이 있을 수 있다.

1. 현재 버전 확인: `git -C design-system describe --tags`
2. 태그 목록 확인: `git -C design-system fetch --tags` 후 `git -C design-system tag -l`. 사용자가 버전을 말하지 않았으면 최신 태그를 제안하고 확인받는다
3. 대상 태그로 이동: `git -C design-system checkout <대상 태그>`
4. `design-system/CHANGELOG.md`에서 현재 버전 다음부터 대상 버전까지의 항목을 읽고, 특히 **Removed**를 사용자에게 요약한다
5. `design-system/MIGRATION.md`에서 해당 구간 섹션을 열고, 적용 방식(import/copy)에 맞는 절차를 따른다. 섹션 안의 **검색 명령어를 실행해서 결과가 0건이 될 때까지** 대응표대로 고친다
6. 이 섹션의 "고정 버전"을 새 태그로 바꾼다
7. 바뀐 파일을 요약해서 보여준다. 커밋은 사용자가 지시할 때만 한다
<!-- END lizzie-design-system -->
