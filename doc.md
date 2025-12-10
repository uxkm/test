# test

{% raw %}
```scss
// 251210 utitlity

// 카테고리 그룹
.sc-category__group {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-2xl) 0;
  // padding-inline: var(--container-padding-mobile);
  padding-right: var(--container-padding-mobile);
  padding-left: var(--container-padding-mobile);
  // padding-block: var(--spacing-xl) var(--spacing-lg);
  padding-top: var(--spacing-xl);
  padding-bottom: var(--spacing-lg);
  .sv-list-title {
    .sv-button {
      gap: var(--spacing-xs);
    }
  }
  .category-filter {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: var(--spacing-md);
    width: 100%;
    min-width: 0;
  }
  .category-filter__left,
  .category-filter__right {
    display: inline-flex;
    align-items: center;
  }
  .sv-dropdown--variant-ghost .sv-dropdown__trigger {
    padding-left: 0;
  }
  .category-filter__label {
    color: var(--text-placeholder-same);
    &.is-active {
      color: var(--text-primary);
    }
  }
  // 카테고리 검색 (사용 : 혜택 이벤트)
  .category-filter__search {
    display: flex;
    align-items: flex-start;
    gap: var(--spacing-md);
    width: 100%;
    min-width: 0;
    margin-top: var(--spacing-4xl);
    margin-bottom: var(--spacing-xl);

    .category-filter__search-icon {
      width: 36px;
      height: 36px;
      border: 1px solid var(--border-tertiary);
      border-radius: 50%;
    }

    .category-filter__search-field {
      display: flex;
      align-items: flex-start;
      gap: var(--spacing-md);
      flex-shrink: 0;
      align-self: flex-start;
      position: relative;

      &.is-focus {
        flex: 1;
        width: 100%;

        .category-filter__search-icon {
          margin-left: var(-spacing-xs);
          border-color: transparent;
          z-index: 1;
          svg {
            margin-left: var(--spacing-sm);
          }
        }
        .category-filter__search-input {
          z-index: 1;
        }
        &::before {
          content: "";
          position: absolute;
          top: 0;
          left: 0;
          width: calc(100% - (31px + 12px));
          height: 100%;
          border-radius: 36px;
          border: 2px solid var(--text-brand);
        }
      }

      .category-filter__search-input {
        display: flex;
        align-items: center;
        gap: var(--spacing-lg);
        flex: 1;
        min-width: 0;
        position: relative;

        .custom-input {
          display: flex;
          align-items: center;
          flex: 1;
          min-width: 0;
          height: 36px;
          padding: 0;
          border: none;
          border-radius: 0;
          background: transparent;

          input {
            flex: 1;
            min-width: 0;
            border: none;
            outline: none;
            background: transparent;
            @include font-set("body-m", 500);
            font-weight: 500;
            color: var(--text-primary);
            caret-color: var(--text-brand, #0066cc); // 커서(캐럿) 색상

            &::placeholder {
              font-weight: 300;
              color: var(--text-placeholder-same);
            }
          }
        }
      }
      .category-filter__search-input-inner {
        display: flex;
        align-items: center;
        flex: 1;
        min-width: 0;
      }
      .category-filter__search-input-clear {
        width: 36px;
        height: 36px;
        @include font-set("body-l", 300);
        font-weight: 300;
        color: var(--text-quaternary);
        svg {
          width: 24px !important;
          height: 24px !important;
        }
      }
      .category-filter__search-cancel {
        height: 36px;
        @include font-set("body-l", 300);
        font-weight: 300;
        color: var(--text-primary);
      }
    }

    .category-filter__search-chip {
      display: flex;
      align-items: flex-start;
      flex: 1;
      position: relative;
      overflow: visible;
      align-self: flex-start;
      min-width: 0;
      padding-top: 0;
      padding-bottom: 0;

      .sv-chip-group {
        width: 100%;
        align-items: flex-start;
      }

      .sv-chip-group--size-m .sv-chip-group__container {
        padding-top: 0;
        padding-bottom: 0;
        padding-left: 0;
        align-items: flex-start;
      }
      .sv-chip-group__container--scrollable {
        .sv-basic-chip {
          margin-bottom: 0;
        }
      }
      .sv-chip-group__container--expanded {
        padding-right: 0;
      }

      .sv-chip-group__expand-button {
        position: relative;
        left: auto;
        top: 0;
        margin: 0;
        flex-shrink: 0;
        align-self: flex-start;
      }
    }
  }

  &.search-type {
    gap: 0;
    padding-bottom: 0;
    .usage-history__dropdown {
      margin-top: var(--spacing-xl);
      margin-bottom: 0;
    }
  }

  ~ .sc-contents__body {
    .cupon-list__wrap {
      padding-top: var(--spacing-lg);
    }
  }
}

// 카테고리 필터 스타일
.category-contents {
  .sc-empty-case .empty-type {
    margin: 0;
  }
}
.category-top__btngroup {
  padding: 0 var(--container-padding-mobile);
  .sv-divider {
    // margin-block: var(--spacing-2xl);
    margin-top: var(--spacing-2xl);
    margin-bottom: var(--spacing-2xl);
  }
}
.category-head {
  flex: 0 0 auto;
  padding: 0 var(--container-padding-mobile) var(--spacing-xl);
  @include font-set(headline-s, 700);
  font-weight: 700;
  .category-count {
    color: var(--text-brand);
    font-style: normal;
  }
}
.category-chip {
  flex: 0 0 auto;
  padding: 0;
  .sv-chip-group__container > * {
    margin: 0;
  }
  .sv-chip-group {
    padding: var(--spacing-xl) 0;
    .sv-chip-group__container {
      gap: var(--spacing-lg);
      padding: 0;
      padding-left: var(--container-padding-mobile);
      .sv-basic-chip.sv-basic-chip--variant-solid:first-child {
        margin-left: 0;
      }
      // 첫 번째 칩만 있을 경우에도 좌측 간격 유지
      &:has(.sv-basic-chip.sv-basic-chip--variant-solid:only-child) {
        padding-left: var(--container-padding-mobile);
      }
    }
    &:has(.sv-chip-group__container--expanded) {
      .sv-chip-group__container {
        padding-left: var(--container-padding-mobile);
      }
    }
  }
  .sv-chip-group .sv-chip-group__expand-button {
    margin: 0;
  }
}
.category-list__wrap {
  padding: var(--spacing-2xl) var(--container-padding-mobile);

  .sv-pagination {
    margin-top: var(--spacing-2xl);
    padding-top: var(--spacing-lg);
  }
}
.category-list__head {
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
  em {
    color: inherit;
    font-style: normal;
  }
  .cupon-head__text {
    @include font-set(body-m, 500);
    font-weight: 500;
    color: var(--text-tertiary);
  }
}
.category-list__body {
  .category-item {
    padding: var(--spacing-lg) 0;
    .sv-list__item_inner > * {
      margin: 0;
    }
    .sv-list__item_inner.align-center {
      gap: var(--spacing-lg);
      justify-content: flex-start;
    }
    .ended-event-item {
      .sv-list__icon {
        &::before {
          content: "";
          position: absolute;
          top: 0;
          left: 0;
          z-index: 1;
          width: 100%;
          height: 100%;
          background-color: var(--gray950-a60);
        }
      }
    }
  }
  .sv-list__texts {
    flex: 1 1 auto;
    .sv-list__text {
      width: 100%;
      min-width: 0;
    }
    em {
      font-style: normal;
      color: var(--text-brand);
    }
  }
  .sv-list__icon {
    overflow: hidden;
    display: flex;
    flex: 0 0 auto;
    align-items: center;
    justify-content: center;
    width: var(--spacing-6xl);
    height: var(--spacing-6xl);
    padding: var(--spacing-sm);
    border-radius: var(--spacing-xl);
    background-color: var(--bg-gray);
    position: relative;
    img {
      max-width: 100%;
      max-height: 100%;
      width: auto;
      height: auto;
      border-radius: 50%;
      object-fit: contain;
    }
    .ended-event-badge {
      display: inline-block;
      justify-content: center;
      align-items: center;
      position: absolute;
      top: 50%;
      left: 50%;
      z-index: 1;
      transform: translate(-50%, -50%);
      height: 22px;
      padding: var(--spacing-xs) var(--spacing-md);
      border-radius: var(--radius-xxs);
      background-color: var(--bg-informative-same);
      @include font-set(detail-s, 500);
      font-weight: 500;
      color: var(--text-ondark_primary-same);
      white-space: nowrap;
    }
  }
  .sv-list__text__main {
    margin-right: 0;
    span {
      display: block;
      @include font-set(body-s, 300);
      font-weight: 300;
      color: var(--text-quaternary);
    }
    strong {
      display: block;
      font-weight: 500;
    }
    .inline-flex {
      display: inline-flex;
    }
    .sv-label {
      margin-bottom: var(--spacing-xs);
      font-size: var(--font-size-detail-s);
      line-height: var(--lineheight-detail-s);
      letter-spacing: var(--letterspace-detail-s);
      font-weight: var(--font-weight-m);
    }
    .sv-label--variant-solid {
      &.sv-label--color-blue,
      &.sv-label--color-cyan,
      &.sv-label--color-green,
      &.sv-label--color-yellow,
      &.sv-label--color-orange,
      &.sv-label--color-red,
      &.sv-label--color-gray {
        color: var(--text-ondark_primary-same);
      }
    }
  }
  .sv-list__text__sub {
    @include font-set(body-s, 300);
    font-weight: 300;
    color: var(--text-quaternary);
    .text {
      display: block;
    }
  }
}
```
{% endraw %}

---
