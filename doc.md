# test

{% raw %}
```scss

//quiz pangpang
    &__contents-body {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: var(--spacing-md);
      margin-top: var(--spacing-3xl);
      margin-bottom: var(--spacing-3xl);
      &.question {
        display: flex;
        flex-direction: column;
        margin-bottom: var(--spacing-4xl);
        .sv-radio-group {
          .sv-radio-group__item-container {
            position: relative;
            min-height: 56px;
            padding: 0;
            border: 1.6px solid var(--border-primary);
            border-radius: var(--radius-xl);
            transition: border-color 0.2s ease-in-out;
            cursor: pointer;
            box-sizing: border-box;

            // 선택된 항목에 is-checked 클래스가 추가되거나, 내부에 checked 상태의 radio-item이 있을 때
            &.is-checked,
            &:has(.sv-radio-item[data-state="checked"]) {
              border-color: var(--text-brand);
              animation: drawBorder 0.25s var(--ease) forwards;
            }
            ~ .sv-radio-group__item-container {
              margin-top: var(--spacing-lg);
            }
          }
          .sv-radio-item {
            position: absolute;
            left: var(--spacing-xl);
            top: 50%;
            transform: translateY(-50%);
          }
          .sv-radio-item__label {
            width: 100%;
            margin: 0;
            label {
              width: 100%;
              padding: var(--spacing-xl);
              padding-left: calc(var(--spacing-xl) + 24px + var(--spacing-md));
              @include font-set(title-s, 500);
              font-weight: 500;
              color: var(--text-secondary);
            }
          }
        }
      }
      .question-select-box.sv-select-box-group {
        .sv-select-box {
          margin: 0;
          padding: var(--spacing-xl) var(--spacing-2xl);
          border: 1px solid var(--border-secondary);
          ~ .sv-select-box {
            margin-top: var(--spacing-lg);
          }
        }
        .sv-select-box__label {
          width: 100%;
          margin-top: 0;
          @include font-set(title-s, 500);
          font-weight: 500;
          color: var(--text-secondary);
          text-align: left;
        }
      }
    }



// IF 에러
.bf-if__error,
.bf-if__login {
  padding: 0 var(--container-padding-mobile);
  &.h344 {
    .bf-if__error-inner {
      height: 344px;
    }
  }
  &-inner {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: var(--spacing-2xl);
    border-radius: var(--radius-xl);
    border: 1px solid var(--border-secondary);
    background-color: var(--bg-canvas_white);
  }
  &-icon {
    width: 48px;
    height: 48px;
    img {
      width: 100%;
      height: 100%;
      object-fit: contain;
    }
  }
  &-text {
    margin-top: var(--spacing-md);
    @include font-set(body-s, 300);
    font-weight: 300;
    color: var(--text-quaternary);
  }
  .sv-button {
    width: auto;
    margin-top: var(--spacing-xl);
  }
  .sv-button--size-s {
    padding-right: var(--spacing-lg);
    padding-left: var(--spacing-lg);
  }
}
/* 이달의 참여현황 BottomSheet */
.participation-status__sheet {
  .month-schedule {
    &__container {
      display: grid;
      grid-template-columns: repeat(5, 1fr);
      gap: var(--spacing-md);
      padding: 0;
    }

    &__item {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      position: relative;
      height: 64px;
      padding: var(--spacing-md);
      border-radius: var(--radius-xl);
      background-color: var(--bg-canvas_white);

      // 참여현황 없음 (미선택/미래 날짜)
      &.is-empty {
        border: 1px dashed var(--border-primary);
      }

      // 미참여
      &.is-not-participated {
        background-color: var(--bg-graylight);
      }

      // 오답
      &.is-incorrect {
        background: var(--bg-red);
      }

      // 정답
      &.is-correct {
        background-color: rgba(0, 93, 249, 0.1);
      }
    }

    &__number {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 24px;
      height: 24px;
      border-radius: var(--radius-full);
      background-color: var(--bg-canvas_white);
      @include font-set(body-s, 500);
      font-weight: 500;
      color: var(--text-tertiary);
    }

    &__label {
      margin-top: var(--spacing-sm);
      @include font-set(detail-s, 500);
      font-weight: 500;
      text-align: center;

      // 미참여
      &.is-not-participated {
        color: var(--text-tertiary);
      }

      // 오답
      &.is-incorrect {
        color: var(--text-new-same);
      }

      // 정답
      &.is-correct {
        color: var(--text-ondark_brand-same);
      }
    }
    &__total {
      display: grid;
      grid-template-columns: 1fr auto 1fr;
      align-items: center;
      gap: var(--spacing-lg);
      margin-top: var(--spacing-4xl);
      padding: var(--spacing-xl) var(--spacing-2xl);
      border-radius: var(--radius-xl);
      border: 1px solid var(--border-secondary);
      background: var(--bg-canvas_white);
      strong,
      em {
        display: block;
      }
      .sv-divider {
        margin-right: var(--spacing-lg);
        margin-left: var(--spacing-lg);
      }
    }
    &__total-item {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }
    &__total-label {
      @include font-set(body-s, 500);
      font-weight: 500;
      color: var(--text-quaternary);
    }
    &__total-value {
      margin-top: var(--spacing-sm);
      @include font-set(title-l, 700);
      font-weight: 700;
      color: var(--text-secondary);
    }
  }
}

// 혜택 - 앱테크 - 로티 크기 추가
  &__img {
    width: var(--spacing-3xl);
    height: var(--spacing-3xl);
    object-fit: contain;
    &.sc-point-card__img {
      width: var(--spacing-3xl);
      height: var(--spacing-3xl);
      object-fit: contain;
    }
  }







// utitlity sc-banner data-color 추가
  &[data-color="bg-gray"] {
    background-color: var(--bg-gray);
  }


// utitlity sc-banner c-image type 추가
  &[data-type="c-image"] {
    --banner-min-height: 88px;
    --banner-image-width: 100px;
    --banner-image-height: 100px;
    display: grid;
    grid-template-columns: var(--banner-image-width) 1fr;
    grid-template-rows: auto auto;
    align-items: center;
    padding: var(--spacing-lg) var(--spacing-2xl);
    .sc-banner__image {
      width: auto;
      max-width: var(--banner-image-width);
      height: var(--banner-image-height);
      border-radius: var(--radius-md);
      grid-row: 1;
      align-self: center;
      img {
        object-fit: cover;
      }
    }
    .sc-banner__text {
      grid-row: 1;
      align-self: center;
    }
    > .footer-button {
      grid-column: 1 / -1;
      grid-row: 2;
      width: 100%;
      margin-top: var(--spacing-lg);
      margin-bottom: calc(var(--spacing-2xl) - var(--spacing-lg));
      &.bg-white {
        background: var(--bg-white) !important;
        color: var(--text-brand) !important;
      }
    }
    &.rtl {
      padding: var(--spacing-lg) var(--spacing-2xl);
    }
  }


// promotion banner 하단 추가
  // 배너 + 버튼 조합
  &__basic-group {
    height: auto;
    margin: 0 var(--container-padding-mobile);
    border-radius: 0;
  }

// utitlity svg 전 삽입

// 공유하기 리스트
.shared-list {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: var(--spacing-xl);
  padding: var(--spacing-3xl) var(--spacing-2xl);
  @media (min-width: 360px) {
    gap: var(--spacing-lg);
  }
  @media (min-width: 320px) {
    padding: var(--spacing-3xl) 0;
  }
  li {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .sv-button--size-m.sv-button--variant-ghost .sv-button__left-icon {
    width: 56px !important;
    height: 56px !important;
  }
  .sv-button--size-m.sv-button--variant-ghost .sv-button__label {
    @include font-set("body-s", 500);
    font-weight: 500;
  }
  .sv-button {
    flex-direction: column;
    gap: var(--spacing-md);
    width: 100%;
    padding: 0;
    .sv-button__left-icon {
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0;
      border-radius: 50%;
      background-color: var(--bg-ongray_graylight_a5);
      .sc-icon {
        width: 36px;
        height: 36px;
      }
    }
    .sv-button__label {
      margin-top: var(--spacing-md);
      margin-left: 0;
      color: var(--text-primary);
    }
    &.link-copy-btn {
      color: var(--fg-primary);
    }
    &.x-btn {
      color: inherit;
      .sv-button__left-icon {
        background-color: var(--bg-informative-same);
      }
    }
  }
}

// 토스트에 삽입된 아이콘 크기
.sv-toast__icon {
  width: 24px;
  height: 24px;
  ~ .sv-toast__text {
    margin-left: var(--spacing-md);
    @include font-set(body-m, 500);
    font-weight: 500;
    color: var(--text-ondark_primary-same);
  }
}

// 플로팅 영역 z-index값 수정 bottom sheet 영역 보다 낮게
.sv-floating-action-container {
  z-index: 500 !important;
}



```
{% endraw %}

---
