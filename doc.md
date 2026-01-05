# test

{% raw %}
```scss


.sc-floating__topbtn {
  // 620px 콘텐츠 영역 기준으로 우측 하단에 위치
  position: fixed !important;
  // 620px 영역의 우측 끝에서 20px 안쪽에 배치
  // 화면 중앙(50%)에서 620px/2 = 310px 오른쪽이 영역의 오른쪽 끝
  // right는 오른쪽에서의 거리이므로: calc(50% - 310px + 20px) = calc(50% - 290px)
  right: calc(50% - 290px) !important;
  bottom: 20px !important;

  @media (max-width: 620px) {
    right: 20px !important; // 620px 이하에서는 화면 우측 기준
  }

  .sv-floating-action-button {
    border-radius: 50%;
    &--color-primary {
      background-color: var(--bg-white);
      color: var(--fg-primary);
      /* Shadow 4 */
      box-shadow: 0 4px 16px 0 rgba(12, 17, 29, 0.18);
    }
  }
  .sv-floating-action-button--size-medium {
    min-width: 48px;
    min-height: 48px;
    &:not(.sv-floating-action-button--has-text) {
      width: 48px;
    }
  }
}

```
{% endraw %}

---
