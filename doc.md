# test

{% raw %}
```scss
// 251212 utitlity


// 공유하기 리스트
.shared-list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: var(--spacing-xl);
  padding: var(--spacing-3xl) var(--spacing-2xl);
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
  }
}


```
{% endraw %}

---
