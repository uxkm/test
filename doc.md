# test
```scss
// 251203
// utility // custom popover style 전

.sc-bottom-info__card {
  padding: var(--spacing-xl);
  border-radius: var(--radius-md);
  background-color: var(--bg-graylight);
  @include font-set("body-m", 300);
  font-weight: 300;
  color: var(--text-quaternary);
}

.sc-banner {
  --banner-image-width: 96px;
  display: grid;
  grid-template-columns: var(--banner-image-width) 1fr;
  align-items: center;
  gap: var(--spacing-md);
  min-height: 96px;
  padding: 0 var(--spacing-2xl);
  padding-left: var(--spacing-lg);
  border-radius: var(--radius-xl);
  background-color: var(--bg-banner_indigo_tint-same);
  &[role="link"] {
    cursor: pointer;
  }

  &__image {
    width: auto;
    height: var(--banner-image-width);
    img {
      width: 100%;
      height: 100%;
      object-fit: contain;
    }
  }
  &__text {
    min-width: 0;
    strong,
    span {
      display: block;
    }
    strong {
      @include font-set("body-l", 700);
      font-weight: 700;
      color: var(--text-primary);
    }
    span {
      @include font-set("detail-l", 500);
      font-weight: 500;
      color: var(--text-quaternary);
    }
  }
  &.rtl {
    direction: rtl;
    padding-right: var(--spacing-lg);
    padding-left: var(--spacing-2xl);
    .sc-banner__text {
      direction: ltr;
    }
  }
}

// common

// benefits 진행중인 쿠폰 전

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
    &:nth-child(1), &:nth-child(2) {
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
