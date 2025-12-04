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

// input-field

  .field-item__rowgroup {
    // 14번 케이스: label 텍스트가 줄바꿈되지 않도록 설정
    .sv-input-label__text {
      white-space: nowrap;
    }


// ScHeader.vue

      v-if="variant === 'main'"
      #title
    >
      <ScIcon iconName="shinhan" />
      <h1>{{ title || '신한카드' }}</h1>
```
