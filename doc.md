# test

{% raw %}
```scss



/* 쿠폰 */
.cupon-contents {
  .sc-empty-case .empty-type {
    margin: 0;
  }
}
.cupon-top__btngroup {
  padding: 0 var(--container-padding-mobile);
  .sv-divider {
    // margin-block: var(--spacing-2xl);
    margin-top: var(--spacing-2xl);
    margin-bottom: var(--spacing-2xl);
  }
}
.cupon-head {
  flex: 0 0 auto;
  padding: 0 var(--container-padding-mobile) var(--spacing-xl);
  @include font-set(headline-s, 700);
  font-weight: 700;
  .cupon-count {
    color: var(--text-brand);
    font-style: normal;
  }
}
.cupon-chip {
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
.cupon-list__wrap {
  padding: var(--spacing-2xl) var(--container-padding-mobile);
}
.cupon-list__head {
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
  // padding: 0 var(--container-padding-mobile);
  em {
    color: inherit;
    font-style: normal;
  }
  .cupon-head__text {
    @include font-set(body-m, 500);
    font-weight: 500;
    color: var(--text-tertiary);
  }
  .cupon-head__text-left {
    flex: 1 1 auto;
  }
  .cupon-head__text-right {
    flex: 0 0 auto;
  }
  &.list-head {
    margin-bottom: var(--spacing-xl);
    .cupon-head__text {
      @include font-set(title-l, 700);
      font-weight: 700;
      color: var(--text-secondary);
    }
  }
}
.cupon-list__body {
  .cupon-item {
    padding: var(--spacing-lg) 0;
    .sv-list__item_inner > * {
      margin: 0;
    }
    .sv-list__item_inner.align-center {
      gap: var(--spacing-lg);
      justify-content: flex-start;
    }
    &.outline {
      border: 1px solid var(--border-secondary);
      border-radius: var(--radius-xl);
      padding: var(--spacing-2xl);
      .flex {
        margin-bottom: var(--spacing-md);
      }
      .sv-list > * {
        margin-right: 0;
      }
      .sv-list .sidetxt > * {
        display: block;
      }
      .sv-list__control {
        width: calc(16px * 3);
        margin-right: calc(var(--spacing-2xl) * -1);
        .sv-icon-button {
          color: var(--fg-quaternary);
        }
      }
      .sv-list__text__main {
        margin-right: var(--spacing-xl);
        @include ellipsis(2);
      }
      .sv-list__text__sub {
        margin-right: var(--spacing-xl);
        @include ellipsis(1);
      }
      .sv-list__icon {
        padding: 0;
        border: 1px solid var(--border-secondary);
        background-color: transparent;
      }
      ~ .outline {
        margin-top: var(--spacing-lg);
      }

      &.is-label {
        padding-top: 10px;
        .sv-list__icon {
          margin-top: calc(var(--spacing-md) + 24px);
        }
        // label이 있을 때도 sub가 위, main이 아래로 오도록 순서 조정
        .sv-list__text {
          // direction-h sidetxt 클래스가 있어도 세로로 배치
          display: flex;
          flex-direction: column;
          &.sidetxt {
            > * {
              display: block;
            }
          }
          .sv-list__text__main {
            order: 2;
            display: block;
            margin-right: var(--spacing-xl);
            @include ellipsis(2);
          }
          .sv-list__text__sub {
            order: 1;
            display: block;
            margin-right: var(--spacing-xl);
            @include ellipsis(1);
          }
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
    img {
      max-width: 100%;
      max-height: 100%;
      width: auto;
      height: auto;
      border-radius: 50%;
      object-fit: contain;
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
    em {
      font-style: normal;
      font-weight: 500;
      color: var(--text-brand);
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
  }
  .sv-list__control {
    flex: 0 0 auto;
    width: 36px;
    height: 36px;
    .sv-icon-button {
      width: 100%;
      height: 100%;
    }
    .sv-icon {
      width: 20px;
      height: 20px;
    }
  }
}
.sc-membership__bs {
  .sv-bottom-sheet__body {
    // padding-inline: 0;
    padding-right: 0;
    padding-left: 0;
  }
}











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
          margin-left: var(--spacing-xs);
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

    &.full-width {
      width: 100%;
      margin: 0;
      padding: 0;
      .category-filter__search-field {
        flex: 1;
        width: 100%;
        border: 1px solid var(--border-primary);
        border-radius: 36px;

        .category-filter__search-icon {
          margin-left: var(--spacing-xs);
          border-color: transparent;
          z-index: 1;
          svg {
            margin-left: var(--spacing-sm);
          }
        }
        .category-filter__search-input {
          z-index: 1;
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

        &.is-focus {
          &::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border-radius: 36px;
            border: 2px solid transparent;
            animation: drawBorder 0.25s ease-in-out forwards;
            pointer-events: none;
          }
        }
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
    // 당첨 정보 버튼
    .ev-detail-btn {
      min-height: 22px;
      margin-top: var(--spacing-md);
      .sv-button__label {
        color: var(--text-secondary);
      }
    }
    // 이벤트 제목에 링크가 있는 경우
    [role="link"] {
      display: block;
      position: relative;
      @include font-set(title-s, 500);
      font-weight: 500;
      color: var(--text-secondary);

      // 클릭 영역 확장하기 위한 요소 추가
      &::after {
        content: "";
        position: absolute;
        top: -20px;
        left: 0;
        width: 100%;
        height: calc(100% + 40px);
      }
    }
    .event-description {
      margin-top: var(--spacing-md);
      @include font-set(body-s, 300);
      font-weight: 300;
      color: var(--text-secondary);
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }
    &.outline {
      border: 1px solid var(--border-secondary);
      border-radius: var(--radius-xl);
      padding: 10px var(--spacing-2xl) var(--spacing-2xl);
      .flex {
        margin-bottom: var(--spacing-md);
      }
      .sv-list > * {
        margin-right: 0;
      }
      .sv-list__control {
        width: calc(16px * 3);
        margin-right: calc(var(--spacing-2xl) * -1);
        .sv-icon-button {
          color: var(--fg-quaternary);
        }
      }
      .sv-list__text__main {
        strong {
          margin-right: var(--spacing-xl);
          @include ellipsis(2);
        }
      }
      .sv-list__text__sub {
        margin-right: var(--spacing-xl);
        @include ellipsis(1);
      }
      .sv-list__icon {
        padding: 0;
        border: 1px solid var(--border-secondary);
        background-color: transparent;
      }
      ~ .outline {
        margin-top: var(--spacing-lg);
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
  .sv-list__control {
    flex: 0 0 auto;
    width: 36px;
    height: 36px;
    .sv-icon-button {
      width: 100%;
      height: 100%;
    }
    .sv-icon {
      width: 20px;
      height: 20px;
    }
  }
}




// border 그리기 애니메이션 (border-radius 고려)
// top → right → bottom → left 순서로 각 0.25초씩
@keyframes drawBorder {
  0% {
    border-top-color: transparent;
    border-right-color: transparent;
    border-bottom-color: transparent;
    border-left-color: transparent;
  }
  25% {
    border-top-color: var(--text-brand);
    border-right-color: transparent;
    border-bottom-color: transparent;
    border-left-color: transparent;
  }
  50% {
    border-top-color: var(--text-brand);
    border-right-color: var(--text-brand);
    border-bottom-color: transparent;
    border-left-color: transparent;
  }
  75% {
    border-top-color: var(--text-brand);
    border-right-color: var(--text-brand);
    border-bottom-color: var(--text-brand);
    border-left-color: transparent;
  }
  100% {
    border-top-color: var(--text-brand);
    border-right-color: var(--text-brand);
    border-bottom-color: var(--text-brand);
    border-left-color: var(--text-brand);
  }
}






// 진행 중인 쿠폰, 쿠폰 검색 하단 토스트 위치 (쿠폰 검색 위에 위치)
.sc-coupon__ongoing {
  ~ .sc-toast-container--bottom {
    bottom: 52px;
  }
}

```
{% endraw %}

---
