# test

{% raw %}
```scss

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



```
{% endraw %}

---
