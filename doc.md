# test

{% raw %}
```scss
// 251211 utitlity
// 1319

  // 참여한 이벤트 스타일
  &.event-applied {
    padding-bottom: var(--spacing-2xl);
    .usage-history__dropdown {
      margin-bottom: 0;
    }
  }

// 1441

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

// 


// 251212 commmon 618

    // 참여한 이벤트 내역 스타일
    &.event-applied__body {
      .category-item {
        padding: 0;
      }
      .sv-list {
        height: 118px;
        padding-top: var(--spacing-lg);
        padding-bottom: var(--spacing-lg);
      }
      .usage-date__title {
        @include font-set("body-s", 300);
        font-weight: 300;
        color: var(--text-tertiary);
        margin-bottom: var(--spacing-sm);
        padding-top: 0;
        padding-bottom: var(--spacing-md);
        border-bottom: 1px solid var(--border-tertiary);
      }
      .usage-history__section {
        ~ .usage-history__section {
          margin-top: var(--spacing-2xl);
        }
      }
    }
```
{% endraw %}

---
