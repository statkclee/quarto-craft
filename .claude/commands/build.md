# /build — SCSS 빌드 및 Quarto 렌더링

## 실행 순서

### 1. SCSS 컴파일
```bash
cd $PROJECT_ROOT
npm run build
```
- `scss/main.scss` → `css/quarto-craft.css` (compressed)
- 에러 발생 시 원인 파악 후 수정

### 2. Extension assets 동기화
```bash
cp css/quarto-craft.css _extensions/quarto-craft/assets/quarto-craft.css
```

### 3. Quarto 렌더링 (선택)
사용자가 특정 템플릿을 지정하면 해당 디렉토리에서 렌더링:
```bash
cd templates/{report|presentation|dashboard|book}
quarto render
```
지정하지 않으면 report 템플릿 기본 렌더링.

### 4. Shiny app 동기화
```bash
cp -r templates/shiny-app/ docs/shiny-app/
```

### 5. 검증
- CSS 파일 생성 확인
- 렌더링 결과 `docs/` 폴더 확인
- 에러/경고 메시지 보고

### 5. 결과 보고
- 컴파일 성공/실패 여부
- 파일 크기
- 경고 사항
