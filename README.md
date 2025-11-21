# 레거시 브라우저 지원 가이드 (Android 6, iOS 7)

## 개요

이 문서는 Android 6 (Marshmallow, API 23) 및 iOS 7을 지원하기 위한 CSS 호환성 가이드입니다.

### 지원 대상

#### Android 6 (Marshmallow, API 23) - 2015년 출시

- Samsung Galaxy S6, S6 Edge, S7, S7 Edge
- LG G4, G5, V10
- HTC One M9, M9+
- Sony Xperia Z5, Z5 Premium
- Motorola Moto X Pure, Moto G (3rd gen)
- 기타 2015-2016년 Android 6.0 기기

#### iOS 7 - 2013년 출시

- iPhone 4, 4S, 5, 5C, 5S
- iPad 2, 3, 4, Mini (1st gen)
- iPod Touch 5세대

---

## 지원되지 않는 CSS 속성 및 기능 요약표

### 🔴 Critical (즉시 수정 필요)

| CSS 속성/기능           | Android 6 | iOS 7     | 대체 방법                       | 현재 프로젝트 사용 여부 |
| ----------------------- | --------- | --------- | ------------------------------- | ----------------------- |
| `var(--variable-name)`  | ❌ 미지원 | ❌ 미지원 | SCSS 변수 또는 직접 값 사용     | ✅ 광범위하게 사용      |
| `gap` (Flexbox/Grid)    | ❌ 미지원 | ❌ 미지원 | `margin` 사용                   | ✅ 사용 중              |
| `:has()` 선택자         | ❌ 미지원 | ❌ 미지원 | JavaScript 또는 클래스 추가     | ✅ 사용 중              |
| `padding-inline`        | ❌ 미지원 | ❌ 미지원 | `padding-left`, `padding-right` | ✅ 사용 중              |
| `padding-block`         | ❌ 미지원 | ❌ 미지원 | `padding-top`, `padding-bottom` | ❓ 확인 필요            |
| `margin-inline`         | ❌ 미지원 | ❌ 미지원 | `margin-left`, `margin-right`   | ❓ 확인 필요            |
| `margin-block`          | ❌ 미지원 | ❌ 미지원 | `margin-top`, `margin-bottom`   | ❓ 확인 필요            |
| `calc()` + `var()` 조합 | ❌ 미지원 | ❌ 미지원 | 직접 계산된 값 사용             | ✅ 사용 중              |

### 🟡 Important (중요)

| CSS 속성/기능                   | Android 6    | iOS 7        | 대체 방법                                         | 현재 프로젝트 사용 여부 |
| ------------------------------- | ------------ | ------------ | ------------------------------------------------- | ----------------------- |
| `display: grid`                 | ❌ 미지원    | ❌ 미지원    | Flexbox 또는 float 사용                           | ❓ 확인 필요            |
| `object-fit`                    | ❌ 미지원    | ❌ 미지원    | `background-image` + `background-size`            | ✅ 사용 중              |
| `env()` 함수                    | ❌ 미지원    | ❌ 미지원    | JavaScript 또는 고정값                            | ✅ 사용 중              |
| `position: sticky`              | ✅ 지원      | ⚠️ 부분 지원 | `-webkit-sticky` prefix 추가                      | ✅ 사용 중              |
| `display: flex` (prefix 없음)   | ⚠️ 부분 지원 | ⚠️ 부분 지원 | `-webkit-box`, `-webkit-flex` 추가                | ✅ 사용 중              |
| `justify-content` (prefix 없음) | ⚠️ 부분 지원 | ⚠️ 부분 지원 | `-webkit-box-pack`, `-webkit-justify-content`     | ✅ 사용 중              |
| `align-items` (prefix 없음)     | ⚠️ 부분 지원 | ⚠️ 부분 지원 | `-webkit-box-align`, `-webkit-align-items`        | ✅ 사용 중              |
| `flex-wrap` (prefix 없음)       | ⚠️ 부분 지원 | ⚠️ 부분 지원 | `-webkit-flex-wrap` 추가                          | ✅ 사용 중              |
| `flex-direction` (prefix 없음)  | ⚠️ 부분 지원 | ⚠️ 부분 지원 | `-webkit-box-direction`, `-webkit-flex-direction` | ✅ 사용 중              |
| `transform` (prefix 없음)       | ⚠️ 부분 지원 | ⚠️ 부분 지원 | `-webkit-transform` 추가                          | ✅ 사용 중              |
| `transition` (prefix 없음)      | ⚠️ 부분 지원 | ⚠️ 부분 지원 | `-webkit-transition` 추가                         | ✅ 사용 중              |
| `border-inline`                 | ❌ 미지원    | ❌ 미지원    | `border-left`, `border-right`                     | ❓ 확인 필요            |
| `inset-inline`                  | ❌ 미지원    | ❌ 미지원    | `left`, `right`                                   | ❓ 확인 필요            |

