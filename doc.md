# test
```scss
// 251205
// utillity


// card grid skeleton style
.card-grid__skeleton {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: var(--spacing-2xl) var(--spacing-xl);
  padding-top: var(--spacing-3xl);
  // padding-inline: var(--container-padding-mobile);
  padding-right: var(--container-padding-mobile);
  padding-left: var(--container-padding-mobile);
  .card-list__item {
    overflow: hidden;
    display: flex;
    flex-direction: column;
    gap: var(--spacing-md);
    justify-content: flex-start;
    position: relative;
    padding: 0;
    .item-img {
      overflow: hidden;
      display: flex;
      flex: 0 0 auto;
      align-items: center;
      justify-content: center;
      min-height: 160px;
      border-radius: var(--radius-xl);
      .sv-loading-skeleton {
        margin: 0 auto;
        background-color: var(--bg-gray);
      }
    }

    .card-item_content {
      display: flex;
      flex-direction: column;
      gap: 6px;
      .sv-loading-skeleton.sv-loading-skeleton--rounded-none {
        border-radius: 2px;
      }
      .sv-loading-skeleton {
        background-color: var(--bg-gray);
        &:last-child {
          background-color: var(--bg-graylight);
        }
      }
    }
  }
  &.cards-first {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-none);
    width: 100%;
    margin: 0;
    padding: 0;
    .coupon-cards .svg-coupon-cards .coupon-line {
      display: none;
    }
    .card-item {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      gap: var(--spacing-md);
      min-height: 68px;
      padding: var(--spacing-xl) var(--spacing-sm) var(--spacing-lg);
      border-radius: var(--radius-lg);
      background-color: var(--bg-gray);
    }
  }
  &.apptech {
    display: block;
    padding: 0;
    article {
      ~ .inlifle-banner {
        margin-top: var(--spacing-5xl);
      }
    }
    .adpicon-banner__content {
      width: 100%;
      .sv-loading-skeleton {
        ~ .sv-loading-skeleton {
          margin-top: var(--spacing-sm);
        }
      }
      .adpicon-banner__actions {
        width: 100%;
        max-width: 100%;
        .sv-loading-skeleton {
          align-self: flex-end;
        }
      }
    }
    .adpicon-banner__card-visual {
      .sv-loading-skeleton--rounded-large {
        border-radius: var(--radius-xl) var(--radius-xl) 0 0;
      }
    }
    .adpicon-banner__controls {
      display: flex;
      justify-content: center;
      align-items: center;
      width: 100%;
      padding: var(--spacing-xl) 0;
      text-align: center;
    }
    .adpicon-banner__more {
      position: absolute;
      bottom: 8px;
      right: 0;
      width: 58px;
      height: 24px;
    }
    .sc-point-more__list {
      padding: 0 var(--container-padding-mobile);
      li {
        padding: var(--spacing-lg) 0;
        &:first-child {
          margin-top: 0;
        }
      }
    }
  }
}


// common


// 오늘의 앱테크 스타일
.today-list {
  $bg-list-brand: var(--bg-brand) !important;
  $bg-list-cyan: var(--bg-cyan) !important;
  $bg-list-red: var(--bg-red) !important;
  $bg-list-orange: var(--bg-orange) !important;
  $bg-list-crimson: var(--bg-red) !important;

  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: var(--spacing-md);

  &__item {
    width: auto;
  }
  &__link {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: var(--spacing-sm);
    // aspect-ratio: 1 / 0.8;
    padding: var(--spacing-lg);
    border-radius: var(--radius-md);
    position: relative;

    &.bg-brand {
      background-color: $bg-list-brand;
    }
    &.bg-cyan {
      background-color: $bg-list-cyan;
    }
    &.bg-red {
      background-color: $bg-list-red;
    }
    &.bg-orange {
      background-color: $bg-list-orange;
    }
    &.bg-red {
      background-color: $bg-list-red;
    }
    &.bg-brand {
      background-color: $bg-list-brand;
    }
    img {
      width: 100%;
      height: 100%;
      max-width: 62px;
      object-fit: contain;
    }
    span {
      @include font-set("body-s", 500);
      font-weight: 500;
      color: var(--text-secondary);
    }
  }

  &__badge.sv-base-badge {
    position: absolute;
    top: -4px;
    right: -1.7px;
  }

  &__icon {
    width: 64px;
    height: 64px;
    margin: auto;

    img {
      width: 100%;
      height: 100%;
      object-fit: contain;
    }
  }

  &__label {
    font-size: var(--font-size-sm);
    font-weight: var(--font-weight-medium);
    color: var(--color-text-primary);
    text-align: center;
    margin-top: auto;
  }
}
// 포인트 더 받기 스타일
.sc-point-more__list {
  .sv-list__icon {
    width: 48px;
    height: 48px;
    border-radius: var(--radius-xl);
    img {
      max-width: 100%;
      max-height: 100%;
      object-fit: contain;
    }
  }
  li {
    margin-top: var(--spacing-md);
    .point-more__item {
      display: block;
      width: 100%;
      padding: var(--spacing-lg) var(--spacing-2xl);
      text-align: left;
    }
    ~ li {
      margin-top: var(--spacing-sm);
    }
  }
}
.point-badge {
  display: flex;
  align-items: center;
  padding: var(--spacing-xs);
  padding-right: var(--spacing-md);
  border-radius: var(--radius-full);
  background-color: var(--bg-brand_strong-same);
  img {
    width: 22px;
    height: 22px;
    object-fit: contain;
  }
  span {
    margin-left: var(--spacing-sm);
    @include font-set("body-s", 700);
    font-weight: 700;
    color: var(--text-ondark_primary-same);
    white-space: nowrap;
  }
}



// benefits


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

```

---
