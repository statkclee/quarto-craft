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
- SCSS는 Quarto가 직접 컴파일하므로 별도 watch 불필요
