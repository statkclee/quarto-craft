# /status — 프로젝트 상태 확인

## 확인 항목

### 1. 파일 구조 검증
필수 파일 존재 여부 확인:
- `_quarto.yml`
- `scss/quarto-theme.scss`
- `scss/quarto-revealjs.scss`
- `assets/brand/favicon.svg`
- `_extensions/quarto-craft/_extension.yml`
- `templates/{report,presentation,dashboard,book,manuscript,blog,confluence,typst-pdf}/`

### 2. PROGRESS.md 최신 항목
가장 최근 날짜의 진행 기록 출력.

### 3. PLAN.md 현재 Phase
진행 중(미완료) Phase와 남은 항목 표시.

### 4. Git 상태
- 현재 브랜치
- 커밋되지 않은 변경사항
- 최근 커밋 3개

### 5. 렌더링 상태
- `docs/templates/<name>/index.html` 마지막 수정 시간
- 누락된 출력물 표시

### 6. 결과 보고
위 항목을 간결하게 요약하여 보고.
