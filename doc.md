# test
```scss
// 251127
// line 293



// 오픈뱅킹, 신한Pay머니, 법인카드, 타사카드 이용내역
.usage-history {
  // 공통 리스트 스타일
  .sv-basic-list__content {
    min-width: 0;
    overflow: hidden;
  }
  .sv-list {
    min-width: 0;
  }
  .sv-list__item {
    min-width: 0;
  }
  .sv-list__item_inner {
    min-width: 0;
    overflow: hidden;
    justify-content: flex-start;
    gap: var(--spacing-md);
  }
  .sv-list__texts {
    min-width: 0;
    flex: 1 1 0%;
    overflow: hidden;
    max-width: 100%;
  }
  .sv-list__text {
    min-width: 0;
    &:not(.sv-list__text--right) {
      flex: 1 1 0%;
      overflow: hidden;
      max-width: 100%;
    }
  }
  time,
  em,
  strong,
  .usage-label,
  .usage-amount,
  .usage-sub {
    font-style: normal;
    font-size: inherit;
    font-weight: inherit;
    line-height: inherit;
    letter-spacing: inherit;
    color: inherit;
  }
  .usage-amount {
    &.is-reject {
      @include font-set("title-s", 500);
      font-weight: 500;
      color: var(--text-disabled-same);
      position: relative;
      text-decoration: line-through;
    }
    &.is-expired {
      @include font-set("title-s", 500);
      font-weight: 500;
      color: var(--text-disabled-same);
      position: relative;
      text-decoration: line-through;
    }
    &.is-income {
      color: var(--text-brand);
    }
    &.is-expense {
      color: var(--text-primary);
    }
  }
  .usage-status {
    .is-reject {
      @include font-set("body-s", 300);
      font-weight: 300;
      color: var(--text-increase-same);
    }
    .is-expired {
      @include font-set("body-s", 300);
      font-weight: 300;
      color: var(--text-quaternary);
    }
  }
  .usage-sub {
    word-break: keep-all;
    overflow-wrap: break-word;
    em {
      position: relative;
      display: inline-block;
      &::after {
        content: "•";
        display: inline-flex;
        justify-content: center;
        align-items: center;
        width: 7px;
        margin-right: var(--spacing-xs);
        margin-left: var(--spacing-xs);
        font-size: inherit;
        font-weight: inherit;
        line-height: inherit;
        letter-spacing: inherit;
        color: var(--text-disabled-same);
      }
      &:last-child {
        &::after {
          display: none;
        }
      }
      &.is-income {
        color: var(--text-deposit);
      }
      &.is-expense {
        color: var(--text-quaternary);
      }
    }
  }
  .sv-list__text__main {
    @include font-set("title-s", 500);
    font-weight: 500;
    color: var(--text-secondary);
    min-width: 0;
    flex: 1 1 0%;
    max-width: 100%;
    .usage-label {
      display: block;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
      max-width: 100%;
    }
  }
  .sv-list__text__sub {
    @include font-set("body-s", 300);
    font-weight: 300;
    color: var(--text-quaternary);
  }
  .sv-list__text--right {
    flex: 0 0 auto;
    flex-shrink: 0;
    flex-grow: 0;
    min-width: fit-content;
    max-width: none;
    margin-left: auto;
    .sv-list__text__main {
      margin-right: 0;
      color: var(--text-withdrawal);
    }
    .sv-button--size-xs {
      color: var(--text-secondary);
    }
  }

  // 대기목로 스타일
  &__pending {
    padding: var(--spacing-2xl) var(--container-padding-mobile) var(--spacing-5xl);
    background-color: var(--bg-graylight);
    &-title {
      @include font-set("title-s", 500);
      font-weight: 500;
      color: var(--text-secondary);
      text-align: center;
      margin-bottom: var(--spacing-2xl);
      em {
        @include font-set("title-s", 700);
        font-weight: 700;
        color: var(--text-secondary);
        font-style: normal;
      }
      .intitle {
        display: inline-flex;
        align-items: center;
        .sc-icon {
          margin-right: var(--spacing-sm);
        }
      }
    }
    ~ .usage-history__header,
    ~ .usage-history__header.is-sticky {
      margin-top: calc(var(--spacing-4xl) - var(--spacing-xl));
    }
    .sv-card__actions {
      min-height: auto;
      padding-bottom: var(--spacing-xl);
    }
    &-actions {
      display: flex;
      justify-content: flex-end;
      gap: var(--spacing-sm);
      width: 100%;
      .sv-button {
        color: var(--text-secondary);
        &.text-decrease {
          color: var(--text-decrease);
        }
      }
    }
  }
  &__dropdown {
    margin-top: 0;
    margin-bottom: var(--spacing-xl);
  }
  &__filter {
    margin-top: 0;
    margin-bottom: var(--spacing-2xl);
    &.is-sticky {
      top: calc(56px + 68px);
      margin-top: 0;
    }
  }

  &__pending-list {
    margin-top: var(--spacing-xl);
    .sv-card__content {
      padding: var(--spacing-xl) var(--spacing-2xl) var(--spacing-lg);
    }
  }
  // 공통 아이템 스타일
  &__pending-item,
  &__item {
    align-items: flex-start;
    margin: 0;
    &.sv-basic-list {
      padding: var(--spacing-lg) 0;
      border-radius: 0;
      .align-center {
        align-items: flex-start !important;
      }
    }
  }
  &__pending-item {
    margin-top: var(--spacing-lg);
  }

  &__header {
    padding: var(--spacing-xl) 0;
    .sv-datepicker {
      // 현재 컴포넌트에 제공된 부분에는 상단 년/월 만 선택하는 부분이 없어서 전체 하단 달력 부분 제공 부분까지 호출 후 해당 영역은 숨김
      .sv-datepicker__body,
      .sv-datepicker__options {
        display: none !important;
      }
    }
    .sv-datepicker__header {
      justify-content: center;
      .sv-datepicker__title {
        margin: 0 var(--spacing-3xl);
      }
      .sv-datepicker__title-content {
        @include font-set("title-l", 500);
        font-weight: 500;
        color: var(--text-primary);
      }
    }
    &.is-sticky {
      margin-top: 0;
    }
  }
  &__body {
    .usage-date__title {
      @include font-set("body-m", 300);
      font-weight: 300;
      color: var(--text-secondary);
      padding-top: var(--spacing-lg);
      padding-bottom: var(--spacing-lg);
    }
    section ~ section,
    section ~ .sv-divider {
      margin-top: 0;
    }
    section ~ .sv-divider {
      margin-top: var(--spacing-2xl);
      margin-bottom: var(--spacing-2xl);
    }
  }
  &__item {
    margin-top: var(--spacing-sm);
  }
}
```
