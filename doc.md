# test

{% raw %}
```scss


.category-list {
      display: flex;
      justify-content: center;
      align-items: center;
      > .category-list__item + .category-list__item {
        margin-left: var(--spacing-2xl);
      }
      > .category-list__item:first-child:nth-last-child(2) ~ .category-list__item {
        margin-left: var(--spacing-6xl);
      }
      &__item {
        display: flex;
        align-items: center;
        justify-content: center;
        flex: 1 1 auto;
        max-width: 90px;
      }
      &__link {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
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





    isolation: isolate;

    // shadow 영역 (59x80) - 핸들 영역 오른쪽 정렬
    &::after {
      content: "";
      position: absolute;
      inset: -27px auto auto -12px;
      width: 59px;
      height: 80px;
      border-radius: 0;
      // box-shadow: 0 4px 16px 0 rgba(12, 17, 29, 0.06);
      box-shadow:
        0 1px 1px -1px rgba(0, 0, 0, 0.06),
        0 2px 2px -2px rgba(0, 0, 0, 0.05),
        0 3px 3px -3px rgba(0, 0, 0, 0.04),
        0 4px 4px -4px rgba(0, 0, 0, 0.03),
        0 5px 5px -5px rgba(0, 0, 0, 0.02),
        0 6px 6px -6px rgba(0, 0, 0, 0.01);
      pointer-events: none;
    }


        0 1px 1px -1px rgba(12, 17, 29, 0.06),
        0 1.2px 1.2px -1.33px rgba(12, 17, 29, 0.057),
        0 1.4px 1.4px -1.67px rgba(12, 17, 29, 0.053),
        0 1.6px 1.6px -2px rgba(12, 17, 29, 0.05),
        0 1.8px 1.8px -2.33px rgba(12, 17, 29, 0.047),
        0 2px 2px -2.67px rgba(12, 17, 29, 0.043),
        0 2.2px 2.2px -3px rgba(12, 17, 29, 0.04),
        0 2.4px 2.4px -3.33px rgba(12, 17, 29, 0.037),
        0 2.6px 2.6px -3.67px rgba(12, 17, 29, 0.033),
        0 2.8px 2.8px -4px rgba(12, 17, 29, 0.03),
        0 3px 3px -4.33px rgba(12, 17, 29, 0.027),
        0 3.2px 3.2px -4.67px rgba(12, 17, 29, 0.023),
        0 3.4px 3.4px -5px rgba(12, 17, 29, 0.02),
        0 3.6px 3.6px -5.33px rgba(12, 17, 29, 0.017),
        0 3.8px 3.8px -5.67px rgba(12, 17, 29, 0.013),
        0 4px 4px -6px rgba(12, 17, 29, 0.01);




        .img-feedback-nodata {
          width: 56px;
          height: 56px;
          object-fit: contain;
        }


// benefits
.cupon-top__btngroup {
  padding: 0 var(--container-padding-mobile);
  .sv-divider {
    // margin-block: var(--spacing-2xl);
    margin-top: var(--spacing-2xl);
    margin-bottom: var(--spacing-2xl);
  }
  .sv-button {
    .sv-button__left-icon {
      width: auto !important;
      height: auto !important;
    }
    .sv-button__label {
      color: var(--text-secondary);
    }
    img {
      width: 34px;
      height: 34px;
      object-fit: contain;
    }
  }
}

  --env-t: env(safe-area-inset-top, 0px);
  --env-l: env(safe-area-inset-left, 0px);
  --env-r: env(safe-area-inset-right, 0px);
  --env-b: env(safe-area-inset-bottom, 0px);


  padding-top: var(--env-t);
  padding-left: var(--env-l);
  padding-right: var(--env-r);
  padding-bottom: var(--env-b);

.promotion-banner__button.sv-button--rounded.sv-button--variant-outline {
    position: absolute;
    bottom: var(--spacing-2xl);
    left: 50%;
    transform: translateX(-50%);
    height: 48px;
    padding: var(--spacing-lg) var(--spacing-xl);
    border-radius: var(--radius-2xl);
    border: none;
    background: var(--white-a60);
    // 레거시 브라우저 fallback: backdrop-filter 미지원 시 기본 배경만 적용
    backdrop-filter: blur(4px);
    &::before {
      content: "";
      clear: both;
      display: block;
      position: absolute;
      top: 50%;
      left: 50%;
      width: 100%;
      min-width: 36px;
      height: 100%;
      min-height: 36px;
      transform: translate(-50%, -50%);
      border-radius: var(--radius-2xl);
      padding: 1px;
      background: linear-gradient(
        180deg,
        rgba(255, 255, 255, 0.3) 0%,
        rgba(255, 255, 255, 0.09) 50%,
        rgba(255, 255, 255, 0.3) 100%
      );
      // 레거시 브라우저 fallback: mask 미지원 시 단순 border로 표시
      border: 1px solid rgba(255, 255, 255, 0.3);
    }
    // 최신 브라우저: mask 지원 시 그라데이션 border 적용
    @supports (mask-composite: exclude) or (-webkit-mask-composite: xor) {
      &::before {
        border: none;
        mask:
          linear-gradient(#fff 0 0) content-box,
          linear-gradient(#fff 0 0);
        -webkit-mask:
          linear-gradient(#fff 0 0) content-box,
          linear-gradient(#fff 0 0);
        -webkit-mask-composite: xor;
        mask-composite: exclude;
      }
    }
    .sv-button__label {
      @include font-set(body-l, 500);
      font-weight: 500;
      color: var(--text-primary-same);
      white-space: nowrap;
      position: relative;
      z-index: 1;
    }
    .sv-button__right-icon {
      width: 20px !important;
      height: 20px !important;
      color: var(--fg-primary);
      position: relative;
      z-index: 1;
    }
  }


```
{% endraw %}

---
