# test
```scss
// 251201
// common
// 이용안내 스타일
.info-cards-popup {
  .sv-bottom-sheet__body {
    padding-bottom: var(--spacing-xl);
  }
}
.info-cards {
  display: flex;
  flex-direction: column;
  .info-card {
    .sv-card__content {
      padding: var(--spacing-xl) var(--spacing-lg);
    }
    ~ .info-card {
      margin-top: var(--spacing-md);
    }
    .sv-list__text__main {
      @include font-set("title-s", 500);
      font-weight: 500;
      color: var(--text-secondary);
    }
    .sv-list__text__sub {
      margin-top: var(--spacing-md);
      @include font-set("body-m", 300);
      font-weight: 300;
      color: var(--text-quaternary);
    }
    .sv-list__icon {
      color: var(--fg-secondary);
    }
  }
}
```
