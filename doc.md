# test
```scss
// 251125
// input-field
// 70 line


  .field-item__rowgroup {
    .sv-text-input--variant-outline .sv-text-input__container {
      padding-inline: var(--spacing-sm);
    }

    // multiple 유형 스타일 (기본 적용)
    .sv-text-input__border-svg {
      display: none;
    }

    .rowgroup-inner {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(0, 1fr));
      gap: var(--spacing-md);
      grid-column: 1 / -1;
      position: relative;

      &::before {
        content: "";
        display: block;
        position: absolute;
        top: calc(1.5rem + var(--spacing-md));
        left: 0;
        width: 100%;
        height: 56px;
        border: 1px solid var(--border-primary);
        border-radius: var(--radius-md);
        transition: border-color 0.2s ease;
      }

      &::after {
        content: "";
        display: block;
        position: absolute;
        top: calc(1.5rem + var(--spacing-md));
        left: 0;
        width: 100%;
        height: 56px;
        border-radius: var(--radius-md);
        border: 2px solid var(--border-brand);
        border-color: transparent;
        opacity: 0;
      }

      &:focus-within::before {
        border-color: transparent;
      }

      &:focus-within::after {
        opacity: 1;
        animation: drawBorderWithRadius 0.25s var(--ease) forwards;
      }
    }

    // 에러 상태
    &.is-error {
      .rowgroup-inner {
        &::before {
          border-color: var(--border-negative-same);
          border-width: 2px;
        }

        &::after {
          display: none;
        }
      }
    }

    .sv-text-input--variant-outline {
      .sv-text-input__container {
        border: 0 !important;
      }
    }

    // 각 InputField의 모든 border 요소 숨김
    .sv-text-input {
      .sv-text-input__container {
        border: 0 !important;
      }
    }

    .field-item {
      margin-bottom: 0;
      position: relative;
      z-index: 1;

      // label이 없는 필드도 첫번째 필드와 동일한 상단 간격 유지
      &:not(:first-child) {
        .sv-form-field {
          padding-top: calc(1.5rem + var(--spacing-md)); // label 높이(body-m) + margin-top
        }
      }

      &::after {
        content: "-";
        display: inline-block;
        position: absolute;
        top: calc(1.5rem + var(--spacing-md) + 28px);
        transform: translateY(-50%);
        right: -6px;
        @include font-set("body-l", 700);
        font-weight: 700;
        color: var(--text-primary);
      }

      &:last-child {
        &::after {
          display: none;
        }
      }

      &__masked {
        .sv-text-input__input {
          @include font-set("body-m", 500);
          font-weight: 500;
        }
      }

      .sv-text-input__input {
        // 입력된 값에 대한 폰트 (기본값)
        @include font-set("body-l", 500);
        font-weight: 500;
        color: var(--text-primary);

        // placeholder에 대한 폰트
        &::placeholder {
          @include font-set("body-m", 500);
          font-weight: 500;
          color: var(--text-placeholder-same);
        }

        // 포커스 상태
        &:focus {
          @include font-set("body-l", 500);
          font-weight: 500;
          color: var(--text-primary);

          // 포커스 시 placeholder 숨김
          &::placeholder {
            color: transparent;
          }
        }
      }
    }

    // 오류 메시지 영역
    .field-item-error {
      grid-column: 1 / -1;
      margin-top: var(--spacing-md);

      .field-error-message {
        display: flex;
        align-items: center;
        @include font-set("detail-l", 300);
        font-weight: 300;
        color: var(--text-negative-same);
        padding-inline: var(--spacing-sm);

        &__icon {
          margin-right: var(--spacing-sm);
          flex-shrink: 0;
        }
      }
    }
  }



// border 그리기 애니메이션 (border-radius 고려)
@keyframes drawBorderWithRadius {
  0% {
    border-top-color: transparent;
    border-right-color: transparent;
    border-bottom-color: transparent;
    border-left-color: transparent;
  }
  25% {
    border-top-color: var(--border-brand);
    border-right-color: transparent;
    border-bottom-color: transparent;
    border-left-color: transparent;
  }
  50% {
    border-top-color: var(--border-brand);
    border-right-color: var(--border-brand);
    border-bottom-color: transparent;
    border-left-color: transparent;
  }
  75% {
    border-top-color: var(--border-brand);
    border-right-color: var(--border-brand);
    border-bottom-color: var(--border-brand);
    border-left-color: transparent;
  }
  100% {
    border-top-color: var(--border-brand);
    border-right-color: var(--border-brand);
    border-bottom-color: var(--border-brand);
    border-left-color: var(--border-brand);
  }
}
```
