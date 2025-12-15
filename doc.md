# test

{% raw %}
```scss




  &.search-type {
    gap: 0;
    padding-bottom: 0;
    .usage-history__dropdown {
      margin-top: var(--spacing-xl);
      margin-bottom: 0;
    }
  }
  // 참여한 이벤트 스타일
  &.event-applied {
    padding-bottom: var(--spacing-2xl);
    .usage-history__dropdown {
      margin-bottom: 0;
    }
  }
  // 진행중인 쿠폰
  &.coupon-ongoing {
    gap: var(--spacing-2xl);
    padding-bottom: 0;
  }

  // 쿠폰 검색
  &.coupon-ongoing__search {
    padding-bottom: 0;
    ~ .sv-chip-group--size-s .sv-chip-group__container {
      padding-top: var(--spacing-xl);
      padding-right: var(--container-padding-mobile);
      padding-left: var(--container-padding-mobile);
    }
    ~ .sc-contents__body .cupon-list__wrap {
      padding-top: var(--spacing-2xl);
    }
    &.is-typing {
      ~ .sc-contents__body {
        margin-top: var(--spacing-xl);
      }
    }
  }

  // 맞춤 혜택
  &.user-benefit {
    padding-bottom: 0;
  }

  ~ .sc-contents__body {
    .cupon-list__wrap {
      padding-top: var(--spacing-lg);
    }
  }

```
{% endraw %}

---
