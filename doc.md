# test
```scss
// 251204
// layout 60 line

 
  .sv-navigation__title {
    > div {
      display: inline-flex;
      align-items: center;
      gap: var(--spacing-sm);
    }
  }
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


// ScHeader.vue

      v-if="variant === 'main'"
      #title
    >
      <ScIcon iconName="shinhan" />
      <h1>{{ title || '신한카드' }}</h1>
```
