---
name: project-design-system
description: Lizzie 개인 브랜딩 디자인 시스템의 구조, 목적, 파일 역할
metadata:
  type: project
---

개인 브랜딩을 위한 SSOT 디자인 시스템 레포. 키워드는 "정밀한 사람", 무드는 "현대적이고 깔끔한"(0.0.2, 2026.10~).

**Why:** AI 작업 시 일관된 톤을 유지하고, 프로젝트마다 같은 컨텍스트를 반복 설명하지 않기 위해 구축.

**How to apply:** 디자인 관련 작업 요청 시 `design-system.md`를 컨텍스트로 읽고, `tokens.css`에서 실제 변수 값을 참조.

## 파일 역할

| 파일                  | 역할                                                       |
| --------------------- | ---------------------------------------------------------- |
| `design-system.md`    | 범용 원칙 전문 (브랜드 철학, 색, 폰트, 컴포넌트, AI 냄새 기준) |
| `tokens.css`          | 원시값 + 역할 토큰(light-dark) + Tailwind v4 @theme 매핑     |
| `base.css`            | reset, 전역 기본값                                          |
| `components.css`      | 재사용 클래스                                               |
| `showcase/index.html` | 실제 CSS로 렌더링한 확인용 페이지                            |
| `guides/slides.md`    | 발표자료 전용 규칙                                          |
| `MIGRATION.md`        | 버전 간 변경 내역, 블로그 적용 체크리스트                     |
| `CHANGELOG.md`        | 버전별 변경 요약                                            |
| `guides/project-claude-md.md` | 사용하는 프로젝트의 CLAUDE.md에 붙이는 표준 섹션 (AI 진입점) |
| `README.md`           | 사람용 빠른 요약, submodule 태그 고정 사용법                  |

## 구조 결정

- `design-system.md`는 범용 원칙만 — 프로젝트별 적용 기록은 각 프로젝트의 `DESIGN_LOG.md`, 목록은 `log/index.md`
- 다른 프로젝트에서는 submodule + 태그로 버전 고정. 태그는 `0.0.x`(v 없음), 아직 어느 태그든 깨지는 변경 가능
- AI 진입점은 프로젝트 루트 CLAUDE.md의 표준 섹션 하나. 레포 안의 SKILL.md는 Claude Code가 로드하지 않아서 삭제(0.0.2)
