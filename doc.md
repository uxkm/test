# test
```scss
// 251202


.not-padding-y {
  padding-top: 0 !important;
  padding-bottom: 0 !important;
  // 모달 내 콘텐츠 상하 영역 간격
  .sv-bottom-sheet__body {
    padding-top: 0 !important;
    padding-bottom: 0 !important;
  }
}
.not-padding-x {
  padding-left: 0 !important;
  padding-right: 0 !important;
  // 모달 내 콘텐츠 좌우 영역 간격
  .sv-bottom-sheet__body {
    padding-left: 0 !important;
    padding-right: 0 !important;
  }
}
.not-padding-t {
  padding-top: 0 !important;
  // 모달 내 콘텐츠 상단 영역 간격
  .sv-bottom-sheet__body {
    padding-top: 0 !important;
  }
}
.not-padding-b {
  padding-bottom: 0 !important;
  // 모달 내 콘텐츠 하단 영역 간격
  .sv-bottom-sheet__body {
    padding-bottom: 0 !important;
  }
}

// 조회 기간 선택
.month-filter {
  &__header {
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
    &.full-width {
      .sv-datepicker__header {
        .sv-datepicker__title {
          flex: 1 1 auto;
          text-align: center;
        }
        .sv-bottom-sheet__body & {
          padding-left: 0;
          padding-right: 0;
        }
      }
    }
  }
  &__body {
    margin-top: var(--spacing-xl);
  }
  &__grid {
    display: grid !important;
    grid-template-columns: repeat(3, 1fr);
    gap: var(--spacing-md);
    flex-direction: unset !important;
    flex-wrap: unset !important;
    .sv-select-box {
      width: 100%;
      margin: 0 !important;
      margin-right: 0 !important;
      margin-bottom: 0 !important;
    }
  }
}
```
