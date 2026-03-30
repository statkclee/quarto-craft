# Skill: Quarto 문서 개발

## 트리거 키워드
"quarto", "문서", "렌더링", "템플릿", "report", "presentation", "dashboard", "book", "qmd", "yaml"

## Quarto 프로젝트 구조

### _quarto.yml 필수 설정
```yaml
project:
  output-dir: docs        # 출력은 항상 docs/

format:
  html:
    theme:
      - cosmo
      - scss/quarto-theme.scss   # Quarto 전용 테마 파일
    lang: ko
    mainfont: "Pretendard Variable"
    monofont: "JetBrains Mono"
```

### QMD 프론트매터 패턴
```yaml
---
title: "제목"
subtitle: "부제목"
author: "작성자"
date: today
date-format: "YYYY년 MM월 DD일"
---
```

### 템플릿별 format 설정

| 템플릿 | format | 비고 |
|--------|--------|------|
| report | html | toc, number-sections |
| presentation | revealjs | 1600x900, fade |
| dashboard | dashboard | valuebox + 차트 |
| book | html + pdf | chapters 구조 |

## Quarto 테마 파일 규칙

Quarto theme SCSS 파일은 반드시 레이어 경계를 포함해야 한다:

```scss
/*-- scss:uses --*/
@use "sass:color";

/*-- scss:defaults --*/
// Bootstrap 변수 오버라이드 (변수 정의만)

/*-- scss:rules --*/
// CSS 규칙 (선택자 + 속성)
```

- `/*-- scss:defaults --*/`에는 변수 정의만 작성
- `/*-- scss:rules --*/`에는 CSS 규칙만 작성
- `@use` 문은 반드시 `/*-- scss:uses --*/` 섹션에 작성
- 일반 `@import`는 `/*-- scss:rules --*/` 내에서 URL import만 허용

## 금지 패턴

- Quarto 테마 파일에 레이어 경계 없이 작성
- `output-dir` 누락 (항상 `docs`)
- `lang: ko` 누락
- 폰트 설정 누락 (mainfont, monofont)

## 트러블슈팅

| 에러 | 원인 | 해결 |
|------|------|------|
| "doesn't contain at least one layer boundary" | 레이어 마커 누락 | `/*-- scss:defaults --*/` + `/*-- scss:rules --*/` 추가 |
| "no module with namespace" | `@use` 누락 | `/*-- scss:uses --*/` 섹션에 추가 |
| 폰트 미적용 | CDN 로드 실패 | `/*-- scss:rules --*/` 내 `@import url(...)` 확인 |
| 스타일 미적용 | defaults/rules 혼동 | 변수는 defaults, 규칙은 rules에 분리 |
