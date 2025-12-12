# test

{% raw %}
```scss
// 251215 benefits SBT158A01

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



```
{% endraw %}

---
