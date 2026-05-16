# Quarto Craft — 디자인 시스템 & 문서 템플릿

## 프로젝트 개요

한국어 문서에 최적화된 Quarto 디자인 시스템.
인디고 브랜드 색상, Major Third 타입 스케일, 한국어 가독성 최적화 규칙을 적용하며
report/presentation/dashboard/book/manuscript/blog/confluence/typst-pdf 8종 템플릿을 포함한다.

## 기술 스택

- **문서 엔진**: Quarto (>= 1.10)
- **스타일링**: Quarto SCSS 레이어 (scss:defaults / scss:rules)
- **폰트**: Pretendard Variable (본문), Noto Serif KR (인용), JetBrains Mono (코드)
- **출력**: HTML, RevealJS, Dashboard, Typst PDF

## 파일 구조

```
quarto-craft/
├── _extensions/quarto-craft/     # Quarto extension
│   ├── _extension.yml
│   └── assets/quarto-craft.css
├── assets/
│   └── brand/                    # 로고, 파비콘, 아이콘 가이드
├── scss/
│   ├── quarto-theme.scss         # HTML 테마 (모든 html 템플릿이 참조)
│   └── quarto-revealjs.scss      # RevealJS 테마
├── templates/
│   ├── report/                   # 보고서 (HTML)
│   ├── presentation/             # RevealJS 슬라이드
│   ├── dashboard/                # 대시보드
│   ├── book/                     # 책 (HTML + Typst PDF)
│   ├── manuscript/               # 학술 원고
│   ├── blog/                     # 블로그 (listing)
│   ├── confluence/               # Confluence 게시용
│   └── typst-pdf/                # Typst PDF
├── images/                       # 디자인 시스템 다이어그램 (SVG)
├── tech_document/                # 기술 의사결정 문서
├── _quarto.yml                   # 전역 설정 (output-dir: docs)
├── CLAUDE.md                     # 이 파일
├── PLAN.md                       # 개발 로드맵
└── PROGRESS.md                   # 진행 기록
```

## 핵심 아키텍처

### SCSS 단일 흐름

`scss/quarto-theme.scss` 한 파일이 Quarto의 SCSS 레이어 규약(`/*-- scss:defaults --*/`, `/*-- scss:rules --*/`)을 따른다.
디자인 토큰은 이 파일 안에 인라인 변수로 선언되어 있다 (Quarto가 직접 컴파일하므로 별도 sass 도구 불필요).

`scss/quarto-revealjs.scss`는 RevealJS 슬라이드 전용 테마로 같은 토큰 규칙을 따른다.

### 디자인 토큰 체계 (quarto-theme.scss 내부)

- **색상**: Primary(인디고 50-900) + Neutral(50-900) + Semantic(success/warning/error/info) + Callout
- **타이포그래피**: Major Third(1.250) 타입 스케일, 한국어 행간 1.75
- **간격**: 4px 단위 시스템

토큰 사양 시각화: `images/01-color-system.svg`, `images/02-typography-scale.svg`

### 한국어 최적화

- `word-break: keep-all` — 단어 단위 줄바꿈
- `line-height: 1.75` — 영문(1.5)보다 넓은 행간
- `letter-spacing: -0.02em` — 큰 제목 자간 조정
- Pretendard 가변 폰트 — 한글 렌더링 최적화

시각화: `images/05-korean-optimization.svg`

## 빌드 & 실행

```bash
quarto render          # 전체 프로젝트 렌더링 → docs/
quarto preview         # 실시간 미리보기
```

각 sub-project(book/manuscript/blog)는 해당 디렉토리에서 `quarto render` 실행.

## 금지 패턴

- Quarto 테마 파일에 레이어 경계(`scss:defaults`/`scss:rules`) 없이 작성 금지
- 하드코딩된 색상/폰트/간격 값 사용 금지 → quarto-theme.scss 토큰 변수 사용
- `docs/`는 GitHub Pages 배포용이므로 직접 편집 금지 (quarto render 결과물)

## 출력 설정

- 모든 템플릿의 Quarto 출력은 `docs/templates/<name>/`으로 지정
- GitHub Pages는 `main` 브랜치 `/docs` 폴더에서 서빙
