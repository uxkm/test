# test

{% raw %}
```scss

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
