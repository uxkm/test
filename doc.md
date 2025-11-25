# test
```scss
// 251125
// common 90

.card-list__lg {
  &.sv-card--type-list {
    .sv-card__content {
      padding: var(--spacing-lg);
    }
  }
  .sv-list__icon {
    flex: 0 0 auto;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    width: 48px;
    height: 48px;
    img {
      max-width: 100%;
      max-height: 100%;
      object-fit: contain;
    }
  }
  .sv-list__text__main {
    @include font-set(body-l, 500);
    font-weight: 500;
    color: var(--text-secondary);
  }
}
```
