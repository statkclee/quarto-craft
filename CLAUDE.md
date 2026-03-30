# Quarto Craft — 디자인 시스템 & 문서 템플릿

## 프로젝트 개요

한국어 문서에 최적화된 Quarto 디자인 시스템.
디자인 토큰 기반의 일관된 타이포그래피, 색상, 간격을 제공하며
report/presentation/dashboard/book 4종 템플릿을 포함한다.

## 기술 스택

- **문서 엔진**: Quarto (>= 1.4)
- **스타일링**: Dart Sass, SCSS
- **폰트**: Pretendard Variable (본문), Noto Serif KR (인용), JetBrains Mono (코드)
- **빌드**: Node.js + sass 패키지
- **출력**: HTML, RevealJS, PDF

## 파일 구조

```
quarto-craft/
├── _extensions/quarto-craft/     # Quarto extension
│   ├── _extension.yml
│   └── assets/quarto-craft.css
├── design-system/
│   ├── tokens/                   # 디자인 토큰 (colors, typography, spacing)
│   └── components/               # 재사용 컴포넌트 (callout, table, code)
├── scss/
│   ├── _variables.scss           # 토큰 → Bootstrap 변수 매핑
│   ├── _mixins.scss              # heading-style, text-style 등
│   ├── main.scss                 # 독립 빌드용 (@use 문법)
│   └── quarto-theme.scss         # Quarto 전용 테마 (레이어 경계)
├── css/quarto-craft.css          # 컴파일된 CSS
├── templates/
│   ├── report/                   # 보고서 (HTML)
│   ├── presentation/             # RevealJS 슬라이드
│   ├── dashboard/                # 대시보드
│   └── book/                     # 책 (HTML + PDF)
├── tech_document/                # 기술 의사결정 문서
├── _quarto.yml                   # 전역 설정 (output-dir: docs)
├── package.json                  # SCSS 빌드 도구
├── CLAUDE.md                     # 이 파일
├── PLAN.md                       # 개발 로드맵
└── PROGRESS.md                   # 진행 기록
```

## 핵심 아키텍처

### SCSS 이중 빌드

| 파일 | 용도 | 문법 |
|------|------|------|
| `scss/main.scss` | 독립 CSS 빌드 (`npm run build`) | Dart Sass `@use`/`@forward` |
| `scss/quarto-theme.scss` | Quarto `theme:` 설정 | Quarto 레이어 (`scss:defaults`, `scss:rules`) |

### 디자인 토큰 체계

- **색상**: Primary(인디고) + Neutral + Semantic + Callout
- **타이포그래피**: Major Third(1.250) 타입 스케일, 한국어 행간 1.75
- **간격**: 4px 단위 시스템 (`$spacing-1` ~ `$spacing-24`)

### 한국어 최적화

- `word-break: keep-all` — 단어 단위 줄바꿈
- `line-height: 1.75` — 영문(1.5)보다 넓은 행간
- `letter-spacing: -0.02em` — 큰 제목 자간 조정
- Pretendard 가변 폰트 — 한글 렌더링 최적화

## 빌드 & 실행

```bash
npm run build          # SCSS → CSS (compressed)
npm run dev            # SCSS → CSS (expanded + source map)
npm run watch          # 파일 변경 감지 자동 빌드
quarto render          # 전체 프로젝트 렌더링
quarto preview         # 실시간 미리보기
```

## 금지 패턴

- `@import`로 SCSS 토큰 불러오기 금지 → `@use`/`@forward` 사용
- Quarto 테마 파일에 레이어 경계 없이 작성 금지
- 하드코딩된 색상/폰트/간격 값 사용 금지 → 토큰 변수 사용
- `node_modules/`, `docs/` 커밋 금지

## 출력 설정

- 모든 템플릿의 Quarto 출력은 `docs/` 폴더로 지정
- `.gitignore`에서 `docs/` 제외
