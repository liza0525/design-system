# Lizzie Design System

개인 브랜딩 디자인 시스템. 키워드: **정밀한 사람**.

## 파일 구조

| 파일 | 용도 |
|------|------|
| `design-system.md` | 원칙 전문 — AI에게 컨텍스트로 제공 |
| `tokens.css` | CSS 변수 + Tailwind @theme 매핑 — 프로젝트에 직접 import |
| `SKILL.md` | Claude Code 자동 적용 룰 (트리거 조건 포함) |

## 핵심 원칙 요약

- **색**: 크림 배경(`#f6f2eb`) 기반. `--accent`(슬레이트블루) + `--accent2`(테라코타) 2색만 포인트로 사용
- **폰트**: Pretendard(레이블/제목) + Hahmlet(본문/설명) 페어링
- **카드**: `radius: 0`, border-only, 그림자 없음
- **AI 냄새 기준**: "이 스타일에 '왜'라고 답할 수 있는가? 기본값을 이유 없이 그대로 쓴 게 아닌가?"

## 사용법

### 새 프로젝트에 tokens 적용

```css
/* globals.css */
@import "../path/to/tokens.css";
```

### AI 작업 시

`design-system.md`를 컨텍스트로 첨부하거나, Claude Code를 이 레포 위에서 실행하면 `SKILL.md` 트리거 조건에 따라 자동 적용된다.

### 프로젝트별 적용 가이드

각 프로젝트 레포에 `DESIGN_LOG.md`를 두어 미정의 컴포넌트 처리 기준, 실제 적용 내역을 기록한다 (이 레포는 범용 원칙만 관리).
