# test

{% raw %}
```scss
// 251212 benefits


/* 혜택 - 이벤트 모음형 페이지 */
.sc-event-collection {
  padding: var(--spacing-5xl) var(--container-padding-mobile);
  background-color: #e2f3fd;
  [data-theme="dark"] & {
    background-color: var(--gray-800);
  }
  .collection-header {
    position: relative;
    padding: 0;
    span,
    strong {
      display: block;
    }
    &__title {
      @include font-set(headline-s, 700);
      font-weight: 700;
      color: var(--text-primary);
    }
    &__title-sub {
      @include font-set(body-m, 300);
      font-weight: 300;
      color: var(--text-secondary);
    }
    img {
      position: absolute;
      top: 50%;
      right: 0;
      transform: translateY(-50%);
      width: 100px;
      height: 100px;
      object-fit: contain;
    }
  }
  .collection-body {
    overflow: hidden;
    position: relative;
    margin-top: var(--spacing-5xl);
    padding-top: 42px;
    border-radius: var(--radius-xl);
    background-color: var(--white-a50);
    [data-theme="dark"] & {
      background-color: var(--white-a5);
    }
    &__header {
      position: absolute;
      top: 0;
      left: 0;
      // 184px ÷ 375px × 100 = 49.07% = width: 50.93% (100% - 49.07%)
      // width: 50.93%;
      width: 100%;
      height: 42px;
      background-repeat: no-repeat;
      background-position: 0 0;
      background-size: auto 42px;
      // background-image: url(#{$cdn-url}/images/pages/benefits/main/bg_event_collection.svg);
      border-top-left-radius: var(--radius-xl);
      .bg_collection-header {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        path[fill="white"] {
          [data-theme="dark"] & {
            background-color: var(--gray-950);
          }
        }
      }
    }
    &__header-title {
      display: flex;
      align-items: flex-end;
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 42px;
      padding: 0 var(--spacing-2xl) var(--spacing-sm);
      white-space: nowrap;
      @include font-set(title-s, 500);
      font-weight: 500;
      color: var(--text-secondary);
      em {
        color: var(--text-brand);
        font-style: normal;
      }
    }
  }
  .collection-inner {
    border-top-right-radius: var(--radius-xl);
    background-color: var(--white);
    padding: var(--spacing-xl);
    [data-theme="dark"] & {
      background-color: var(--gray-950);
    }
  }
  .sharebtn {
    max-width: 101px;
    margin: var(--spacing-3xl) auto 0;
  }
}

/* 혜택 - 이벤트 하단 꼭! 알아두세요 아코디언 형태 */
.event-collection__notice {
  margin-top: 10px;
  padding: 0;
  .sv-accordion-item {
    border-bottom: 1px solid var(--border-secondary);
  }
  .sv-accordion-item__title {
    @include font-set(title-m, 500);
    font-weight: 500;
    color: var(--text-secondary);
  }
  .sv-text-list__content ul {
    margin-top: var(--spacing-md);
  }
  .sv-list {
    color: var(--text-quaternary);
  }
}
```
{% endraw %}

---
