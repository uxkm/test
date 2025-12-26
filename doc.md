# test

{% raw %}
```scss

/* 혜택 - 메인 */
.benefits_main {
  padding: 0;
}
.bf {
  &-main {
    section ~ section,
    section ~ .sv-divider {
      margin-top: 0;
    }
    section ~ .bf-banner-group,
    section ~ .bf-quiz-pangpang {
      margin-top: var(--spacing-4xl);
    }
    .bg-gray {
      background-color: var(--bg-canvas_gray_light);
    }
    .title-sub {
      @include font-set(title-l, 700);
      font-weight: 700;
      color: var(--text-primary);
    }
    .bf-section__header {
      margin-bottom: var(--spacing-lg);
      .description {
        display: block;
        @include font-set(body-s, 500);
        font-weight: 500;
        color: var(--text-quaternary);
        ~ .title-sub {
          margin-top: var(--spacing-xs);
        }
      }
    }
    .bf-section__footer {
      display: flex;
      justify-content: center;
      margin-top: var(--spacing-lg);
      .sv-button--size-m {
        padding-right: var(--spacing-lg);
        padding-left: var(--spacing-lg);
      }
    }
    .cupon-chip {
      .sv-chip-group {
        padding: 0;
        .sv-chip-group__container {
          gap: var(--spacing-md);
        }
      }
    }
    .export-banner {
      width: 100%;
      height: auto;
      object-fit: contain;
    }
    .bf-if__error,
    .bf-if__login {
      padding: 0 var(--container-padding-mobile);
      &.h344 {
        .bf-if__error-inner {
          height: 344px;
        }
      }
      &-inner {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        padding: var(--spacing-2xl);
        border-radius: var(--radius-xl);
        border: 1px solid var(--border-secondary);
        background-color: var(--bg-canvas_white);
      }
      &-icon {
        width: 48px;
        height: 48px;
        img {
          width: 100%;
          height: 100%;
          object-fit: contain;
        }
      }
      &-text {
        margin-top: var(--spacing-md);
        @include font-set(body-s, 300);
        font-weight: 300;
        color: var(--text-quaternary);
      }
      .sv-button {
        width: auto;
        margin-top: var(--spacing-xl);
      }
      .sv-button--size-s {
        padding-right: var(--spacing-lg);
        padding-left: var(--spacing-lg);
      }
    }
  }
  // 혜택 대시보드
  &-benefit-dashboard {
    padding-top: var(--spacing-sm);
    padding-bottom: var(--spacing-5xl);
    .dashboard-divider {
      margin-top: var(--spacing-lg);
      margin-bottom: var(--spacing-lg);
    }
    .dashboard-box {
      position: relative;
      margin-right: var(--container-padding-mobile);
      margin-left: var(--container-padding-mobile);
      padding: 2px;
      border-radius: var(--radius-xl);
      background: linear-gradient(
        90.98deg,
        var(--border-indigo-same) 1.84%,
        var(--border-blue) 53.05%,
        var(--border-indigo-same) 98.92%
      );
      /* Shadow 1 */
      box-shadow: 0 4px 16px 0 rgba(12, 17, 29, 0.06);

      &__inner {
        // min-height: calc(130px - 4px);
        border-radius: var(--radius-xl);
        padding: calc(var(--spacing-2xl) - 2px) calc(var(--spacing-2xl) - 2px)
          calc(var(--spacing-xl) - 2px);
        background-color: var(--bg-canvas_white);
        em {
          font-style: normal;
        }
        @media (max-width: 320px) {
          padding-right: 16px;
          padding-left: 16px;
        }
      }
      .dashboard-body {
        display: grid;
        grid-template-columns: 1fr auto 1fr;
        align-items: center;
        .dashboard-divider-vertical {
          height: 100%;
          margin: 0 var(--spacing-xl);
          align-self: stretch;
        }
        &__link {
          display: flex;
          flex-direction: column;
          align-items: flex-start;
          padding: 0;
        }
        &__label {
          display: flex;
          align-items: center;
          @include font-set(body-s, 300);
          font-weight: 300;
          color: var(--text-secondary);
          .sv-icon {
            flex-shrink: 0;
            margin-left: var(--spacing-sm);
            color: var(--fg-quaternary);
          }
        }
        &__value {
          margin-top: var(--spacing-sm);
          @include font-set(title-l, 700);
          font-weight: 700;
          color: var(--text-secondary);
          white-space: nowrap;
          // 기본: 16px (title-m) - 천만원대 이상 1억 미만
          @include font-set(title-m);
          font-weight: 700;
          // 천만원대 이하: 18px (title-l)
          &--large {
            @include font-set(title-l);
          }
          // 1억 이상: 14px (title-s)
          &--small {
            @include font-set(title-s);
          }
          @media (max-width: 320px) {
            width: 100%;
            height: 29px;
            .sv-loading-skeleton {
              width: 100% !important;
            }
          }
        }
        &__error {
          display: flex;
          align-items: center;
          justify-content: space-between;
          padding-top: var(--spacing-lg);
          padding-bottom: var(--spacing-lg);
        }
        &__error-text {
          @include font-set(body-s, 300);
          font-weight: 300;
          color: var(--text-quaternary);
        }
      }
      .dashboard-footer {
        &__list {
          display: flex;
          align-items: center;
          justify-items: space-between;
          padding: 0;
          .dashboard-membership__icon {
            width: 16px;
            height: 16px;
            line-height: 0;
            img {
              width: 100%;
              height: 100%;
              object-fit: contain;
            }
          }
          .sv-divider {
            flex-shrink: 0;
            margin: 0 var(--spacing-xl);
          }
          .sv-divider--orientation-vertical.sv-divider--color-tertiary
            .sv-divider__item {
            background-color: var(--border-primary_strong-same);
            opacity: 0.3;
          }
          .dashboard-divider-vertical {
            height: 12px;
          }
          .sv-button__label {
            white-space: nowrap;
          }
          // "참여한 이벤트" 버튼만 줄바꿈 허용 (마지막 항목)
          .dashboard-footer__item:last-of-type .sv-button__label {
            white-space: normal;
            word-break: keep-all;
          }
          // 툴팁 위치 디자인과 동기화
          .sc-popover__custom {
            &[data-placement="bottom-left"] {
              top: calc(100% + 10px);
              left: 6px;
              &::after {
                left: 16px;
              }
            }
            &[data-placement="bottom-center"] {
              top: calc(100% + 10px);
              margin-left: -10px;
            }
            &[data-placement="bottom-right"] {
              top: calc(100% + 10px);
              right: 18px;
              &::after {
                right: 18px;
              }
            }
          }
        }
        &__item {
          display: flex;
          align-items: center;
          justify-content: center;
          flex: 1 1 auto;
          position: relative;
          text-align: center;
        }
        &__link {
          flex: 1 1 auto;
          align-items: center;
        }
        .sv-button--size-s.sv-button--variant-ghost .sv-button__left-icon,
        .sv-button--size-m.sv-button--variant-ghost .sv-button__left-icon {
          width: auto !important;
          height: auto !important;
        }
      }
    }
  }
  // 추천 혜택
  &-recommend-benefit {
    &__inner {
      position: relative;
      padding: 0;
      .title-sub {
        margin-bottom: var(--spacing-lg);
      }
      &.skeleton {
        padding: 0 var(--container-padding-mobile);
        .bf-recommend-benefit__intro {
          height: auto;
          margin: var(--spacing-lg) 0 0;
          padding: 0;
          background: transparent;
          &::before,
          &::after {
            display: none;
          }
        }
      }
    }
    &__intro {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      position: relative;
      height: 214px;
      margin: 0 var(--container-padding-mobile);
      padding: var(--spacing-4xl) 0;
      border-radius: var(--radius-xl);
      background:
        linear-gradient(
          221deg,
          var(--bg-brand_strong-same, rgba(0, 93, 249, 0.08)) 7.99%,
          rgba(0, 93, 249, 0) 54.28%
        ),
        var(--bg-canvas_gray_a50, rgba(240, 244, 250, 0.5));
      text-align: center;
      transition: opacity 0.2s ease-in;
      &[hidden] {
        position: absolute;
        top: 0;
        left: 0;
        z-index: -1;
        width: 0;
        height: 0;
        padding: 0;
        pointer-events: none;
      }
      &::before {
        content: "";
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: var(--bg-canvas_gray_a50);
      }
      &::after {
        content: "";
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: var(--bg-canvas_white_a70-elevated);
      }
    }
    &__button {
      position: relative;
      z-index: 1;
      width: 150px;
      height: 150px;
      margin-top: 40px;
      line-height: 0;
      img {
        width: 100%;
        height: 100%;
        max-width: 150px;
        max-height: 150px;
        object-fit: contain;
      }
    }
    .tooltip-recommend-benefit {
      position: absolute;
      top: -40px;
      left: 50%;
      transform: translateX(-50%);
      z-index: 1;
      width: 128px;
      height: 66px;
      padding: 0;
      animation: tooltipBouncy 3s ease-in-out infinite;
      .bg-tooltip {
        position: absolute;
        top: 0;
        left: 0;
      }
      .tooltip-custom__text {
        position: absolute;
        top: 16px;
        left: 50%;
        transform: translateX(-50%);
        z-index: 1;
        @include font-set(body-s, 500);
        font-weight: 500;
        color: var(--text-secondary);
        white-space: nowrap;
      }
    }
    &__body {
      padding: 0 var(--container-padding-mobile);
      opacity: 0;
      &.is-visible {
        animation: bodyFadeIn 300ms ease-in forwards 10ms;
      }
      .webzine-list {
        li {
          opacity: 0;
          &.is-visible {
            animation: itemFadeIn 200ms ease-in forwards;
            @for $i from 1 through 3 {
              &:nth-child(#{$i}) {
                animation-delay: #{$i * 600}ms;
              }
            }
          }
        }
      }
      .sv-pagination {
        margin-top: var(--spacing-3xl);
        display: none;
        opacity: 0;
        &.is-visible {
          display: block;
          animation: paginationFadeIn 300ms ease-in forwards;
          opacity: 1;
        }
      }
    }
  }
  // 배너그룹
  &-banner-group {
    margin-top: var(--spacing-4xl);
    padding: 0 var(--container-padding-mobile);
  }
  // 인라인 배너
  &-inline-banner {
    &__item {
      display: block;
      position: relative;
      ~ .bf-inline-banner__item {
        margin-top: var(--spacing-md);
      }
    }
    &__link {
      display: block;
      position: relative;
    }
    .sv-infobox--color-info {
      background-color: var(--bg-ongray_gray_a10);
    }
    .sv-icon-button {
      position: absolute;
      top: 50%;
      right: calc(24px - var(--spacing-xl));
      transform: translateY(-50%);
      width: 32px;
      height: 32px;
      color: var(--fg-tertiary);
      &:active:not(:disabled) {
        position: absolute;
        transform: translateY(-50%) scale(0.96);
      }
      &.sv-icon-button--size-s .sv-icon-button__icon-container {
        width: 16px !important;
        height: 16px !important;
        .sv-icon {
          width: 16px !important;
          height: 16px !important;
        }
      }
    }
    .infobox-bell,
    .infobox-gift {
      .sv-infobox__header {
        padding: var(--spacing-lg) var(--spacing-xl);
      }
      .sv-infobox__header-label {
        position: relative;
        padding-left: calc(var(--spacing-2xl) + var(--spacing-sm));
        padding-right: var(--spacing-4xl);
        @include font-set(body-s, 300);
        font-weight: 300;
        color: var(--text-tertiary);
        &::before,
        &::after {
          content: "";
          position: absolute;
          top: 50%;
          left: 0;
          transform: translateY(-50%);
          width: 20px;
          height: 20px;
          border-radius: var(--radius-full);
          background-color: var(--bg-canvas_white);
        }
        &::after {
          left: 3px;
          width: 14px;
          height: 14px;
          background-repeat: no-repeat;
          background-position: center;
          background-size: contain;
          background-image: url(#{$cdn-url}/images/pages/benefits/main/Bell.png);
        }
      }
    }
    .infobox-gift {
      .sv-infobox__header-label {
        &::after {
          background-image: url(#{$cdn-url}/images/pages/benefits/main/Gift.png);
        }
      }
    }
    ~ .bf-recommend-banner {
      margin-top: var(--spacing-3xl);
    }
  }
  // 추천 배너
  &-recommend-banner {
    &__inner {
      &.skeleton {
        display: flex;
        flex-direction: column;
        align-items: center;
        .sv-loading-skeleton ~ .sv-loading-skeleton {
          margin-top: var(--spacing-lg);
        }
      }
    }
    // 캐러셀 스타일
    .bf-recommend-banner-carousel {
      width: 100%;
      overflow: hidden;
      .swiper {
        overflow: hidden;
        width: 100%;
      }
      .swiper-wrapper {
        display: flex;
      }
      .swiper-slide {
        height: auto;
        flex-shrink: 0;
        width: 100%;
      }
    }

    &__text {
      flex: 1;
      display: flex;
      flex-direction: column;
      padding-right: var(--spacing-lg);
      color: var(--white);
    }
    &__title {
      @include ellipsis(2);
      @include font-set(title-m, 700);
      font-weight: 700;
      color: var(--text-primary);
      white-space: pre-line;
      word-break: keep-all;
    }
    &__subtitle {
      display: flex;
      align-items: center;
      margin-top: var(--spacing-sm);
      @include ellipsis(2);
      @include font-set(body-s, 500);
      font-weight: 500;
      color: var(--text-quaternary);
      .days {
        font-style: normal;
      }
    }
    &__image {
      display: flex;
      align-items: center;
      justify-content: center;
      flex-shrink: 0;
      width: 80px;
      height: 80px;
      img {
        display: block;
        max-width: 100%;
        max-height: 100%;
        object-fit: contain;
      }
    }
    &__slide {
      display: block;
      width: 100%;
      text-decoration: none;
    }
    &__content {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: var(--spacing-md) var(--spacing-xl);
      border-radius: var(--radius-xl);
      background: var(--bg-banner_gray_solid);
      box-sizing: border-box;
      min-height: 96px;
      &[data-color="bg-banner_gray-solid-same"],
      &[data-color="bg-banner_indigo_solid-same"],
      &[data-color="bg-banner_brand_solid"] {
        height: 136px;
        padding: var(--spacing-xl);
        .bf-recommend-banner__text {
          padding-right: 0;
        }
        .bf-recommend-banner__image {
          width: 104px;
          height: 104px;
        }
      }
      &[data-color="bg-banner_gray-solid-same"] {
        background: var(--bg-banner_gray_solid-same);
        .bf-recommend-banner__title,
        .bf-recommend-banner__subtitle {
          color: var(--text-ondark_primary-same);
        }
      }
      &[data-color="bg-banner_indigo_solid-same"] {
        background: var(--bg-banner_indigo_solid-same);
        .bf-recommend-banner__title,
        .bf-recommend-banner__subtitle {
          color: var(--text-ondark_primary-same);
        }
      }
      &[data-color="bg-banner_brand_solid"] {
        background: var(--bg-banner_brand_solid);
      }
    }
    // 캐러셀 네비게이션 및 페이지네이션 스타일
    .sv-carousel__controls {
      margin: 0;
      padding: var(--spacing-lg) 0;
    }
    .sv-carousel__navigation-prev,
    .sv-carousel__navigation-next {
      color: var(--text-tertiary);
    }
    .sv-pagination__number-navi {
      height: 24px;
      padding: 0 var(--spacing-lg);
      border-radius: var(--radius-md);
    }
    .sv-pagination--color-fixed-black .sv-pagination__number-navi {
      background-color: var(--bg-gray);
      .sv-icon-button:not(:disabled) {
        color: var(--fg-tertiary);
      }
      .sv-pagination__number-text {
        color: var(--text-placeholder-same);
      }
      .sv-pagination__number-current {
        color: var(--text-quaternary);
      }
    }
    .sv-pagination__number-navi + .sv-icon-button {
      margin-left: var(--spacing-lg);
    }
    .sv-pagination--color-fixed-black > .sv-icon-button {
      color: var(--fg-quaternary);
      .sv-icon-button__icon-container:before {
        background-color: var(--bg-gray);
      }
    }
  }
  // 퀴즈팡팡
  &-quiz-pangpang {
    margin-bottom: var(--spacing-4xl);
    padding: 0;
    &__contents {
      margin-right: var(--container-padding-mobile);
      margin-left: var(--container-padding-mobile);
      padding: var(--spacing-2xl);
      border-radius: var(--radius-xl);
      border: 1px solid var(--border-secondary);
      background: var(--bg-canvas_white);
    }
    &__contents-header {
      display: grid;
    }
    &__contents-body {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: var(--spacing-md);
      margin-top: var(--spacing-3xl);
      margin-bottom: var(--spacing-3xl);
      &.question {
        display: flex;
        flex-direction: column;
        margin-bottom: var(--spacing-4xl);
        .sv-radio-group {
          .sv-radio-group__item-container {
            position: relative;
            min-height: 56px;
            padding: 0;
            border: 1.6px solid var(--border-primary);
            border-radius: var(--radius-xl);
            transition: border-color 0.2s ease-in-out;
            cursor: pointer;
            box-sizing: border-box;

            // 선택된 항목에 is-checked 클래스가 추가되거나, 내부에 checked 상태의 radio-item이 있을 때
            &.is-checked,
            &:has(.sv-radio-item[data-state="checked"]) {
              border-color: var(--text-brand);
              animation: drawBorder 0.25s var(--ease) forwards;
            }
            ~ .sv-radio-group__item-container {
              margin-top: var(--spacing-lg);
            }
          }
          .sv-radio-item {
            position: absolute;
            left: var(--spacing-xl);
            top: 50%;
            transform: translateY(-50%);
          }
          .sv-radio-item__label {
            width: 100%;
            margin: 0;
            label {
              width: 100%;
              padding: var(--spacing-xl);
              padding-left: calc(var(--spacing-xl) + 24px + var(--spacing-md));
              @include font-set(title-s, 500);
              font-weight: 500;
              color: var(--text-secondary);
            }
          }
        }
      }
    }
    &__contents-footer {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      column-gap: var(--spacing-md);
      row-gap: var(--spacing-lg);
      position: relative;
      .bf-quiz-pangpang__contents-item {
        &:nth-child(3) {
          grid-column: 1 / -1;
        }
      }
      .sv-infobox--color-info {
        background-color: transparent;
      }
      .sv-infobox--size-small .sv-infobox__header {
        padding: 0;
      }
      .sv-infobox__header-label {
        justify-content: center;
        text-align: center;
      }
    }
    &__contents-result {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: space-between;
      margin-right: var(--container-padding-mobile);
      margin-left: var(--container-padding-mobile);
      padding: var(--spacing-2xl);
      border-radius: var(--radius-xl);
      border: 1px solid var(--border-secondary);
      .bf-quiz-pangpang__contents-header {
        display: flex;
        flex-direction: row;
        width: 100%;
        .bf-quiz-pangpang__title {
          flex: 1 1 auto;
          margin-right: var(--spacing-md);
          @include font-set(title-m, 700);
          font-weight: 700;
          color: var(--text-secondary);
          text-align: left;
        }
        .sv-button {
          flex: 0 0 auto;
          width: auto;
          margin: 0;
          color: var(--text-quaternary);
          .sv-button__label {
            font-weight: 300;
          }
        }
      }
      .bf-quiz-pangpang__contents-body {
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
        width: 100%;
        margin-top: var(--spacing-xl);
        margin-bottom: var(--spacing-xl);
        .sv-button__left-icon {
          flex-shrink: 0;
          margin: 0;
          img {
            width: 100%;
            height: 100%;
            object-fit: contain;
          }
        }
        .sv-button__right-icon {
          flex-shrink: 0;
          color: var(--fg-quaternary);
        }
        .sv-button__label {
          text-align: left;
        }
        .sv-button--size-s.sv-button--variant-ghost .sv-button__left-icon {
          width: 36px !important;
          height: 36px !important;
        }
        .level-button {
          flex: 0 0 auto;
          justify-content: flex-start;
          width: auto;
          margin: 0;
          .sv-button__label,
          .level-label {
            justify-content: flex-start;
            @include font-set(body-m, 500);
            font-weight: 500;
            color: var(--text-secondary);
          }
          .sv-button__label {
            margin-left: var(--spacing-md);
          }
          .sv-button__right-icon {
            margin-left: var(--spacing-sm) !important;
          }
        }
        .level-desc {
          flex: 1 1 auto;
          justify-content: flex-end;
          min-width: 0;
          width: auto;
          margin: 0;
          @include font-set(body-s, 300);
          font-weight: 300;
          color: var(--text-quaternary);
          text-align: right;
        }
      }
      .bf-quiz-pangpang__contents-footer {
        display: block;
        width: 100%;
        .sv-button ~ .sv-button {
          margin-top: var(--spacing-lg);
        }
      }
    }
    &__hint-desc {
      @include font-set(body-s, 300);
      font-weight: 300;
      color: var(--text-tertiary);
      text-align: center;
    }
    &__title {
      margin-bottom: var(--spacing-xs);
      @include font-set(body-s, 500);
      font-weight: 500;
      color: var(--text-brand);
      text-align: center;
    }
    &__problem-output {
      @include font-set(body-l, 700);
      font-weight: 700;
      color: var(--text-secondary);
      text-align: center;
    }
    &__contents-item {
      position: relative;
    }
    .sv-button {
      width: 100%;
    }
    .sv-icon-button,
    .sv-select-box {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      width: 100%;
      max-height: 100px;
      padding: var(--spacing-2xl);
      padding-bottom: var(--spacing-xl);
      border-radius: var(--radius-lg);
      border: 0;
      &.icon-button-true {
        background-color: var(--bg-gray);
        .sv-icon-button__label {
          color: var(--text-brand);
        }
      }
      &.icon-button-false {
        background-color: var(--bg-negative);
        .sv-icon-button__label {
          color: var(--border-red-same);
        }
        .sv-select-box__border-svg.sv-select-box__border-svg--selected
          .sv-select-box__border-path {
          stroke: var(--border-red-same);
        }
      }
      .sv-select-box__label {
        margin-top: var(--spacing-md);
      }
    }

    .sv-icon-button--size-m.sv-icon-button--label
      .sv-icon-button__icon-container {
      width: 32px !important;
      height: 32px !important;
    }
    .hint-badge {
      position: absolute;
      top: -14px;
      left: 50%;
      transform: translateX(-50%);
      z-index: 1;
      border-radius: var(--radius-full);
      box-shadow: 4px 4px 4px 0 rgba(0, 0, 0, 0.06);
      backdrop-filter: blur(1.5px);
      .sv-base-badge__indicator {
        min-width: 44px;
        height: 22px;
        padding: 0 var(--spacing-sm) 0 var(--spacing-xs);
        border-radius: var(--radius-full);
        border: 1px solid var(--white-a50);
        background: var(--bg-canvas_white_a70-elevated);
      }
      &.sv-base-badge--variant-tint.sv-base-badge--color-gray {
        .sv-base-badge__indicator {
          min-width: 44px;
          height: 22px;
          background: var(--bg-canvas_white_a70-elevated);
          color: var(--text-primary);
        }
      }
      &.sv-base-badge--type-text {
        .sv-base-badge__indicator {
          min-height: auto;
          margin: 0;
          padding: 0 var(--spacing-sm) 0 var(--spacing-xs);
          border-radius: var(--radius-full);
        }
      }
      &-image {
        width: 20px;
        height: 20px;
        margin-right: var(--spacing-xs);
        img {
          width: 100%;
          height: 100%;
          object-fit: contain;
        }
      }
      &-text {
        @include font-set(body-s, 700);
        font-weight: 700;
        color: var(--text-primary);
        white-space: nowrap;
      }
    }
  }
  // 포인트팡팡
  &-point-pangpang {
    margin-right: var(--container-padding-mobile);
    margin-left: var(--container-padding-mobile);
    padding: 0 0 var(--spacing-4xl);
    text-align: center;
    .sv-loading-skeleton {
      margin-right: auto;
      margin-left: auto;
    }

    &__inner {
      position: relative;
    }
    &__contents {
      position: relative;
      z-index: 1;
      padding: var(--spacing-md) 0;
    }
    &__title {
      margin-bottom: var(--spacing-lg);
      @include font-set(body-m, 700);
      font-weight: 700;
      color: var(--text-primary);
      text-align: center;
      span {
        display: block;
        color: inherit;
        font-weight: inherit;
        font-size: inherit;
        line-height: inherit;
        letter-spacing: inherit;
      }
    }
    &__lottie-item {
      position: absolute;
      top: 0;
      z-index: 0;
      width: 80px;
      height: 80px;
      &:first-of-type {
        left: 0;
      }
      &:nth-of-type(2) {
        right: 0;
      }
      // ScLottie 컴포넌트가 래퍼를 생성할 경우를 대비
      &:nth-child(2) {
        right: 0;
      }
    }
  }
  // 혜택 주요 카테고리 진입점
  &-category {
    padding-top: var(--spacing-xl);
    padding-bottom: var(--spacing-xl);
    .category-list {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      align-items: center;
      &__item {
        display: grid;
        align-items: center;
        justify-items: center;
      }
      &__link {
        display: grid;
        align-items: center;
        justify-items: center;
        gap: var(--spacing-md);
        width: 100%;
        max-width: 90px;
        padding: var(--spacing-lg) var(--spacing-sm);
      }
      &__icon {
        width: 36px;
        height: 36px;
        img {
          width: 100%;
          height: 100%;
          object-fit: contain;
        }
      }
      .sv-button--variant-ghost {
        padding: var(--spacing-lg) var(--spacing-sm);
      }
      .sv-button--size-s.sv-button--variant-ghost .sv-button__left-icon,
      .sv-button--size-m.sv-button--variant-ghost .sv-button__left-icon {
        width: auto !important;
        height: auto !important;
      }
      .sv-button--size-s.sv-button--variant-ghost > * + *,
      .sv-button--size-m.sv-button--variant-ghost > * + * {
        margin-left: 0;
      }
    }
  }
  // 앱테크 영역
  &-apptech {
    padding-top: var(--spacing-5xl);
    padding-bottom: var(--spacing-4xl);
    article {
      ~ article {
        margin-top: var(--spacing-5xl);
      }
    }
    .export-banner__link {
      display: block;
      width: 100%;
      height: auto;
      line-height: 0;
    }
  }
  // 이벤트 영역
  &-event {
    padding-top: var(--spacing-4xl);
    padding-bottom: var(--spacing-4xl);
    article {
      ~ article {
        margin-top: var(--spacing-5xl);
      }
    }
    &__list {
      .category-list__body {
        margin-top: var(--spacing-xl);
        .sv-list__icon {
          overflow: visible;
          img {
            max-width: 48px;
            max-height: 48px;
            border-radius: var(--radius-xl);
          }
        }
        .rank-badge {
          display: flex;
          justify-content: center;
          align-items: center;
          position: absolute;
          top: -8px;
          left: -8px;
          z-index: 1;
          width: 20px;
          height: 20px;
          border-radius: var(--radius-full);
          border: 1px solid var(--gray-100);
          background-color: var(--white-a10);
          @include font-set(detail-s, 500);
          font-weight: 500;
          color: var(--text-tertiary);
          backdrop-filter: blur(10px);
          box-shadow: 0px 2px 4px 0px var(--gray-a10);
          backdrop-filter: blur(5px);
        }
      }
    }
  }
  // 이벤트 프로모션
  &-promotion {
    padding-top: var(--spacing-3xl);
    padding-bottom: var(--spacing-3xl);
  }
  // 놓치면 아까운 할인·쿠폰
  &-discount {
    padding-top: var(--spacing-4xl);
    padding-bottom: var(--spacing-5xl);
    .bf-if__error {
      padding: 0;
    }
  }
  // 혜택 서비스
  &-service {
    padding-top: var(--spacing-3xl);
    padding-bottom: var(--spacing-5xl);
    .title-sub {
      @include font-set(title-s, 500);
      font-weight: 500;
      color: var(--text-secondary);
    }
    &__list {
      display: grid;
      grid-template-columns: repeat(4, auto);
      gap: var(--spacing-sm);
      justify-items: start;
      justify-content: start;
      // @media (max-width: 320px) {
      //   grid-template-columns: repeat(2, auto);
      // }

      .sv-button--size-m.sv-button--variant-ghost .sv-button__left-icon {
        width: auto !important;
        height: auto !important;
      }
    }
    &__item,
    .sv-button--variant-ghost {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      width: 70px;
      max-width: 162px;
      margin: 0 auto;
      padding: var(--spacing-xl) var(--spacing-sm) var(--spacing-lg);

      @media (max-width: 320px) {
        max-width: 70px;
      }
    }
    &__icon {
      overflow: hidden;
      width: 32px;
      height: 32px;
      border-radius: var(--radius-xs);
      img {
        width: 100%;
        height: 100%;
        object-fit: contain;
      }
    }
    &__label,
    .sv-button--size-m.sv-button--variant-ghost .sv-button__label {
      margin-top: var(--spacing-sm);
      margin-left: 0;
      @include font-set(body-s, 500);
      font-weight: 500;
      color: var(--text-secondary);
    }
  }
}

/* 혜택 - 앱테크 서브 메인화면 */
.apptech {
  .export-banner {
    width: 100%;
    height: auto;
    object-fit: contain;
  }
  article {
    ~ article {
      margin-top: var(--spacing-5xl);
    }
    ~ .inlifle-banner {
      margin-top: var(--spacing-lg);
    }
  }
  &-title {
    margin-bottom: var(--spacing-lg);
    padding-right: var(--container-padding-mobile);
    padding-left: var(--container-padding-mobile);
    @include font-set(title-l, 700);
    font-weight: 700;
    color: var(--text-primary);
  }
  &-today {
    padding-right: var(--container-padding-mobile);
    padding-left: var(--container-padding-mobile);
    .apptech-title {
      margin: 0;
      padding: 0;
      flex: 1 1 auto;
      min-width: 0;
    }
    &__header {
      display: flex;
      align-items: center;
      gap: var(--spacing-sm);
      margin-bottom: var(--spacing-lg);
    }
    &__actions {
      display: inline-flex;
      align-items: center;

      .action-btn {
        display: inline-flex;
        align-items: center;
        padding: var(--spacing-sm);
        border-radius: var(--radius-xs);

        &:active:not(:disabled) {
          position: relative;
          transform: scale(0.96);
          &:after {
            pointer-events: none;
            content: "";
            overflow: hidden;
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: var(--bg-dark_a10);
            border-radius: inherit;
            animation: svBgOverlayDisplay-c995a15f 0.25s var(--ease);
          }
        }

        &__icon {
          flex-shrink: 0;
          width: 20px;
          height: 20px;
          margin-right: var(--spacing-xs);
        }

        &__text {
          @include font-set("body-m", 300);
          color: var(--text-quaternary);
          white-space: nowrap;
        }
      }

      .sv-divider {
        flex-shrink: 0;

        &--orientation-vertical {
          height: 16px;
          width: 1px;
          margin: 0 var(--spacing-sm);
        }
      }
    }
    &__body {
      margin: 0;
    }
  }

  .banner-item {
    display: flex;
    align-items: center;
    position: relative;
    ~ .banner-item {
      margin-top: var(--spacing-lg);
    }

    &__more {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      position: absolute;
      top: 0;
      right: calc(var(--spacing-2xl) - var(--spacing-xl));
      width: auto;
      height: auto;
      padding: var(--spacing-xl);
      @include font-set(body-s, 500);
      color: var(--text-secondary);
      span {
        text-decoration: underline;
      }
    }

    &.coupang {
      .banner-item__link {
        min-height: 118px;
        padding-right: var(--spacing-2xl);
        background-color: var(--bg-banner_gray_solid);
      }
    }
    &.inlifle {
      .banner-item__link {
        display: block;
        min-height: unset;
        padding: 0;
        background-color: var(--bg-banner_gray_solid);
        line-height: 0;
        .banner-item__img {
          display: block;
          width: 100%;
          height: 100%;
          img {
            width: 100%;
            height: 100%;
            min-height: 118px;
            border-radius: var(--radius-xl);
            object-fit: cover;
          }
        }
        .banner-item__actions {
          align-self: unset;
          position: absolute;
          bottom: var(--spacing-xl);
          right: var(--spacing-2xl);
          width: auto;
          height: auto;
          padding: 0;
        }
      }
      .banner-item__more {
        color: var(--text-ondark_primary);
      }
    }

    &__link {
      overflow: hidden;
      display: flex;
      align-items: center;
      width: 100%;
      min-height: 82px;
      padding: 0 var(--spacing-2xl);
      padding-right: 15px;
      border-radius: var(--radius-xl);
      background-color: var(--bg-banner_brand_solid);
    }
    &__img {
      width: 77px;
      height: 77px;
      img {
        width: 100%;
        height: 100%;
        object-fit: contain;
      }
      ~ .today-mission__label {
        margin-left: var(--spacing-lg);
      }

      &.row-flex {
        display: inline-flex;
        flex: 1 1 auto;
        justify-content: flex-start;
        min-width: 0;
        width: auto;
        height: auto;

        img {
          width: 86px;
          height: 86px;
          border-radius: var(--radius-xs);
          ~ img {
            margin-left: var(--spacing-md);
          }
        }
      }
    }
    &__label {
      display: flex;
      flex-direction: column;
      min-width: 0;
      flex: 1 1 auto;
      span,
      strong {
        display: block;
      }
    }
    &__actions {
      display: flex;
      flex-shrink: 0;
      flex-direction: column;
      align-items: flex-end;
      justify-content: flex-end;
      align-self: stretch;
      padding-bottom: var(--spacing-xl);
      .logo {
        display: inline-flex;
        img {
          width: 100%;
          max-width: 65px;
          height: auto;
          object-fit: contain;
        }
      }
      .point-badge {
        margin-top: var(--spacing-md);
      }
    }
  }
  // 오늘의 미션
  .today-mission {
    padding: 0 var(--container-padding-mobile);
  }

  // 인라이플 배너
  .inlifle-banner {
    padding: 0 var(--container-padding-mobile);
  }

  // 애드팝콘 배너
  .adpicon-banner {
    position: relative;
    margin-top: var(--spacing-5xl);
    .sv-carousel__navigation-prev,
    .sv-carousel__navigation-next {
      display: none;
      margin-top: 0;
    }
    .sv-carousel__controls {
      margin-top: 0;
      padding: var(--spacing-xl) 0;
    }

    &__carousel {
      img {
        width: 100%;
      }
    }

    &__card-inner {
      background: var(--bg-canvas_white);
      box-shadow: 0 4px 16px 0 rgba(12, 17, 29, 0.06);
      margin: 0;
    }
    &__card-visual {
      display: block;
      overflow: hidden;
      width: 100%;
      height: 100%;
      line-height: 0;
      font-size: 0;
      margin: 0;
      padding: 0;
      img {
        display: block;
        width: 100%;
        height: 100%;
        margin: 0;
        padding: 0;
        border: 0;
        border-radius: var(--radius-lg) var(--radius-lg) 0 0;
        object-fit: cover;
      }
    }

    &__card {
      display: flex;
      flex-direction: column;
      gap: var(--spacing-md);
      width: 100%;
      min-width: 0;
    }

    &__content {
      display: flex;
      flex-direction: column;
      width: fit-content;
      min-width: 0;
      padding: var(--spacing-xl);
      border-radius: 0 0 var(--radius-lg) var(--radius-lg);
      border: 1px solid var(--border-secondary);
      border-top: none;
    }
    &__title {
      @include font-set(title-m, 500);
      font-weight: 500;
      color: var(--text-secondary);
      @include ellipsis(1);
    }
    &__description {
      margin-top: var(--spacing-xs);
      @include font-set(body-s, 300);
      color: var(--text-quaternary);
      @include ellipsis(2);
    }
    &__actions {
      display: inline-flex;
      flex-direction: column;
      gap: var(--spacing-md);
      width: fit-content;
      max-width: fit-content;
      align-self: flex-end;
      flex-shrink: 0;
      margin-top: var(--spacing-md);
    }
    &__more {
      position: absolute;
      bottom: var(--spacing-lg);
      right: 0;
      width: auto;
      height: auto;
      padding: 0;
    }
  }
}

/* 혜택 - 이벤트 서브 메인화면 */
.p_events {
  .title-sub {
    display: flex;
    align-items: center;
    position: relative;
    padding-right: 28px;
    @include font-set(title-l, 700);
    font-weight: 700;
    color: var(--text-primary);
    .more-btn {
      position: absolute;
      top: 0;
      right: 0;
      width: 100%;
      height: 28px;
      flex-direction: row;
      justify-content: flex-end;
    }
    .sv-icon-button:active:not(:disabled) {
      position: absolute;
      transform: none;
    }
  }
  section ~ section {
    margin-top: var(--spacing-5xl);
  }
}

/* 혜택 - 할인・쿠폰 서브 메인화면 */
.discount-coupon {
  .bg-canvas_gray {
    padding: var(--spacing-xl) var(--container-padding-mobile)
      var(--spacing-4xl);
    background-color: var(--bg-canvas_gray);
    ~ section {
      margin-top: var(--spacing-5xl);
    }
  }
  &__banner {
    display: flex;
    align-items: center;
    position: relative;
    margin-bottom: var(--spacing-2xl);
    padding: var(--spacing-xl) var(--spacing-2xl);
    border-radius: var(--radius-xl);
    background-color: var(--bg-canvas_white);
    .banner-link {
      display: flex;
      align-items: center;
      flex: 1 1 auto;
      min-width: 0;
      margin-right: calc(var(--spacing-2xl) + 20px);
    }
    &-img {
      flex-shrink: 0;
      width: 100%;
      height: 100%;
      max-width: 40px;
      object-fit: contain;
    }
    &-contents {
      display: flex;
      flex-direction: column;
      flex: 1 1 auto;
      min-width: 0;
      margin-left: var(--spacing-md);
    }
    strong {
      @include font-set(title-m, 500);
      font-weight: 500;
      color: var(--text-secondary);
    }
    span {
      @include font-set(body-s, 300);
      font-weight: 300;
      color: var(--text-quaternary);
    }
    p {
      margin-top: var(--spacing-xs);
      @include font-set(body-s, 300);
      color: var(--text-quaternary);
      &.text-bold {
        @include font-set(title-m, 500);
        font-weight: 500;
        color: var(--text-secondary);
      }
    }
    .sv-icon-button {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      right: var(--spacing-md);
      flex-shrink: 0;
      width: 40px;
      height: 40px;
      padding: 0;
      color: var(--fg-quaternary);
      &:active:not(:disabled) {
        position: absolute;
        transform: translateY(-50%) scale(0.96);
      }
    }
    &[data-color="solid-same"] {
      margin-bottom: 0;
      padding: 0 var(--spacing-2xl);
      background-color: transparent;

      .banner-link {
        min-height: 68px;
        margin-right: 0;
        padding: var(--spacing-md) var(--spacing-2xl);
        border-radius: var(--radius-xl);
        background-color: var(--bg-banner_gray_solid-same);
      }
      strong {
        color: var(--text-ondark_primary-same);
      }
      p {
        color: var(--text-ondark_primary-same);
      }
      .discount-coupon__banner-contents {
        margin-right: var(--spacing-md);
        margin-left: 0;
      }
      .discount-coupon__banner-img {
        max-width: 52px;
      }
    }
  }
  &__header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: var(--spacing-lg);
  }
  &__title {
    flex: 1 1 auto;
    min-width: 0;
    @include font-set(title-l, 700);
    font-weight: 700;
    color: var(--text-primary);
  }
  &__search {
    display: flex;
    align-items: center;
    .sv-form-field {
      flex: 1 1 auto;
    }
    .sv-text-input--variant-outline {
      .sv-text-input__container {
        padding-right: 0;
      }
    }
    .sv-text-input__container[data-v-8b742627] > *:not(svg) + * {
      margin-left: 0;
    }
    .sv-text-input__button-slot {
      display: inline-flex;
      align-items: center;
      justify-content: center;
    }
    .sv-icon-button--size-m .sv-icon-button__icon-container {
      width: 20px !important;
      height: 20px !important;
      .sv-icon {
        width: 20px !important;
        height: 20px !important;
      }
    }
    .sv-icon-button {
      width: auto;
      height: 38px;
      padding-right: var(--spacing-xl);
      padding-left: var(--spacing-lg);
    }
    .sv-icon-button.circle-type {
      flex-shrink: 0;
      width: 36px;
      height: 36px;
      margin-left: var(--spacing-md);
      padding: 0;
      border-radius: 50%;
      border: 1px solid var(--border-tertiary);
    }
  }
  &__body {
    margin-top: var(--spacing-2xl);
  }
}
// 할인 쿠폰 내 맞춤 혜택 도탁
.couponbook-cards__area {
  display: block;
  margin: 0;
  padding: 0;
}
.couponbook-cards {
  display: flex;
  flex-direction: column;
  padding: var(--spacing-4xl) var(--spacing-2xl) var(--spacing-2xl);
  border-radius: var(--radius-xl);
  background-color: var(--bg-canvas_white);
  &__head {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin-bottom: var(--spacing-2xl);
  }
  &__title {
    @include font-set(headline-s, 700);
    font-weight: 700;
    color: var(--text-primary);
    text-align: center;
  }
  &__description {
    margin-top: var(--spacing-sm);
    @include font-set(body-s, 300);
    font-weight: 300;
    color: var(--text-quaternary);
    text-align: center;
    word-break: keep-all;
    word-wrap: break-word;
  }
  &__body {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin-bottom: var(--spacing-2xl);
  }
  &__img {
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    width: 92px;
    height: 92px;
    margin-bottom: var(--spacing-3xl);
    padding: var(--spacing-xl);
    border-radius: var(--radius-2xl);
    background-color: var(--bg-gray);
    img {
      max-width: 100%;
      max-height: 100%;
      object-fit: contain;
    }
  }
  &__content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin-bottom: var(--spacing-2xl);
    strong {
      @include font-set(title-l, 700);
      font-weight: 700;
      color: var(--text-primary);
      @include ellipsis(2);
    }
    p {
      margin-top: var(--spacing-sm);
      @include font-set(body-s, 300);
      color: var(--text-quaternary);
      @include ellipsis(1);
    }
  }
  &__foot {
    display: flex;
    align-items: center;
    justify-content: center;
    .sv-button-group {
      &.column {
        flex-direction: column;
        .sv-button--variant-ghost {
          margin: var(--spacing-2xl) 0 0;
          .sv-button__right-icon {
            width: auto !important;
            height: auto !important;
          }
          .badge-count {
            @include font-set(body-m, 500);
            font-weight: 500;
            color: var(--text-brand);
            font-style: normal;
          }
        }
        .sv-button--variant-underline {
          align-self: center;
          width: auto;
          margin: var(--spacing-2xl) 0 0;
        }
      }
    }
  }
}

// 이벤트 메인에 사용된 이벤트 모음.ZIP 카드 리스트
.collection-card {
  &__header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    position: relative;
    margin-bottom: var(--spacing-lg);
    padding: 0 var(--container-padding-mobile);
    &-left {
      display: flex;
      align-items: center;
      flex: 1 1 auto;
      overflow: hidden;
      position: relative;
      min-width: 0;
    }
    &-right {
      display: flex;
      align-items: center;
      justify-content: flex-end;
      flex-shrink: 0;
    }
  }
  &__list {
    display: grid;
    grid-auto-flow: column;
    grid-auto-columns: 160px;
    column-gap: var(--spacing-lg);
    min-width: 0;
    overflow-x: auto;
    -webkit-overflow-scrolling: touch;
    scrollbar-width: none; // Firefox
    padding-left: var(--spacing-2xl);
    padding-right: var(--spacing-2xl);
    &::-webkit-scrollbar {
      display: none; // Chrome, Safari
    }
    &.skeleton {
      overflow: hidden;
      grid-auto-columns: minmax(160px, 1fr);
      margin: 0;
      padding: 0;
      padding-left: var(--container-padding-mobile);
      .collection-card__item {
        margin: 0;
        padding: 0;
        min-width: 160px;
        width: 100%;
      }
    }
  }
  &__item {
    width: 160px;
    height: 228px;
    background-repeat: no-repeat;
    background-position: center center;
    padding: 38px var(--spacing-2xl) var(--spacing-xl);
    img {
      width: 86px;
      height: 86px;
    }
  }
  &__item-content {
    margin-top: var(--spacing-xl);
  }
  &__text-main {
    @include font-set(title-m, 700);
    font-weight: 700;
    color: var(--text-primary-same);
  }
  &__text-sub {
    @include font-set(body-s, 300);
    font-weight: 300;
    color: var(--text-quaternary);
  }
}

/* 혜택 - 이벤트 모음형 페이지 */
.sc-event-collection {
  padding: var(--spacing-5xl) var(--container-padding-mobile);
  background-color: #e2f3fd;
  [data-theme="dark"] & {
    background-color: var(--gray-800);
  }
  .collection-header {
    position: relative;
    padding: 0;
    span,
    strong {
      display: block;
    }
    &__title {
      @include font-set(headline-s, 700);
      font-weight: 700;
      color: var(--text-primary);
    }
    &__title-sub {
      @include font-set(body-m, 300);
      font-weight: 300;
      color: var(--text-secondary);
    }
    img {
      position: absolute;
      top: 50%;
      right: 0;
      transform: translateY(-50%);
      width: 100px;
      height: 100px;
      object-fit: contain;
    }
  }
  .collection-body {
    overflow: hidden;
    position: relative;
    margin-top: var(--spacing-5xl);
    padding-top: 42px;
    border-radius: var(--radius-xl);
    background-color: var(--white-a50);
    [data-theme="dark"] & {
      background-color: var(--white-a5);
    }
    &__header {
      position: absolute;
      top: 0;
      left: 0;
      // 184px ÷ 375px × 100 = 49.07% = width: 50.93% (100% - 49.07%)
      // width: 50.93%;
      width: 100%;
      height: 42px;
      background-repeat: no-repeat;
      background-position: 0 0;
      background-size: auto 42px;
      // background-image: url(#{$cdn-url}/images/pages/benefits/main/bg_event_collection.svg);
      border-top-left-radius: var(--radius-xl);
      .bg_collection-header {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        path[fill="white"] {
          [data-theme="dark"] & {
            background-color: var(--gray-950);
          }
        }
      }
    }
    &__header-title {
      display: flex;
      align-items: flex-end;
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 42px;
      padding: 0 var(--spacing-2xl) var(--spacing-sm);
      white-space: nowrap;
      @include font-set(title-s, 500);
      font-weight: 500;
      color: var(--text-secondary);
      em {
        color: var(--text-brand);
        font-style: normal;
      }
    }
  }
  .collection-inner {
    border-top-right-radius: var(--radius-xl);
    background-color: var(--white);
    padding: var(--spacing-xl);
    [data-theme="dark"] & {
      background-color: var(--gray-950);
    }
  }
  .sharebtn {
    max-width: 101px;
    margin: var(--spacing-3xl) auto 0;
  }
}

/* 혜택 - 이벤트 하단 꼭! 알아두세요 아코디언 형태 */
.event-collection__notice {
  margin-top: 10px;
  padding: 0;
  .sv-accordion-item {
    border-bottom: 1px solid var(--border-secondary);
  }
  .sv-accordion-item__title {
    @include font-set(title-m, 500);
    font-weight: 500;
    color: var(--text-secondary);
  }
  .sv-text-list__content ul {
    margin-top: var(--spacing-md);
  }
  .sv-list {
    color: var(--text-quaternary);
  }
}

/* 혜택 - 앱테크 */
.sc-point-card {
  ~ .sc-point-card,
  ~ .sc-unordered__list {
    margin-top: var(--spacing-4xl);
  }
  &__left-content {
    display: inline-flex;
    align-items: center;
    gap: var(--spacing-md);
  }

  &__img {
    width: var(--spacing-3xl);
    height: var(--spacing-3xl);
    object-fit: contain;
  }

  &__label {
    @include font-set(title-s, 500);
    color: var(--text-primary);
  }

  &__right-content {
    display: inline-flex;
    justify-content: space-between;
    align-items: center;
    gap: var(--spacing-md);
    width: 100%;
  }

  &__amount {
    @include font-set(title-xl, 700);
    color: var(--text-brand);
  }

  &__icon {
    color: var(--text-tertiary);
  }

  &__shadow {
    .sv-card__content {
      padding: var(--spacing-2xl) var(--spacing-xl);
    }
  }

  &__solid {
    .sv-card__content {
      padding: var(--spacing-xl);
    }

    .sc-point-card__amount {
      @include font-set(body-l, 700);
      color: var(--text-primary);
    }
  }
}
// 앱테크 포인트 리스트
.sc-point__list {
  .sv-basic-list {
    .sv-basic-list__content {
      overflow: hidden;
      width: 100%;
      min-width: 0;
    }
  }

  .sc-point__item {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-xs);
    width: 100%;
    min-width: 0;
  }

  .sc-point__main {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: var(--spacing-lg);
    width: 100%;
    min-width: 0;

    strong {
      @include font-set(title-s, 500);
      color: var(--text-secondary);
      flex: 1 1 auto;
      min-width: 0;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
      padding-right: 5rem;
    }

    span {
      @include font-set(body-l, 700);
      color: var(--text-primary);
      flex-shrink: 0;
    }
  }

  .sc-point__sub {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: var(--spacing-md);

    time {
      @include font-set(body-s, 300);
      color: var(--text-quaternary);
    }

    span {
      @include font-set(body-s, 300);
      color: var(--text-quaternary);

      &.text-brand {
        color: var(--text-brand);
      }
    }
  }

  .sv-pagination {
    margin-top: var(--spacing-lg);
  }
}
// 이벤트 리스트
.sc-event__list {
  padding-top: var(--spacing-xl);
  // padding-inline: var(--container-padding-mobile);
  padding-right: var(--container-padding-mobile);
  padding-left: var(--container-padding-mobile);
  .sv-divider {
    // margin-block: var(--spacing-sm);
    margin-top: var(--spacing-sm);
    margin-bottom: var(--spacing-sm);
  }
  .sv-basic-list {
    // padding-inline: 0;
    padding-right: 0;
    padding-left: 0;
    // padding-block: var(--spacing-lg);
    padding-top: var(--spacing-lg);
    padding-bottom: var(--spacing-lg);
  }
  @at-root .sv-tabs__panel .sc-event__list .sv-basic-list {
    // padding-inline: 0;
    padding-right: 0;
    padding-left: 0;
  }
  .sv-basic-list {
    .sv-basic-list__content {
      overflow: hidden;
      width: 100%;
      min-width: 0;
    }
  }

  .sc-evt__item {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-xs);
    width: 100%;
    min-width: 0;
  }

  .sc-evt__main {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: var(--spacing-lg);
    width: 100%;
    min-width: 0;

    strong {
      @include font-set(title-s, 500);
      color: var(--text-secondary);
      flex: 1 1 auto;
      min-width: 0;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }

    span {
      @include font-set(body-l, 700);
      color: var(--text-primary);
      flex-shrink: 0;
    }
  }

  .sc-evt__sub {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: var(--spacing-md);

    time {
      @include font-set(body-s, 300);
      color: var(--text-quaternary);
    }

    span {
      @include font-set(body-s, 300);
      color: var(--text-quaternary);

      &.text-brand {
        color: var(--text-brand);
      }
    }
  }
  &.card-list__grid {
    padding-top: var(--spacing-3xl);
    // padding-inline: var(--container-padding-mobile);
    padding-right: var(--container-padding-mobile);
    padding-left: var(--container-padding-mobile);
  }
  @at-root .sc-container:has(.sc-evt__tabs) {
    padding-top: 0;
  }
}
/* FullPopup 좌/우 패딩 제거 (sc-point__list가 있을 경우) */
.sv-popup__body:has(.sc-point__list) {
  // padding-inline: 0;
  padding-right: 0;
  padding-left: 0;
}
/* 앱테크 설정 */
.sc-setting__section {
  --sv-text-list-gap: var(--spacing-md);

  .sv-list-title__title {
    margin-bottom: var(--spacing-md);
    @include font-set(title-m, 500);
    color: var(--text-primary);
  }
  .sv-button.sv-button--size-s.sv-button--variant-underline .sv-button__label {
    @include font-set(body-s, 300);
    color: var(--text-secondary);
  }
  .sv-button--size-s.sv-button--variant-underline:before {
    bottom: 4px;
  }
  ~ .sc-setting__section {
    margin-top: var(--spacing-4xl);
  }
  /* 개인정보 동의 리스트 */
  .sc-privacy__list {
    margin-top: var(--spacing-md);
    margin-bottom: var(--spacing-xl);

    .sv-basic-list__content {
      @include font-set(body-m, 300);
      color: var(--text-secondary);
    }
  }
  /* 꼭 확인해주세요 아코디언 */
  .sv-accordion-item.sv-accordion-item--variant-solid {
    margin-top: var(--spacing-xl);
    .sv-accordion-panel__content {
      padding-top: 0;
    }
  }
  .sv-accordion-item__header {
    padding: var(--spacing-xl);
  }
  .sv-accordion-item__title {
    gap: var(--spacing-md);
    color: var(--text-tertiary);
  }
  .sv-icon {
    color: var(--fg-quaternary);
  }

  .sc-accordion__image {
    width: 100%;
    max-width: 100%;
    height: auto;
    margin: 0;
    margin-bottom: var(--spacing-xl);
  }
}
/* 앱테크 포인트 더 받기 */
.sc-detail-shortform {
  padding-top: var(--spacing-3xl);

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
    .sv-card {
      .sv-icon {
        vertical-align: middle;
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
  }
}

/* 혜택 - 투데이 */
// 마케팅 롤링배너 전체보기
.sc-tody-banner-list {
  li + li {
    margin-top: var(--spacing-3xl);
  }
  button {
    position: relative;
    aspect-ratio: 335/269;
    width: 100%;
  }
  &__thumbnail {
    aspect-ratio: 335/269;
    display: block;
    border-radius: 2px;
    overflow: hidden;
    img {
      width: 100%;
      height: 100%;
      vertical-align: top;
      object-fit: cover;
    }
  }
  &__title-wrap {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    padding: 22px;
    text-align: left;
    .main-title {
      display: block;
      @include ellipsis(2);
      @include font-set("title-xl", 700);
      font-weight: 700;
      color: var(--text-ondark_primary-same);
    }
    .sub-text {
      display: block;
      @include ellipsis;
      @include font-set("body-m", 300);
      font-weight: 300;
      color: var(--text-ondark_primary-same);
    }
  }
}

/* 쿠폰 */
.cupon-contents {
  .sc-empty-case .empty-type {
    margin: 0;
  }
}
.cupon-top__btngroup {
  padding: 0 var(--container-padding-mobile);
  .sv-divider {
    // margin-block: var(--spacing-2xl);
    margin-top: var(--spacing-2xl);
    margin-bottom: var(--spacing-2xl);
  }
}
.cupon-head {
  flex: 0 0 auto;
  padding: 0 var(--container-padding-mobile) var(--spacing-xl);
  @include font-set(headline-s, 700);
  font-weight: 700;
  .cupon-count {
    color: var(--text-brand);
    font-style: normal;
  }
}
.cupon-chip {
  flex: 0 0 auto;
  padding: 0;
  .sv-chip-group__container > * {
    margin: 0;
  }
  .sv-chip-group {
    padding: var(--spacing-xl) 0;
    .sv-chip-group__container {
      gap: var(--spacing-lg);
      padding: 0;
      padding-left: var(--container-padding-mobile);
      .sv-basic-chip.sv-basic-chip--variant-solid:first-child {
        margin-left: 0;
      }
      // 첫 번째 칩만 있을 경우에도 좌측 간격 유지
      &:has(.sv-basic-chip.sv-basic-chip--variant-solid:only-child) {
        padding-left: var(--container-padding-mobile);
      }
    }
    &:has(.sv-chip-group__container--expanded) {
      .sv-chip-group__container {
        padding-left: var(--container-padding-mobile);
      }
    }
  }
  .sv-chip-group .sv-chip-group__expand-button {
    margin: 0;
  }
  &.skeleton {
    overflow: hidden;
    display: flex;
    align-items: center;
    padding-left: var(--container-padding-mobile);
    .sv-loading-skeleton {
      flex-shrink: 0;
      ~ .sv-loading-skeleton {
        margin-left: var(--spacing-md);
      }
      &:last-child {
        margin-right: var(--container-padding-mobile);
      }
    }
  }
}
.cupon-list__wrap {
  padding: var(--spacing-2xl) var(--container-padding-mobile);
}
.cupon-list__head {
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
  // padding: 0 var(--container-padding-mobile);
  em {
    color: inherit;
    font-style: normal;
  }
  .cupon-head__text {
    @include font-set(body-m, 500);
    font-weight: 500;
    color: var(--text-tertiary);
  }
  .cupon-head__text-left {
    flex: 1 1 auto;
  }
  .cupon-head__text-right {
    flex: 0 0 auto;
  }
  &.list-head {
    margin-bottom: var(--spacing-xl);
    .cupon-head__text {
      @include font-set(title-l, 700);
      font-weight: 700;
      color: var(--text-secondary);
    }
  }
}
.cupon-list__body {
  .cupon-item {
    padding: var(--spacing-lg) 0;
    .sv-list__item_inner > * {
      margin: 0;
    }
    .sv-list__item_inner.align-center {
      gap: var(--spacing-lg);
      justify-content: flex-start;
    }
    &.outline {
      border: 1px solid var(--border-secondary);
      border-radius: var(--radius-xl);
      padding: var(--spacing-2xl);
      .flex {
        margin-bottom: var(--spacing-md);
      }
      .sv-list > * {
        margin-right: 0;
      }
      .sv-list .sidetxt > * {
        display: block;
      }
      .sv-list__control {
        width: calc(16px * 3);
        margin-right: calc(var(--spacing-2xl) * -1);
        .sv-icon-button {
          color: var(--fg-quaternary);
        }
      }
      .sv-list__text__main {
        margin-right: var(--spacing-xl);
        @include ellipsis(2);
      }
      .sv-list__text__sub {
        margin-right: var(--spacing-xl);
        @include ellipsis(1);
      }
      .sv-list__icon {
        padding: 0;
        border: 1px solid var(--border-secondary);
        background-color: transparent;
        img {
          border-radius: 0;
        }
      }
      ~ .outline {
        margin-top: var(--spacing-lg);
      }

      &.is-label {
        padding-top: 10px;
        .sv-list__icon {
          margin-top: calc(var(--spacing-md) + 24px);
        }
        // label이 있을 때도 sub가 위, main이 아래로 오도록 순서 조정
        .sv-list__text {
          // direction-h sidetxt 클래스가 있어도 세로로 배치
          display: flex;
          flex-direction: column;
          &.sidetxt {
            > * {
              display: block;
            }
          }
          .sv-list__text__main {
            order: 2;
            display: block;
            margin-right: var(--spacing-xl);
            @include ellipsis(2);
          }
          .sv-list__text__sub {
            order: 1;
            display: block;
            margin-right: var(--spacing-xl);
            @include ellipsis(1);
          }
        }
      }
    }
    &.skeleton {
      padding-top: var(--spacing-lg);
      .content {
        display: flex;
        margin-top: var(--spacing-md);
        .left {
          flex: 1 1 auto;
          min-width: 0;
          .sv-loading-skeleton:last-child {
            margin-top: var(--spacing-xs);
          }
        }
        .right {
          flex: 0 0 auto;
          margin-left: var(--spacing-xl);
        }
      }
    }
  }
  .sv-list__texts {
    flex: 1 1 auto;
    .sv-list__text {
      width: 100%;
      min-width: 0;
    }
  }
  .sv-list__icon {
    overflow: hidden;
    display: flex;
    flex: 0 0 auto;
    align-items: center;
    justify-content: center;
    width: var(--spacing-6xl);
    height: var(--spacing-6xl);
    padding: var(--spacing-sm);
    border-radius: var(--spacing-xl);
    background-color: var(--bg-gray);
    img {
      max-width: 100%;
      max-height: 100%;
      width: auto;
      height: auto;
      border-radius: 50%;
      object-fit: contain;
    }
  }
  .sv-list__text__main {
    margin-right: 0;
    span {
      display: block;
      @include font-set(body-s, 300);
      font-weight: 300;
      color: var(--text-quaternary);
    }
    strong {
      display: block;
      font-weight: 500;
    }
    em {
      font-style: normal;
      font-weight: 500;
      color: var(--text-brand);
    }
    .inline-flex {
      display: inline-flex;
    }
    .sv-label {
      margin-bottom: var(--spacing-xs);
      font-size: var(--font-size-detail-s);
      line-height: var(--lineheight-detail-s);
      letter-spacing: var(--letterspace-detail-s);
      font-weight: var(--font-weight-m);
    }
    .sv-label--variant-solid {
      &.sv-label--color-blue,
      &.sv-label--color-cyan,
      &.sv-label--color-green,
      &.sv-label--color-yellow,
      &.sv-label--color-orange,
      &.sv-label--color-red,
      &.sv-label--color-gray {
        color: var(--text-ondark_primary-same);
      }
    }
  }
  .sv-list__text__sub {
    @include font-set(body-s, 300);
    font-weight: 300;
    color: var(--text-quaternary);
  }
  .sv-list__control {
    flex: 0 0 auto;
    // width: 36px;
    min-width: 36px;
    height: 36px;
    .sv-icon-button {
      width: 100%;
      height: 100%;
    }
    .sv-icon {
      width: 20px;
      height: 20px;
    }
  }
}
.sc-membership__bs {
  .sv-bottom-sheet__body {
    // padding-inline: 0;
    padding-right: 0;
    padding-left: 0;
  }
}

/* 반갑 꾸러미 */
.welcome-intro {
  position: relative;
  z-index: 1;
  // padding-inline: var(--container-padding-mobile);
  padding-right: var(--container-padding-mobile);
  padding-left: var(--container-padding-mobile);
  color: var(--white);
  &__dim {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-repeat: no-repeat;
    background-position: 100% calc(var(--sc-header-height) + 45px);
    background-color: var(--fg-primary);
  }

  &__head {
    margin-bottom: 12px;
  }
  &__medium-text {
    color: inherit;
    font-size: 18px;
    line-height: 22px;
    font-weight: 700;
    color: var(--white);
  }
  &__large-text {
    margin-top: 6px;
    color: inherit;
    font-size: 25px;
    line-height: 32px;
    font-weight: 700;
    color: var(--white);
  }
  &__title {
    display: flex;
    flex-direction: column;
    gap: 8px;
    width: 100%;
    font-size: 51px;
    line-height: 120%;
    font-weight: 800;
    span {
      display: flex;
      gap: 14px;
      align-items: center;
      width: 100%;
      min-width: 0;
    }
    strong {
      flex: 0 0 auto;
      &:first-of-type {
        color: #5cb1ff;
      }
    }
    .line {
      display: inline-flex;
      flex: 1 1 auto;
      min-width: 0;
      height: 6px;
      border-radius: 3px;
      opacity: 0.7;
      background: linear-gradient(90deg, #5cb1ff 0%, #ffffff 100%);
    }
  }
  &__content {
    margin-top: 28px;
    padding: 28px 24px 32px;
    border-radius: var(--radius-lg);
    background-color: rgba(0, 0, 0, 0.5);
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    gap: 24px;
  }

  .content-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    padding: 0;

    &__image {
      display: flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 4px;
      width: 76px;
      height: 64px;

      img {
        width: 100%;
        height: 100%;
        object-fit: contain;
      }
    }

    &__text {
      color: var(--white);
      strong {
        display: block;
        color: inherit;
        font-size: 14px;
        line-height: 18px;
        font-weight: 800;
      }
      span {
        display: block;
        color: inherit;
        font-size: 12px;
        line-height: 18px;
        font-weight: 300;
      }
    }
  }
}

/* 네비게이션 안에 .sv-navigation--fixed .sv-navigation__placeholder 가 없으면 네비게이션 높이만큼 패딩 추가 */
.sc-wrap:not(:has(.sv-navigation__placeholder)) {
  .welcome-intro {
    padding-top: calc(var(--spacing-xl) + var(--sc-header-height));
    ~ .sv-bottom-action-container .sv-bottom-action-container__inner {
      padding-bottom: var(--spacing-2xl);
    }
  }
}

/* 반갑꾸러미 탭 */
.welcome-lounge {
  .sv-tabs__btns {
    position: sticky;
    top: var(--sc-header-height);
    z-index: 10;
  }
  // 디바이스에서 useTabSwipe가 panels에 touch-action:none을 적용해 세로 스크롤이 막히는 문제가 있어
  // swipe 동작은 유지하면서 기본 스크롤은 허용하도록 pan-y로 덮어쓴다.
  .sv-tabs__panels {
    touch-action: pan-y !important;
  }
  em {
    font-style: normal;
  }
  .payment-panel {
    padding: var(--spacing-xl) 0 var(--spacing-4xl);
    &__daily {
      .section {
        &.bg-gray {
          padding-top: var(--spacing-4xl);
        }
      }
    }
    &__monthly {
      .img-group {
        width: 100%;
        height: auto;
        max-width: 1024px; // 태블릿 최대 사이즈 제한
        margin-top: 0;
        margin-bottom: 0;
        padding-top: var(--spacing-3xl);
        background-repeat: no-repeat;
        background-position: center;
        background-size: contain;
        aspect-ratio: 375 / 140; // 원본 비율에 맞춰 조정 필요 시 여기 값만 변경
        img {
          width: auto;
          height: auto;
          max-width: 100%;
        }
        &::before,
        &::after {
          content: "";
          position: absolute;
          top: 0;
          z-index: 1;
          width: 44px;
          height: 100%;
        }
        &::before {
          left: 0;
          background: linear-gradient(
            -270deg,
            #fff 0%,
            rgba(255, 255, 255, 0) 69.44%
          );
          [data-theme="dark"] & {
            background: linear-gradient(
              -270deg,
              #0c111d 0%,
              rgba(12, 17, 29, 0) 69.44%
            );
          }
        }
        &::after {
          right: 0;
          background: linear-gradient(
            270deg,
            #fff 0%,
            rgba(255, 255, 255, 0) 69.44%
          );
          [data-theme="dark"] & {
            background: linear-gradient(
              270deg,
              #0c111d 0%,
              rgba(12, 17, 29, 0) 69.44%
            );
          }
        }
      }
    }
  }
  .text-daily__title,
  .text-first__title,
  .text-monthly__title {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: var(--spacing-md);
    margin-bottom: var(--spacing-lg);
    padding-top: var(--spacing-4xl);
    .text-daily02 {
      display: inline-flex;
      align-items: center;
      gap: var(--spacing-md);
      &__point {
        color: var(--text-brand);
        font-size: 30px;
        font-weight: 800;
        line-height: var(--line-height-title-xl);
        letter-spacing: var(--letter-spacing-title-xl);
      }
      em {
        color: inherit;
        font-size: inherit;
        font-weight: inherit;
        line-height: inherit;
        letter-spacing: inherit;
      }
    }
    .text-daily01 {
      display: inline-flex;
      align-items: center;
    }
  }
  .text-daily__title {
    gap: var(--spacing-sm);
  }
  .img-group {
    overflow: hidden;
    position: relative;
    margin-top: var(--spacing-xl);
    margin-bottom: var(--spacing-xl);
    width: auto;
    height: auto;
    text-align: center;
    img {
      width: 100%;
      height: 100%;
      max-width: 140px;
      object-fit: contain;
    }
  }
  .sv-button--variant-underline.sv-button--color-secondary {
    color: var(--text-tertiary);
  }
  .sv-button--size-m.sv-button--variant-underline {
    .sv-button__label {
      @include font-set(body-m, 500);
      font-weight: 500;
    }
  }
  .custum-card__group {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 8px;

    // 각 아이템(IconButtonGroup 루트)의 폭을 셀에 맞춤
    > .sv-button-group {
      width: 100%;
    }

    // 마지막(7번째) 아이템만 가로 전체(span 2 cols)
    > .sv-button-group:last-child {
      grid-column: 1 / -1;
    }

    .sv-button-group {
      &.sv-button-group--type-icon {
        padding: 0;
      }
    }
    .sv-icon-button--label {
      padding: 0;
    }
    .sv-icon-button--size-m {
      .sv-icon-button__icon-container {
        width: 100% !important;
        height: 100% !important;
      }

      img {
        width: 100%;
        height: 100%;
        object-fit: contain;
      }
      .sv-icon {
        width: auto !important;
        height: auto !important;
      }
    }
    .sv-icon-button {
      position: relative;
      padding: var(--spacing-2xl);
      border-radius: var(--radius-xl);
      background: var(--bg-white-elevated);
      box-shadow: 0 4px 16px 0 rgba(12, 17, 29, 0.06);
    }
    .text-vector__group {
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      justify-content: flex-start;
      text-align: left;
      gap: calc(var(--spacing-md) + 1px);
      span {
        line-height: 1;
      }
    }
    .text_description {
      font-size: 12px;
      font-weight: 500;
      line-height: 140%;
      color: var(--text-quaternary);
    }
    .text-price {
      display: flex;
      align-items: center;
      justify-content: flex-start;
      gap: var(--spacing-sm);
    }
    .symbol-vector__group {
      display: flex;
      align-items: center;
      justify-content: center;
      position: absolute;
      bottom: 4px;
      right: 6px;
      width: 48px;
      height: 48px;
    }
    .symbol-vector {
      width: 100%;
      height: 100%;
      object-fit: contain;
    }
    &.first-cards {
      grid-template-columns: repeat(3, minmax(0, 1fr));
      padding: var(--spacing-2xl);
      border-radius: var(--radius-xl);
      background-color: var(--bg-white-elevated);
      box-shadow: 0 4px 16px 0 rgba(12, 17, 29, 0.06);
      > .sv-button-group:last-child {
        grid-column: auto;
      }
      .sv-icon-button--size-m {
        img {
          width: 48px;
          height: 48px;
        }
        .sv-icon-button__icon-container {
          width: 48px !important;
          height: 48px !important;
        }
      }
      .sv-icon-button {
        gap: var(--spacing-sm);
        padding: var(--spacing-lg) var(--spacing-sm) var(--spacing-lg);
        border-radius: var(--radius-lg);
        background: var(--bg-gray);
        box-shadow: none;
        .sv-icon-button__label {
          margin: 0;
          @include font-set(body-s, 500);
          font-weight: 500;
          color: var(--text-tertiary);
        }
        &.mission-completed {
          border: 2px solid var(--border-brand);
          .sv-icon-button__label {
            color: var(--text-primary);
          }
          &.sv-icon-button--disabled {
            .sv-icon-button__icon-container {
              mix-blend-mode: normal;
              color: inherit;
            }
            svg path {
              fill: revert;
            }
            img {
              opacity: 1;
              filter: none;
            }
          }
          &:disabled {
            .sv-icon-button__icon-container {
              mix-blend-mode: normal;
              color: inherit;
            }
            svg path {
              fill: revert;
            }
            img {
              opacity: 1;
              filter: none;
            }
            .sv-icon-button__label {
              color: var(--text-primary);
            }
          }
        }
      }
      ~ .coupon-cards {
        margin-top: var(--spacing-md);
        margin-bottom: 0;
        &::before,
        &::after {
          content: "";
          position: absolute;
          top: -16px;
          z-index: 1;
          width: 8px;
          height: 24px;
          border-radius: 100px;
          background: #b1b7c4;
        }
        &::before {
          left: 32px;
        }
        &::after {
          right: 32px;
        }
      }
    }
    &.monthly-cards {
      align-items: flex-start;
      justify-content: flex-start;
      text-align: left;
      .sv-icon-button {
        align-items: flex-start;
        justify-content: flex-start;
        text-align: left;
        min-height: 133px;
        padding-bottom: var(--spacing-5xl);
      }
      .sv-icon-button__icon-container {
        gap: calc(var(--spacing-lg) + 1px);
        flex-direction: column;
        align-items: flex-start;
        justify-content: flex-start;
        text-align: left;
      }
    }
  }
  .section-head {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
  }
  section {
    &.bg-gray {
      // padding-block: var(--spacing-4xl);
      padding-top: var(--spacing-4xl);
      padding-bottom: var(--spacing-4xl);
      background-color: var(--bg-gray);
    }
  }
  section,
  .section {
    display: flex;
    flex-direction: column;
    &.bg-gray {
      // padding-block: var(--spacing-4xl);
      padding-top: var(--spacing-4xl);
      padding-bottom: var(--spacing-4xl);
      background-color: var(--bg-gray);
      &:has(.coupon-cards) {
        // padding-block: var(--spacing-3xl);
        padding-top: var(--spacing-3xl);
        padding-bottom: var(--spacing-3xl);
      }
    }
    &.payment-notice {
      background-color: var(--bg-canvas_white);
      .title-sub {
        margin-bottom: var(--spacing-2xl);
        @include font-set(title-m, 700);
        font-weight: 700;
        color: var(--text-secondary);
        &__small {
          @include font-set(title-s, 500);
          font-weight: 500;
          color: var(--text-secondary);
        }
      }
      .sv-text-list {
        color: var(--text-quaternary);
        strong {
          font-weight: 700;
        }
        ul {
          margin-left: 0 !important;
        }
      }
    }
    .article {
      ~ .custom-divider ~ .article {
        margin-top: 0;
      }
    }
  }
  .article {
    // padding-inline: var(--container-padding-mobile);
    padding-right: var(--container-padding-mobile);
    padding-left: var(--container-padding-mobile);
  }
  article {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-md);
    ~ article {
      margin-top: var(--spacing-4xl);
    }
  }
  @at-root .sc-container:has(.welcome-lounge) {
    padding-top: 0;
  }
}
.welcome-content {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-lg);
  em {
    font-style: normal;
  }
  .custom-card {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: var(--spacing-none);
    width: 100%;
    padding: var(--spacing-2xl);
    border-radius: var(--radius-xl);
    border: 2px solid transparent;
    background:
      linear-gradient(var(--bg-canvas_white), var(--bg-canvas_white))
        padding-box,
      linear-gradient(90deg, #479cff 0%, #59e0e0 100%) border-box;
    &__header {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: var(--spacing-md);
      width: 100%;
      padding: var(--spacing-xl);
      border-radius: var(--radius-xl);
    }
    &__header-title {
      display: flex;
      justify-content: center;
      align-items: center;
      width: 100%;
      min-height: 25px;
      path {
        fill: var(--text-primary);
      }
    }
    &__header-content {
      display: inline-flex;
      align-items: center;
      gap: var(--spacing-md);
      min-height: 42px;
      path {
        fill: var(--text-primary);
      }
    }
    &__price {
      display: inline-flex;
      align-items: center;
      @include font-set(title-xl, 700);
      font-size: 30px;
      font-weight: 700;
      color: var(--text-brand);
    }
    &__content {
      display: flex;
      flex-direction: column;
      width: 100%;
    }
    &__content-item {
      display: flex;
      align-items: center;
      gap: var(--spacing-lg);
      width: 100%;
      .custom-card__title {
        @include font-set(body-l, 300);
        font-weight: 300;
        color: var(--text-quaternary);
      }
      .custom-card__price {
        justify-content: flex-end;
        flex: 1 1 auto;
        min-width: 0;
        @include font-set(title-xl, 700);
        font-size: 22px;
        font-weight: 700;
        color: var(--text-primary);
      }
    }
  }
  .sv-divider {
    // margin-block: var(--spacing-xl);
    margin-top: var(--spacing-xl);
    margin-bottom: var(--spacing-xl);
  }
}
.custom-divider {
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  width: 100%;
  height: 1px;
  // padding-block: var(--spacing-4xl);
  padding-top: var(--spacing-4xl);
  padding-bottom: var(--spacing-4xl);
  &::before {
    content: "";
    position: absolute;
    top: 50%;
    left: 0;
    transform: translateY(-50%);
    width: 100%;
    height: 1px;
    background-color: var(--border-secondary);
  }
  &.bg-gray {
    background-color: transparent;
  }
  &[data-type="group"] {
    height: 10px;
    &::before {
      height: 10px;
    }
  }
  .svgicon-plus-fill {
    position: relative;
    z-index: 1;
  }
}
.custom-cards {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-none);
  &__group {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-xl);
    &:has(.custom-cards__group-head) {
      gap: var(--spacing-4xl);
    }
  }
  &__gray-group {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-xl);
    width: 100%;
    // padding-inline: var(--container-padding-mobile);
    padding-right: var(--container-padding-mobile);
    padding-left: var(--container-padding-mobile);
    &.center {
      .sv-card__content {
        text-align: center;
      }
    }
  }
  &__group-head {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 10px;
    width: 100%;
    .sv-base-badge--inline {
      .sv-base-badge__indicator {
        min-height: 32px;
        margin: 0;
        padding: 0 var(--spacing-lg);
        border-radius: var(--radius-full);
        @include font-set(body-m, 700);
        font-weight: 700;
      }
    }
  }
  &__group-head-title {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: var(--spacing-md);
    width: 100%;
  }
  .sv-card__content {
    padding: var(--spacing-2xl);
    padding-bottom: var(--spacing-xl);
  }
  .sv-divider {
    // margin-block: var(--spacing-xl);
    margin-top: var(--spacing-xl);
    margin-bottom: var(--spacing-xl);
  }
  .sv-base-badge--inline {
    .sv-base-badge__indicator {
      min-width: 22px;
      margin-left: 0;
    }
  }
  &__header {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: var(--spacing-md);
  }
  &__header-label,
  &__header-text,
  &__header-title {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    gap: var(--spacing-md);
  }
  &__content {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-md);
  }
  &__content-item {
    display: flex;
    align-items: center;
    gap: var(--spacing-lg);
    position: relative;
    width: 100%;
    img {
      width: 100%;
      height: 100%;
      max-width: 140px;
      object-fit: contain;
    }
    .sv-label {
      position: absolute;
      top: 0;
      right: 0;
    }
    &:has(img) {
      justify-content: center;
    }
  }
  &__title {
    flex: 1 1 auto;
    min-width: 0;
    @include font-set(body-l, 300);
    font-weight: 300;
    color: var(--text-quaternary);
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }

  &__content-item > .custom-cards__title:only-child {
    // margin-inline: auto;
    margin-right: auto;
    margin-left: auto;
    overflow: visible;
    text-overflow: initial;
    white-space: normal;
    text-align: center;
  }
  &__price {
    flex: 0 0 auto;
    @include font-set(title-xl, 800);
    font-weight: 800;
    color: var(--text-primary);
  }
  &__gray-info {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-md);
    @include font-set(title-s, 500);
    font-weight: 500;
    color: var(--text-secondary);
    p {
      margin: 0;
    }
    em {
      font-style: normal;
      @include font-set(body-m, 700);
      font-weight: 700;
      color: var(--text-brand);
    }
    small {
      @include font-set(body-l, 300);
      font-weight: 300;
      color: var(--text-quaternary);
    }
  }
}
.coupon-cards {
  display: flex;
  position: relative;
  width: 100%;
  min-width: 0;
  align-self: stretch;
  // margin-block: var(--spacing-xl);
  margin-top: var(--spacing-xl);
  margin-bottom: var(--spacing-xl);

  .svg-coupon-cards {
    width: 100%;
    height: auto;
    display: block;
    max-width: 100%;
    overflow: visible;
    filter: drop-shadow(0 4px 8px rgba(12, 17, 29, 0.06));
    path[fill="white"] {
      fill: var(--bg-canvas_white-elevated);
      [data-theme="dark"] & {
        fill: var(--bg-gray);
      }
    }
    svg {
      overflow: visible;
    }
    .coupon-line {
      display: none;
    }
  }
  &.mission-completed {
    .coupon-line {
      display: block;
    }
  }
  &:has(.svg-coupon-cards.top) {
    margin-top: 0;
    .coupon-cards__item .svg-coupon-text__group {
      gap: var(--spacing-md);
      svg {
        + svg {
          margin-top: var(--spacing-xs);
        }
      }
    }
  }
  &__inner {
    display: flex;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }
  &__item {
    display: flex;
    flex-direction: column;
    flex: 1 1 auto;
    align-self: center;
    align-items: flex-start;
    gap: var(--spacing-md);
    min-width: 0;
    // width: calc(100% - 64px);
    flex: 0 0 80.16%; // SVG 구분선 비율 (255px / 303px)
    padding: var(--spacing-xl) 24px;
    .svg-coupon-text__group {
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      gap: var(--spacing-md);
    }
    .coupon-cards__item-desc {
      @include font-set(body-s, 300);
      font-weight: 300;
      color: var(--text-quaternary);
      strong {
        font-weight: 500;
      }
    }
  }
  &__status {
    display: flex;
    flex-direction: column;
    // flex: 0 0 auto;
    flex: 0 0 18.84%; // SVG 구분선 비율 (48px / 303px)
    align-items: center;
    justify-content: center;
    // width: 64px;
    min-width: 0;
    height: 100%;
    svg {
      max-width: 32px;
      height: auto;
    }
    .svg-icon-check {
      path {
        fill: var(--text-brand);
      }
    }
    span {
      display: block;
      @include font-set(body-s, 500);
      font-weight: 500;
      color: var(--text-brand);
      text-align: center;
      word-break: keep-all;
    }
    .gradient-border-wrapper {
      position: absolute;
      z-index: 2;
      transform: translateY(-50%);
      top: 50%;
      touch-action: none;
      // gradient-border-wrapper와 내부의 role="button" 요소가 포커스를 받지 않도록 설정
      pointer-events: none;

      .sv-tooltip-base-wrapper {
        pointer-events: none;
      }

      .sv-tooltip-base__anchor {
        pointer-events: none;
        cursor: default;
        outline: none;

        // 포커스 시 outline 제거
        &:focus,
        &:focus-visible {
          outline: none !important;
          box-shadow: none !important;
        }

        // tabindex 속성이 있어도 포커스 시각적 표시 제거
        &[tabindex] {
          pointer-events: none;
        }

        svg {
          color: transparent;
        }
      }
      .sv-tooltip-base__content {
        .bounce-y {
          position: relative;
          margin-right: var(--spacing-md);
          animation: bounceIcon 1s ease-in-out infinite alternate;
        }
      }
      .sv-tooltip-base {
        min-width: 220px;
      }
    }
    .sc-icon--custom {
      z-index: 1;
    }
  }
  &:disabled *,
  &[disabled] * {
    color: var(--text-disabled-same);
    svg path {
      fill: var(--text-disabled-same);
    }
  }
  &.not-mission {
    .coupon-cards__status {
      .svg-download-fill {
        path:first-child {
          fill: var(--text-disabled-same);
        }
      }
    }
  }
}
// 웰컴 체크인
.welcome-checkin {
  --pink-020: #ffdde2;
  --pink-110: #ff0065;
  --welcome-checkin-head-spacing: 17px;
  &__head {
    display: flex;
    flex-direction: column;
    justify-content: center;
    position: relative;
    height: calc(232px - 56px);
    padding: var(--spacing-3xl);
    background: linear-gradient(180deg, #f97e94 11.8%, #ee536e 88.2%);
    .welcome-checkin__title {
      margin-bottom: 10px;
    }
    .welcome-checkin__description {
      margin-bottom: var(--welcome-checkin-head-spacing);
      @include font-set(body-m, 300);
      font-weight: 300;
      color: var(--white);
    }
    &::after {
      content: "";
      position: absolute;
      bottom: var(--welcome-checkin-head-spacing);
      right: 21px;
      width: 160px;
      height: 110px;
      background-repeat: no-repeat;
      background-position: center;
      background-size: contain;
      background-image: url(#{$cdn-url}/images/pages/benefits/welcome/benefis_welcome_checkin_img01.png);
    }
  }
  &__body {
    z-index: 1;
    margin-top: calc(var(--welcome-checkin-head-spacing) * -1);
    padding: var(--spacing-4xl) var(--spacing-3xl);
    border-radius: var(--radius-md) var(--radius-md) 0 0;
    background-color: var(--bg-canvas_gray_light);
  }
  &__section {
    display: flex;
    flex-direction: column;
  }
  &__subtitle {
    text-align: center;
  }
  &__label {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 106px;
    height: 36px;
    margin: var(--spacing-4xl) auto var(--spacing-3xl);
    border-radius: 100px;
    border: 2px solid var(--pink-020);
    @include font-set(body-m, 700);
    font-weight: 700;
    color: var(--pink-110);
    text-align: center;
  }
  &__description {
    margin-bottom: var(--spacing-3xl);
    color: var(--text-secondary);
    font-size: 20px;
    font-weight: 400;
    line-height: 26px;
  }
  &__list {
    display: flex;
    flex-direction: column;
  }
  &__item {
    ~ .welcome-checkin__item {
      margin-top: var(--spacing-lg);
    }
  }
  &__item-link {
    display: flex;
    align-items: center;
    gap: 0;
    min-height: 106px;
  }
  &__item-content {
    display: flex;
    align-items: center;
    flex: 1 1 auto;
    align-self: stretch;
    min-width: 0;
    padding: var(--spacing-xl) var(--spacing-2xl) calc(var(--spacing-xl) + 2px);
    border-radius: var(--radius-sm);
    background: var(--bg-white-elevated);
    box-shadow: 0 6px 12px 0 rgba(0, 0, 0, 0.05);

    img {
      flex-shrink: 0;
      max-width: 60px;
      max-height: 72px;
      margin-right: var(--spacing-lg);
    }
  }
  &__item-info {
    display: flex;
    flex-direction: column;
    justify-content: center;
    flex: 1 1 auto;
    min-width: 0;

    .sv-label {
      flex: 0 0 auto;
      width: fit-content;
      align-self: flex-start;
      margin-bottom: var(--spacing-sm);
      padding-right: 6px;
      padding-left: 6px;
      border-radius: 2px;
      background-color: var(--pink-110);
      @include font-set(body-s, 700);
      font-weight: 700;
      color: var(--white);
    }
  }
  &__item-info-text {
    display: flex;
    align-items: center;
  }
  &__item-info-description {
    margin-top: 3px;
    @include font-set(body-s, 300);
    font-weight: 300;
    color: var(--text-quaternary);
  }
  &__item-btn {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    flex: 0 0 auto;
    align-self: stretch;
    width: 62px;
    padding: var(--spacing-2xl) 0;
    border-radius: 10px;
    background: var(--pink-110);
    box-shadow: 0 6px 12px 0 rgba(0, 0, 0, 0.05);
    text-align: center;
  }
  &__item-btn-text {
    margin-top: var(--spacing-md);
    font-size: 10px;
    font-weight: 500;
    color: var(--white);
  }
  &__divider {
    display: flex;
    align-items: center;
    justify-content: center;
    margin: var(--spacing-5xl);
  }
  .sv-divider.sv-divider--variant-basic {
    margin: var(--spacing-4xl) auto var(--spacing-3xl);
  }
  svg.checkin-text-icon {
    path[fill="white"] {
      fill: var(--white);
    }
  }
}

// 웰컴 기프트팩
.welcome-giftpack {
  &__head {
    display: flex;
    flex-direction: column;
    position: relative;
    height: 185px;
    padding: 25px var(--spacing-2xl);
    background-image: url(#{$cdn-url}/images/pages/benefits/welcome/giftpack_img_top.png);
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
  }
  &__title {
    display: flex;
    flex-direction: column;
    .solpay-bi {
      align-self: flex-start;
      width: fit-content;
      height: 24px;
    }
    strong {
      display: block;
      margin-top: 14px;
      @include font-set(headline-s, 500);
      font-weight: 500;
      color: var(--gray-500);
    }
  }
  &__body {
    padding: var(--spacing-4xl) var(--container-padding-mobile);
  }
  &__subtitle {
    margin-bottom: var(--spacing-md);
    @include font-set(title-m, 800);
    font-weight: 800;
    color: var(--text-primary);
  }
  &__content {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-template-rows: repeat(2, 1fr);
    gap: 0;
    padding: var(--spacing-4xl) 0 var(--spacing-2xl);
    ~ .sc-banner {
      margin-top: var(--spacing-3xl);
    }
  }
  &__item {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: var(--spacing-3xl) 0;
    border-top: 1px solid var(--border-secondary);
    &:nth-child(2n) {
      border-left: 1px solid var(--border-secondary);
    }
    &:nth-child(1),
    &:nth-child(2) {
      border-top: none;
    }
  }
  &__item-image {
    overflow: hidden;
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 52px;
    height: 52px;
    margin-bottom: var(--spacing-lg);
    border-radius: var(--radius-full);
    img {
      width: 100%;
      height: 100%;
      border-radius: var(--radius-full);
      object-fit: contain;
      &.tbd {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        border-radius: none;
      }
      // 다크 모드 이미지는 기본적으로 숨김
      &[src*="_dark"] {
        display: none;
      }
    }
    // 다크 모드일 때 라이트 모드 이미지 숨김, 다크 모드 이미지 표시
    [data-theme="dark"] & {
      img:not([src*="_dark"]) {
        display: none;
      }
      img[src*="_dark"] {
        display: block;
      }
    }
  }
  &__item-text {
    display: flex;
    flex-direction: column;
    text-align: center;
    strong,
    span {
      display: block;
    }
    strong {
      @include font-set(title-s, 500);
      font-weight: 500;
      color: var(--text-secondary);
    }
    span {
      @include font-set(body-s, 300);
      font-weight: 300;
      color: var(--text-quaternary);
    }
  }
  .sv-divider.sv-divider--variant-group {
    margin: 0;
  }
  .sv-divider.sv-divider--variant-basic {
    margin: var(--spacing-4xl) auto var(--spacing-3xl);
  }
}

// 진행 중인 쿠폰
.sc-contents__category {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-2xl);
  padding: 0 var(--container-padding-mobile);
  .category-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: var(--spacing-md);
    width: 100%;
    min-width: 0;
  }
  .category-item__left,
  .category-item__right {
    display: inline-flex;
    align-items: center;
  }
  .sv-dropdown--variant-ghost .sv-dropdown__trigger {
    padding-left: 0;
  }
  ~ .sc-contents__body {
    .cupon-list__wrap {
      padding-top: var(--spacing-lg);
    }
  }
}
.svg {
  &_custom_card_price_title,
  &_custom_card_header_title {
    .path_text01 {
      fill: var(--text-primary);
    }
  }
}

// 쿠폰북
.coupon-book {
  &__title {
    padding-right: var(--container-padding-mobile);
    padding-left: var(--container-padding-mobile);
    @include font-set(headline-s, 700);
    font-weight: 700;
    color: var(--text-primary);
  }
  &__title-sub {
    margin-bottom: var(--spacing-lg);
    padding-right: var(--container-padding-mobile);
    padding-left: var(--container-padding-mobile);
    @include font-set(title-l, 700);
    font-weight: 700;
    color: var(--text-secondary);
  }
  section {
    margin-top: var(--spacing-4xl);
  }
  &__carousel {
    display: flex;
    overflow-x: auto;
    -webkit-overflow-scrolling: touch;
    scroll-snap-type: x mandatory;
    padding: 0;
    scrollbar-width: none; // Firefox
    -ms-overflow-style: none; // IE/Edge
    &::-webkit-scrollbar {
      display: none; // Chrome, Safari, Opera
    }
  }
  &__card {
    scroll-snap-align: center;
    display: flex;
    align-items: center;
    flex-shrink: 0;
    &:first-child {
      padding-left: var(--container-padding-mobile);
      .coupon-book__card-item {
        margin-left: 0;
      }
    }
    &:last-child {
      padding-right: var(--container-padding-mobile);
      .coupon-book__card-item {
        margin-right: 0;
      }
    }
  }

  &__card-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    width: 136px;
    height: 182px;
    margin-left: var(--spacing-md);
    padding: var(--spacing-md) 0;
    border-radius: var(--radius-xl);
    background: var(--bg-canvas_gray_light);
  }

  &__card-img {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    overflow: hidden;
    width: 48px;
    height: 48px;
    border-radius: var(--radius-xl);

    img {
      width: 100%;
      height: 100%;
      object-fit: contain;
    }
  }

  &__card-texts {
    text-align: center;
    color: var(--text-secondary);
    display: flex;
    flex-direction: column;
    gap: var(--spacing-2xs);
  }

  &__card-brand {
    margin-top: var(--spacing-lg);
    margin-bottom: var(--spacing-sm);
    @include font-set("body-s", 300);
    font-weight: 300;
    color: var(--text-tertiary);
  }

  &__card-reward {
    @include font-set("title-m", 700);
    font-weight: 700;
    color: var(--text-secondary);
  }
}

// 진행 중인 쿠폰, 쿠폰 검색 하단 토스트 위치 (쿠폰 검색 위에 위치)
.sc-coupon__ongoing {
  ~ .sc-toast-container--bottom {
    bottom: 52px;
  }
}

// tooltip-recommend-benefit 바운스 애니메이션
@keyframes tooltipBouncy {
  0% {
    transform: translateX(-50%) translateY(0);
  }
  50% {
    transform: translateX(-50%) translateY(5px);
  }
  100% {
    transform: translateX(-50%) translateY(0);
  }
}

// bf-recommend-benefit__body 페이드인 애니메이션
@keyframes bodyFadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

// webzine-list li 페이드인 애니메이션
@keyframes itemFadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

// sv-pagination 페이드인 애니메이션
@keyframes paginationFadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}















// 배너 타입
.sc-banner {
  --banner-min-height: 96px;
  --banner-image-width: 80px;
  display: grid;
  grid-template-columns: var(--banner-image-width) 1fr;
  align-items: center;
  gap: var(--spacing-md);
  min-height: var(--banner-min-height);
  padding: 0 var(--spacing-2xl);
  padding-left: var(--spacing-lg);
  border-radius: var(--radius-xl);
  background-color: var(--bg-banner_gray_solid);
  &[role="link"],
  &[role="button"] {
    cursor: pointer;
  }

  /* 배너 컬러 정의
  data-color="bg-banner_gray_solid"
  data-color="bg-banner_brand_tint-same"
  data-color="bg-banner_indigo_tint-same"
  data-color="bg-banner_purple_tint-same"
  data-color="bg-banner_gray_solid-same"
  data-color="bg-banner_brand_solid-same"
  data-color="bg-banner_indigo_solid-same"
  data-color="bg-banner_purple_solid-same"
  data-color="seafoam-700"
  */
  &[data-color="bg-banner_gray_solid"] {
    background-color: var(--bg-banner_gray_solid);
  }
  &[data-color="bg-banner_brand_tint-same"] {
    background-color: var(--bg-banner_brand_tint-same);
  }
  &[data-color="bg-banner_indigo_tint-same"] {
    background-color: var(--bg-banner_indigo_tint-same);
  }
  &[data-color="bg-banner_purple_tint-same"] {
    background-color: var(--bg-banner_purple_tint-same);
  }
  &[data-color="bg-banner_gray_solid-same"] {
    background-color: var(--bg-banner_gray_solid-same);
  }
  &[data-color="bg-banner_brand_solid-same"] {
    background-color: var(--bg-banner_brand_solid-same);
  }
  &[data-color="bg-banner_indigo_solid-same"] {
    background-color: var(--bg-banner_indigo_solid-same);
  }
  &[data-color="bg-banner_purple_solid-same"] {
    background-color: var(--bg-banner_purple_solid-same);
  }
  &[data-color="seafoam-700"] {
    background-color: var(--seafoam-700);
  }
  &[data-color="bg-banner_brand_solid-same"],
  &[data-color="bg-banner_indigo_solid-same"],
  &[data-color="bg-banner_purple_solid-same"],
  &[data-color="seafoam-700"] {
    .sc-banner__text {
      strong, span {
        color: var(--text-ondark_primary-same) !important;
      }
    }
  }
  &[data-type^="b"] {
    padding: var(--spacing-md) 0;
    border-radius: 0;
    background-color: var(--bg-canvas_white);
    .sc-banner__image {
      overflow: hidden;
    }
    .sc-banner__text {
      strong {
        color: var(--text-secondary);
        &.banner-button {
          display: flex;
          align-items: center;
          color: var(--text-brand);
          .sv-icon {
            color: var(--fg-brand-same);
          }
        }
      }
      span {
        color: var(--text-quaternary);
      }
    }
  }
  &[data-type="b"] {
    --banner-min-height: 104px;
    --banner-image-width: 80px;
  }
  &[data-type="b-image"] {
    --banner-min-height: 88px;
    --banner-image-width: 100px;
    --banner-image-height: 70px;
    .sc-banner__image {
      width: auto;
      max-width: var(--banner-image-width);
      height: var(--banner-image-height);
      border-radius: var(--radius-md);
      img {
        object-fit: cover;
      }
    }
  }
  &[data-type^="c"] {
    --banner-min-height: 56px;
    --banner-image-width: 56px;
    padding: var(--spacing-lg);
    .sc-banner__text {
      strong {
        color: var(--text-secondary);
      }
      span {
        color: var(--text-quaternary);
      }
    }
  }
  &[data-type="c-button"] {
    .sc-banner__text {
      span.more-button {
        color: var(--text-brand);
        .sv-icon {
          color: var(--fg-brand-same);
        }
      }
    }
  }
  &__image {
    width: auto;
    max-width: var(--banner-image-width);
    height: var(--banner-image-width);
    img {
      width: 100%;
      height: 100%;
      object-fit: contain;
    }
  }
  &__text {
    display: flex;
    flex-direction: column;
    min-width: 0;
    strong,
    span {
      display: block;
    }
    strong {
      @include font-set("body-l", 700);
      font-weight: 700;
      color: var(--text-primary);
      word-break: keep-all;
    }
    span {
      @include font-set("detail-l", 500);
      font-weight: 500;
      color: var(--text-quaternary);
      &.more-button {
        display: flex;
        align-items: center;
        .sv-icon {
          margin: 0;
          margin-left: var(--spacing-xs);
          color: var(--fg-secondary);
        }
      }
    }
  }
  &.is-reverse {
    .sc-banner__text {
      flex-direction: column-reverse;
    }
  }
  &.rtl {
    direction: rtl;
    padding-right: var(--spacing-lg);
    padding-left: var(--spacing-2xl);
    .sc-banner__text {
      direction: ltr;
    }
    &[data-type^="b"] {
      padding-right: 0;
      padding-left: 0;
    }
  }
}
// 프로모션 배너
.promotion-banner {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
  position: relative;
  height: 80px;
  margin: 0 var(--container-padding-mobile);
  padding: 0;
  border-radius: var(--radius-xl);
  background-color: var(--bg-canvas_white);
  background-repeat: no-repeat;
  // background-attachment: fixed;
  background-size: 100% 100%;
  // 애니메이션 중에는 transition 비활성화
  animation-fill-mode: forwards;
  .banner-link {
    overflow: hidden;
    display: flex;
    align-items: center;
    flex: 1 1 auto;
    min-width: 0;
    padding: var(--spacing-xl) var(--container-padding-mobile);
    background-color: var(--bg-canvas_white);
  }
  &.sc-swipe-dismissed {
    // 펼침(등장): 500ms, 강조-감속(0.05, 0.7, 0.1, 1.0)
    // 애니메이션이 끝난 후 최종 상태 유지
    animation: promotionBannerExpand 500ms cubic-bezier(0.05, 0.7, 0.1, 1) 300ms
      forwards;
  }

  // 접힘(퇴장) 애니메이션
  &.promotion-banner-collapse {
    animation: promotionBannerCollapse 200ms cubic-bezier(0.3, 0, 0.8, 0.15)
      forwards;
  }

  // 펼침(등장) keyframes 애니메이션
  @keyframes promotionBannerExpand {
    0% {
      height: 80px;
      padding: 0;
    }
    100% {
      height: 178px;
      padding: 0;
    }
  }

  // 접힘(퇴장) keyframes 애니메이션
  @keyframes promotionBannerCollapse {
    from {
      height: 178px;
      padding: 0;
    }
    to {
      height: 80px;
      padding: 0;
    }
  }
  &__inner {
    overflow: hidden;
    display: flex;
    align-items: center;
    flex: 1 1 auto;
    position: absolute;
    top: 0;
    left: 0;
    width: var(--inner-width, calc(100% - 24px));
    min-width: 0;
    border-radius: 0 var(--radius-xl) var(--radius-xl) 0;
    background-color: var(--bg-canvas_white);
    touch-action: pan-x;
    opacity: var(--inner-opacity, 1);
    transition: width var(--transition-duration, 300ms)
      cubic-bezier(0.4, 0, 0.2, 1);

    &[style*="--is-dismissed: 1"] {
      pointer-events: none;
      visibility: hidden;
      display: none;
    }

    &:not([style*="--is-dismissed: 1"]) {
      pointer-events: auto;
      visibility: visible;
      display: flex;
    }
  }
  @at-root .promotion-banner .promotion-banner__inner .banner-link {
    padding-right: 0;
    padding-left: 0;
    span,
    p {
      white-space: nowrap;
    }
  }
  &__bg {
    width: 100%;
    max-height: 100%;
    border-radius: var(--radius-xl);
  }
  &__img {
    flex-shrink: 0;
    width: 100%;
    height: 100%;
    max-width: 48px;
    object-fit: contain;
  }
  &__contents {
    display: flex;
    flex-direction: column;
    flex: 1 1 auto;
    min-width: 0;
    margin-left: var(--spacing-md);
  }
  strong {
    @include font-set(title-m, 500);
    font-weight: 500;
    color: var(--text-secondary);
  }
  span {
    @include font-set(body-s, 300);
    font-weight: 300;
    color: var(--text-quaternary);
  }
  p {
    margin-top: var(--spacing-xs);
    @include font-set(body-s, 300);
    color: var(--text-quaternary);
    &.text-bold {
      @include font-set(title-m, 500);
      font-weight: 500;
      color: var(--text-secondary);
    }
  }
  .sv-icon-button {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    right: var(--spacing-md);
    flex-shrink: 0;
    width: 40px;
    height: 40px;
    padding: 0;
    color: var(--fg-quaternary);
    &:active:not(:disabled) {
      position: absolute;
      transform: translateY(-50%) scale(0.96);
    }
  }
  .close-button {
    position: absolute;
    top: 10px;
    right: 10px;
    z-index: 1;
    transform: none;
    width: 34px;
    height: 34px;
    color: var(--fg-ondark_primary-same);
    &::before,
    &::after {
      display: none;
    }
    &:active:not(:disabled) {
      transform: none;
    }
  }
  .promotion-banner__button.sv-button--rounded.sv-button--variant-outline {
    position: absolute;
    bottom: var(--spacing-2xl);
    left: 50%;
    transform: translateX(-50%);
    height: 48px;
    padding: var(--spacing-lg) var(--spacing-xl);
    border-radius: var(--radius-2xl);
    border: 1px solid transparent;
    background:
      linear-gradient(var(--white-a60), var(--white-a60)) padding-box,
      linear-gradient(
          180deg,
          rgba(255, 255, 255, 0.3) 0%,
          rgba(255, 255, 255, 0.09) 50%,
          rgba(255, 255, 255, 0.3) 100%
        )
        border-box;
    backdrop-filter: blur(2px);
    .sv-button__label {
      @include font-set(body-l, 500);
      font-weight: 500;
      color: var(--text-primary-same);
      white-space: nowrap;
    }
    .sv-button__right-icon {
      width: 20px !important;
      height: 20px !important;
      color: var(--fg-primary);
    }
  }
  &__handle {
    position: absolute;
    top: 27.5px;
    right: 15px;
    width: 56px;
    height: 25px;
    border-radius: var(--radius-full);
    background: linear-gradient(90deg, #ffffff 0%, #c2d3ff 100%);
    touch-action: pan-x;
    opacity: var(--handle-opacity, 1);
    transition: opacity var(--transition-duration, 300ms)
      cubic-bezier(0.4, 0, 0.2, 1);
    .handle-button {
      display: flex;
      align-items: center;
      justify-content: center;
      position: absolute;
      right: 0;
      width: 25px;
      height: 25px;
      border-radius: 50%;
      border: 0;
      background: var(--fg-brand-same);
      cursor: pointer;
      touch-action: pan-x;
      // promotion-banner__handle 영역의 가운데까지 좌우 반복 애니메이션
      animation: handleButtonSway 2.5s ease-out 1ms infinite;
      transition: transform var(--transition-duration, 300ms)
        cubic-bezier(0.4, 0, 0.2, 1);

      // --handle-offset이 0px가 아닐 때는 애니메이션 비활성화하고 transform 적용
      &[style*="--handle-offset"]:not([style*="--handle-offset: 0px"]) {
        animation: none;
        transform: translateX(var(--handle-offset, 0px));
      }
      .sv-icon {
        color: var(--fg-ondark_primary-same);
        // 좌우로 움직이는 애니메이션
        animation: iconSway 2s ease-out infinite;
      }
    }

    // handle-button 좌우 반복 애니메이션 (가운데까지)
    @keyframes handleButtonSway {
      0%,
      100% {
        transform: translateX(0px);
      }
      50% {
        transform: translateX(-15.5px); // (56px - 25px) / 2 = 15.5px
      }
    }

    // sv-icon 좌우 반복 애니메이션
    @keyframes iconSway {
      0%,
      100% {
        transform: translateX(0px);
      }
      50% {
        transform: translateX(-2px); // 작은 범위로 좌우 움직임
      }
    }

    // sc-popover__custom 위아래 반복 애니메이션 (위에서 시작해서 아래로)
    @keyframes popoverBounce {
      0%,
      100% {
        transform: translateX(-50%) translateY(-4px); // 위 위치
      }
      50% {
        transform: translateX(-50%) translateY(4px); // 아래로 움직임
      }
    }
    .sc-popover__custom {
      padding: 4px 8px;
      border-radius: var(--radius-full);
      // 위아래로 움직이는 애니메이션
      animation: popoverBounce 2.5s ease-out 1ms infinite;
      &.hide-close[data-placement^="top-"] {
        opacity: 1 !important;
      }
      &[data-placement="top-center"] {
        left: 50%;
        transform: translateX(-50%);
        bottom: calc(100% + 12px);
        &::after {
          content: "";
          position: absolute;
          width: 0;
          height: 0;
          top: auto;
          bottom: -10px;
          left: 50%;
          transform: translateX(-50%);
          z-index: 11;
          // 화살표 border 설정 (popover가 위에 위치하므로 화살표는 위를 가리킴)
          border-top: 5px solid var(--bg-dark);
          border-right: 5px solid transparent;
          border-bottom: 5px solid transparent;
          border-left: 5px solid transparent;
        }
      }
      &[data-placement="bottom-center"] {
        left: 50%;
        transform: translateX(-50%);
        top: calc(100% + 16px);
        &::after {
          content: "";
          position: absolute;
          width: 0;
          height: 0;
          bottom: auto;
          top: -16px;
          left: 50%;
          transform: translateX(-50%);
          z-index: 11;
          // 화살표 border 설정 (popover가 아래에 위치하므로 화살표는 아래를 가리킴)
          border-top: 8px solid transparent;
          border-right: 8px solid transparent;
          border-bottom: 8px solid var(--bg-dark);
          border-left: 8px solid transparent;
        }
      }
      // 애니메이션 중지 클래스
      &.animation-paused {
        animation: none;
      }
      .sc-popover__custom-content {
        @include font-set("detail-s", 500);
        font-weight: 500;
        color: var(--text-ondark_primary);
        span {
          font-size: inherit;
          line-height: inherit;
          letter-spacing: inherit;
          font-weight: inherit;
          font-weight: inherit;
          color: inherit;
        }
      }
    }
  }
  &[data-color="solid-same"] {
    margin-bottom: 0;
    padding: 0 var(--spacing-2xl);
    background-color: transparent;

    .banner-link {
      min-height: 68px;
      margin-right: 0;
      padding: var(--spacing-md) var(--spacing-2xl);
      border-radius: var(--radius-xl);
      background-color: var(--bg-banner_gray_solid-same);
    }
    strong,
    span,
    p,
    .text-bold {
      color: var(--text-ondark_primary-same);
    }
    .promotion-banner__contents {
      margin-right: var(--spacing-md);
      margin-left: 0;
    }
    .promotion-banner__img {
      max-width: 52px;
    }
  }
  &__basic {
    height: auto;
    margin: 0 var(--container-padding-mobile);
    border-radius: 0;
    .sc-banner {
    }
  }
  ~ [class^="promotion-banner"] {
    margin-top: var(--spacing-lg);
  }
}

// 웹진형 리스트
.webzine-list {
  display: flex;
  width: 100%;
  &.skeleton {
    display: block;
    margin: 0;
    padding: 0;
    .webzine-item {
      display: flex;
      padding: var(--spacing-lg) var(--container-padding-mobile);
      ~ .webzine-item {
        margin-top: var(--spacing-sm);
      }
    }
    .webzine-item__thumbnail {
      display: flex;
      align-items: center;
      justify-content: center;
      flex: 0 0 auto;
      min-width: 48px;
      max-width: 48px;
    }
    .webzine-item__content {
      display: flex;
      flex-direction: column;
      gap: var(--spacing-xs);
      flex: 1 1 auto;
      min-width: 0;
      margin-left: var(--spacing-lg);
    }
  }
  &.vertical {
    flex-direction: column;
    li ~ li {
      margin-top: var(--spacing-md);
    }
  }
}
.webzine-item {
  display: flex;
  width: 100%;
  &__before {
    flex: 0 0 auto;
    width: 56px;
    height: 56px;
    img {
      width: 100%;
      height: 100%;
      object-fit: contain;
    }
    &.circle {
      width: 32px;
      height: 32px;
      border-radius: 50%;
      border: 1px solid var(--white-a80);
      background-color: var(--white-a60);
      img {
        border-radius: 50%;
      }
    }
  }
  &__contents {
    flex: 1 1 auto;
    display: flex;
    gap: var(--spacing-sm);
    flex-direction: column;
    align-items: center;
    margin-left: var(--spacing-md);
    margin-right: var(--spacing-sm);
  }
  &__after {
    display: flex;
    align-items: center;
    justify-content: center;
    flex: 0 0 auto;
    width: 56px;
    height: 56px;
  }
  &.sv-basic-list {
    display: flex;
    align-items: center;
    justify-content: flex-start;
    width: 100%;
    padding: var(--spacing-md) var(--spacing-lg);
    border-radius: var(--radius-md);
    &[data-color="--palette-blue-100"] {
      background-color: var(--palette-blue-100);
    }
    &[data-color="--palette-monotone-100"] {
      background-color: var(--palette-monotone-100);
    }
    &[data-color="--palette-indigo-100"] {
      background-color: var(--palette-indigo-100);
    }
    .webzine-item__contents {
      justify-content: center;
      align-items: flex-start;
      text-align: left;
      .webzine-item__label {
        @include ellipsis(1);
        @include font-set("title-s", 500);
        font-weight: 500;
        color: var(--text-primary-same);
      }
    }
    .webzine-item__after {
      width: auto;
      height: auto;
      .sv-base-badge__indicator {
        top: 0;
        right: 0;
      }
      .sv-base-badge--inline {
        border-radius: var(--radius-full);
        /* Shadow 1 */
        box-shadow: 0 4px 16px 0 rgba(12, 17, 29, 0.06);
        .sv-base-badge__indicator {
          margin: 0;
        }
      }
      .sv-base-badge--variant-tint.sv-base-badge--color-gray {
        .sv-base-badge__indicator {
          position: relative;
          border-radius: var(--radius-full);
          background: var(--white-a40);
          border: 1px solid transparent;
          color: var(--text-primary-same);

          &::before {
            content: "";
            position: absolute;
            inset: 0;
            border-radius: var(--radius-full, 9999px);
            padding: 1px;
            background: linear-gradient(
              180deg,
              var(--white, rgba(255, 255, 255, 0.3)) 0%,
              var(--white-white-a30, rgba(255, 255, 255, 0.09)) 50%,
              var(--white, rgba(255, 255, 255, 0.3)) 100%
            );
            -webkit-mask:
              linear-gradient(#fff 0 0) content-box,
              linear-gradient(#fff 0 0);
            -webkit-mask-composite: xor;
            mask:
              linear-gradient(#fff 0 0) content-box,
              linear-gradient(#fff 0 0);
            mask-composite: exclude;
            pointer-events: none;
            z-index: -1;
          }
        }
      }
      .sv-base-badge--type-text {
        .sv-base-badge__indicator {
          min-height: 28px;
          padding: var(--spacing-xs) var(--spacing-md);
          border-radius: var(--radius-full);
        }
      }
    }
  }
  .sv-basic-list__content {
    display: flex;
    flex: 1 1 auto;
    align-items: center;
    min-width: 0;
    margin: 0;
  }
}

// custom popover style
.sc-popover__custom {
  display: block;
  position: absolute;
  z-index: 10;
  width: max-content;
  max-width: 260px;
  height: auto;
  padding: var(--spacing-md) var(--spacing-lg);
  border-radius: var(--radius-xs);
  background-color: var(--bg-dark);
  &-content {
    display: block;
    @include font-set("body-s", 500);
    font-weight: 500;
    color: var(--text-ondark_primary);
    span {
      white-space: nowrap;
    }
  }
  // 화살표 공통 스타일
  &::after {
    content: "";
    position: absolute;
    width: 0;
    height: 0;
    border-top: 8px solid transparent;
    border-right: 8px solid transparent;
    border-bottom: 8px solid transparent;
    border-left: 8px solid transparent;
  }
  // placement별 위치 및 화살표 설정
  $placements: (
    "bottom-center": (
      "container-position": "top",
      "container-align": "left",
      "container-transform": "translateX(-50%)",
      "arrow-position": "top",
      "arrow-align": "left",
      "arrow-transform": "translateX(-50%)",
      "arrow-border": "border-bottom",
    ),
    "bottom-left": (
      "container-position": "top",
      "container-align": "left",
      "container-transform": "translateX(0)",
      "arrow-position": "top",
      "arrow-align": "left",
      "arrow-transform": "translateX(0)",
      "arrow-border": "border-bottom",
    ),
    "bottom-right": (
      "container-position": "top",
      "container-align": "right",
      "container-transform": "translateX(0)",
      "arrow-position": "top",
      "arrow-align": "right",
      "arrow-transform": "translateX(0)",
      "arrow-border": "border-bottom",
    ),
    "top-center": (
      "container-position": "bottom",
      "container-align": "left",
      "container-transform": "translateX(-50%)",
      "arrow-position": "bottom",
      "arrow-align": "left",
      "arrow-transform": "translateX(-50%)",
      "arrow-border": "border-top",
    ),
    "top-left": (
      "container-position": "bottom",
      "container-align": "left",
      "container-transform": "translateX(0)",
      "arrow-position": "bottom",
      "arrow-align": "left",
      "arrow-transform": "translateX(0)",
      "arrow-border": "border-top",
    ),
    "top-right": (
      "container-position": "bottom",
      "container-align": "right",
      "container-transform": "translateX(0)",
      "arrow-position": "bottom",
      "arrow-align": "right",
      "arrow-transform": "translateX(0)",
      "arrow-border": "border-top",
    ),
    "right-center": (
      "container-position": "right",
      "container-align": "top",
      "container-transform": "translateY(-50%)",
      "arrow-position": "left",
      "arrow-align": "top",
      "arrow-transform": "translateY(-50%)",
      "arrow-border": "border-left",
    ),
    "left-center": (
      "container-position": "left",
      "container-align": "top",
      "container-transform": "translateY(-50%)",
      "arrow-position": "right",
      "arrow-align": "top",
      "arrow-transform": "translateY(-50%)",
      "arrow-border": "border-right",
    ),
  );

  @each $placement, $config in $placements {
    &[data-placement="#{$placement}"] {
      #{map.get($config, "container-position")}: calc(100% + 8px);
      #{map.get($config, "container-align")}: 50%;
      transform: #{map.get($config, "container-transform")};
      &::after {
        #{map.get($config, "arrow-position")}: -16px;
        #{map.get($config, "arrow-align")}: 50%;
        transform: #{map.get($config, "arrow-transform")};
        z-index: 11;
        // 모든 border를 transparent로 초기화 후 특정 border만 색상 적용
        border-top: 8px solid transparent;
        border-right: 8px solid transparent;
        border-bottom: 8px solid transparent;
        border-left: 8px solid transparent;
        #{map.get($config, "arrow-border")}: 8px solid var(--bg-dark);
      }
    }
  }

  // bottom-left 특별 스타일
  &[data-placement="bottom-left"] {
    top: calc(100% + 8px);
    left: 0;
    transform: translateX(0);
    &::after {
      left: 24px;
      transform: translateX(0);
    }
  }

  // bottom-right 특별 스타일
  &[data-placement="bottom-right"] {
    top: calc(100% + 8px);
    right: 0;
    transform: translateX(0);
    &::after {
      right: 24px;
      transform: translateX(0);
    }
  }

  // top-left 특별 스타일
  &[data-placement="top-left"] {
    bottom: calc(100% + 8px);
    left: 0;
    transform: translateX(0);
    &::after {
      left: 24px;
      transform: translateX(0);
    }
  }

  // top-right 특별 스타일
  &[data-placement="top-right"] {
    bottom: calc(100% + 8px);
    right: 0;
    transform: translateX(0);
    &::after {
      right: 24px;
      transform: translateX(0);
    }
  }
}

```
{% endraw %}

---
