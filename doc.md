# test

{% raw %}
```scss


.sc-wrap {
  background-color: transparent;
  max-width: 620px;
  margin: 0 auto;

  @media (max-width: 620px) {
    width: 100%;
    margin: 0;
  }
}

// 하단 fixed 영역도 동일하게 적용
.sv-bottom-action-container__inner {
  max-width: 620px;
  left: 50%;
  transform: translateX(-50%);

  @media (max-width: 620px) {
    width: 100%;
    left: 0;
    transform: none;
  }
}

```
{% endraw %}

---
