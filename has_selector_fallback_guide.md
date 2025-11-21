

# `:has()` 선택자 대응 방법 가이드

## iOS 15.0-15.3 및 Android 7 지원을 위한 Fallback 구현

검토 일자: 2025.11.20

---

## 📋 목차

1. [문제 상황](#1-문제-상황)
2. [대응 방법 개요](#2-대응-방법-개요)
3. [CSS @supports 방법](#3-css-supports-방법)
4. [JavaScript Fallback 방법](#4-javascript-fallback-방법)
5. [Vue Directive 방법](#5-vue-directive-방법) ⭐ **권장**
6. [주요 사용 패턴별 대응](#6-주요-사용-패턴별-대응)
7. [구현 예시](#7-구현-예시)

---

## 1. 문제 상황

### 지원 현황

- **iOS 15.0-15.3**: ❌ `:has()` 미지원
- **iOS 15.4+**: ✅ `:has()` 지원
- **Android 7 (Chrome 51-59)**: ❌ `:has()` 미지원
- **Chrome 105+**: ✅ `:has()` 지원

### 프로젝트 사용 현황

- **resources/assets/styles**: 71개 사용
- **packages/solid/src**: 5개 사용
- **총 76개 사용**

---

## 2. 대응 방법 개요

### 옵션 1: CSS @supports (권장 - 간단한 경우)

- 장점: CSS만으로 해결, JavaScript 불필요
- 단점: 복잡한 선택자는 대응 어려움
- 적용: 단순한 `:has()` 사용에 적합

### 옵션 2: JavaScript Fallback (권장 - 복잡한 경우)

- 장점: 모든 경우에 대응 가능, 유연함
- 단점: JavaScript 코드 필요
- 적용: 복잡한 선택자나 동적 콘텐츠에 적합

### 옵션 3: Vue Directive (⭐ 권장)

- 장점: Vue스러운 선언적 방식, 컴포넌트에서 직접 사용 가능, 자동 클래스 관리
- 단점: Vue 프로젝트에서만 사용 가능
- 적용: **가장 권장되는 방법**

### 옵션 4: 하이브리드

- Vue Directive + CSS @supports 조합
- 최적의 호환성과 성능 제공

---

## 3. CSS @supports 방법

### ⚠️ 중요: @supports selector() 지원 여부

**@supports 기본 구문**:

- ✅ iOS 15: 지원 (Safari 9+)
- ✅ Android 7: 지원 (Chrome 28+)

**@supports selector() 구문**:

- ⚠️ iOS 15.0-15.3: 미지원 (Safari 15.0-15.3)
- ✅ iOS 15.4+: 지원 (Safari 15.4+)
- ❌ Android 7: 미지원 (Chrome 51-59)
- ✅ Chrome 88+: 지원

**결론**: `@supports selector(:has(*))` 구문은 iOS 15.0-15.3과 Android 7에서 **지원되지 않습니다**.

따라서 `@supports selector()`를 사용할 수 없으므로, **JavaScript Fallback 방법을 사용해야 합니다**.

### 대안: @supports 속성 기반 감지 (제한적)

`:has()` 선택자 자체를 직접 감지할 수 없으므로, 대신 다른 방법을 사용해야 합니다:

```scss
// ❌ 작동하지 않음 (iOS 15.0-15.3, Android 7 미지원)
@supports selector(:has(*)) {
  // ...
}

// ✅ 대안: JavaScript로 클래스 추가 후 CSS에서 사용
.sc-container.has-bottom-action-container {
  overscroll-behavior: contain;
}
```

### 기본 사용법 (JavaScript Fallback 필수)

```scss
// :has() 미지원 시 (JavaScript로 클래스 추가 필요)
.sc-container.has-bottom-action-container {
  overscroll-behavior: contain;
}

// :has() 지원 시 (선택적 - 성능 최적화)
@supports selector(:has(*)) {
  .sc-container:has(.sv-bottom-action-container) {
    overscroll-behavior: contain;
  }
}
```

### 실제 적용 예시

#### 예시 1: 단순 자식 요소 확인

```scss
// layouts/_layout.scss
.sc-container {
  // 기본 스타일
  padding-top: var(--spacing-xl);

  // :has() 미지원 시 (JavaScript로 클래스 추가 - 필수)
  &.has-bottom-action-container {
    overscroll-behavior: contain;
    -webkit-overflow-scrolling: touch;
  }

  // :has() 지원 시 (선택적 - 성능 최적화)
  // iOS 15.4+, Chrome 105+에서만 작동
  @supports selector(:has(*)) {
    &:has(.sv-bottom-action-container) {
      overscroll-behavior: contain;
      -webkit-overflow-scrolling: touch;
    }
  }
}
```

#### 예시 2: :not()과 조합

```scss
// layouts/_layout.scss
.error-boundary-wrap {
  min-height: 100vh;
  min-height: 100dvh;

  // :has() 미지원 시 (JavaScript로 클래스 추가 - 필수)
  // JavaScript에서 .sv-bottom-action-container가 없으면 클래스 추가
  &:not(.has-bottom-action-container) {
    padding-bottom: calc(var(--spacing-4xl) + env(safe-area-inset-bottom));
    min-height: 100vh;
    min-height: 100dvh;
  }

  // :has() 지원 시 (선택적 - 성능 최적화)
  @supports selector(:has(*)) {
    &:not(:has(.sv-bottom-action-container)) {
      padding-bottom: calc(var(--spacing-4xl) + env(safe-area-inset-bottom));
      min-height: 100vh;
      min-height: 100dvh;
    }
  }
}
```

---

## 4. JavaScript Fallback 방법

### 4.1 유틸리티 함수 생성

`packages/shared/src/utils/hasSelectorFallback.ts` 파일 생성:

```typescript
/**
 * :has() 선택자 fallback 유틸리티
 * iOS 15.0-15.3 및 Android 7에서 :has() 선택자를 대체하기 위한 클래스 추가
 */

/**
 * :has() 선택자 지원 여부 확인
 */
export function supportsHasSelector(): boolean {
  try {
    return CSS.supports("selector(:has(*))");
  } catch {
    return false;
  }
}

/**
 * 특정 선택자에 해당하는 요소에 클래스 추가
 * @param selector - :has() 선택자를 포함한 전체 선택자
 * @param className - 추가할 클래스명
 * @param rootElement - 검색 시작 요소 (기본값: document)
 */
export function addHasSelectorClass(
  selector: string,
  className: string,
  rootElement: Document | HTMLElement = document
): void {
  if (supportsHasSelector()) {
    return; // :has() 지원 시 JavaScript 처리 불필요
  }

  // :has() 선택자에서 실제 선택자와 :has() 부분 분리
  const hasMatch = selector.match(/:has\(([^)]+)\)/);
  if (!hasMatch) {
    return;
  }

  const baseSelector = selector.replace(/:has\([^)]+\)/, "").trim();
  const hasSelector = hasMatch[1];

  // baseSelector로 요소 찾기
  const elements = rootElement.querySelectorAll(baseSelector);

  elements.forEach((element) => {
    // :has() 내부 선택자로 자식 요소 확인
    const hasChild = element.querySelector(hasSelector);
    if (hasChild) {
      element.classList.add(className);
    } else {
      element.classList.remove(className);
    }
  });
}

/**
 * MutationObserver를 사용하여 동적 콘텐츠 변경 감지
 * @param selector - :has() 선택자를 포함한 전체 선택자
 * @param className - 추가할 클래스명
 * @param rootElement - 관찰 대상 요소 (기본값: document.body)
 */
export function observeHasSelector(
  selector: string,
  className: string,
  rootElement: HTMLElement = document.body
): MutationObserver | null {
  if (supportsHasSelector()) {
    return null; // :has() 지원 시 관찰 불필요
  }

  const hasMatch = selector.match(/:has\(([^)]+)\)/);
  if (!hasMatch) {
    return null;
  }

  const baseSelector = selector.replace(/:has\([^)]+\)/, "").trim();
  const hasSelector = hasMatch[1];

  const observer = new MutationObserver(() => {
    const elements = rootElement.querySelectorAll(baseSelector);
    elements.forEach((element) => {
      const hasChild = element.querySelector(hasSelector);
      if (hasChild) {
        element.classList.add(className);
      } else {
        element.classList.remove(className);
      }
    });
  });

  observer.observe(rootElement, {
    childList: true,
    subtree: true,
  });

  // 초기 실행
  const elements = rootElement.querySelectorAll(baseSelector);
  elements.forEach((element) => {
    const hasChild = element.querySelector(hasSelector);
    if (hasChild) {
      element.classList.add(className);
    }
  });

  return observer;
}
```

### 4.2 Vue Composable 생성

`packages/shared/src/composables/useHasSelectorFallback.ts` 파일 생성:

```typescript
import { onMounted, onUnmounted } from "vue";
import { observeHasSelector, supportsHasSelector } from "@/utils/hasSelectorFallback";

interface HasSelectorConfig {
  selector: string;
  className: string;
  rootElement?: HTMLElement;
}

/**
 * :has() 선택자 fallback을 위한 Vue Composable
 */
export function useHasSelectorFallback(configs: HasSelectorConfig[]) {
  let observers: (MutationObserver | null)[] = [];

  onMounted(() => {
    if (supportsHasSelector()) {
      return; // :has() 지원 시 처리 불필요
    }

    observers = configs.map((config) =>
      observeHasSelector(config.selector, config.className, config.rootElement)
    );
  });

  onUnmounted(() => {
    observers.forEach((observer) => {
      if (observer) {
        observer.disconnect();
      }
    });
  });
}
```

---

## 5. Vue Directive 방법 ⭐ **권장**

Vue Directive를 사용하면 더 선언적이고 Vue스러운 방식으로 `:has()` fallback을 구현할 수 있습니다.

### 5.1 Directive 구현

`packages/shared/src/directives/hasSelector.ts` 파일 생성:

```typescript
import type { App, Directive, DirectiveBinding } from "vue";

/**
 * :has() 선택자 지원 여부 확인
 */
function supportsHasSelector(): boolean {
  try {
    return CSS.supports("selector(:has(*))");
  } catch {
    return false;
  }
}

/**
 * v-has directive 타입 정의
 */
interface HasDirectiveValue {
  selector: string; // :has() 내부 선택자
  className?: string; // 추가할 클래스명 (기본값: 'has-{selector}')
}

/**
 * v-has directive 구현
 * 사용법: v-has="'.sv-bottom-action-container'"
 * 또는: v-has="{ selector: '.sv-bottom-action-container', className: 'has-bottom-action' }"
 */
const hasDirective: Directive = {
  mounted(el: HTMLElement, binding: DirectiveBinding<string | HasDirectiveValue>) {
    if (supportsHasSelector()) {
      return; // :has() 지원 시 처리 불필요
    }

    const value = binding.value;
    let selector: string;
    let className: string;

    if (typeof value === "string") {
      selector = value;
      // 클래스명 자동 생성 (예: '.sv-bottom-action-container' -> 'has-sv-bottom-action-container')
      className = `has-${selector.replace(/^\./, "").replace(/\s+/g, "-")}`;
    } else {
      selector = value.selector;
      className = value.className || `has-${selector.replace(/^\./, "").replace(/\s+/g, "-")}`;
    }

    // 초기 체크
    checkAndUpdateClass(el, selector, className);

    // MutationObserver로 동적 변경 감지
    const observer = new MutationObserver(() => {
      checkAndUpdateClass(el, selector, className);
    });

    observer.observe(el, {
      childList: true,
      subtree: true,
    });

    // cleanup을 위해 observer를 el에 저장
    (el as any).__hasObserver = observer;
  },

  updated(el: HTMLElement, binding: DirectiveBinding<string | HasDirectiveValue>) {
    if (supportsHasSelector()) {
      return;
    }

    // 값이 변경된 경우 재체크
    const value = binding.value;
    let selector: string;
    let className: string;

    if (typeof value === "string") {
      selector = value;
      className = `has-${selector.replace(/^\./, "").replace(/\s+/g, "-")}`;
    } else {
      selector = value.selector;
      className = value.className || `has-${selector.replace(/^\./, "").replace(/\s+/g, "-")}`;
    }

    checkAndUpdateClass(el, selector, className);
  },

  unmounted(el: HTMLElement) {
    // cleanup
    const observer = (el as any).__hasObserver;
    if (observer) {
      observer.disconnect();
      delete (el as any).__hasObserver;
    }
  },
};

/**
 * 요소에 자식 요소가 있는지 확인하고 클래스 추가/제거
 */
function checkAndUpdateClass(el: HTMLElement, selector: string, className: string) {
  const hasChild = el.querySelector(selector);
  if (hasChild) {
    el.classList.add(className);
  } else {
    el.classList.remove(className);
  }
}

/**
 * v-has-not directive (반대 로직)
 * :not(:has()) 패턴에 사용
 */
const hasNotDirective: Directive = {
  mounted(el: HTMLElement, binding: DirectiveBinding<string | HasDirectiveValue>) {
    if (supportsHasSelector()) {
      return;
    }

    const value = binding.value;
    let selector: string;
    let className: string;

    if (typeof value === "string") {
      selector = value;
      className = `has-${selector.replace(/^\./, "").replace(/\s+/g, "-")}`;
    } else {
      selector = value.selector;
      className = value.className || `has-${selector.replace(/^\./, "").replace(/\s+/g, "-")}`;
    }

    // 반대 로직: 자식이 없으면 클래스 추가
    checkAndUpdateClassNot(el, selector, className);

    const observer = new MutationObserver(() => {
      checkAndUpdateClassNot(el, selector, className);
    });

    observer.observe(el, {
      childList: true,
      subtree: true,
    });

    (el as any).__hasNotObserver = observer;
  },

  updated(el: HTMLElement, binding: DirectiveBinding<string | HasDirectiveValue>) {
    if (supportsHasSelector()) {
      return;
    }

    const value = binding.value;
    let selector: string;
    let className: string;

    if (typeof value === "string") {
      selector = value;
      className = `has-${selector.replace(/^\./, "").replace(/\s+/g, "-")}`;
    } else {
      selector = value.selector;
      className = value.className || `has-${selector.replace(/^\./, "").replace(/\s+/g, "-")}`;
    }

    checkAndUpdateClassNot(el, selector, className);
  },

  unmounted(el: HTMLElement) {
    const observer = (el as any).__hasNotObserver;
    if (observer) {
      observer.disconnect();
      delete (el as any).__hasNotObserver;
    }
  },
};

function checkAndUpdateClassNot(el: HTMLElement, selector: string, className: string) {
  const hasChild = el.querySelector(selector);
  if (!hasChild) {
    el.classList.add(className);
  } else {
    el.classList.remove(className);
  }
}

/**
 * Vue Plugin으로 등록
 */
export const hasSelectorDirectivePlugin = {
  install(app: App) {
    app.directive("has", hasDirective);
    app.directive("has-not", hasNotDirective);
  },
};

export default hasSelectorDirectivePlugin;
```

### 5.2 Plugin 등록

`packages/shared/src/directives/index.ts` 파일 생성:

```typescript
export { hasSelectorDirectivePlugin } from "./hasSelector";
```

`packages/shared/src/index.ts`에 export 추가:

```typescript
export { hasSelectorDirectivePlugin } from "./directives";
```

`apps/@pms/src/plugins/index.ts` 수정:

```typescript
import "@/plugins/aggrid";
import vuetify from "@/plugins/vuetify";
import { hasSelectorDirectivePlugin } from "@shc-nss/shared";
import { createPinia } from "pinia";
import type { App, Plugin } from "vue";
import Vue3Lottie from "vue3-lottie";

const pinia = createPinia();

/**
 * 플러그인 등록
 * @param {Object} app Vue 인스턴스
 */
export const registerPlugins = (app: App) => {
  app.use(pinia);
  app.use(vuetify);
  app.use(Vue3Lottie as unknown as Plugin, { name: "Vue3Lottie" });
  app.use(hasSelectorDirectivePlugin); // v-has directive 등록
};
```

### 5.3 사용 예시

#### 예시 1: 기본 사용 (문자열)

```vue
<template>
  <!-- .sc-container:has(.sv-bottom-action-container) -->
  <div
    class="sc-container"
    v-has="'.sv-bottom-action-container'"
  >
    <div class="sv-bottom-action-container">...</div>
  </div>
</template>
```

#### 예시 2: 커스텀 클래스명

```vue
<template>
  <div
    class="sc-container"
    v-has="{ selector: '.sv-bottom-action-container', className: 'has-bottom-action' }"
  >
    <div class="sv-bottom-action-container">...</div>
  </div>
</template>
```

#### 예시 3: :not(:has()) 패턴

```vue
<template>
  <!-- .error-boundary-wrap:not(:has(.sv-bottom-action-container)) -->
  <div
    class="error-boundary-wrap"
    v-has-not="'.sv-bottom-action-container'"
  >
    <!-- .sv-bottom-action-container가 없으면 'has-sv-bottom-action-container' 클래스 추가 -->
  </div>
</template>
```

#### 예시 4: 복잡한 선택자

```vue
<template>
  <!-- .sc-container:has(> .sc-contents__body > .sc-tabs__group > .sv-tabs) -->
  <div
    class="sc-container"
    v-has="{
      selector: '> .sc-contents__body > .sc-tabs__group > .sv-tabs',
      className: 'has-tabs-group',
    }"
  >
    <div class="sc-contents__body">
      <div class="sc-tabs__group">
        <div class="sv-tabs">...</div>
      </div>
    </div>
  </div>
</template>
```

#### 예시 5: 동적 선택자

```vue
<script setup lang="ts">
import { ref } from "vue";

const hasContent = ref(".sv-bottom-action-container");
</script>

<template>
  <div
    class="sc-container"
    v-has="hasContent"
  >
    <div class="sv-bottom-action-container">...</div>
  </div>
</template>
```

### 5.4 SCSS와 함께 사용

```scss
// layouts/_layout.scss
.sc-container {
  padding-top: var(--spacing-xl);

  // :has() 미지원 시 (v-has directive로 클래스 추가)
  &.has-sv-bottom-action-container {
    overscroll-behavior: contain;
    -webkit-overflow-scrolling: touch;
  }

  // :has() 지원 시 (선택적 - 성능 최적화)
  @supports selector(:has(*)) {
    &:has(.sv-bottom-action-container) {
      overscroll-behavior: contain;
      -webkit-overflow-scrolling: touch;
    }
  }
}
```

### 5.5 장점

1. **선언적**: 템플릿에서 직접 사용 가능
2. **자동 관리**: 클래스 추가/제거 자동 처리
3. **반응형**: Vue의 반응성 시스템과 통합
4. **타입 안전**: TypeScript 지원
5. **성능**: `:has()` 지원 브라우저에서는 자동으로 비활성화

---

## 6. 주요 사용 패턴별 대응

### 패턴 1: 단순 자식 요소 확인

```scss
// 원본
.sc-container:has(.sv-bottom-action-container) {
  overscroll-behavior: contain;
}

// 대응 (JavaScript Fallback 필수)
.sc-container.has-bottom-action-container {
  overscroll-behavior: contain;
}

// 선택적: :has() 지원 브라우저용 (성능 최적화)
@supports selector(:has(*)) {
  .sc-container:has(.sv-bottom-action-container) {
    overscroll-behavior: contain;
  }
}
```

```typescript
// JavaScript
observeHasSelector(".sc-container:has(.sv-bottom-action-container)", "has-bottom-action-container");
```

### 패턴 2: :not()과 조합

```scss
// 원본
&:not(:has(.sv-bottom-action-container)) {
  padding-bottom: calc(var(--spacing-4xl) + env(safe-area-inset-bottom));
}

// 대응 (JavaScript Fallback 필수)
&:not(.has-bottom-action-container) {
  padding-bottom: calc(var(--spacing-4xl) + env(safe-area-inset-bottom));
}

// 선택적: :has() 지원 브라우저용
@supports selector(:has(*)) {
  &:not(:has(.sv-bottom-action-container)) {
    padding-bottom: calc(var(--spacing-4xl) + env(safe-area-inset-bottom));
  }
}
```

```typescript
// JavaScript - :not()은 클래스 추가 로직이 반대
const elements = document.querySelectorAll(".error-boundary-wrap");
elements.forEach((element) => {
  const hasChild = element.querySelector(".sv-bottom-action-container");
  if (!hasChild) {
    element.classList.add("has-bottom-action-container");
  } else {
    element.classList.remove("has-bottom-action-container");
  }
});
```

### 패턴 3: 복잡한 자식 선택자

```scss
// 원본
.sc-container:has(> .sc-contents__body > .sc-tabs__group > .sv-tabs) {
  padding-top: 0;
}

// 대응 (JavaScript Fallback 필수)
.sc-container.has-tabs-group {
  padding-top: 0;
}

// 선택적: :has() 지원 브라우저용
@supports selector(:has(*)) {
  .sc-container:has(> .sc-contents__body > .sc-tabs__group > .sv-tabs) {
    padding-top: 0;
  }
}
```

```typescript
// JavaScript
observeHasSelector(
  ".sc-container:has(> .sc-contents__body > .sc-tabs__group > .sv-tabs)",
  "has-tabs-group"
);
```

### 패턴 4: 인접 형제 선택자와 조합

```scss
// 원본 (table/_table.scss)
&:not(:has(~ .#{$baseClass}__th--sticky-left)) {
  border-right: 0;
}

// 대응 (JavaScript Fallback 필수)
&:not(.has-sticky-left-sibling) {
  border-right: 0;
}

// 선택적: :has() 지원 브라우저용
@supports selector(:has(*)) {
  &:not(:has(~ .#{$baseClass}__th--sticky-left)) {
    border-right: 0;
  }
}
```

```typescript
// JavaScript - 형제 요소 확인
const elements = document.querySelectorAll(`.${baseClass}__th`);
elements.forEach((element) => {
  const nextSibling = element.nextElementSibling;
  const hasStickyLeft = nextSibling?.classList.contains(`${baseClass}__th--sticky-left`);
  if (!hasStickyLeft) {
    element.classList.add("has-sticky-left-sibling");
  } else {
    element.classList.remove("has-sticky-left-sibling");
  }
});
```

### 패턴 5: 속성 선택자와 조합

```scss
// 원본 (discoverNew_comp.scss)
&:has([src=""]),
&:has([src]),
&:has([src="about:invalid"]),
&:has([src^="data:image/svg+xml"]) {
  // ...
}

// 대응 (JavaScript Fallback 필수)
&.has-empty-src,
&.has-src,
&.has-invalid-src,
&.has-svg-src {
  // ...
}

// 선택적: :has() 지원 브라우저용
@supports selector(:has(*)) {
  &:has([src=""]),
  &:has([src]),
  &:has([src="about:invalid"]),
  &:has([src^="data:image/svg+xml"]) {
    // ...
  }
}
```

```typescript
// JavaScript
const images = document.querySelectorAll("img");
images.forEach((img) => {
  const src = img.getAttribute("src");
  if (!src || src === "" || src === "about:invalid") {
    img.classList.add("has-empty-src", "has-invalid-src");
  } else if (src.startsWith("data:image/svg+xml")) {
    img.classList.add("has-svg-src");
  } else {
    img.classList.add("has-src");
  }
});
```

---

## 7. 구현 예시

### 7.1 Vue Directive 방법 (권장)

#### 7.1.1 Directive 및 Plugin 생성

위의 [5. Vue Directive 방법](#5-vue-directive-방법-⭐-권장) 섹션을 참고하여 구현합니다.

#### 7.1.2 컴포넌트에서 사용

```vue
<template>
  <!-- layouts/_layout.scss의 .sc-container:has(.sv-bottom-action-container) -->
  <div
    class="sc-container"
    v-has="'.sv-bottom-action-container'"
  >
    <div class="sc-contents__body">...</div>
    <div class="sv-bottom-action-container">...</div>
  </div>

  <!-- layouts/_layout.scss의 .error-boundary-wrap:not(:has(.sv-bottom-action-container)) -->
  <div
    class="error-boundary-wrap"
    v-has-not="'.sv-bottom-action-container'"
  >
    <!-- 내용 -->
  </div>
</template>
```

### 7.2 전역 초기화 방법 (대안)

```typescript
// apps/@pms/src/main.ts 또는 plugins/hasSelectorFallback.ts
import { observeHasSelector, supportsHasSelector } from "@shc-nss/shared/utils/hasSelectorFallback";

if (!supportsHasSelector()) {
  // 주요 :has() 사용 패턴에 대한 fallback 설정

  // 1. .sc-container:has(.sv-bottom-action-container)
  observeHasSelector(
    ".sc-container:has(.sv-bottom-action-container)",
    "has-bottom-action-container"
  );

  // 2. .sc-container:has(> .sc-contents__body > .sc-tabs__group > .sv-tabs)
  observeHasSelector(
    ".sc-container:has(> .sc-contents__body > .sc-tabs__group > .sv-tabs)",
    "has-tabs-group"
  );

  // 3. .sc-container:has(> .sc-contents__body > .sc-tabs__group > .sv-tabs.sv-tabs--type-segment)
  observeHasSelector(
    ".sc-container:has(> .sc-contents__body > .sc-tabs__group > .sv-tabs.sv-tabs--type-segment)",
    "has-segment-tabs"
  );

  // 4. .sc-container:has(.sc-body__title ~ .sc-contents__body > .sc-tabs__group)
  observeHasSelector(
    ".sc-container:has(.sc-body__title ~ .sc-contents__body > .sc-tabs__group)",
    "has-title-tabs-group"
  );

  // 5. .sc-container:has(.sv-linear-progress-step)
  observeHasSelector(".sc-container:has(.sv-linear-progress-step)", "has-linear-progress");

  // 6. .sc-tabs__group:has(.sv-tabs.sv-tabs--type-segment)
  observeHasSelector(".sc-tabs__group:has(.sv-tabs.sv-tabs--type-segment)", "has-segment-tabs");

  // 7. .error-boundary-wrap:not(:has(.sv-bottom-action-container))
  // :not()은 반대 로직으로 처리
  const errorBoundaryElements = document.querySelectorAll(".error-boundary-wrap");
  errorBoundaryElements.forEach((element) => {
    const hasChild = element.querySelector(".sv-bottom-action-container");
    if (!hasChild) {
      element.classList.add("has-bottom-action-container");
    }
  });

  // MutationObserver로 동적 변경 감지
  const errorBoundaryObserver = new MutationObserver(() => {
    const elements = document.querySelectorAll(".error-boundary-wrap");
    elements.forEach((element) => {
      const hasChild = element.querySelector(".sv-bottom-action-container");
      if (!hasChild) {
        element.classList.add("has-bottom-action-container");
      } else {
        element.classList.remove("has-bottom-action-container");
      }
    });
  });
  errorBoundaryObserver.observe(document.body, {
    childList: true,
    subtree: true,
  });
}
```

### 7.3 컴포넌트별 사용 (Vue Composable - 대안)

```vue
<!-- 컴포넌트에서 사용 -->
<script setup lang="ts">
import { useHasSelectorFallback } from "@shc-nss/shared/composables/useHasSelectorFallback";

// :has() fallback 설정
useHasSelectorFallback([
  {
    selector: ".sc-container:has(.sv-bottom-action-container)",
    className: "has-bottom-action-container",
  },
  {
    selector: ".sc-container:has(> .sc-contents__body > .sc-tabs__group > .sv-tabs)",
    className: "has-tabs-group",
  },
]);
</script>
```

### 7.4 SCSS 파일 수정 예시

```scss
// layouts/_layout.scss 수정 예시

// 원본
.sc-container:has(.sv-bottom-action-container) {
  overscroll-behavior: contain;
  -webkit-overflow-scrolling: touch;
}

// 수정 후
.sc-container {
  // :has() 지원 시
  @supports selector(:has(*)) {
    &:has(.sv-bottom-action-container) {
      overscroll-behavior: contain;
      -webkit-overflow-scrolling: touch;
    }
  }

  // :has() 미지원 시 (JavaScript로 클래스 추가)
  &.has-bottom-action-container {
    overscroll-behavior: contain;
    -webkit-overflow-scrolling: touch;
  }
}
```

---

## 📝 체크리스트

### 구현 단계

#### 방법 1: Vue Directive (권장)

1. **Directive 및 Plugin 생성**
   - [ ] `packages/shared/src/directives/hasSelector.ts` 생성
   - [ ] `v-has` directive 구현
   - [ ] `v-has-not` directive 구현
   - [ ] Plugin 등록 함수 구현

2. **Plugin 등록**
   - [ ] `packages/shared/src/directives/index.ts` 생성
   - [ ] `packages/shared/src/index.ts`에 export 추가
   - [ ] `apps/@pms/src/plugins/index.ts`에 plugin 등록

3. **SCSS 파일 수정**
   - [ ] fallback 클래스 스타일 추가

4. **컴포넌트에서 사용**
   - [ ] 템플릿에 `v-has` 또는 `v-has-not` directive 추가

#### 방법 2: 전역 초기화 (대안)

1. **유틸리티 함수 생성**
   - [ ] `packages/shared/src/utils/hasSelectorFallback.ts` 생성
   - [ ] `supportsHasSelector()` 함수 구현
   - [ ] `addHasSelectorClass()` 함수 구현
   - [ ] `observeHasSelector()` 함수 구현

2. **Vue Composable 생성**
   - [ ] `packages/shared/src/composables/useHasSelectorFallback.ts` 생성

3. **SCSS 파일 수정**
   - [ ] `layouts/_layout.scss` 수정 (8개)
   - [ ] `base/_utility.scss` 수정 (5개)
   - [ ] `pay/_auth.scss` 수정 (6개)
   - [ ] `module/_agree-list.scss` 수정 (18개)
   - [ ] `pay/_benefits.scss` 수정 (7개)
   - [ ] 기타 파일들 수정

4. **JavaScript 초기화**
   - [ ] 전역 초기화 코드 추가 (main.ts 또는 plugin)
   - [ ] 주요 패턴에 대한 observer 설정

5. **테스트**
   - [ ] iOS 15.0-15.3 테스트
   - [ ] Android 7 테스트
   - [ ] iOS 15.4+ 테스트 (기존 동작 확인)

---

## 🎯 권장 구현 순서

### Vue Directive 방법 (권장)

1. **1단계**: Directive 및 Plugin 생성
   - `packages/shared/src/directives/hasSelector.ts` 생성
   - `v-has`, `v-has-not` directive 구현

2. **2단계**: Plugin 등록
   - `apps/@pms/src/plugins/index.ts`에 등록

3. **3단계**: SCSS 파일 수정
   - fallback 클래스 스타일 추가 (layouts/\_layout.scss 등)

4. **4단계**: 컴포넌트에서 사용
   - 템플릿에 `v-has` directive 추가

5. **5단계**: 테스트 및 검증

### 전역 초기화 방법 (대안)

1. **1단계**: 유틸리티 함수 및 Composable 생성
2. **2단계**: 가장 많이 사용되는 패턴부터 SCSS 수정 (layouts/\_layout.scss)
3. **3단계**: 전역 JavaScript 초기화 코드 추가
4. **4단계**: 나머지 파일들 순차적으로 수정
5. **5단계**: 테스트 및 검증

---

## 📚 참고 자료

- [MDN - :has()](https://developer.mozilla.org/en-US/docs/Web/CSS/:has)
- [MDN - @supports](https://developer.mozilla.org/en-US/docs/Web/CSS/@supports)
- [Can I Use - :has()](https://caniuse.com/css-has)
- [CSS :has() Polyfill](https://github.com/csstools/postcss-plugins/tree/main/plugins/css-has-pseudo)
