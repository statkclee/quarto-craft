# Skill: SCSS 디자인 시스템

## 트리거 키워드
"scss", "sass", "css", "디자인 토큰", "색상", "타이포", "폰트", "간격", "컴포넌트", "스타일", "테마"

## 디자인 토큰 체계

### 색상 토큰 (`design-system/tokens/colors.scss`)

**네이밍 규칙**: `$color-{카테고리}-{단계}`

```scss
// 팔레트: $color-{name}-{50~900}
$color-primary-600: #4F46E5;

// 시맨틱: $color-{용도}
$color-bg-primary: #FFFFFF;
$color-text-primary: $color-neutral-900;
$color-border-default: $color-neutral-200;
$color-callout-note: $color-info;
```

새 색상 추가 시:
1. 팔레트 변수 정의 (50~900 단계)
2. 시맨틱 변수로 매핑
3. `quarto-theme.scss`의 `/*-- scss:defaults --*/`에도 동기화

### 타이포그래피 토큰 (`design-system/tokens/typography.scss`)

**타입 스케일**: Major Third (1.250)
```
base(16px) × 1.250 = lg(20px) × 1.250 = xl(25px) × 1.250 = 2xl(31.25px) ...
```

**행간 (한국어 최적)**:
- 제목: 1.3 (tight)
- 부제목: 1.5 (snug)
- 본문: 1.75 (normal) ← 한국어 기본
- 넓은 본문: 1.9 (relaxed)

새 텍스트 스타일 추가 시:
1. `typography.scss`에 스타일 맵 정의
2. `_mixins.scss`의 `text-style()` mixin으로 적용
3. `quarto-theme.scss`에도 동기화

### 간격 토큰 (`design-system/tokens/spacing.scss`)

**기본 단위**: 4px (`$spacing-unit: 0.25rem`)

```scss
$spacing-{n}: $spacing-unit * {n};
// $spacing-4 = 1rem = 16px
```

## 컴포넌트 작성 규칙

### 새 컴포넌트 추가 절차
1. `design-system/components/{name}.scss` 생성
2. 파일 상단에 `@use "../tokens" as *;` 추가
3. `design-system/components/_index.scss`에 `@forward "{name}";` 추가
4. `scss/main.scss`에 `@use "../design-system/components/{name}";` 추가
5. `scss/quarto-theme.scss`의 `/*-- scss:rules --*/`에 규칙 복사

### 컴포넌트 파일 구조
```scss
@use "sass:color";          // 필요시
@use "../tokens" as *;      // 토큰 접근

.component-name {
  // 토큰 변수만 사용, 하드코딩 금지
  font-size: $font-size-base;     // O
  font-size: 16px;                // X
  color: $color-text-primary;     // O
  color: #171717;                 // X
}
```

## 빌드 동기화

`main.scss`와 `quarto-theme.scss`는 동일한 스타일을 다른 문법으로 표현:

| 변경 대상 | main.scss | quarto-theme.scss |
|-----------|-----------|-------------------|
| 토큰 추가 | tokens/ 파일 수정 → 자동 반영 | defaults 섹션에 수동 추가 |
| 컴포넌트 추가 | components/ + @use | rules 섹션에 수동 복사 |
| mixin 변경 | _mixins.scss 수정 | rules에 mixin 결과를 풀어서 작성 |

**중요**: 토큰이나 컴포넌트 변경 시 `quarto-theme.scss` 동기화를 잊지 말 것.

## 금지 패턴

- 하드코딩된 색상/폰트/간격 값 사용
- `@import`로 토큰 불러오기 (→ `@use`/`@forward`)
- 컴포넌트에서 다른 컴포넌트 직접 참조
- `!important` 사용 (Quarto 오버라이드 제외)
