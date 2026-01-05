# test

{% raw %}
```scss

.sc-wrap {
  background-color: transparent;

  @media (min-width: 621px) {
    max-width: 620px;
    margin: 0 auto;
  }
}

// 하단 fixed 영역도 동일하게 적용
.sv-bottom-action-container {
  @media (min-width: 621px) {
    max-width: 620px;
    left: 50%;
    transform: translateX(-50%);
  }
}


```
{% endraw %}

---