### 🟢 Nice to have (선택적)

| CSS 속성/기능               | Android 6    | iOS 7        | 대체 방법                      | 현재 프로젝트 사용 여부 |
| --------------------------- | ------------ | ------------ | ------------------------------ | ----------------------- |
| `:is()` 선택자              | ❌ 미지원    | ❌ 미지원    | 개별 선택자 나열               | ❓ 확인 필요            |
| `:where()` 선택자           | ❌ 미지원    | ❌ 미지원    | 개별 선택자 나열               | ❓ 확인 필요            |
| `object-position`           | ❌ 미지원    | ❌ 미지원    | `background-position`          | ❓ 확인 필요            |
| `line-clamp` (표준)         | ❌ 미지원    | ❌ 미지원    | `-webkit-line-clamp` 사용      | ✅ 이미 사용 중         |
| `calc()` (단순)             | ⚠️ 부분 지원 | ⚠️ 부분 지원 | 직접 계산된 값 사용            | ✅ 사용 중              |
| `animation` (prefix 없음)   | ⚠️ 부분 지원 | ⚠️ 부분 지원 | `-webkit-animation` 추가       | ❓ 확인 필요            |
| `@keyframes` (prefix 없음)  | ⚠️ 부분 지원 | ⚠️ 부분 지원 | `@-webkit-keyframes` 추가      | ❓ 확인 필요            |
| `backdrop-filter`           | ❌ 미지원    | ❌ 미지원    | 반투명 배경 사용               | ❓ 확인 필요            |
| `filter: blur()`            | ⚠️ 부분 지원 | ⚠️ 부분 지원 | `-webkit-filter` 추가          | ❓ 확인 필요            |
| `filter: grayscale()`       | ⚠️ 부분 지원 | ⚠️ 부분 지원 | `-webkit-filter` 추가          | ❓ 확인 필요            |
| `will-change`               | ❌ 미지원    | ❌ 미지원    | 제거 (기능 영향 없음)          | ❓ 확인 필요            |
| `contain`                   | ❌ 미지원    | ❌ 미지원    | 제거 (성능 최적화용)           | ❓ 확인 필요            |
| `appearance`                | ⚠️ 부분 지원 | ⚠️ 부분 지원 | `-webkit-appearance` 추가      | ❓ 확인 필요            |
| `user-select`               | ⚠️ 부분 지원 | ⚠️ 부분 지원 | `-webkit-user-select` 추가     | ❓ 확인 필요            |
| `touch-action`              | ❌ 미지원    | ⚠️ 부분 지원 | JavaScript로 처리              | ❓ 확인 필요            |
| `scroll-behavior`           | ❌ 미지원    | ❌ 미지원    | JavaScript로 처리              | ❓ 확인 필요            |
| `overscroll-behavior`       | ❌ 미지원    | ❌ 미지원    | JavaScript로 처리              | ❓ 확인 필요            |
| `clip-path`                 | ❌ 미지원    | ⚠️ 부분 지원 | `-webkit-clip-path` 추가       | ❓ 확인 필요            |
| `mask`                      | ⚠️ 부분 지원 | ⚠️ 부분 지원 | `-webkit-mask` 추가            | ❓ 확인 필요            |
| `shape-outside`             | ❌ 미지원    | ❌ 미지원    | float 사용                     | ❓ 확인 필요            |
| `columns` (Multi-column)    | ⚠️ 부분 지원 | ⚠️ 부분 지원 | `-webkit-columns` 추가         | ❓ 확인 필요            |
| `writing-mode`              | ⚠️ 부분 지원 | ⚠️ 부분 지원 | `-webkit-writing-mode` 추가    | ❓ 확인 필요            |
| `text-decoration` (신규 값) | ⚠️ 부분 지원 | ⚠️ 부분 지원 | 기본 값 사용                   | ❓ 확인 필요            |
| `@supports`                 | ❌ 미지원    | ❌ 미지원    | JavaScript로 feature detection | ❓ 확인 필요            |

