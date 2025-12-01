# test
```scss
// 251201
//ters-popup 다음 라인


// 나만의 우주 카드신청 tabs
.my-space-card {
  .space-card-tabs {
    padding-top: var(--spacing-xl);
    padding-right: var(--container-padding-mobile);
    padding-left: var(--container-padding-mobile);
    &.is-sticky {
      margin-top: 0 !important;
      padding-top: var(--spacing-xl);
      .sv-tabs__btns {
        position: sticky;
        z-index: 10;
      }
    }
  }
  .sc-body__title ~ & {
    margin-top: calc(var(--spacing-4xl) - var(--spacing-xl)) !important;
  }
  .space-card__contents {
    padding-top: var(--spacing-3xl);
  }
  .space-card__default {
    overflow: hidden;
    position: relative;
    width: 100%;
    // Android 6 등 구형 브라우저 대응: clamp() 미지원 시 fallback
    // vw 단위는 Android 4.4+부터 지원, clamp()는 Chrome 79+부터 지원
    min-height: 97.3vw; // fallback: 최소값
    height: 50vw; // fallback: 기본값 (2:1 비율)
    max-height: 120vw; // fallback: 최대값

    // clamp() 지원 브라우저에서만 적용
    @supports (height: clamp(1px, 1px, 1px)) {
      // 가로 사이즈에 비례해서 높이가 조정되도록 vw 단위 사용
      // 최소 높이 보장 (약 365px 기준, 375px 화면에서 약 97.3vw)
      min-height: clamp(97.3vw, 50vw, 120vw);
      // 가로 사이즈의 50%를 높이로 사용 (2:1 비율)
      // 필요시 비율 조정 가능 (예: 56.25vw = 16:9, 75vw = 4:3)
      height: clamp(97.3vw, 50vw, 120vw);
    }
    border-radius: var(--radius-xl);

    background-image: url(#{$cdn-url}/images/pages/auth/space_card_default_bg.png);
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
    text-align: center;
  }
  // 기념 카드 날짜 선택
  .space-card__default-contents {
    overflow: hidden;
    max-width: 335px;
    min-height: 365px;
    margin: 0 auto;
    padding: 2rem 1.625rem 0;
    border-radius: var(--radius-xl);
  }
  .space-card__title {
    img {
      width: 100%;
      height: auto;
    }
  }
  .space-card__tabs-input {
    display: flex;
    gap: var(--spacing-md);
    min-width: 0;
    flex: 1 1 auto;
    margin: var(--spacing-xl) 0 var(--spacing-lg);
    .space-card__input-label {
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .space-card__input {
      width: 100%;
      min-width: 60px;
      height: 60px;
      padding: 0;
      border-width: 3px;
      border-style: solid;
      border-color: #b9b0ff;
      border-radius: var(--radius-sm);
      background-color: #0b103d;
      font-size: var(--font-size-headline-m);
      line-height: var(--line-height-headline-m);
      letter-spacing: var(--letter-spacing-headline-m);
      font-weight: 700;
      color: #fff;
      text-align: center;

      &::placeholder {
        color: #4d5491;
      }

      &:focus,
      &:not(:placeholder-shown) {
        outline: none;
        border-width: 3px;
        border-color: #fff;
        color: var(--text-ondark_primary-same);
      }

      &::-webkit-inner-spin-button {
        display: none;
        -webkit-appearance: none;
        margin: 0;
      }
    }
  }
  .space-card__tabs-input-actions {
    .space-card__input-button {
      width: 100%;
      height: 42px;
      padding: 0;
      border: 0;
      border-radius: var(--radius-sm);
      background: linear-gradient(90deg, #1fa7e2 0%, #a23dff 100%);
      color: var(--text-ondark_primary-same);
      @include font-set("title-s", 500);
      font-weight: 500;
      &:disabled {
        background: linear-gradient(90deg, #325897 0%, #523098 100%);
        opacity: 0.5;
      }
    }
  }
  // 카드 선택 결과
  .space-card__result {
    position: relative;
    display: flex;
    flex-direction: column;
    width: 100%;
    // Android 6 등 구형 브라우저 대응: clamp() 미지원 시 fallback
    // .space-card__default보다 높이가 더 크므로 다른 값 사용
    // 600px 기준, 375px 화면에서 약 160vw
    min-height: 160vw; // fallback: 최소값 (600px 기준)

    // clamp() 지원 브라우저에서만 적용
    @supports (height: clamp(1px, 1px, 1px)) {
      // 가로 사이즈에 비례해서 높이가 조정되도록 vw 단위 사용
      // 최소 높이 보장 (600px 기준, 375px 화면에서 약 160vw)
      min-height: clamp(160vw, 50vw, 200vw);
    }
    border-radius: var(--radius-xl);
    // background-image: url(#{$cdn-url}/images/pages/auth/space_card_result_bg.png);
    background-image: url(#{$cdn-url}/images/pages/auth/space_card_result_bg.jpg);
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
    text-align: center;
    padding: var(--spacing-4xl) var(--spacing-2xl);

    .space-card__result-figure {
      position: relative;
    }
    .space-card__result-title {
      text-align: center;
      color: var(--text-secondary);
      span {
        display: block;
        @include font-set("title-s", 300);
        font-weight: 300;
        color: var(--brand-200);
      }
      strong {
        display: block;
        @include font-set("title-xl", 700);
        font-weight: 700;
        color: var(--text-ondark_primary-same);
      }
    }
    .space-card__result-image-container {
      position: relative;
      width: 100%;
      min-height: 200px;
      min-width: 176px;
      max-width: 100%;
      max-height: 280px;
      margin: var(--spacing-2xl) auto;
      &::before {
        content: "";
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        max-height: 280px;
        background: url(#{$cdn-url}/images/pages/auth/space_universe_orbit_bg.png) no-repeat center
          center;
        background-size: contain;
        z-index: 0;
      }
      img {
        position: relative;
        width: 100%;
        height: auto;
        max-height: 280px;
        object-fit: contain;
        display: block;
        z-index: 1;
      }
    }
    .space-card__result-caption {
      @include font-set("body-m", 300);
      font-weight: 300;
      color: var(--text-ondark_primary-same);
    }
    .space-card__result-actions {
      display: flex;
      justify-content: center;
      margin-top: var(--spacing-2xl);
      text-align: center;
      .space-card__result-button {
        display: flex;
        flex-shrink: 0;
        justify-content: center;
        align-items: center;
        gap: var(--spacing-sm, 4px);
        height: 38px;
        padding: var(--spacing-lg, 12px);
        border-radius: var(--radius-full, 9999px);
        border: 1px solid #c697ff;
        background: linear-gradient(96deg, #7026c6 0%, #3a80e1 100%);

        color: var(--text-ondark_primary-same, #fff);
        @include font-set("body-m", 500);
        font-weight: 500;
        text-align: center;
      }
    }
  }
  // 카드 선택 배경의 별 효과
  .star {
    position: absolute;
    z-index: 5;
    transform-origin: center;
    display: block;
    border-radius: 50%;
    background-color: #fff;
    animation: twinkle infinite ease-in-out;
    &:after {
      content: "";
      position: absolute;
      top: 0rem;
      left: 0rem;
      width: 100%;
      height: 100%;
      background-color: #fff;
      border-radius: 50%;
      filter: blur(2px);
      backdrop-filter: blur(2px);
      -webkit-backdrop-filter: blur(2px);
    }
  }
  @keyframes twinkle {
    0% {
      opacity: 1;
      transform: scale(1);
    }
    50% {
      opacity: 0.3;
      transform: scale(0.5);
    }
    100% {
      opacity: 1;
      transform: scale(1);
    }
  }
  // 월별 선택 탭
  .space-card__subtabs {
    display: flex;
    gap: var(--spacing-md);
    overflow-x: auto;
    margin-left: -20px;
    margin-right: -20px;
    padding: var(--spacing-3xl) 0 0;
    background-color: var(--bg-white);
    -webkit-overflow-scrolling: touch;
    scrollbar-width: none;
    &::-webkit-scrollbar {
      display: none;
    }
    &.is-sticky {
      position: sticky;
      top: calc(var(--sc-header-height) - var(--spacing-2xl));
      z-index: 1;
    }
  }
  .space-card__tab {
    display: grid;
    grid-template-rows: auto auto;
    justify-items: center;
    align-items: center;
    gap: var(--spacing-sm);
    padding: var(--spacing-xl) 0;
    cursor: pointer;
    &:first-child {
      margin-left: 20px;
    }
    &:last-child {
      margin-right: 20px;
    }
    .space-card__tab-image {
      position: relative;
      width: 62px;
      height: 62px;
      border-radius: 50%;
      overflow: visible;
      background: var(--bg-white);
      img {
        position: absolute;
        top: 50%;
        left: 50%;
        z-index: 1;
        transform: translate(-50%, -50%);
        width: 50px;
        height: 50px;
        object-fit: cover;
        display: block;
        border-radius: 50%;
        opacity: 0.4;
      }
      &::before {
        content: "";
        position: absolute;
        top: 50%;
        left: 50%;
        z-index: 0;
        transform: translate(-50%, -50%);
        width: calc(100% - 6px);
        height: calc(100% - 6px);
        border-radius: 50%;
        background: var(--bg-white);
      }
    }
    .space-card__tab-label {
      @include font-set("body-m", 300);
      font-weight: 300;
      color: var(--text-disabled-same);
      white-space: nowrap;
    }
    &.is-active {
      .space-card__tab-image {
        background: linear-gradient(90deg, #1fa7e2 0%, #cc3fff 100%);
        img {
          opacity: 1;
        }
      }
      .space-card__tab-label {
        color: var(--text-primary);
        font-weight: 700;
      }
    }
  }
  .space-card__list {
    margin: var(--spacing-3xl) 0 0;
    padding: 0;
    .space-card__list-item {
      & ~ .space-card__list-item {
        margin-top: var(--spacing-lg);
      }
    }
    .sv-card__content .sv-list__item_inner .sv-list__icon {
      width: 108px;
      height: 108px;
    }
    .sv-icon {
      color: var(--text-quaternary);
      svg {
        color: var(--text-quaternary);
      }
    }
  }
}
.space-card__details {
  .space-card__details-image-container {
    max-width: 375px;
    height: 218px;
    margin-bottom: var(--spacing-xl);
    padding: 0 var(--spacing-5xl);
    text-align: center;
    img {
      width: auto;
      height: 100%;
      object-fit: contain;
    }
  }
  .space-card__details-title {
    text-align: center;
    color: var(--text-secondary);
    span {
      display: block;
      @include font-set("title-s", 500);
      font-weight: 500;
      color: var(--text-primary);
    }
    strong {
      display: block;
      @include font-set("title-l", 700);
      font-weight: 700;
      color: var(--text-primary);
    }
  }
  .space-card__details-caption {
    margin-top: var(--spacing-3xl);
    padding: var(--spacing-xl);
    border-radius: var(--radius-md);
    background-color: var(--bg-graylight);
    @include font-set("body-m", 300);
    font-weight: 300;
    color: var(--text-tertiary);
  }
}


// utilits sc-infobox 다름라인

// 개별 방향 offset (해당 속성이 있을 때만 적용)
// 사용자가 선택한 property 타입에 따라 CSS 속성이 동적으로 적용됨
// data-offset-target 속성으로 타겟 클래스 지정 가능 (예: .sv-popover)
$directions: (
  "top": "top",
  "bottom": "bottom",
  "left": "left",
  "right": "right",
);

@each $direction, $css-prop in $directions {
  // 기본: position 속성 (top, bottom, left, right)
  // CSS 변수에 attr() 사용하여 data 속성 값 읽기
  [data-offset-#{$direction}]:not([data-offset-#{$direction}-property]) {
    // CSS 변수에 attr() 사용 (단위 포함)
    --offset-#{$direction}: attr(data-offset-#{$direction} px);

    // .sv-popover (하위 요소)
    .sv-popover {
      #{$css-prop}: var(--offset-#{$direction}) !important;
      z-index: 10 !important;
    }

    // 사용자 지정 타겟 (data-offset-target 속성으로 지정)
    // data-offset-target="self"인 경우 본인 요소에 적용
    &[data-offset-target="self"] {
      #{$css-prop}: var(--offset-#{$direction}) !important;
    }

    // data-offset-target에 클래스가 지정된 경우
    // JavaScript에서 설정한 CSS 변수를 사용하여 타겟 요소에 적용
    &[data-offset-target] {
      // JavaScript에서 설정한 CSS 변수 사용 (없으면 기본 변수 사용)
      * {
        #{$css-prop}: var(--offset-target-#{$direction}, var(--offset-#{$direction})) !important;
      }
    }
  }

  // margin 속성 사용 시
  [data-offset-#{$direction}][data-offset-#{$direction}-property="margin"] {
    --offset-#{$direction}: attr(data-offset-#{$direction} px);

    &[data-offset-target="self"] {
      margin-#{$css-prop}: var(--offset-#{$direction}) !important;
    }

    &[data-offset-target] {
      * {
        margin-#{$css-prop}: var(
          --offset-target-#{$direction},
          var(--offset-#{$direction})
        ) !important;
      }
    }
  }

  // padding 속성 사용 시
  [data-offset-#{$direction}][data-offset-#{$direction}-property="padding"] {
    --offset-#{$direction}: attr(data-offset-#{$direction} px);

    &[data-offset-target="self"] {
      padding-#{$css-prop}: var(--offset-#{$direction}) !important;
    }

    &[data-offset-target] {
      * {
        padding-#{$css-prop}: var(
          --offset-target-#{$direction},
          var(--offset-#{$direction})
        ) !important;
      }
    }
  }

  // transform 속성 사용 시
  [data-offset-#{$direction}][data-offset-#{$direction}-property="transform"] {
    --offset-#{$direction}: attr(data-offset-#{$direction} px);

    &[data-offset-target="self"] {
      @if $direction == "top" {
        transform: translateY(calc(var(--offset-#{$direction}) * -1)) !important;
      } @else if $direction == "bottom" {
        transform: translateY(var(--offset-#{$direction})) !important;
      } @else if $direction == "left" {
        transform: translateX(calc(var(--offset-#{$direction}) * -1)) !important;
      } @else {
        transform: translateX(var(--offset-#{$direction})) !important;
      }
    }

    &[data-offset-target] {
      * {
        @if $direction == "top" {
          transform: translateY(
            calc(var(--offset-target-#{$direction}, var(--offset-#{$direction})) * -1)
          ) !important;
        } @else if $direction == "bottom" {
          transform: translateY(
            var(--offset-target-#{$direction}, var(--offset-#{$direction}))
          ) !important;
        } @else if $direction == "left" {
          transform: translateX(
            calc(var(--offset-target-#{$direction}, var(--offset-#{$direction})) * -1)
          ) !important;
        } @else {
          transform: translateX(
            var(--offset-target-#{$direction}, var(--offset-#{$direction}))
          ) !important;
        }
      }
    }
  }
}

// 툴팁 닫히는 효과 class hide-close가 있는 곳 아래 요소에 적용 예) .hide-close .sv-popover
// 방향별로 애니메이션 적용
@each $direction, $css-prop in $directions {
  .hide-close {
    // top 방향일 때는 아래로 사라지는 애니메이션
    @if $direction == "top" {
      .sv-popover--placement-top-left,
      .sv-popover--placement-top-center,
      .sv-popover--placement-top-right {
        animation: tooltip-fade-down 0.5s forwards;
        -webkit-animation-delay: 3s;
        animation-delay: 3s;
      }
    }
    // bottom 방향일 때는 위로 사라지는 애니메이션
    @else if $direction == "bottom" {
      .sv-popover--placement-bottom-left,
      .sv-popover--placement-bottom-center,
      .sv-popover--placement-bottom-right {
        animation: tooltip-fade-up 0.5s forwards;
        -webkit-animation-delay: 3s;
        animation-delay: 3s;
      }
    }
  }
}


```
