# test

{% raw %}
```scss


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
    p {
      margin-top: var(--spacing-xs);
      @include font-set(body-s, 300);
      color: var(--text-quaternary);
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





  &.discount-coupon {
    display: block;
    padding: 0;
    .couponbook-cards__img {
      padding: 0;
      background-color: transparent;
    }
    .couponbook-cards__content {
      width: 100%;
      min-width: 200px;
      padding-right: 28px;
      padding-left: 28px;
      .p {
        margin-top: var(--spacing-sm);
      }
    }
    .couponbook-cards__foot {
      .sv-loading-skeleton {
        flex: 1;
        min-width: 0;
        margin-left: var(--spacing-md);
      }
      .sv-button-group.sv-box-button-group--varinat-35_65 .sv-loading-skeleton:first-child {
        flex: 0 0 35%;
        margin-left: 0;
      }
    }
    .discount-coupon__search {
      .sv-loading-skeleton.right {
        margin-left: var(--spacing-md);
      }
    }
    .cupon-list__body {
      .cupon-item.skeleton {
        padding-top: var(--spacing-lg);
        .content{
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
  }

```
{% endraw %}

---
