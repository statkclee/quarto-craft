# /status — 프로젝트 상태 확인

## 확인 항목

### 1. 파일 구조 검증
필수 파일 존재 여부 확인:
- `_quarto.yml`
- `package.json`
- `scss/quarto-theme.scss`
- `scss/main.scss`
- `css/quarto-craft.css`
- `design-system/tokens/colors.scss`
- `design-system/tokens/typography.scss`
- `design-system/tokens/spacing.scss`
- `design-system/components/callout.scss`
- `design-system/components/table.scss`
- `design-system/components/code.scss`
- `_extensions/quarto-craft/_extension.yml`

### 2. PROGRESS.md 최신 항목
가장 최근 날짜의 진행 기록 출력.

### 3. PLAN.md 현재 Phase
진행 중(미완료) Phase와 남은 항목 표시.

### 4. Git 상태
- 현재 브랜치
- 커밋되지 않은 변경사항
- 최근 커밋 3개

### 5. 빌드 상태
- `css/quarto-craft.css` 마지막 수정 시간
- `scss/` 파일 중 CSS보다 최신인 파일 여부 (재빌드 필요 표시)
- `node_modules/` 존재 여부

### 6. 결과 보고
위 항목을 간결하게 요약하여 보고.