### ✅ 지원되는 CSS 속성 (사용 가능)

| CSS 속성/기능             | Android 6 | iOS 7   | 비고 |
| ------------------------- | --------- | ------- | ---- |
| `text-shadow` (복수)      | ✅ 지원   | ✅ 지원 | -    |
| `box-shadow` (복수)       | ✅ 지원   | ✅ 지원 | -    |
| `border-radius`           | ✅ 지원   | ✅ 지원 | -    |
| `opacity`                 | ✅ 지원   | ✅ 지원 | -    |
| `rgba()`                  | ✅ 지원   | ✅ 지원 | -    |
| `@media` queries          | ✅ 지원   | ✅ 지원 | -    |
| `float`                   | ✅ 지원   | ✅ 지원 | -    |
| `clear`                   | ✅ 지원   | ✅ 지원 | -    |
| `z-index`                 | ✅ 지원   | ✅ 지원 | -    |
| `overflow`                | ✅ 지원   | ✅ 지원 | -    |
| `text-align`              | ✅ 지원   | ✅ 지원 | -    |
| `font-family`             | ✅ 지원   | ✅ 지원 | -    |
| `font-size`               | ✅ 지원   | ✅ 지원 | -    |
| `font-weight`             | ✅ 지원   | ✅ 지원 | -    |
| `line-height`             | ✅ 지원   | ✅ 지원 | -    |
| `color`                   | ✅ 지원   | ✅ 지원 | -    |
| `background-color`        | ✅ 지원   | ✅ 지원 | -    |
| `background-image`        | ✅ 지원   | ✅ 지원 | -    |
| `background-size`         | ✅ 지원   | ✅ 지원 | -    |
| `background-position`     | ✅ 지원   | ✅ 지원 | -    |
| `background-repeat`       | ✅ 지원   | ✅ 지원 | -    |
| `border`                  | ✅ 지원   | ✅ 지원 | -    |
| `margin`                  | ✅ 지원   | ✅ 지원 | -    |
| `padding`                 | ✅ 지원   | ✅ 지원 | -    |
| `width`, `height`         | ✅ 지원   | ✅ 지원 | -    |
| `max-width`, `max-height` | ✅ 지원   | ✅ 지원 | -    |
| `min-width`, `min-height` | ✅ 지원   | ✅ 지원 | -    |
| `display: block`          | ✅ 지원   | ✅ 지원 | -    |
| `display: inline`         | ✅ 지원   | ✅ 지원 | -    |
| `display: inline-block`   | ✅ 지원   | ✅ 지원 | -    |
| `display: table`          | ✅ 지원   | ✅ 지원 | -    |
| `position: static`        | ✅ 지원   | ✅ 지원 | -    |
| `position: relative`      | ✅ 지원   | ✅ 지원 | -    |
| `position: absolute`      | ✅ 지원   | ✅ 지원 | -    |
| `position: fixed`         | ✅ 지원   | ✅ 지원 | -    |

**범례:**

- ❌ 미지원: 완전히 지원되지 않음
- ⚠️ 부분 지원: prefix 필요하거나 제한적 지원
- ✅ 지원: 완전히 지원됨
- 🔴 Critical: 즉시 수정 필요
- 🟡 Important: 중요하지만 긴급하지 않음
- 🟢 Nice to have: 선택적 개선 사항

**범례:**

- ❌ 미지원: 완전히 지원되지 않음
- ⚠️ 부분 지원: prefix 필요하거나 제한적 지원
- ✅ 지원: 완전히 지원됨
- 🔴 Critical: 즉시 수정 필요
- 🟡 Important: 중요하지만 긴급하지 않음
- 🟢 Nice to have: 선택적 개선 사항

---

## 지원되지 않는 CSS 속성 및 기능

