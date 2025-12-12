# test

{% raw %}
```scss
// 251212 utitlity

  &.p_events {
    display: block;
    padding: 0;
    .collection-card__list {
      overflow: hidden;
      grid-auto-columns: minmax(160px, 1fr);
      margin: 0;
      padding: 0;
      padding-left: var(--container-padding-mobile);
      .collection-card__item {
        margin: 0;
        padding: 0;
        min-width: 160px;
        width: 100%;
      }
    }
    .webzine-list {
      margin: 0;
      padding: 0;
      .webzine-item {
        display: flex;
        padding: var(--spacing-lg) var(--container-padding-mobile);
        ~ .webzine-item {
          margin-top: var(--spacing-sm);
        }
      }
      .webzine-item__thumbnail {
        display: flex;
        align-items: center;
        justify-content: center;
        flex: 0 0 auto;
        min-width: 48px;
        max-width: 48px;
      }
      .webzine-item__content {
        display: flex;
        flex-direction: column;
        gap: var(--spacing-xs);
        flex: 1 1 auto;
        min-width: 0;
        margin-left: var(--spacing-lg);
      }
    }
  }






/* 혜택 - 이벤트 서브 메인화면 */
.p_events {
  .title-sub {
    display: flex;
    align-items: center;
    position: relative;
    padding-right: 28px;
    @include font-set(title-l, 700);
    font-weight: 700;
    color: var(--text-primary);
    .more-btn {
      position: absolute;
      top: 0;
      right: 0;
      width: 100%;
      height: 28px;
      flex-direction: row;
      justify-content: flex-end;
    }
    .sv-icon-button:active:not(:disabled) {
      position: absolute;
      transform: none;
      &::after {
        // display: none;
      }
    }
  }
  section ~ section {
    margin-top: var(--spacing-5xl);
  }
}

// 이벤트 메인에 사용된 이벤트 모음.ZIP 카드 리스트
.collection-card {
  &__header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    position: relative;
    margin-bottom: var(--spacing-lg);
    padding: 0 var(--container-padding-mobile);
    &-left {
      display: flex;
      align-items: center;
      flex: 1 1 auto;
      overflow: hidden;
      position: relative;
      min-width: 0;
    }
    &-right {
      display: flex;
      align-items: center;
      justify-content: flex-end;
      flex-shrink: 0;
    }
  }
  &__list {
    display: grid;
    grid-auto-flow: column;
    grid-auto-columns: 160px;
    column-gap: var(--spacing-lg);
    min-width: 0;
    overflow-x: auto;
    -webkit-overflow-scrolling: touch;
    scrollbar-width: none; // Firefox
    padding-left: var(--spacing-2xl);
    padding-right: var(--spacing-2xl);
    &::-webkit-scrollbar {
      display: none; // Chrome, Safari
    }
  }
  &__item {
    width: 160px;
    height: 228px;
    background-repeat: no-repeat;
    background-position: center center;
    padding: 38px var(--spacing-2xl) var(--spacing-xl);
    img {
      width: 86px;
      height: 86px;
    }
  }
  &__item-content {
    margin-top: var(--spacing-xl);
  }
  &__text-main {
    @include font-set(title-m, 700);
    font-weight: 700;
    color: var(--text-primary-same);
  }
  &__text-sub {
    @include font-set(body-s, 300);
    font-weight: 300;
    color: var(--text-quaternary);
  }
}
```
{% endraw %}

---
