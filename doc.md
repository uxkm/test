# test

{% raw %}
```scss


/* 혜택 - 메인 */
.benefits_main {
  padding: 0;
}
.bf {
  &-main {
    section ~ section,
    section ~ .sv-divider {
      margin-top: 0;
    }
    .bg-gray {
      background-color: var(--bg-canvas_gray_light);
    }
    .title-sub {
      @include font-set(title-l, 700);
      font-weight: 700;
      color: var(--text-primary);
    }
    .bf-section__header {
      margin-bottom: var(--spacing-lg);
      .description {
        display: block;
        @include font-set(body-s, 500);
        font-weight: 500;
        color: var(--text-quaternary);
        ~ .title-sub {
          margin-top: var(--spacing-xs);
        }
      }
    }
    .bf-section__footer {
      display: flex;
      justify-content: center;
      margin-top: var(--spacing-lg);
      .sv-button--size-m {
        padding-right: var(--spacing-lg);
        padding-left: var(--spacing-lg);
      }
    }
    .cupon-chip  {
      .sv-chip-group {
        padding: 0;
        .sv-chip-group__container {
          gap: var(--spacing-md);
        }
      }
    }
    .export-banner {
      width: 100%;
      height: auto;
      object-fit: contain;
    }
    .img-dummy {
      width: 100%;
    }
  }
  &-apptech {
    padding-top: var(--spacing-5xl);
    padding-bottom: var(--spacing-4xl);
    article {
      ~ article {
        margin-top: var(--spacing-5xl);
      }
    }
    .export-banner__link {
      display: block;
      width: 100%;
      height: auto;
      line-height: 0;
    }
  }
  // 이벤트 영역
  &-event {
    padding-top: var(--spacing-4xl);
    padding-bottom: var(--spacing-4xl);
    article {
      ~ article {
        margin-top: var(--spacing-5xl);
      }
    }
    &__list {
      .category-list__body {
        margin-top: var(--spacing-xl);
        .sv-list__icon  {
          overflow: visible;
          img {
            max-width: 48px;
            max-height: 48px;
            border-radius: var(--radius-xl);
          }
        }
        .rank-badge {
          display: flex;
          justify-content: center;
          align-items: center;
          position: absolute;
          top: -8px;
          left: -8px;
          z-index: 1;
          width: 20px;
          height: 20px;
          border-radius: var(--radius-full);
          border: 1px solid var(--gray-100);
          background-color: var(--white-a10);
          @include font-set(detail-s, 500);
          font-weight: 500;
          color: var(--text-tertiary);
          backdrop-filter: blur(10px);
          box-shadow: 0px 2px 4px 0px var(--gray-a10);
          backdrop-filter: blur(5px);
        }
      }
    }
  }
  // 이벤트 프로모션
  &-promotion {
    padding-top: 6.58px;
    padding-bottom: 0;
    // padding-top: var(--spacing-3xl);
    // padding-bottom: var(--spacing-3xl);
  }
  // 놓치면 아까운 할인·쿠폰
  &-discount {
    padding-top: var(--spacing-4xl);
    padding-bottom: var(--spacing-5xl);
  }
  // 혜택 서비스
  &-service {
    padding-top: var(--spacing-3xl);
    padding-bottom: var(--spacing-5xl);
    .title-sub {
      @include font-set(title-s, 500);
      font-weight: 500;
      color: var(--text-secondary);
    }
    &__list {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: var(--spacing-sm);
      @media (max-width: 320px) {
        grid-template-columns: repeat(2, 1fr);
      }
    }
    &__item {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      width: 70px;
      max-width: 162px;
      margin: 0 auto;
      padding: var(--spacing-xl) var(--spacing-sm) var(--spacing-lg);

      @media (max-width: 320px) {
        max-width: 70px;
      }
    }
    &__icon {
      overflow: hidden;
      width: 32px;
      height: 32px;
      border-radius: var(--radius-xs);
      img {
        width: 100%;
        height: 100%;
        object-fit: contain;
      }
    }
    &__label {
      margin-top: var(--spacing-sm);
      @include font-set(body-s, 500);
      font-weight: 500;
      color: var(--text-secondary);
    }
  }
}


//cartegory__body, cupon-list__body outlie utitlity/benefits
    &.skeleton {
      padding-top: var(--spacing-lg);
      .content{
        display: flex;
        margin-top: var(--spacing-md);
        .left {
          flex: 1 1 auto;
          min-width: 0;
          .sv-loading-skeleton:last-child {
            margin-top: var(--spacing-xs);
          }
        }
        .right {
          flex: 0 0 auto;
          margin-left: var(--spacing-xl);
        }
      }
    }

```
{% endraw %}

---