### 1. CSS Custom Properties (CSS Variables) ❌

**문제:**

```scss
// ❌ 지원 안됨
.element {
  padding: var(--spacing-lg);
  color: var(--text-primary);
  background: var(--bg-canvas_white);
}
```

**해결 방법:**

```scss
// ✅ 대체 방법
.element {
  padding: 12px; // 직접 값 사용
  color: #1a1a1a;
  background: #ffffff;
}

// 또는 SCSS 변수 사용
$spacing-lg: 12px;
$text-primary: #1a1a1a;
.element {
  padding: $spacing-lg;
  color: $text-primary;
}
```

**현재 프로젝트 사용 현황:**

- `var(--spacing-*)` - 모든 spacing 토큰
- `var(--text-*)` - 모든 텍스트 색상
- `var(--bg-*)` - 모든 배경 색상
- `var(--border-*)` - 모든 border 색상
- `var(--radius-*)` - border-radius 값
- `var(--font-size-*)` - 폰트 크기

---

### 2. CSS Grid ❌

**문제:**

```scss
// ❌ 지원 안됨
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}
```

**해결 방법:**

```scss
// ✅ Flexbox 사용 (부분 지원)
.container {
  display: -webkit-box; // iOS 7
  display: -webkit-flex; // iOS 7
  display: flex;
  -webkit-flex-wrap: wrap;
  flex-wrap: wrap;
}

.item {
  -webkit-box-flex: 1;
  -webkit-flex: 1;
  flex: 1;
  margin: 8px; // gap 대신 margin 사용
}
```

---

### 3. Flexbox Gap 속성 ❌

**문제:**

```scss
// ❌ 지원 안됨
.flex-container {
  display: flex;
  gap: var(--spacing-lg);
}
```

**해결 방법:**

```scss
// ✅ margin 사용
.flex-container {
  display: -webkit-box; // iOS 7
  display: -webkit-flex;
  display: flex;

  > * + * {
    margin-left: 12px; // gap 대신
  }
}

// 또는 flex-direction: column인 경우
.flex-container--column {
  > * + * {
    margin-top: 12px;
  }
}
```

**현재 프로젝트 사용 현황:**

- `.sortable-card__list` - `gap: var(--spacing-lg)`
- `.sv-select-box-group`, `.sv-card` - `gap: var(--spacing-lg)`
- `.password-bottomsheet__field .sv-cell-input` - `gap: var(--spacing-2xl)`

---

### 4. `:has()` 선택자 ❌

**문제:**

```scss
// ❌ 지원 안됨
.container:has(.child) {
  padding: 20px;
}

.sv-popup__body:has(.sortable-card__section) {
  padding-inline: 0;
}
```

**해결 방법:**

```scss
// ✅ 클래스 추가 또는 JavaScript 사용
.container.has-child {
  padding: 20px;
}

// 또는 인접 선택자 활용
.child {
  .container {
    padding: 20px;
  }
}
```

**현재 프로젝트 사용 현황:**

- `.sc-container:has(.sv-bottom-action-container)`
- `.sc-container:has(> .sc-contents__body > .sc-tabs__group > .sv-tabs)`
- `.sc-container:has(.sc-body__title ~ .sc-contents__body > .sc-tabs__group)`
- `.sc-container:has(.sv-linear-progress-step)`
- `.sc-container:has(.sv-tabs.sv-tabs--type-segment)`
- `.sv-popup__body:has(.sortable-card__section)`

---

### 5. CSS Logical Properties ❌

**문제:**

```scss
// ❌ 지원 안됨
.element {
  padding-inline: var(--spacing-2xl);
  margin-inline: auto;
  border-inline: 1px solid #ccc;
}
```

**해결 방법:**

```scss
// ✅ 물리적 속성 사용
.element {
  padding-left: 20px;
  padding-right: 20px;
  margin-left: auto;
  margin-right: auto;
  border-left: 1px solid #ccc;
  border-right: 1px solid #ccc;
}
```

**현재 프로젝트 사용 현황:**

- `.sv-popup__body:has(.sortable-card__section)` - `padding-inline: 0`
- `.sc-container:has(.sv-tabs.sv-tabs--type-segment)` - `padding-inline: var(--spacing-2xl)`

