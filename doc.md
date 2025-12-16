# test

{% raw %}
```scss

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

```
{% endraw %}

---
