---
name: project-design-system
description: Lizzie 개인 브랜딩 디자인 시스템의 구조, 목적, 파일 역할
metadata:
  type: project
---

개인 브랜딩을 위한 SSOT 디자인 시스템 레포. 키워드는 "정밀한 사람".

**Why:** AI 작업 시 일관된 톤을 유지하고, 프로젝트마다 같은 컨텍스트를 반복 설명하지 않기 위해 구축.

**How to apply:** 디자인 관련 작업 요청 시 `design-system.md`를 컨텍스트로 읽고, `tokens.css`에서 실제 변수 값을 참조.

## 파일 역할

| 파일               | 역할                                                           |
| ------------------ | -------------------------------------------------------------- |
| `design-system.md` | 범용 원칙 전문 (브랜드 철학, 색, 폰트, 컴포넌트, AI 냄새 기준) |
| `tokens.css`       | CSS 변수 + Tailwind @theme inline 매핑 + 콜아웃 9색            |
| `SKILL.md`         | Claude Code 트리거 룰 (디자인 키워드 감지 시 자동 로드)        |
| `README.md`        | 사람용 빠른 요약                                               |

## 구조 결정

- `design-system.md`는 범용 원칙만 — 프로젝트별 적용 기록은 log 폴더에 작성
- 블로그 적용 내역(2026.06)은 log 폴더의 blog.md로 이전
- SKILL.md 트리거: 디자인 키워드 감지 방식