---

### 6. `object-fit` 속성 ❌

**문제:**

```scss
// ❌ 지원 안됨
img {
  object-fit: contain;
  object-fit: cover;
}
```

**해결 방법:**

```scss
// ✅ background-image 사용
.image-container {
  width: 100%;
  height: 100%;
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;
}

// 또는 JavaScript로 처리
```

**현재 프로젝트 사용 현황:**

- `.card-list__body .sv-list__icon img` - `object-fit: contain`
- `.loading-lottie img` - 주석 처리됨 (`// object-fit: contain;`)

---

### 7. `line-clamp` (표준 속성) ⚠️

**문제:**

```scss
// ⚠️ 표준 line-clamp는 지원 안됨
.text {
  line-clamp: 2;
}
```

**해결 방법:**

```scss
// ✅ -webkit-line-clamp 사용 (이미 사용 중)
.text {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

**현재 프로젝트 사용 현황:**

- `.sortable-card__list .sv-list__text__main` - 이미 `-webkit-line-clamp` 사용 중 ✅

---

### 8. `position: sticky` ⚠️

**문제:**

```scss
// ⚠️ iOS 7에서 부분 지원, Android 6에서 지원
.sticky-element {
  position: sticky;
  top: 0;
}
```

**해결 방법:**

```scss
// ✅ JavaScript로 폴백 구현 또는 position: fixed 사용
.sticky-element {
  position: -webkit-sticky; // iOS 7
  position: sticky;
  top: 0;
}
```

**현재 프로젝트 사용 현황:**

- `.sc-container:has(.sv-linear-progress-step) .sv-linear-progress-step` - `position: sticky`
- `.sc-header__title` - `position: sticky`
- `.sc-header__title--sticky` - `position: sticky`

---

### 9. `calc()` 함수 ⚠️

**문제:**

```scss
// ⚠️ iOS 7에서 부분 지원, 복잡한 calc()는 문제 발생 가능
.element {
  width: calc(100% - 20px);
  margin-top: calc(var(--spacing-4xl) - var(--spacing-xl)); // var()와 함께 사용 불가
}
```

**해결 방법:**

```scss
// ✅ 직접 계산된 값 사용
.element {
  width: calc(100% - 20px); // 단순 calc는 가능
  margin-top: 20px; // 32px - 12px = 20px
}
```

**현재 프로젝트 사용 현황:**

- `calc(var(--spacing-4xl) + env(safe-area-inset-bottom))` - var()와 함께 사용 ❌
- `calc(var(--spacing-4xl) - var(--spacing-xl))` - var()와 함께 사용 ❌
- `calc(var(--spacing-xl) * -1)` - var()와 함께 사용 ❌

---

### 10. `env()` 함수 ❌

**문제:**

```scss
// ❌ 지원 안됨
.element {
  padding-bottom: env(safe-area-inset-bottom);
  padding-top: calc(var(--spacing-4xl) + env(safe-area-inset-bottom));
}
```

**해결 방법:**

```scss
// ✅ JavaScript로 safe-area 계산 또는 고정값 사용
.element {
  padding-bottom: 0; // 기본값
}

// JavaScript로 처리
// const safeAreaBottom = window.safeAreaInsets?.bottom || 0;
```

---

### 11. Flexbox (부분 지원) ⚠️

**문제:**

```scss
// ⚠️ 구버전 prefix 필요
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

**해결 방법:**

```scss
// ✅ 구버전 prefix 추가
.container {
  display: -webkit-box; // iOS 7 (구버전 flexbox)
  display: -webkit-flex; // iOS 7 (신버전 flexbox)
  display: flex;

  -webkit-box-pack: center; // justify-content (구버전)
  -webkit-justify-content: center; // justify-content (신버전)
  justify-content: center;

  -webkit-box-align: center; // align-items (구버전)
  -webkit-align-items: center; // align-items (신버전)
  align-items: center;
}
```

**현재 프로젝트 사용 현황:**

- 대부분의 flexbox 사용에 prefix 누락 가능성

---

### 12. `backdrop-filter` ❌

**문제:**

```scss
// ❌ 지원 안됨
.modal-backdrop {
  backdrop-filter: blur(10px);
}
```

