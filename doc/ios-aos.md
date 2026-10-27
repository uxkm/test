# iOS 15 및 Android 7 지원 가이드
## 완전한 호환성 검토 및 대응 방안

검토 일자: 2025.11.20  
대상 브라우저:
- iOS 15 (Safari 15)
- Android 7 (Chrome 51-59)

검토 범위: `resources/assets/styles/**/*.scss`

---

## 📋 목차

1. [적용된 설정](#1-적용된-설정)
2. [속성별 호환성 비교표](#2-속성별-호환성-비교표)
3. [주요 CSS 속성 상세 분석](#3-주요-css-속성-상세-분석)
4. [파일별 검토 결과](#4-파일별-검토-결과)
5. [대응 방안](#5-대응-방안)
6. [체크리스트](#6-체크리스트)
7. [참고 자료](#7-참고-자료)

---

## 1. 적용된 설정

### 1.1 Browserslist 설정
`package.json`에 다음 browserslist 설정이 추가되었습니다:
```json
"browserslist": [
  "iOS >= 15",
  "Android >= 7",
  "Chrome >= 51",
  "Safari >= 15"
]
```

### 1.2 Vite 빌드 타겟
`vite.config.ts`에서 `build.target`을 `es2017`로 설정하여 iOS 15와 Android 7에서 안정적으로 동작하도록 했습니다.

### 1.3 Autoprefixer 설정
CSS vendor prefix를 자동으로 추가하도록 autoprefixer를 설정했습니다:
- Flexbox: `no-2009` (구버전 호환)
- Grid: `autoplace` (CSS Grid 자동 배치 지원)

```javascript
autoprefixer({
  overrideBrowserslist: [
    "iOS >= 15",
    "Android >= 7",
    "Chrome >= 51",
    "Safari >= 15"
  ],
  flexbox: "no-2009",
  grid: "autoplace",
})
```

---

## 2. 속성별 호환성 비교표

| 속성/기능 | iOS 15 | Android 7 | 프로젝트 사용 | 비고 |
|----------|--------|-----------|--------------|------|
| **`:has()` 선택자** | ⚠️ 15.4+ | ❌ 미지원 | ✅ 81개 | iOS 15.0-15.3 미지원 |
| **`:not()` 선택자** | ✅ 지원 | ✅ 지원 | ✅ 69개 | 완전 지원 |
| **Flexbox 전체** | ✅ 지원 | ✅ 지원 | ✅ 1,210개 | 완전 지원 |
| **CSS Grid** | ✅ 지원 | ⚠️ 부분 | ✅ 102개 | Android 7 부분 지원 |
| **`gap` 속성** | ✅ 지원 | ⚠️ 부분 | ✅ 243개 | Grid/Flexbox gap |
| **`filter`** | ✅ 지원 | ✅ 지원 | ✅ 45개 | 완전 지원 |
| **`backdrop-filter`** | ✅ 지원 | ⚠️ 부분 | ✅ 여러 개 | Android 7 부분 지원 |
| **`aspect-ratio`** | ✅ 지원 | ✅ 지원 | ✅ 여러 개 | 완전 지원 |
| **`calc()`** | ✅ 지원 | ✅ 지원 | ✅ 많이 사용 | 완전 지원 |
| **`max()`, `min()`, `clamp()`** | ⚠️ 15.4+ | ❌ 미지원 | ✅ 3개 | iOS 15.0-15.3 미지원 |
| **`dvh`, `dvw`** | ⚠️ 15.4+ | ❌ 미지원 | ✅ 2개 | iOS 15.0-15.3 미지원 |
| **`env(safe-area-inset-*)`** | ✅ 지원 | ⚠️ 부분 | ✅ 14개 | Android 9+ |

---

## 3. 주요 CSS 속성 상세 분석

### 3.1 `:has()` 선택자

#### 지원 현황
- **iOS 15.0-15.3**: ❌ 미지원
- **iOS 15.4+**: ✅ 지원
- **Android 7 (Chrome 51-59)**: ❌ 미지원
- **Chrome 105+**: ✅ 지원

#### 프로젝트 사용 현황
**총 81개 사용**

주요 사용 파일:
- `layouts/_layout.scss`: 8개
- `module/_agree-list.scss`: 18개
- `pay/_auth.scss`: 6개
- `pay/_benefits.scss`: 7개
- `pay/_my-junior.scss`: 3개
- `module/_keypad.scss`: 3개
- `discover/pages/_discoverNew_comp.scss`: 4개
- 기타 여러 파일

#### 사용 예시
```scss
// layouts/_layout.scss
&:not(:has(.sv-bottom-action-container)) { ... }
.sc-container:has(.sv-bottom-action-container) { ... }
.sc-container:has(> .sc-contents__body > .sc-tabs__group > .sv-tabs) { ... }

// module/_agree-list.scss
&:has(.sc-agree__head-description) { ... }
&:has(.agree-content) { ... }
```

#### 대응 방법
1. **iOS 15.4+만 지원** (권장): 현재 코드 유지
2. **iOS 15.0-15.3도 지원**: JavaScript로 대체 또는 `@supports` 사용
   ```scss
   // :has() 지원 시
   @supports selector(:has(*)) {
     .sc-container:has(.sv-bottom-action-container) {
       overscroll-behavior: contain;
     }
   }
   
   // :has() 미지원 시 (JavaScript로 클래스 추가)
   .sc-container.has-bottom-action-container {
     overscroll-behavior: contain;
   }
   ```

---

### 3.2 `:not()` 선택자

#### 지원 현황
- **iOS 15**: ✅ 완전 지원
- **Android 7 (Chrome 51-59)**: ✅ 완전 지원

#### 프로젝트 사용 현황
**총 69개 사용**

#### 사용 예시
```scss
// layouts/_layout.scss
&:not(:has(.sv-bottom-action-container)) { ... }

// pay/_auth.scss
&:not(:has(.sv-tabs--type-segment)) { ... }

// abstracts/_mixins.scss
&:active:not(:disabled) { ... }
```

#### 대응 방법
✅ **추가 작업 불필요** - 모든 대상 브라우저에서 완전 지원

---

### 3.3 Flexbox 관련 속성

#### 지원 현황
- **iOS 15**: ✅ 완전 지원
- **Android 7 (Chrome 51-59)**: ✅ 완전 지원

#### 프로젝트 사용 현황
**총 1,210개 이상 사용**

#### 주요 사용 속성

##### `flex` 단축 속성
```scss
flex: 0 0 auto;      // ✅ 지원
flex: 1 1 auto;      // ✅ 지원
flex: 1;             // ✅ 지원
flex: 0 0 80.16%;    // ✅ 지원
```

##### `flex-direction`
```scss
flex-direction: column;  // ✅ 지원
flex-direction: row;     // ✅ 지원
```

##### `flex-wrap`
```scss
flex-wrap: wrap;      // ✅ 지원
flex-wrap: nowrap;    // ✅ 지원
```

##### `justify-content`
```scss
justify-content: center;           // ✅ 지원
justify-content: space-between;    // ✅ 지원
justify-content: flex-start;       // ✅ 지원
justify-content: flex-end;         // ✅ 지원
```

##### `align-items`
```scss
align-items: center;      // ✅ 지원
align-items: flex-start;  // ✅ 지원
align-items: flex-end;    // ✅ 지원
```

##### `align-self`
```scss
align-self: center;      // ✅ 지원
align-self: flex-start;  // ✅ 지원
align-self: flex-end;    // ✅ 지원
align-self: stretch;     // ✅ 지원
```

##### `align-content`
```scss
align-content: center;           // ✅ 지원
align-content: space-between;    // ✅ 지원
```

##### 개별 속성
```scss
flex-grow: 0;     // ✅ 지원
flex-shrink: 0;   // ✅ 지원
flex-basis: auto; // ✅ 지원
```

#### 대응 방법
✅ **추가 작업 불필요** - 모든 대상 브라우저에서 완전 지원

---

### 3.4 CSS Grid 관련 속성

#### 지원 현황
- **iOS 15**: ✅ 완전 지원
- **Android 7 (Chrome 51-59)**: ⚠️ 부분 지원
  - Chrome 51-56: Grid 미지원
  - Chrome 57+: Grid 지원 (autoprefixer로 대응 가능)

#### 프로젝트 사용 현황
**총 102개 사용**

#### 주요 사용 속성

##### 기본 Grid
```scss
display: grid;  // ⚠️ Android 7 Chrome 51-56 미지원
```

##### `grid-template-columns`
```scss
grid-template-columns: 1fr 1fr;                    // ⚠️ 부분 지원
grid-template-columns: repeat(2, minmax(0, 1fr));  // ⚠️ 부분 지원
grid-template-columns: repeat(3, 1fr);             // ⚠️ 부분 지원
grid-template-columns: auto 1fr;                   // ⚠️ 부분 지원
grid-template-columns: none;                       // ⚠️ 부분 지원
```

##### `grid-template-rows`
```scss
grid-template-rows: 1fr 1fr;                    // ⚠️ 부분 지원
grid-template-rows: repeat(4, 1fr);             // ⚠️ 부분 지원
```

##### `grid-column` / `grid-row`
```scss
grid-column: 1 / -1;      // ⚠️ 부분 지원
grid-column: span 1;      // ⚠️ 부분 지원
grid-row: 1;              // ⚠️ 부분 지원
```

##### `grid-auto-flow`
```scss
grid-auto-flow: column;   // ⚠️ 부분 지원
```

##### `place-items` / `place-content`
```scss
place-items: center;      // ⚠️ 부분 지원 (Chrome 59+)
place-content: center;    // ⚠️ 부분 지원 (Chrome 59+)
```

#### 대응 방법
1. **Autoprefixer 설정** (이미 적용됨)
   ```javascript
   autoprefixer({
     grid: "autoplace", // CSS Grid 자동 배치 지원
   })
   ```

2. **Fallback 제공** (필요 시)
   ```scss
   // Grid 미지원 시 Flexbox로 대체
   .grid-container {
     display: flex;
     flex-wrap: wrap;
     
     @supports (display: grid) {
       display: grid;
       grid-template-columns: repeat(2, 1fr);
     }
   }
   ```

---

### 3.5 `gap` 속성

#### 지원 현황
- **iOS 15**: ✅ 완전 지원
- **Android 7 (Chrome 51-59)**: ⚠️ 부분 지원
  - Flexbox `gap`: Chrome 84+ (Android 7 미지원)
  - Grid `gap`: Chrome 57+ (부분 지원)

#### 프로젝트 사용 현황
**총 243개 사용**

#### 사용 예시
```scss
// Flexbox gap
gap: var(--spacing-lg);
gap: var(--spacing-md);
gap: var(--spacing-sm);

// Grid gap
gap: var(--spacing-2xl) var(--spacing-xl);
column-gap: var(--spacing-xl);
row-gap: var(--spacing-lg);
```

#### 대응 방법
1. **Autoprefixer** (이미 적용됨) - Grid gap에 대한 prefix 추가

2. **Flexbox gap fallback** (필요 시)
   ```scss
   .flex-container {
     // gap 미지원 시 margin 사용
     > * + * {
       margin-left: var(--spacing-lg);
     }
     
     @supports (gap: 1px) {
       gap: var(--spacing-lg);
       > * + * {
         margin-left: 0;
       }
     }
   }
   ```

---

### 3.6 `filter` 속성

#### 지원 현황
- **iOS 15**: ✅ 완전 지원
- **Android 7 (Chrome 51-59)**: ✅ 완전 지원

#### 프로젝트 사용 현황
**총 45개 사용**

#### 사용 예시
```scss
// 기본 filter
filter: none;
filter: blur(1px);
filter: brightness(0.7);
filter: contrast(0.8);
filter: grayscale(100%);
filter: drop-shadow(0 4px 8px rgba(12, 17, 29, 0.06));

// 복합 filter
filter: brightness(0.7) contrast(0.8);
filter: brightness(1.2) contrast(1.15) saturate(1.1);
filter: invert(16%) sepia(30%) saturate(7115%) hue-rotate(218deg) brightness(91%) contrast(90%);
```

#### 대응 방법
✅ **추가 작업 불필요** - 모든 대상 브라우저에서 완전 지원

---

### 3.7 `backdrop-filter` 속성

#### 지원 현황
- **iOS 15**: ✅ 완전 지원
- **Android 7 (Chrome 51-59)**: ⚠️ 부분 지원
  - Chrome 76+ 지원
  - Android 7 Chrome 51-59: 미지원

#### 프로젝트 사용 현황
**여러 개 사용**

#### 사용 예시
```scss
backdrop-filter: blur(10px);
backdrop-filter: blur(5px);
backdrop-filter: blur(24px);
backdrop-filter: blur(48px);

// -webkit- prefix 포함
-webkit-backdrop-filter: blur(10px);
```

#### 대응 방법
1. **-webkit- prefix 사용** (이미 적용됨)
   ```scss
   backdrop-filter: blur(10px);
   -webkit-backdrop-filter: blur(10px);
   ```

2. **Fallback 배경색 제공**
   ```scss
   .backdrop-element {
     background-color: rgba(255, 255, 255, 0.8); // fallback
     backdrop-filter: blur(10px);
     -webkit-backdrop-filter: blur(10px);
   }
   ```

---

### 3.8 기타 주요 속성

#### 3.8.1 `aspect-ratio`
- **iOS 15**: ✅ 지원
- **Android 7**: ✅ 지원 (Chrome 88+)
- **프로젝트 사용**: 여러 개

```scss
aspect-ratio: 335/269;
aspect-ratio: 1 / 1;
aspect-ratio: 0.911;
```

#### 3.8.2 `env(safe-area-inset-*)`
- **iOS 15**: ✅ 지원
- **Android 7**: ⚠️ 부분 지원 (Android 9+)
- **프로젝트 사용**: 14개

```scss
padding-left: env(safe-area-inset-left);
padding-right: env(safe-area-inset-right);
padding-bottom: env(safe-area-inset-bottom);
```

#### 3.8.3 `calc()`
- **iOS 15**: ✅ 지원
- **Android 7**: ✅ 지원
- **프로젝트 사용**: 많이 사용

```scss
padding-bottom: calc(var(--spacing-4xl) + env(safe-area-inset-bottom));
```

#### 3.8.4 `max()`, `min()`, `clamp()`
- **iOS 15.4+**: ✅ 지원
- **iOS 15.0-15.3**: ❌ 미지원
- **Android 7**: ❌ 미지원 (Chrome 79+)
- **프로젝트 사용**: 3개 (`max()`)

**사용 위치**:
- `discover/pages/_discoverNew_main.scss` (1개)
- `discover/pages/_discoverNew_comp.scss` (2개)

**사용 예시**:
```scss
// 현재 사용 (iOS 15.4+만 지원)
padding-bottom: max(calc(env(safe-area-inset-bottom) + 2px), var(--spacing-xl));
bottom: max(calc(env(safe-area-inset-bottom) - 18px), 0px);

// Fallback 필요
padding-bottom: calc(env(safe-area-inset-bottom) + 2px);
padding-bottom: max(calc(env(safe-area-inset-bottom) + 2px), var(--spacing-xl));
```

#### 3.8.5 `dvh`, `dvw` (Dynamic Viewport Units)
- **iOS 15.4+**: ✅ 지원
- **iOS 15.0-15.3**: ❌ 미지원
- **Android 7**: ❌ 미지원 (Chrome 108+)
- **프로젝트 사용**: 2개 (`dvh`)

**사용 위치**:
- `layouts/_layout.scss` (2개)

**사용 예시**:
```scss
// 현재 사용 (iOS 15.4+만 지원)
min-height: 100dvh;

// Fallback 필요
min-height: 100vh;  // fallback
min-height: 100dvh; // iOS 15.4+
```

---

## 4. 파일별 검토 결과

### 4.1 주요 레이아웃 파일

#### `layouts/_layout.scss`
- ⚠️ `:has()` 선택자: 8개 사용
- ⚠️ `dvh` 단위: 2개 사용
- ✅ `env(safe-area-inset-*)`: 사용 (iOS 11+ 지원)

#### `base/_utility.scss`
- ⚠️ `:has()` 선택자: 5개 사용
- ✅ `gap` 속성: 많이 사용 (지원됨)
- ✅ CSS Grid: 사용 (autoprefixer로 대응)

### 4.2 모듈 파일

#### `module/_agree-list.scss`
- ⚠️ `:has()` 선택자: 18개 사용 (가장 많이 사용)
- ✅ `gap` 속성: 많이 사용

#### `module/_input-field.scss`
- ✅ CSS Grid: 사용 (autoprefixer로 대응)
- ✅ `gap` 속성: 사용

#### `module/_keypad.scss`
- ⚠️ `:has()` 선택자: 3개 사용
- ✅ CSS Grid: 사용

### 4.3 페이지 파일

#### `pay/_benefits.scss`
- ⚠️ `:has()` 선택자: 7개 사용
- ✅ `aspect-ratio`: 사용
- ✅ `gap` 속성: 많이 사용

#### `pay/_auth.scss`
- ⚠️ `:has()` 선택자: 6개 사용
- ✅ `gap` 속성: 사용
- ✅ `@media (prefers-reduced-motion: reduce)`: 사용 (지원됨)

#### `discover/pages/_discoverNew_comp.scss`
- ⚠️ `:has()` 선택자: 4개 사용
- ⚠️ `max()` 함수: 2개 사용
- ✅ `backdrop-filter`: 사용
- ✅ `aspect-ratio`: 사용

#### `discover/pages/_discoverNew_main.scss`
- ⚠️ `max()` 함수: 1개 사용

---

## 5. 대응 방안

### 5.1 종합 대응 방안

#### ✅ 즉시 사용 가능 (추가 작업 불필요)
1. `:not()` 선택자
2. Flexbox 전체 속성
3. `filter` 속성
4. `calc()` 함수
5. CSS Custom Properties
6. `aspect-ratio`

#### ⚠️ 주의 필요 (부분 지원)
1. **`:has()` 선택자**
   - iOS 15.4+만 지원
   - Android 7 미지원
   - **대응**: iOS 15.4+ 지원으로 제한 또는 JavaScript 대체

2. **CSS Grid**
   - Android 7 Chrome 51-56 미지원
   - **대응**: Autoprefixer 설정 (이미 적용됨)

3. **`gap` 속성**
   - Flexbox gap: Android 7 미지원
   - Grid gap: Android 7 부분 지원
   - **대응**: Autoprefixer 설정 (이미 적용됨)

4. **`backdrop-filter`**
   - Android 7 Chrome 51-59 미지원
   - **대응**: -webkit- prefix 사용 (이미 적용됨), fallback 배경색 제공

5. **`max()`, `min()`, `clamp()`**
   - iOS 15.0-15.3 미지원
   - Android 7 미지원
   - **대응**: Fallback 값 제공

6. **`dvh`, `dvw`**
   - iOS 15.0-15.3 미지원
   - Android 7 미지원
   - **대응**: `vh`, `vw` fallback 제공

---

### 5.2 권장 대응 방안

#### 옵션 1: iOS 15.4+ 지원 (권장)
**장점**:
- 현재 코드 유지 가능
- 추가 작업 불필요
- 최신 기능 활용 가능

**단점**:
- iOS 15.0-15.3 사용자는 일부 기능 미지원

**적용 방법**:
- 현재 설정 유지
- 사용자에게 iOS 15.4+ 권장 안내

---

#### 옵션 2: iOS 15.0+ 완전 지원
**필요 작업**:

1. **`dvh` 단위 fallback 추가** (2개 위치):
   ```scss
   // layouts/_layout.scss
   .error-boundary-wrap {
     min-height: 100vh;  // fallback
     min-height: 100dvh; // iOS 15.4+
     
     &:not(:has(.sv-bottom-action-container)) {
       min-height: 100vh;  // fallback
       min-height: 100dvh; // iOS 15.4+
     }
   }
   ```

2. **`max()` 함수 fallback 추가** (3개 위치):
   ```scss
   // discover/pages/_discoverNew_main.scss
   padding-bottom: calc(env(safe-area-inset-bottom) + 02px);
   padding-bottom: max(calc(env(safe-area-inset-bottom) + 02px), var(--spacing-2xl));
   
   // discover/pages/_discoverNew_comp.scss
   bottom: calc(env(safe-area-inset-bottom) - 18px);
   bottom: max(calc(env(safe-area-inset-bottom) - 18px), 0px);
   ```

3. **`:has()` 선택자 대체** (81개 위치):
   - JavaScript로 동적 클래스 추가
   - 또는 다른 CSS 선택자로 대체
   - 또는 `@supports selector(:has(*))` 사용하여 조건부 스타일 적용

**예시**:
```scss
// :has() 대체 예시
.sc-container {
  // 기본 스타일
  padding-top: var(--spacing-xl);
  
  // :has() 지원 시
  @supports selector(:has(*)) {
    &:has(.sv-bottom-action-container) {
      overscroll-behavior: contain;
    }
  }
  
  // :has() 미지원 시 (JavaScript로 클래스 추가 필요)
  &.has-bottom-action-container {
    overscroll-behavior: contain;
  }
}
```

---

#### 옵션 3: Android 7 완전 지원
**필요 작업**:
1. CSS Grid → Flexbox fallback (102개)
2. Flexbox `gap` → margin fallback (일부)
3. `backdrop-filter` → 배경색 fallback (여러 개)

---

### 5.3 추가 설정 필요 시

#### PostCSS 플러그인 추가
더 나은 호환성을 위해 다음 플러그인 고려:
- `postcss-preset-env`: 최신 CSS를 구버전 브라우저용으로 변환
- `postcss-normalize`: 브라우저 간 스타일 정규화

#### Polyfill 추가
필요한 경우:
- `core-js`: JavaScript 기능 polyfill
- `regenerator-runtime`: async/await 지원

---

## 6. 체크리스트

### 즉시 적용 가능
- [x] Browserslist 설정 추가
- [x] Vite build.target 설정
- [x] Autoprefixer 설정 강화

### 추가 작업 필요 (iOS 15.0-15.3 지원 시)
- [ ] `dvh` 단위 fallback 추가 (2개 위치)
- [ ] `max()` 함수 fallback 추가 (3개 위치)
- [ ] `:has()` 선택자 대체 또는 JavaScript 대응 (81개 위치)

### 테스트 필요
- [ ] iOS 15.0 실제 기기 테스트
- [ ] iOS 15.4+ 실제 기기 테스트
- [ ] Android 7 실제 기기 테스트
- [ ] 주요 화면 UI 확인

---

## 7. 참고 자료

### 브라우저 호환성
- [Can I Use - :has()](https://caniuse.com/css-has)
- [Can I Use - CSS Grid](https://caniuse.com/css-grid)
- [Can I Use - gap](https://caniuse.com/flexbox-gap)
- [Can I Use - backdrop-filter](https://caniuse.com/css-backdrop-filter)
- [Can I Use - max()](https://caniuse.com/css-math-functions)
- [Can I Use - dvh](https://caniuse.com/viewport-unit-variants)

### iOS Safari 버전별 기능 지원
- iOS 15.0: Safari 15.0
- iOS 15.4: Safari 15.4 (`:has()`, `dvh`, `max()` 지원 시작)

### Android 7 Chrome 버전
- Android 7.0: Chrome 51-59
- CSS Grid: Chrome 57+ 지원
- Flexbox gap: Chrome 84+ 지원 (Android 7 미지원)

---

## 🎯 결론

현재 코드베이스는 **iOS 15.4+**를 기준으로 작성되어 있습니다.

**권장 사항**:
1. **iOS 15.4+ 지원으로 제한** (현재 코드 유지) - 가장 간단하고 권장되는 방법
2. 또는 **iOS 15.0-15.3도 지원**하려면 위의 추가 작업 필요

