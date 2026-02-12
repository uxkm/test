
{% raw %}
```js

// 레거시 폰 대응 그리드 사용
// 2457 line
&__list {
    min-width: 0;
    overflow-x: auto;
    -webkit-overflow-scrolling: touch;
    scrollbar-width: none; // Firefox
    padding-left: var(--spacing-2xl);
    padding-right: var(--spacing-2xl);
    &::-webkit-scrollbar {
      display: none; // Chrome, Safari
    }
    // 레거시: Grid 미지원 시 Flex 기반 가로 스크롤
    display: flex;
    flex-wrap: nowrap;
    gap: 0 var(--spacing-lg);
    > * {
      flex: 0 0 160px; // 레거시: Flex에서 열 너비 고정
    }
    @supports (display: grid) {
      display: grid;
      grid-auto-flow: column;
      grid-auto-columns: 160px;
      column-gap: var(--spacing-lg);
      gap: unset;
      > * {
        flex: unset;
      }
    }
    &.skeleton {
      overflow: hidden;
      @supports (display: grid) {
        grid-auto-columns: minmax(160px, 1fr);
      }
      margin: 0;
      padding: 0;
      padding-left: var(--container-padding-mobile);
      .collection-card__item {
        margin: 0;
        padding: 0;
        min-width: 160px;
        flex: 0 0 160px; // 레거시 Flex 대응
        @supports (display: grid) {
          flex: unset;
          width: 100%;
        }
      }
    }
  }


.level-progress {
    position: relative;
    margin-top: var(--spacing-3xl);
    font-family: var(--font-family-base, "OneShinhan", sans-serif);
    display: flex; // 레거시: Grid 미지원 시 Flex 기반
    @supports (display: grid) {
      display: grid;
    }
    &__label {
      display: flex;
      flex-wrap: nowrap;
      justify-content: space-between;
      align-items: flex-start;
      width: 100%;
      @supports (display: grid) {
        display: grid;
        grid-template-columns: 65px 56px 1fr 56px 1fr 56px;
        justify-content: stretch;
        width: 100%;
      }
    }
    &__text {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      position: relative;
      z-index: 1;
      width: 56px;
      height: 62px;
      text-align: center;
      line-height: 0;
      box-sizing: border-box;
      flex-shrink: 0;
      &.level0 {
        width: 65px;
        @supports (display: grid) {
          grid-column: 1;
        }
      }
      &.level1 {
        @supports (display: grid) {
          grid-column: 2;
        }
      }
      &.level2 {
        @supports (display: grid) {
          grid-column: 4;
        }
      }
      &.level3 {
        @supports (display: grid) {
          grid-column: 6;
        }
      }
      img {
        width: 36px;
        height: 36px;
      }
      em {
        display: block;
        margin-top: var(--spacing-sm);
        @include font-set(body-s, 500, true); // 레거시(고정) 폰트 대응: -fixed 토큰 사용
        font-weight: 500;
        color: var(--text-quaternary);
      }
      .is-achieved {
        position: absolute;
        top: 10px;
        left: 50%;
        transform: translateX(-50%);
        display: inline-flex;
        justify-content: center;
        align-items: center;
        width: 24px;
        height: 24px;
        border-radius: var(--radius-full);
        background-color: var(--bg-brand_strong-same);
      }
    }
  }


```
{% endraw %}
---
