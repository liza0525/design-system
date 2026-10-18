# 발표자료 가이드

> 범용 원칙(`design-system.md`)에 더해 발표자료에서만 적용하는 규칙.

## 레이아웃

- 한 슬라이드에 한 메시지. 표지·섹션 구분 슬라이드는 가운데 정렬, 내용 슬라이드는 좌측 정렬
- 섹션 제목은 `.display` (`--size-display`), 보충 설명은 `.lead`
- 슬라이드 안의 긴 문장은 `.prose`로 감싸지 않는다 — 발표 화면은 장문이 아니므로 세리프를 쓰지 않는다

## 내비게이션

- 키보드 ← → 및 화면 좌/우 클릭으로 전환
- 상단 progress bar로 진행도 표시 (1px 높이 `--border` 바 위에 `--accent` 진행분)
- 슬라이드 번호는 우측 상단, `.meta` 스타일 (`tabular-nums`)
- 내비게이션 버튼은 `.btn-ghost`

## 전환

- fade-in/out, `var(--motion-base) var(--motion-ease)`
- `prefers-reduced-motion`이면 전환 없이 바로 바꾼다 (base.css가 처리)
