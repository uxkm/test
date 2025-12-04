# test
```scss
// 251204
// layout 60 line

  @at-root .sc-main .sv-navigation {
    .sv-navigation__title {
      .sc-icon {
        display: none;
      }
      h1 {
        @include font-set(title-l, 700);
        font-weight: 700;
        color: var(--text-secondary);
      }
    }
    .sv-navigation__right {
      .sv-button--color-primary {
        color: var(--text-primary);
      }
    }
  }
```
