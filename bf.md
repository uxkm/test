
{% raw %}
```js

// _layout
@use "sass:math";
@use "sass:map";
@use "@assets/styles/shared" as *;
@use "@assets/styles/base/functions" as *;

$prefix: "sv-";

$sc-header-height: 3.5rem;
$sc-foot-height: 4.75rem;

// Spacing 변수 (레거시 브라우저 대응을 위해 SCSS 변수 사용)
$spacing-xs: 2px;
$spacing-sm: 4px;
$spacing-md: 8px;
$spacing-lg: 12px;
$spacing-xl: 16px;
$spacing-2xl: 20px;
$spacing-3xl: 24px;
$spacing-4xl: 32px;
$spacing-5xl: 40px;
$spacing-6xl: 48px;
$spacing-7xl: 80px;

:root {
  --sc-header-height: #{$sc-header-height};
  --sc-foot-height: #{$sc-foot-height};
}
html {
  touch-action: manipulation; // 더블탭 확대 방지
  overscroll-behavior: contain;
  -webkit-overflow-scrolling: touch;
}

body {
  background-color: var(--bg-canvas_white);
}

.sc-wrap {
  background-color: transparent;
}

.transitions-wrap {
  background-color: transparent;
}

.error-boundary-wrap {
  display: flex;
  flex-direction: column;
  max-width: 620px;
  margin: 0 auto;
  min-height: 100vh;
  min-height: 100dvh;
  box-sizing: border-box;
  background-color: var(--bg-canvas_white);
  padding-left: env(safe-area-inset-left);
  padding-right: env(safe-area-inset-right);
  padding-bottom: env(safe-area-inset-bottom);

  @media (max-width: 620px) {
    width: 100%;
    margin: 0;
  }
  // 하단 fixed 영역도 동일하게 적용
  .sv-bottom-action-container__inner {
    width: 100%;
    max-width: 620px;
    left: 50%;
    transform: translateX(-50%);

    @media (max-width: 620px) {
      width: 100%;
      left: 0;
      transform: none;
    }
  }
}

.bg-canvas_white {
  background-color: var(--bg-canvas_white);
}
.bg-canvas_gray {
  background-color: var(--bg-canvas_gray);
  .error-boundary-wrap {
    background-color: inherit;
  }
}
.sc-wrap.full-width-app {
  .error-boundary-wrap {
    max-width: 100%;
  }
}
.max-width {
  max-width: 620px;
  margin: 0 auto;
}
.sv-navigation {
  .sv-navigation__title-text + .sv-base-badge {
    padding: 3px 0 2px;
    .sv-base-badge__indicator {
      margin-left: 0;
    }
  }
  .sv-navigation__title {
    > div {
      display: inline-flex;
      align-items: center;
      gap: var(--spacing-sm);
    }
    .sv-navigation__title-text {
      @include font-set(title-m, 500);
      font-weight: 500;
      // color: var(--text-primary);
      color: inherit;
    }
  }
  @at-root .sc-main .sv-navigation {
    .sv-navigation__title {
      .sc-icon {
        display: none;
      }
      h1 {
        @include font-set(title-l, 700);
        font-weight: 700;
        color: var(--text-secondary);
      }
    }
    .sv-navigation__right {
      .sv-button--color-primary {
        color: var(--text-primary);
      }
    }
  }
  &--color-gray {
    .sv-navigation__inner {
      background-color: var(--bg-canvas_gray_light) !important;
    }
    &.sv-navigation--font-color-black {
      .sv-navigation__inner {
        color: $text-primary !important;
      }
      .sv-navigation__search-input {
        color: $text-primary !important;
      }
      [class*="sv-icon"] {
        color: $fg-primary !important;
      }
    }
  }
  &--fixed {
    z-index: 500;
    &.sv-navigation--scrolled .sv-navigation__inner {
      &::after {
        content: "";
        display: block;
        position: absolute;
        bottom: 0;
        left: 0;
        width: 100%;
        height: 2px;
        background-color: var(--border-secondary);
      }
    }
  }
  &--color-clear.sv-navigation--scrolled .sv-navigation__inner {
    &::after {
      display: none;
    }
  }
}
.sc-container {
  position: relative;
  display: flex;
  flex-direction: column;
  flex: 1 1 auto;
  min-height: 0;
  padding-top: $spacing-xl;
  padding-bottom: $spacing-4xl;

  .sc-contents__head {
    flex: 0 0 auto;
  }
  .sc-contents__body {
    flex: 1 1 auto;
    min-height: 0;
    // 기본적으로 하단 마진 32px 적용
    // margin-bottom: $spacing-4xl;
  }
  .sc-contents__foot {
    flex: 0 0 auto;
    width: 100%;
    // 기본적으로 하단 마진 32px 적용
    // margin-bottom: $spacing-4xl;
  }
  .sv-bottom-action-container {
    flex: 0 0 auto;
    width: 100%;
    // margin-top: $spacing-4xl;
    &--scroll-dim {
      .sv-bottom-action-container__inner {
        background-color: var(--bg-canvas_white);
        .sv-bottom-action-container__gradient {
          background: linear-gradient(
            180deg,
            var(--bg-canvas_white_a0) 0%,
            var(--bg-canvas_white) 100%
          );
        }
      }
    }
  }
  .sv-bottom-action-container__placeholder {
    width: 100%;
  }
  // .sc-contents__body ~ .sv-bottom-action-container,
  // .sc-contents__foot ~ .sv-bottom-action-container {
  //   margin-top: 0;
  // }
}

.sc-contents__body > .sc-tabs__group {
  ~ section,
  ~ .section {
    margin-top: $spacing-3xl;
  }
}
.sc-container,
.sc-contents__body {
  > .is-sticky {
    position: sticky;
    top: $sc-header-height;
    margin-top: calc(#{$spacing-xl} * -1);
    background-color: var(--bg-canvas_white);
    z-index: 100;

    @at-root .sv-popup__body & {
      top: calc(#{$spacing-xl} * -1);
      padding-top: $spacing-xl;
    }
  }
}
.sc-contents__body {
  > .is-sticky {
    margin-top: unset;
  }
}
.sv-popup .sc-contents__body > .is-sticky {
  background-color: var(--bg-canvas_white-elevated);
}

// 하단 BottomSheet max width 620 대응
.sc-wrap ~ .sv-bottom-sheet {
  left: 50%;
  transform: translateX(-50%) !important;
  width: 100%;
  max-width: 620px;
}

.sc-wrap ~ .sv-bottom-sheet--leave-to {
  transform: translateX(-50%) translateY(100%) !important;
}

// full popup max width 620 대응
.sv-popup.sv-popup--variant-full {
  .sv-popup__body,
  .sv-popup__footer {
    width: 100%;
    max-width: 620px;
    margin: 0 auto;
  }
  // 풀팝업 내 하단 고정 width 620 대응
  .sv-bottom-action-container__inner {
    left: 50%;
    transform: translateX(-50%);
    width: 100%;
    max-width: 620px;
  }
}




// _benefits
/* 앱테크 포인트 더 받기 */
.shortform-container {
  padding-top: 0;
}
.detail-shortform__body {
  padding: var(--spacing-5xl) 0 var(--spacing-4xl);
  background-color: var(--bg-canvas_white);
}
.detail-shortform__footer {
  padding: var(--spacing-4xl) 0 0;
}
.sc-detail-shortform {
  padding-top: 0;
  .sc-body__title {
    padding: 0;
    .title-type {
      padding: 0;
    }
  }

  &__visual {
    max-width: 375px;
    margin: var(--spacing-xl) auto;
    img {
      width: 100%;
      height: auto;
      vertical-align: top;
    }
  }
  &__card {
    .sv-card--type-list .sv-card__content {
      min-height: 104px;
    }
    .sv-card {
      .sv-icon {
        vertical-align: middle;
      }
      .sc-point-card__img {
        width: 40px;
        height: 40px;
        object-fit: contain;
      }
      .sc-detail-shortform__card__main-text {
        color: var(--text-primary);
        strong {
          font-weight: inherit;
          color: var(--text-brand);
        }
      }
    }

    .sv-button-group {
      margin-top: var(--spacing-4xl);
    }
    .text-tertiary {
      color: var(--text-tertiary);
      &.sv-button--variant-underline.sv-button--color-secondary {
        color: var(--text-tertiary);
      }
    }
  }
}

<route lang="yaml">
meta:
  id: SBT099A01
  title: 신한 SOL페이
  menu: 혜택 > 앱테크 > 포인트 더 받기 > 숏폼보고 포인트 받기(숏핑플러스)
  layout: SubLayout
  category: 혜택
  publish: 최선화[김대민]
  publishVersion: 0.8
  status: 재작업
  qa: 검수완료
  etc: | 
    [디자인 QA]260109: 디자인 업데이트로 메타정보의 class 추가, 전체 구조 수정,
    [디자인 QA]260109: 디자인 업데이트로 하단 구조 수정, 아이콘 변경, text-tertiary class 추가,
  header:
    fixed: true
    close: true
  appClassList: "full-width-app, bg-canvas_gray"
  mainClassList: "pt-none"
</route>
<template>
  <div class="sc-contents__body sc-detail-shortform max-width-contents">
    <!-- 260109 : 디자인 업데이트에 따른 영역 구분-->
    <div class="detail-shortform__body">
      <section class="section max-width">
        <ScTitle
          :isHero="true"
          mainTitle="숏핑 플러스"
          description="재밌는 숏폼 영상도 보고, 포인트도 쌓고,<br />특가 구매 혜택까지 1석 3조의 혜택!"
        />
        <div class="sc-detail-shortform__visual">
          <img
            :src="`${$cdnURL}/images/pages/benefits/img_detail_shortform.png`"
            alt=""
          />
        </div>
        <BoxButtonGroup size="large">
          <BoxButton
            color="primary"
            text="숏폼보고 포인트 받기"
          />
        </BoxButtonGroup>
      </section>
    </div>
    <!-- 260109 : 구분선 제거 -->
    <!-- <Divider
      color="tertiary"
      orientation="horizontal"
      size="full"
      variant="group"
    /> -->
    <!-- 260109 : 디자인 업데이트에 따른 class shortform-footer 추가 -->
    <div class="detail-shortform__footer">
      <section class="section sc-detail-shortform__card shortform-footer max-width">
        <ListCard
          shadow
          variant="outline"
        >
          <ListItem
            align="centered"
            :left="{ subText: '포인트 적립 조건', direction: 'column-reverse' }"
          >
            <template #leftIcon>
              <!-- 260109 : 디자인 업데이트에 따른 아이콘 수정 -->
              <!-- <ScIcon
                size="36"
                iconName="sample-icon"
              /> -->
              <img
                :src="`${$cdnURL}/images/pages/base/Coin_Point.png`"
                class="sc-point-card__img"
              />
            </template>
            <template #leftMainText>
              <span class="sc-detail-shortform__card__main-text">
                숏폼 영상 15초 이상 시청 시,<br />
                마이신한포인트
                <strong>5P 적립</strong>
              </span>
            </template>
          </ListItem>
        </ListCard>
  
        <!-- case: 이용해지 버튼 있을 경우 -->
        <!-- 260109 : 디자인 업데이트에 따른 color 값 수정 class 추가 text-tertiary -->
        <TextButtonGroup size="xsmall">
          <TextButtonUnderline
            color="secondary"
            text="이용해지"
            class="text-tertiary"
          />
        </TextButtonGroup>
      </section>
    </div>
  </div>
</template>

<script setup>
import { ScIcon, ScTitle } from "@shc-nss/ui/shc";
import {
  BoxButton,
  BoxButtonGroup,
  Divider,
  ListCard,
  ListItem,
  TextButtonGroup,
  TextButtonUnderline,
} from "@shc-nss/ui/solid";
</script>



```
{% endraw %}
---
