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

### 단순하게 쓰기 (clone + gitignore)

혼자 쓰는 프로젝트라면 이게 더 단순해요.

```bash
# 처음 세팅
git clone <이-레포-URL> design-system
echo "design-system/" >> .gitignore

# 업데이트할 때
git -C design-system pull
```

버전을 git이 추적하지 않는다는 차이만 있고, 솔로 프로젝트에선 문제없어요.

### Git Submodule로 다른 프로젝트에서 사용하기

버전을 고정하고 싶을 때 (팀 프로젝트 등).

**1. 처음 추가**

```bash
# 프로젝트 루트에서
git submodule add <이-레포-URL> design-system
git commit -m "Add design-system submodule"
```

**2. 이 레포를 포함한 프로젝트를 클론할 때**

```bash
git clone --recurse-submodules <프로젝트-URL>

# 이미 클론한 경우
git submodule update --init
```

**3. 디자인 시스템 최신 버전으로 업데이트**

```bash
git submodule update --remote design-system
git commit -m "Update design-system"
```

**4. tokens.css import**

```css
/* globals.css */
@import "./design-system/tokens.css";
```

**5. AI 작업 시**

```
design-system/design-system.md 읽어서 적용해줘
```

### 프로젝트별 적용 가이드

프로젝트 레포에 `DESIGN_LOG.md`를 두어 미정의 컴포넌트 처리 기준, 실제 적용 내역을 기록한다 (이 레포는 범용 원칙만 관리).
