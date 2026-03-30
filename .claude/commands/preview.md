# /preview — Quarto 미리보기 실행

## 실행 방법

### 특정 템플릿 미리보기
```bash
cd templates/{report|presentation|dashboard|book}
quarto preview
```

### 전체 프로젝트 미리보기
```bash
cd $PROJECT_ROOT
quarto preview
```

## 참고사항
- 미리보기는 파일 변경 시 자동 새로고침
- 포트 충돌 시: `quarto preview --port 4200`
- 중지: Ctrl+C
- SCSS 변경 시 `npm run watch`를 별도 터미널에서 실행하면 CSS 자동 빌드