**해결 방법:**

```scss
// ✅ 반투명 배경 사용
.modal-backdrop {
  background: rgba(0, 0, 0, 0.5);
  // blur 효과는 불가능
}
```

---

### 13. `will-change` ❌

**문제:**

```scss
// ❌ 지원 안됨
.animated {
  will-change: transform;
}
```

**해결 방법:**

```scss
// ✅ 제거 (성능 최적화는 불가능하지만 기능에는 영향 없음)
.animated {
  // will-change 제거
}
```

---

### 14. `transform` 속성 (부분 지원) ⚠️

**문제:**

```scss
// ⚠️ 일부 transform 함수는 지원 안됨
.element {
  transform: translate3d(0, 0, 0);
  transform: scale(1.2);
}
```

**해결 방법:**

```scss
// ✅ -webkit-transform prefix 사용
.element {
  -webkit-transform: translate3d(0, 0, 0);
  transform: translate3d(0, 0, 0);
}
```

---

### 15. `transition` 속성 (부분 지원) ⚠️

**문제:**

```scss
// ⚠️ 일부 속성은 transition 불가
.element {
  transition: all 0.3s ease;
}
```

**해결 방법:**

```scss
// ✅ -webkit-transition prefix 사용
.element {
  -webkit-transition: all 0.3s ease;
  transition: all 0.3s ease;
}
```

---

## 우선순위별 대응 가이드

### 🔴 Critical (즉시 수정 필요)

1. **CSS Variables (var())** - 가장 광범위하게 사용됨
2. **`:has()` 선택자** - 여러 곳에서 사용
3. **`gap` 속성** - Flexbox 레이아웃에 사용
4. **CSS Logical Properties** - `padding-inline` 등

### 🟡 Important (중요)

5. **`object-fit`** - 이미지 표시에 영향
6. **`calc()` + `var()` 조합** - 레이아웃 계산
7. **`env()` 함수** - Safe area 처리

### 🟢 Nice to have (선택적)

8. **Flexbox prefix** - 대부분 동작하지만 prefix 추가 권장
9. **`position: sticky`** - 폴백 구현 고려
10. **`line-clamp`** - 이미 `-webkit-` prefix 사용 중

---

## 자동화 도구 제안

### PostCSS 플러그인

```json
{
  "postcss-custom-properties": {
    "preserve": false
  },
  "postcss-logical": {
    "dir": "ltr"
  },
  "autoprefixer": {
    "overrideBrowserslist": ["iOS 7", "Android 6"]
  }
}
```

### SCSS Mixin 예시

```scss
// CSS Variables 폴백 mixin
@mixin legacy-var($property, $var-name, $fallback) {
  #{$property}: #{$fallback};
  #{$property}: var(#{$var-name});
}

// 사용 예시
.element {
  @include legacy-var(padding, --spacing-lg, 12px);
}

// Gap 폴백 mixin
@mixin legacy-gap($gap-value, $direction: row) {
  @if $direction == row {
    > * + * {
      margin-left: #{$gap-value};
    }
  } @else {
    > * + * {
      margin-top: #{$gap-value};
    }
  }
}
```

---

## 테스트 체크리스트

- [ ] CSS Variables가 모든 브라우저에서 동작하는지 확인
- [ ] Flexbox 레이아웃이 올바르게 표시되는지 확인
- [ ] `:has()` 선택자 사용 부분 JavaScript로 대체
- [ ] `gap` 속성 사용 부분 `margin`으로 대체
- [ ] `object-fit` 사용 부분 `background-image`로 대체
- [ ] `padding-inline`, `margin-inline` 등 Logical Properties 수정
- [ ] `calc()` + `var()` 조합 수정
- [ ] `env()` 함수 사용 부분 JavaScript로 대체
- [ ] 실제 디바이스에서 테스트 (Android 6, iOS 7)

---

## 참고 자료

- [Can I Use - Android Browser](https://caniuse.com/?compare=android+6)
- [Can I Use - iOS Safari 7](https://caniuse.com/?compare=ios_saf+7)
- [MDN Web Docs - CSS Custom Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)
- [MDN Web Docs - :has() selector](https://developer.mozilla.org/en-US/docs/Web/CSS/:has)

---
