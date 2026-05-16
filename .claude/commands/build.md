# /build — Quarto 렌더링

## 실행 순서

### 1. 루트 프로젝트 렌더링
```bash
cd $PROJECT_ROOT
quarto render
```
- `_quarto.yml`의 `render:` 목록에 포함된 템플릿만 빌드 (report, presentation, dashboard, typst-pdf, confluence)
- 출력: `docs/templates/<name>/`

### 2. Sub-project 렌더링 (book / manuscript / blog)
각 sub-project는 자체 `_quarto.yml`을 갖고 있어 별도 실행 필요:
```bash
cd templates/book      && quarto render && cd ../..
cd templates/manuscript && quarto render && cd ../..
cd templates/blog      && quarto render && cd ../..
```

### 3. 검증
- 출력 디렉토리 확인: `ls docs/templates/`
- 에러/경고 메시지 보고
- SCSS 변경 시 Quarto가 자동으로 재컴파일 (별도 도구 불필요)

### 4. 결과 보고
- 렌더링 성공/실패
- 생성된 파일 개수
- 경고 사항
